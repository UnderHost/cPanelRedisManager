# Implementation Overview

A technical description of cPanel Redis Manager's architecture and components.

> This document describes the system at a conceptual level. The plugin source code is proprietary and not publicly distributed.

---

## Component Map

```
cPanel Redis Manager
│
├── cPanel Plugin (per-user)
│   ├── index.live.php          — UI and action dispatcher
│   ├── RedisManager.php        — Core instance management class
│   └── redis_style.css         — Plugin stylesheet
│
├── WHM Plugin (server admin)
│   ├── whm_index.php           — WHM dashboard UI
│   ├── WHMRedisManager.php     — Server-level management class
│   └── api/whm_api.php         — AJAX endpoint for WHM UI
│
├── Installer
│   ├── install.sh              — Main installer / upgrader
│   ├── uninstall.sh            — Plugin removal script
│   └── migrations/             — Version-specific migration scripts
│
└── License System
    ├── .license                 — Protected key file (server-side, not public)
    └── /var/lib/redis-manager/  — Root-owned metadata store
```

---

## cPanel Plugin

The cPanel plugin runs in the Jupiter theme context and is accessible to every cPanel user on the licensed server. Each user sees only their own Redis instance.

**Key responsibilities:**
- Render the instance status page
- Handle start/stop actions (POST with CSRF token)
- Return real-time stats via a JSON endpoint
- Read and display connection details

**Instance data stored per user:**
```
~/.cpanel/plugin/redis/
├── redis.conf          — Redis configuration (chmod 0640)
├── redis.pid           — Process ID file (not trusted for stop operations)
├── redis.enabled       — State file (presence = intentionally running)
├── redis.lock          — flock lock for cron concurrency
├── data/               — Redis data directory (RDB/AOF files)
└── log/
    └── <username>.log  — Activity log
```

---

## WHM Plugin

The WHM plugin runs as root in the WHM CGI context. It provides server-wide visibility and control.

**Key responsibilities:**
- Display all cPanel accounts and their Redis status
- Start/stop instances on behalf of accounts
- Rotate authentication keys
- Manage global configuration defaults
- Provide a web-based Redis CLI
- Trigger BGSAVE backups

**Root-owned metadata store:**
```
/var/lib/redis-manager/
├── users/
│   └── <username>.json     — Authoritative per-account metadata (chmod 600)
├── whm_config.json          — Global configuration defaults (chmod 600)
├── .license_cache           — WHM license validation cache (chmod 600)
├── .csrf_<session>          — Per-session CSRF tokens (chmod 600)
└── audit.log                — Admin action audit log (planned v2.3)
```

The metadata store is always the authoritative source for WHM operations. User-home config files are treated as display data only — WHM never trusts user-writable files for privileged operations such as process termination.

---

## Process Management

**Start flow:**
1. Create config file if it doesn't exist (using WHM global defaults if set)
2. Launch `redis-server` via the system binary with the config file path
3. Wait for the configured port to accept connections (TCP check, up to 10 seconds)
4. Write the `redis.enabled` state file
5. Register the cron job

**Stop flow:**
1. Read port and password from the authoritative source (root meta for WHM, config file for cPanel user)
2. Run `redis-cli SHUTDOWN NOSAVE` against the authenticated instance
3. Wait for the port to stop responding (up to 10 seconds)
4. Remove state file and PID file
5. Remove the cron job

**Status check:**
Status is determined by attempting a TCP connection to the configured port. If the connection succeeds, the instance is running. This is the only status check used — PID file existence alone is not considered sufficient evidence.

---

## Cron Keep-Alive

Each running instance has a per-user cron entry in this format:

```bash
* * * * * [ -f ~/.cpanel/plugin/redis/redis.enabled ] && \
  /usr/bin/flock -n ~/.cpanel/plugin/redis/redis.lock \
  redis-server ~/.cpanel/plugin/redis/redis.conf --daemonize yes \
  >> /dev/null 2>&1
```

Key behaviors:
- The `[ -f redis.enabled ]` check prevents restarts after an intentional stop
- `flock` prevents multiple concurrent restart attempts
- The cron only fires if the instance is supposed to be running and is not

---

## License Validation

The license key is stored in `<plugin_dir>/.license` — a file separate from all PHP source, with `chmod 600` and owned by root.

Validation is cached locally to avoid a remote call on every page load:
- Cache TTL: 1 hour
- Grace period: 24–72 hours if the license server is unreachable
- Cache stored in `/var/lib/redis-manager/` with `chmod 600`

---

## Security Boundaries

| Boundary | Mechanism |
|---|---|
| WHM trusts only root-owned metadata | `/var/lib/redis-manager/users/<user>.json` |
| Process stop via authentication | `redis-cli SHUTDOWN`, not PID kill |
| Web CLI injection prevention | `proc_open()` with argument array, command allowlist |
| CSRF protection | Session-bound tokens via cpsess identifier |
| Config file permissions | `0640` — no world-readable configs |
| License key protection | `0600`, root-owned, never in source code |
| Network isolation | All instances bound to `127.0.0.1` only |

---

## Installer

`install.sh` is the single entry point for both fresh installs and upgrades.

**Install flow:**
1. Check root privileges
2. Detect OS
3. Validate license key
4. Install Redis server (if not present)
5. Configure CageFS (if CloudLinux)
6. Detect existing installation → enter upgrade mode if VERSION file found
7. Back up existing plugin files
8. Deploy new plugin files
9. Register plugin with cPanel
10. Write license file
11. Write `.htaccess` protection for sensitive files
12. Write VERSION file
13. Run pending migrations in sorted order
14. Clean up `/tmp`

The installer is idempotent — running it multiple times on the same server is safe. User data in `~/.cpanel/plugin/redis/` is never modified by the installer.

---

> cPanel® is a registered trademark of cPanel, L.L.C. This project is not affiliated with or endorsed by cPanel, L.L.C.
