# Implementation Overview

A technical description of cPanel Redis Manager architecture and components.

> This document describes the system at a conceptual level. The plugin source code is proprietary and not publicly distributed.

---

## Component Map

```text
cPanel Redis Manager
│
├── cPanel Plugin (per-user)
│   ├── index.live.php          - UI and action dispatcher
│   ├── RedisManager.php        - Core instance management class
│   └── redis_style.css         - Plugin stylesheet
│
├── WHM Plugin (server admin)
│   ├── whm_index.php           - WHM dashboard UI
│   ├── WHMRedisManager.php     - Server-level management class
│   └── api/whm_api.php         - AJAX endpoint for WHM UI
│
├── Installer
│   ├── install.sh              - Main installer / upgrader
│   ├── uninstall.sh            - Plugin removal script
│   └── migrations/             - Version-specific migration scripts
│
└── License System
    ├── .license                - Protected key file (server-side, not public)
    └── /var/lib/redis-manager/ - Root-owned metadata store
```

---

## cPanel Plugin

The cPanel plugin runs in the Jupiter theme context and is accessible to every cPanel user on the licensed server. Each user sees only their own Redis instance.

**Key responsibilities:**
- Render instance status and configuration
- Handle start/stop actions (POST with CSRF)
- Provide real-time stats endpoint
- Display connection details

**Instance data stored per user:**
```text
~/.cpanel/plugin/redis/
├── redis.conf
├── redis.pid           - Not trusted for privileged operations
├── redis.enabled       - Desired state flag
├── redis.lock          - Concurrency lock (flock)
├── data/
└── log/
```

---

## WHM Plugin

The WHM plugin runs as root and provides server-wide control.

**Key responsibilities:**
- Server-wide Redis visibility
- Per-account lifecycle management
- Password rotation
- Global configuration defaults
- Backup control
- CLI access (restricted)

**Root-owned metadata store:**
```text
/var/lib/redis-manager/
├── users/
│   └── <username>.json
├── whm_config.json
├── .license_cache
├── .csrf_<session>
└── audit.log
```

This store is the authoritative source for all privileged operations.

User-home files are never trusted for control decisions.

---

## Process Management

### Start Flow

1. Validate configuration values
2. Generate config if needed
3. Launch `redis-server` with config path
4. Wait for port availability
5. Write desired state (`redis.enabled`)
6. Register cron

### Stop Flow

1. Read connection details from trusted source
2. Execute authenticated `redis-cli SHUTDOWN`
3. Wait for port closure
4. Remove state and PID files
5. Remove cron entry

### Status Model

Instance state is determined using multiple signals:

- Process validation
- TCP connectivity
- Authenticated Redis PING
- State file (`redis.enabled`)

States include:

- `stopped`
- `running`
- `degraded`
- `broken`
- `stale_pid`

PID file presence alone is never trusted.

---

## Cron Keep-Alive

Each instance has a per-user cron:

```bash
* * * * * [ -f ~/.cpanel/plugin/redis/redis.enabled ] && \
  /usr/bin/flock -n ~/.cpanel/plugin/redis/redis.lock \
  redis-server ~/.cpanel/plugin/redis/redis.conf --daemonize yes \
  >> /dev/null 2>&1
```

**Behavior:**

- Only runs if instance should be active
- Prevents duplicate execution via flock
- Avoids restarting intentionally stopped instances

---

## License System

- License key stored separately from source (`0600`)
- Validation performed remotely
- Results cached locally
- Grace period allows continued operation if unreachable
- Shared validation logic between WHM and cPanel

---

## Security Model

### Root-Owned Control Plane

All critical metadata is stored in:

```text
/var/lib/redis-manager/
```

- Owned by root
- Not user-writable
- Used for all privileged decisions

### Process Validation

Before trusting a running instance:

- Verify `/proc/<pid>/exe`
- Verify process owner
- Verify command-line arguments

### Safe Configuration

Only allowlisted directives are used:

- `maxmemory`
- eviction policy
- `timeout`
- persistence

No arbitrary config input is accepted.

### Command Execution

- No shell concatenation
- `proc_open()` with argument arrays
- Strict command allowlist

### File Safety

- No world-writable files
- Atomic writes for config and metadata
- Strict permission enforcement

### Network Isolation

- All Redis instances bind to `127.0.0.1`
- No external exposure

---

## Installer

`install.sh` handles installation and upgrades.

**Flow:**

- Validate root access
- Detect OS
- Validate license
- Install Redis if needed
- Configure environment (CageFS if applicable)
- Detect existing installation
- Backup previous version
- Deploy new files
- Register plugin
- Apply migrations
- Cleanup

The installer is idempotent. User data is preserved.

---

cPanel® is a registered trademark of cPanel, L.L.C.
This project is not affiliated with or endorsed by cPanel, L.L.C.
