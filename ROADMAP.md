# cPanel Redis Manager - Development Roadmap

This roadmap reflects the public release position and planned milestone direction.

> Last updated: 2026-09-14  
> Release references: [CHANGELOG.md](CHANGELOG.md) and [docs/changelog-summary.md](docs/changelog-summary.md)

## Current Release

### v2.6.10 - Security, Abuse Prevention and Licensing Automation

Status: Released

The v2.6.x line adds security and abuse prevention (report-only), stronger AUTH protection, and signed, database-backed licensing with WHMCS automation, plus a much faster WHM dashboard and expanded branding. The latest patches (v2.6.8-v2.6.10) default cache instances to no on-disk snapshots, make server IP detection resilient, and keep per-account config ownership correct on upgrade and config changes. Everything is additive and report-only or fail-safe by default; existing Redis accounts are always preserved.

## Next Milestone

### v2.7.x - Observability and Debugging

Status: Planned

Goal: turn "service online" into deep operational visibility.

Planned scope:

- advanced monitoring, graphs, and command-level visibility
- a debug mode and slowlog tooling
- a WHM security tab surfacing the abuse, credential-hygiene, and auth-audit reports
- improved health scoring and stronger audit visibility

## Completed Milestones

- v2.6.0-2.6.10: Security, abuse prevention, and licensing automation; stability and config-ownership fixes
- v2.5.0: Provider enforcement and monetization; guided Redis ↔ Valkey migration
- v2.4.0-2.4.2: Redis and Valkey compatibility foundation
- v2.3.11: Connection Helper Wizard, Application Detection, Setup Preflight, Diagnostics Bundle
- v2.3.6-2.3.10: Public rollout baseline, historical graphs, health score, CageFS handling

## Planned Later Milestones

- `v2.8.x` Infrastructure Upgrade (background workers, restart backoff, auto-healing)
- `v2.9.x` Advanced Features (template profiles, config integrity, export/import)
- `v2.10.x` Developer and Integration Layer (REST API, webhooks)
- `v3.0.x` Enterprise and Multi-Control-Panel (Sentinel/cluster, DirectAdmin)
