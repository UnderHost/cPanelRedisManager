# Changelog Summary

High-level version history for cPanel Redis Manager.

For the full development roadmap and planned releases, see [ROADMAP.md](../ROADMAP.md).

---

## v2.3.6 — Current Development State *(Internal)*

> Focus: production hardening, installer reliability, and security alignment.

**Installer & Deployment**
- Fixed invisible license prompt (stdout/stderr separation)
- Safe cron installation with validation and fallback handling
- Removed python3 dependency from license cron
- Improved installer robustness and error reporting

**Compatibility**
- cPanel Jupiter theme compliance (SVG icon requirement)

**Security**
- CSRF token TTL reduced (4h → 1h)
- Improved CSRF lifecycle consistency

**Validation & Safety**
- JSON decoding safety (`is_array` guard)
- Safer handling of server metadata

**Migrations**
- Cleanup of deprecated assets (old icons)
- CSRF token cleanup aligned with new TTL
- Migration audit logging

---

## v2.3.3 — Security & Core Architecture Stabilization *(Internal)*

> Major internal milestone introducing foundational systems used in current builds.

**Security Hardening**
- Final CSRF protection implementation:
  - Atomic token read (TOCTOU-safe)
  - Token regeneration fallback
  - Failure logging via `error_log()`

**Core Architecture**
- Centralized `LicenseService.php` introduced
- Unified license validation logic (foundation layer)

**Infrastructure**
- 3-tier IP resolution system:
  1. Installer-generated metadata (`server_meta.json`)
  2. Runtime cache
  3. External fallback (ipify)
- Installer now writes secure server metadata (root-owned)

**Validation**
- Branding validation using `parse_url()` (HTTPS + structure enforcement)
- Strict input validation improvements

**Codebase Hardening**
- Silent failure audit (`@` usage reviewed and minimized)
- Safer filesystem operations

---

## v2.1.1 — Security & Stability Hardening *(Planned: June 2026)*

**Control Plane & Security**

- Root-owned metadata system for all WHM operations
- No reliance on user-writable files for privileged actions
- Strict POST + CSRF enforcement for all mutating endpoints
- Removal of unsafe shell execution paths
- `proc_open()` argument arrays for all command execution

**Validation & Safety**

- Strict configuration validation before writing Redis configs
- Centralized username validation
- Safe handling of user input across all endpoints

**File Safety**

- Atomic file writes for config, metadata, and secrets
- Improved permission enforcement for all sensitive files

**Audit Logging**

- Structured JSON logs for administrative actions
- Includes actor, action, target, and result

---

## v2.1.0 — WHM Plugin *(Planned: June 2026)*

**WHM Plugin**

- Full WHM admin dashboard with server-wide Redis instance overview
- Per-account memory and connection statistics
- Per-account password rotation via live `CONFIG SET`
- Web-based Redis CLI with safe execution and command allowlist
- WHM global configuration editor (memory, policy, databases, CLI toggle)
- Backup system for all accounts from WHM
- CSF firewall auto-configuration for Redis ports

**Architecture Improvements**

- Root-owned metadata store for instance control
- No reliance on user-controlled PID files
- Stop operations via authenticated `redis-cli SHUTDOWN`
- Improved instance detection beyond PID file checks

**Installer & Migrations**

- Upgrade-aware installer (`install.sh`)
- Version detection and safe migration system
- Idempotent deployment
- `uninstall.sh` for clean removal

---

## v2.0.4 — Stability & Production Readiness *(Planned: April 30, 2026)*

🧪 Currently available to early-access users and new installations. Public release scheduled for April.

### Summary
Foundation rewrite from previous obfuscated codebase.

### Added
- Fully readable `RedisManager.php`
- License system using `.license` file
- License validation endpoint with JSON-backed store
- State tracking via `redis.enabled`
- TCP-based instance detection
- Real stats endpoint using Redis INFO
- CSRF protection for cPanel actions
- Versioned installer and migration system
- Upgrade-safe installation flow

### Security
- Safe command execution via `proc_open()`
- Root metadata store for trusted operations
- No trust in user-home config for privileged actions
- Redis shutdown via authenticated CLI, not PID signals
- CSRF protection on all mutating endpoints

**Core cPanel Plugin Improvements**

- Improved process handling and reliability
- More accurate instance state detection
- Enhanced logging and edge-case handling
- Stability improvements across instance lifecycle (start, stop, restart)
- Minor UI improvements in cPanel interface

---

## v2.0.3 — Current Public Production Release

**Core cPanel Plugin**

- One-click Redis start/stop from cPanel interface
- Automatic port assignment per account
- Secure AUTH key generation per instance
- Per-user config generation with proper permissions (`0640`)
- Instance isolation — each account runs its own Redis process
- Local-only binding (`127.0.0.1`) — no public exposure
- Automatic cron-based process monitoring and restart
- State-aware cron respecting intentional stops
- Concurrency protection using `flock`
- Real-time stats endpoint (connections, memory, uptime)
- Per-user activity logging
- License system with local caching and grace period
- CSRF protection on mutating actions
- Compatible with PHP 8.x environments
- Idempotent installer with OS detection and CageFS support

---

## Earlier Development

Prior to v2.0.3, the plugin was in internal development and testing. No public changelog is available.

## [2.0.3] and earlier

Legacy obfuscated release. Not documented.

---

> cPanel® is a registered trademark of cPanel, L.L.C.  
> This project is not affiliated with or endorsed by cPanel, L.L.C.
