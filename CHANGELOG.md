# Changelog

## [2.6.10] - 2026-09-14

### Fixed
- WHM config changes no longer leave the per-account Redis config owned by root. Ownership was reverting on every edit and restart, and per-account memory (and other) changes did not apply because the instance (which runs as the account user) could not read a root-owned config. WHM now writes each account config owned by the account user, and a heal migration restores any config already left root-owned.

### Note
- The global **Default Max Memory** applies to newly provisioned instances; change an existing account from its per-account configuration.

## [2.6.9] - 2026-09-14

### Fixed
- Corrects a v2.6.8 regression where the RDB-disable migration could leave a per-account config root-owned under CloudLinux CageFS (`redis.conf: Permission denied` on start). Configs are now rewritten in place, and a heal migration restores any already left root-owned.

## [2.6.8] - 2026-09-14

Stability and visibility under load (field-driven).

### Changed
- Cache instances default to no on-disk snapshots (RDB off) to avoid latency spikes under memory pressure; on-demand backups are unaffected.

### Fixed
- Server IP detection uses a consensus across several services instead of a single one, so a misbehaving service can no longer return a wrong IP and invalidate an IP-locked license.
- The dashboard shows last-known metrics with a "busy" indicator instead of blank values when the backend is briefly under heavy load.
- The diagnostics bundle gained eviction/fragmentation/policy/persistence detail, plus a per-account diagnostics export in WHM.

## [2.6.0 - 2.6.7] - 2026-07

Security, abuse prevention, and licensing automation. Additive and report-only or fail-safe by default.

### Added
- Report-only resource abuse detection (memory, connection, eviction, ops-per-second signals with a 0-100 score).
- AUTH brute-force protection with an escalating lockout and an append-only audit log; credential strength and reuse scoring; rollback-safe password rotation.
- Signed license tokens with a machine-id-anchored server fingerprint, and a database-backed licensing service as the single source of truth with a WHMCS provisioning module automating the full service lifecycle. Fail-safe: identical to the prior release until the signing key is deployed.
- Branding expansion with one-click UnderHost / Redis / Valkey presets and readability warnings.

### Fixed
- WHM dashboard load reduced roughly 93x by caching backend detection per request.
- Installer no longer aborts an upgrade when the shared Redis service is password-protected, on a non-default port, or slow to answer.

## [2.5.0] - 2026-07-15

Provider enforcement and monetization. Report-only by default.

### Added
- Package-tier cache availability enforcement via a tamper-proof, root-owned policy mirror.
- Per-reseller instance and total-memory quotas; monetization hook events for billing automation; Simple / Developer / Advanced exposure modes.
- One-click guided Redis-to-Valkey migration with snapshot, verification, and automatic rollback.

## [2.4.0 - 2.4.2] - 2026-06

Redis and Valkey compatibility foundation.

### Added
- Full Valkey backend compatibility while preserving Redis support, with OS-aware fresh-install backend selection and a WHM backend selector.
- Backend diagnostics for Redis and Valkey binaries, CLI tools, services, versions, and account counts.
- Recovery Tools reliability improvements and installer migration-tracking self-heal.

## [2.3.11] - 2026-04-30

Connection Helper Wizard, Application Detection, Setup Preflight, and Diagnostics Bundle.

### Added
- Connection Helper Wizard in cPanel with ready-to-copy snippets for WordPress, Laravel, Magento, PHP, Node.js, Python, and LiteSpeed Cache
- Application Detection scanning `public_html` for installed applications and checking Redis integration status (WordPress, WordPress + LiteSpeed Cache, Laravel, Magento)
- LiteSpeed Cache detection with targeted WP Admin guidance when LSCache is present
- Setup Preflight panel in cPanel for instance initialized, instance running, and auth configured checks
- Diagnostics Bundle export with masked passwords for support-safe sharing

### Changed
- CageFS network namespace fix now applied when CloudLinux and `cagefs.conf` are present
- Health score and ONLINE badges updated to static solid-pill style
- Wizard, app detection, and preflight panels aligned to the current plugin visual style

### Fixed
- Connection Wizard copy button handling corrected for safe attribute rendering
- Wizard JavaScript handlers exposed correctly for button actions
- User-facing preflight content refined for end-user relevance
- New panel CSS corrected for cPanel light theme cards

## [2.3.10] - 2026-04-28

### Changed
- CageFS `NETWORK_NAMESPACE=0` handling corrected for CloudLinux + CageFS environments

## [2.3.9] - 2026-04-26

### Added
- Redis Health Score out of 100 with grade labels
- Smart Suggestions panel with plain-language recommendations

## [2.3.8] - 2026-04-23

### Added
- Historical trend storage (24h and 7d) for memory, connections, and cache efficiency
- WHM-side usage rollups and retention controls

## [2.3.7] - 2026-04-23

### Added
- Hardening and release-integrity improvements
- Installer and deployment verification refinements

## [2.3.6] - 2026-04-22

### Added
- Public rollout baseline for cPanel + WHM package
- Installer and upgrade-flow reliability improvements

## [2.3.0 - 2.3.5] - 2026 Q1-Q2

Hosting foundation series (packages, reseller groundwork, branding, usage history groundwork, and licensing foundation).

## [2.2.0 - 2.2.2] - 2026

Stability and user-control series.

## [2.1.1] - 2026

Internal WHM hardening build.

## [2.1.0] - 2026

WHM plugin release.

## [2.0.4] - 2026

Foundation rewrite and migration baseline.

## [2.0.3] - 2026

Legacy public production baseline before the current architecture.
