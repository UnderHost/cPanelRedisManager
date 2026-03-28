# Changelog Summary

High-level version history for cPanel Redis Manager.

For the full development roadmap and planned releases, see [ROADMAP.md](../ROADMAP.md).

---

## v2.1.0 — In Development

**WHM Plugin**

- Full WHM admin dashboard with server-wide Redis instance overview
- Real-time Chart.js memory and connections graphs per account
- Per-account password rotation via live `CONFIG SET` (no restart required)
- Web-based Redis CLI with injection-safe `proc_open()` execution and command allowlist
- WHM Global Configuration editor (maxmemory, eviction policy, databases, CLI toggle)
- Global backup system — trigger BGSAVE across all running accounts simultaneously
- CSF firewall auto-configuration for Redis ports
- Root-owned metadata store — WHM operations no longer trust user-writable files
- CSRF protection on all mutating actions (session-bound to cpsess)
- License validation caching with grace period in both cPanel and WHM contexts
- Stop via authenticated `redis-cli SHUTDOWN` — PID files no longer trusted for stop operations
- Status detection via TCP port check — more reliable than PID file existence
- `install.sh` upgrade mode — detects installed version, backs up, applies migrations, preserves license
- Migration system — per-version migration scripts applied in order, tracked to prevent re-runs
- `uninstall.sh` for clean removal

---

## v2.0.4 — Current Stable Release

**Core cPanel Plugin**

- One-click Redis start/stop from cPanel Software section
- Automatic port assignment per cPanel account using OS socket binding
- Cryptographically random AUTH key generation per instance
- Per-user config file generation with correct permissions (`chmod 0640`)
- Instance isolation — each account runs its own Redis process as that user
- All instances bound to `127.0.0.1` — no public network exposure
- Automatic cron job creation for process keep-alive
- State-aware cron — respects intentional stops via `redis.enabled` state file
- `flock` concurrency protection on cron restarts
- Real-time stats endpoint — connections, memory, latency, uptime (JSON)
- Per-user activity log at `~/.cpanel/plugin/redis/log/<username>.log`
- License key stored in separate `.license` file (`chmod 600`) — never in source code
- License validation with 1-hour cache and 24-hour grace period
- UHREDIS-KEY and UHREDISIP-KEY license formats supported
- CSRF protection on start/stop actions (POST-only)
- `FILTER_SANITIZE_STRING` removed — compatible with PHP 8.1, 8.2, 8.3
- Config values read from file in PHP — no `shell_exec grep/awk` for config parsing
- `install.sh` with OS detection, idempotent deployment, CageFS support

---

## Earlier Development

Prior to v2.0.4, the plugin was in internal development and testing. No public changelog is available for earlier builds.

---

> cPanel® is a registered trademark of cPanel, L.L.C. This project is not affiliated with or endorsed by cPanel, L.L.C.
