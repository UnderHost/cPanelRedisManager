# Changelog

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
