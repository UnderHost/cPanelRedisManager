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

### v2.0.4 — Stability Update *(Planned: April 30, 2026)*

> Goal: Finalize v2.0 branch stability before WHM introduction.

**Improvements**
- Bug fixes and performance improvements
- Improved process handling reliability
- Better logging and edge-case handling
- Minor UI improvements in cPanel interface

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

### v2.3.0 — Hosting Features Release *(Planned: Q3 2026)*

> Goal: Make the plugin valuable for hosting providers and resellers.

**Hosting Package Integration**
- Assign Redis limits per cPanel package
- Enable/disable Redis per package
- Control CLI and backup access per package

**Reseller Support**
- Reseller-level visibility and controls
- Delegated management of sub-accounts
- Optional reseller dashboard

**Advanced Monitoring**
- Time-series stats (24-hour rolling metrics)
- Per-account drill-down
- Background stats collection via cron

**Alerting System**
- Alerts for downtime, memory spikes, auth failures, backup issues
- Delivery via WHM dashboard and email
- Configurable thresholds

**Audit Log System**
- Structured logs: who, what, when, IP
- Before/after config tracking
- Exportable logs

**CLI Hardening (Final Form)**
- Strict command parsing and validation
- Command categories (safe / restricted / blocked)
- Per-account CLI permissions

**Service Recovery Tools**
- Rebuild config, reset password, restart instances
- Fix permissions and reassign ports
- Guided recovery workflows

**Licensing System Upgrade (Planned)**
- Transition to signed license validation model
- Feature-based licensing (WHM, backups, CLI, etc.)
- Machine-bound licensing (fingerprint-based)
- Improved anti-abuse and activation tracking

---

## Future Vision

### v2.4.0 — Advanced Infrastructure

> Goal: Reduce admin workload and increase reliability at scale.

- Auto-healing system for crash recovery
- Intelligent restart backoff logic
- Port conflict detection and resolution
- Metadata integrity verification and repair
- Scheduled and compressed backups
- Performance tuning presets (WordPress, Magento, Laravel)

---

### v2.5.0 — Power User Features

- Multi-instance support per cPanel account
- Per-domain Redis mapping
- Advanced config editor (expert mode)
- REST API and webhook support

---

### v3.0.0 — Enterprise & Scaling

- Redis Sentinel (high availability)
- Redis Cluster support
- Auto-scaling capabilities
- External Redis integration
- Hybrid deployment support

---

## Commercial Direction

cPanel Redis Manager is currently offered as a **one-time license per server** with lifetime updates.

Future versions may introduce optional subscription tiers for advanced features.  
**Existing lifetime customers will always retain their benefits.**

---

## Feedback and Feature Requests

- Email: support@underhost.com  
- Website: https://cpanelredismanager.com  
- GitHub Issues: https://github.com/UnderHost/cPanelRedisManager/issues

> cPanel® is a registered trademark of cPanel, L.L.C. This project is not affiliated with or endorsed by cPanel, L.L.C.
