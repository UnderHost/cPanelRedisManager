# Upgrade Guide - v2.6.10

All installation and upgrade actions are managed through the official website workflow:

- https://cpanelredismanager.com/documentation.php
- https://cpanelredismanager.com/documentation.php#configuration

## Supported Upgrade Paths

- `v2.0.4 -> v2.6.10`
- `v2.1.x -> v2.6.10`
- `v2.2.x -> v2.6.10`
- `v2.3.x -> v2.6.10`
- `v2.4.x / v2.5.0 / v2.6.x -> v2.6.10`

For legacy deployments on `v2.0.3` or older, follow the current migration instructions from the website documentation.

## What's New in v2.6.x

- Security and abuse prevention (report-only), stronger AUTH protection, and signed, database-backed licensing with WHMCS automation
- Redis or Valkey backends with OS-aware selection; provider enforcement, reseller quotas, and exposure modes (report-only by default)
- Cache instances default to no on-disk snapshots (RDB off) to avoid latency spikes; resilient multi-source server IP detection
- Faster WHM dashboard, branding presets, and a per-account diagnostics export
- v2.6.9 and v2.6.10 fixes: per-account config ownership is kept with the account user, so config changes apply reliably and ownership does not revert to root

## Verification

After upgrade, verify:

- Reported version is `2.6.10`
- cPanel and WHM plugin pages load normally
- Redis instance lifecycle actions respond correctly
- Health score and diagnostics export are available
- A per-account memory/limit change applies and persists across stop/start

## Notes

- Per-account Redis data and user config are preserved during normal in-place upgrades.
- For current production instructions, always use the website documentation as source of truth.
