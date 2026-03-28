# cPanel Redis Manager — Development Roadmap

This document reflects the current development status and planned release schedule for cPanel Redis Manager by UnderHost.

> **Last updated:** 2025 · See [changelog summary](docs/changelog-summary.md) for version history.

---

## Released

### v2.0.4 — Current Stable Release

**Core Functionality**
- One-click Redis server start and stop from cPanel
- Automatic port assignment per user account
- Secure AUTH key generation per instance
- Automatic configuration file generation

**Configuration**
- Global settings integration
- cPanel Redis Manager UI (Jupiter theme)
- UHREDIS-KEY IP-locked license system
- Per-user config file isolation

**cPanel Integration**
- User-specific Redis instance management
- Automatic cron job creation for process keep-alive
- Comprehensive per-account activity logging
- State-aware start/stop (intentional stop is respected by cron)

---

## In Development

### v2.1.0 — WHM Plugin

**WHM Enhanced Monitoring**
- Real-time performance metrics across all accounts
- Connection statistics per account
- Memory usage graphs per account (Chart.js)
- Server-wide Redis summary dashboard

**Security**
- CSF firewall auto-configuration for Redis ports
- Per-account password rotation from WHM
- Root-owned metadata store — no user-writable trust paths
- CSRF protection on all mutating actions
- License validation caching (1-hour TTL, 24-hour grace period)

**Management**
- Web-based Redis CLI for administrators (injection-safe, allowlisted commands)
- WHM global configuration editor (maxmemory, eviction policy, databases)
- Global account-level backup system (BGSAVE per account + Backup All)
- Per-account config editing from WHM

---

## Planned

### v2.2.0 — Stability + User Control Release

> Goal: Make Redis safe and predictable per cPanel account.

**Per-Account Redis Limits**
- `maxmemory` per account
- `maxmemory-policy` per account
- Optional: `maxclients`, `timeout`
- Simple preset selector + advanced toggle in cPanel UI

**cPanel-Side Monitoring**
- Memory usage, uptime, connections, hit/miss ratio
- Lightweight display — no heavy graphs needed at this level

**Proper Backup + Restore System**
- List backups per account
- Restore from backup with rollback protection
- Configurable retention (3–7 backups)
- Size validation before restore

**Safe Config Editor (cPanel)**
- Allow only safe directives: `maxmemory`, eviction policy, `timeout`, persistence toggle
- Block all other directives at the UI and API level

**Improved Process Handling**
- Verify `/proc/<pid>/exe` points to `redis-server`
- Verify process owner matches cPanel account
- Verify command line includes expected config file
- Detect and clean up stale PID files automatically

**Redis Health Check System**
- Authenticated `PING` validation (not just port check)
- Auto-detect broken or unresponsive instances
- Surface real health state separately from running/stopped

**License System Completion**
- Full caching in both WHM and cPanel contexts
- Configurable grace period (24–72 hours)
- Background license validation via system cron

---

### v2.3.0 — Hosting Features Release

> Goal: Make the plugin valuable for hosting providers and resellers.

**Hosting Package Integration**
- Assign Redis memory limits per cPanel package in WHM
- Enable or disable Redis per package
- Control CLI access and backup access per package
- This is a significant commercial differentiator for hosting providers

**Reseller Support**
- Reseller-level visibility and limits
- Delegated control over accounts under a reseller
- Optional reseller dashboard

**Advanced WHM Monitoring with Historical Stats**
- Time-series graphs (24-hour rolling memory and connections)
- Per-account breakdown with drill-down
- Stats snapshots written by background cron

**Alerting System**
- Alerts for: Redis instance down, high memory usage, failed auth spikes, backup failures
- Delivery via WHM dashboard and email
- Configurable thresholds per account or globally

**Audit Log System**
- Structured audit log: who, what, when, from which IP
- Before/after values for all config changes
- Exportable log format

**CLI Hardening (Final Form)**
- Strict command parser with argument validation
- Command categories: safe, restricted, blocked
- Per-account CLI enable/disable flag (from package settings)

**Service Recovery Tools**
- WHM tools: rebuild config, reset password, restart broken instance
- Fix permissions, reassign port
- Guided recovery wizard for common failure scenarios

---

### v2.4.0 — Advanced Infrastructure

> Goal: Reduce admin workload and increase reliability at scale.

**Auto-Healing System**
- Detect Redis crash loops and back off intelligently
- Auto-restart with exponential backoff
- Notify admin on repeated failure

**Port Management System**
- Detect and resolve port conflicts automatically
- Track all assigned ports in root-owned registry
- Safe port reassignment without data loss

**Metadata Integrity System**
- Detect mismatches between config file, metadata store, and running process
- Auto-repair option for common drift scenarios

**Backup Improvements**
- Compression for backup archives
- Scheduled backups per account (configurable frequency)
- Retention policy enforcement

**Performance Tuning Presets**
- WordPress
- Magento
- Laravel
- Generic PHP session cache
- Applied through the safe config editor

**Improved Uninstall and Cleanup**
- `--purge` flag for full data removal
- Selective cleanup: configs, ports, metadata, backups
- Optional data wipe with confirmation gate

---

## Future Vision

### v2.5.0 — Power User Features

> Only after the system is fully stable.

- Multi-instance support per cPanel account
- Per-domain Redis instance mapping
- Advanced config editor (expert mode — all safe Redis directives)
- REST API and webhook support
- Integration hooks for popular CMS and hosting automation platforms

---

### v3.0.0 — Enterprise and Scaling

> For environments that go beyond shared hosting.

- Redis Sentinel (high availability with automatic failover)
- Redis Cluster (multi-node topology)
- Auto-scaling based on memory headroom and load
- External Redis support (connect to remote Redis servers)
- Hybrid on-server and remote configurations

---

## Commercial Direction

cPanel Redis Manager is currently offered as a **one-time license at $29.95 USD per server** with free lifetime updates.

A **monthly subscription option** may be introduced in the future as the product expands toward enterprise features. This will be an optional alternative — not a replacement.

**Early adopters are permanently protected.** Any customer who purchases a lifetime license before a subscription model is introduced will retain their lifetime license and all future updates at no additional cost.

---

## Feedback and Feature Requests

We welcome input from the community and our customers.

- Email: [support@underhost.com](mailto:support@underhost.com)
- Website: [cpanelredismanager.com](https://cpanelredismanager.com)
- GitHub Issues: [Open an issue](https://github.com/UnderHost/cPanelRedisManager/issues)

> cPanel® is a registered trademark of cPanel, L.L.C. This project is not affiliated with or endorsed by cPanel, L.L.C.
