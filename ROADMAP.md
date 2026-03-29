# cPanel Redis Manager — Development Roadmap

This document reflects the current development status and planned release schedule for cPanel Redis Manager by UnderHost.

> **Last updated:** 2026 · See [changelog summary](docs/changelog-summary.md) for version history.

---

## Released

### v2.0.3 — Current Production Version

- Stable Redis instance management for cPanel users
- Per-account Redis instances with isolated configs
- Automatic port assignment and AUTH key generation
- Cron-based process monitoring and recovery
- Basic logging and lifecycle management

---

## Upcoming Releases

### v2.0.4 - Stability & Production Readiness *(Planned: April 30, 2026)*

> Goal: Finalize the v2.0 foundation for reliable production deployment before WHM integration.

**Improvements**
- Improved process handling and reliability
- More accurate instance state detection
- Enhanced logging and edge-case handling
- Stability improvements across instance lifecycle (start, stop, restart)
- Minor UI improvements in cPanel interface

>  Currently available to early access users and new installations. Official public release in April with updated documentation and website.

---

### v2.1.0 — WHM Plugin *(Planned: June 2026)*

> Goal: Introduce full WHM-level control and visibility.

**WHM Monitoring**
- Server-wide Redis overview dashboard
- Per-account connection and memory statistics
- Basic performance visibility

**Security**
- CSF firewall auto-configuration for Redis ports
- Per-account password rotation from WHM
- Root-owned metadata storage (no user-writable trust paths)
- CSRF protection on mutating actions

**Management**
- WHM global configuration editor
- Redis CLI (restricted and injection-safe)
- Backup all accounts from WHM
- Per-account control from WHM interface

---

## Current UnderHost.com Build

### v2.1.1 — WHM Stability & Hardening *(Planned: Late June 2026)*

> Goal: Secure and stabilize WHM control plane.

**Security Hardening**
- Restricted WHM access (no broad ACL exposure)
- Full POST + CSRF enforcement on mutating endpoints
- Removal of unsafe shell execution paths
- Atomic file writes for configs, metadata, and secrets
- Structured audit logging for administrative actions

**Validation & Safety**
- Strict config validation before writing Redis configs
- Centralized username validation
- Improved error handling (no internal leakage)

**Internal Improvements**
- CLI access gated behind configuration flags
- Idempotent migration handling
- Improved internal service structure

---

## In Development

### v2.2.x — Stability + User Control Release *(Planned: July–August 2026)*

> Goal: Make Redis safe, predictable, and production-ready per cPanel account.

**Per-Account Redis Limits**
- `maxmemory` per account
- `maxmemory-policy` per account
- `maxclients` and `timeout` support
- Preset selector + advanced configuration mode in cPanel UI

**cPanel-Side Monitoring**
- Memory usage, uptime, connections
- Cache hit/miss ratio
- Lightweight status display (no heavy graphs)

**Backup + Restore System**
- List backups per account
- Restore with automatic rollback protection
- Configurable retention (3–7 backups)
- Size and integrity validation before restore

**Safe Config Editor**
- Strict allowlist: `maxmemory`, eviction policy, `timeout`, persistence toggle
- Full server-side validation
- No arbitrary directive injection possible

**Improved Process Handling**
- Validate `/proc/<pid>/exe` matches Redis binary
- Verify process owner matches cPanel account
- Validate command line against expected config file
- Automatic stale PID detection and cleanup

**Redis Health System**
- Authenticated `PING` validation
- Detection of broken or unresponsive instances
- Separate health state from running/stopped:
  - running
  - degraded
  - broken
  - stopped

**License System Completion**
- Full caching in WHM and cPanel contexts
- Configurable grace period (24–72 hours)
- Background validation via system cron
- Centralized license service layer (internal)

**Security & Hardening**
- Full control-plane hardening from v2.1.1
- Consistent validation across all endpoints
- Safe file handling and permission enforcement

---

## Planned

### v2.3.0 — Hosting Foundation *(Q3 2026)*

> Goal: Introduce core hosting features and white-label capabilities.

- Package-based Redis enable/disable
- Per-package Redis limits
- Package default configurations (auto-provisioning)
- Basic reseller visibility (read-only)
- White-label branding (logo, title, custom CSS)
- Basic alerting (instance down, memory limits)

---

### v2.4.0 — Hosting Control & Monetization

> Goal: Enable hosting providers to monetize and control Redis usage.

- Full reseller management (limits and controls)
- Reseller quotas (account limits, memory caps)
- Monetization hooks (enable Redis per package tiers)
- Per-account usage history (memory, connections, peaks)
- Enhanced alerting (custom thresholds and notifications)
- One-click optimization (WHM)

---

### v2.5.0 — Security & Abuse Protection

> Goal: Protect servers and enforce fair usage.

- Smart resource enforcement (soft and hard limits)
- Memory pressure detection
- Abuse detection system (connections, writes, auth attempts)
- Redis AUTH protection (rate limiting, tracking, optional IP restriction)
- License system upgrade (signed tokens)
- Server fingerprinting (IP, hostname, machine ID)

---

### v2.6.0 — Observability & Debugging

> Goal: Improve visibility and reduce support overhead.

- Advanced monitoring (graphs and drill-down)
- Instance debug mode (slowlog, verbose logging, command stats)
- Quick health score (Good / Warning / Critical)
- Improved audit logging

---

### v2.7.0 — Infrastructure Upgrade

> Goal: Improve internal architecture and scalability.

- Background worker system (replace heavy cron usage)
- Auto-healing system for failed instances
- Intelligent restart backoff logic
- Auto cleanup system (remove orphan instances and files)

---

### v2.8.0 — Advanced Features

> Goal: Improve usability and advanced configuration.

- Redis template profiles (WordPress, Magento, Laravel, etc.)
- Snapshot-based backups with rollback support
- Config integrity validation (signed configs)
- Export and import configurations between servers

---

### v2.9.0 — Developer & Integration Layer

> Goal: Enable integrations and automation.

- REST API
- Webhook system
- Redis version manager (safe upgrade and downgrade)
- External Redis support (basic integration)

---

### v3.0.0 — Enterprise, Scaling & Multi-Control-Panel Support

- Redis Sentinel (high availability)
- Redis Cluster support
- Auto-scaling capabilities
- External Redis integration
- Hybrid deployment support
- DirectAdmin support
- User-level Redis management for DirectAdmin
- Admin-level Redis management for DirectAdmin
- Shared architecture for cPanel/WHM and DirectAdmin environments

---

## Commercial Direction

cPanel Redis Manager is currently offered as a one-time license per server with lifetime updates.

Future versions may introduce optional subscription tiers for advanced features.
Existing lifetime customers will always retain their benefits.

---

## Feedback and Feature Requests

- Email: support@underhost.com
- Website: https://cpanelredismanager.com
- GitHub Issues: https://github.com/UnderHost/cPanelRedisManager/issues

cPanel® is a registered trademark of cPanel, L.L.C.
This project is not affiliated with or endorsed by cPanel, L.L.C.
