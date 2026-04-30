# Upgrade Guide - v2.3.11

All installation and upgrade actions are managed through the official website workflow:

- https://cpanelredismanager.com/documentation.php
- https://cpanelredismanager.com/documentation.php#configuration

## Supported Upgrade Paths

- `v2.0.4 -> v2.3.11`
- `v2.1.x -> v2.3.11`
- `v2.2.x -> v2.3.11`
- `v2.3.x -> v2.3.11`

For legacy deployments on `v2.0.3` or older, follow the current migration instructions from the website documentation.

## What's New in v2.3.11

- Connection Helper Wizard for common application stacks
- Application Detection with integration status checks
- Setup Preflight for readiness checks in cPanel
- Diagnostics Bundle export for support workflows

## Verification

After upgrade, verify:

- Reported version is `2.3.11`
- cPanel and WHM plugin pages load normally
- Redis instance lifecycle actions respond correctly
- Health score and diagnostics export are available

## Notes

- Per-account Redis data and user config are preserved during normal in-place upgrades.
- For current production instructions, always use the website documentation as source of truth.
