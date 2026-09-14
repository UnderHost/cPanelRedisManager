# Changelog Summary

This summary tracks the major release progression for cPanel Redis Manager from the legacy `v2.0.3` baseline through the current `v2.6.10` release and next planned milestone path.

## Release Summary

| Version | Status | Summary |
|---|---|---|
| `v2.0.3` | Released | Legacy public baseline with isolated per-account Redis instances. |
| `v2.0.4` | Released | Foundation rewrite with installer-driven migration path. |
| `v2.1.0` | Released | WHM plugin introduced with dashboard and account controls. |
| `v2.1.1` | Internal | WHM hardening cycle. |
| `v2.2.x` | Released | Added per-account limits, monitoring, backup/restore, and safer config flows. |
| `v2.3.0 - v2.3.5` | Internal development | Hosting foundation series. |
| `v2.3.6 - v2.3.11` | Released | Public rollout, historical graphs, Health Score, CageFS handling, Connection Helper Wizard, Application Detection, and Diagnostics Bundle. |
| `v2.4.0 - v2.4.2` | Released | Redis and Valkey compatibility: backend auto-detection, WHM backend selector, diagnostics, and Recovery Tools/installer maintenance. |
| `v2.5.0` | Released | Provider enforcement and monetization: package-tier availability, reseller quotas, monetization hooks, exposure modes, and guided Redis ↔ Valkey migration. Report-only by default. |
| `v2.6.0 - v2.6.7` | Released | Security, abuse prevention, and licensing automation: report-only abuse detection, AUTH protection, signed + database-backed licensing with WHMCS automation, ~93× faster WHM dashboard, and branding presets. |
| `v2.6.8 - v2.6.9` | Released | Stability: RDB-off default, multi-source server IP detection, dashboard metrics resilience, diagnostics export, and a config-ownership regression fix. |
| `v2.6.10` | Current release | WHM config changes keep the per-account config owned by the account user, so config changes apply reliably and ownership no longer reverts to root. |
| `v2.7.x` | Planned | Observability and debugging. |

## Public Release Path

```text
v2.0.3 -> v2.0.4 -> v2.1.x -> v2.2.x -> v2.3.0-2.3.11 -> v2.4.0-2.4.2 -> v2.5.0 -> v2.6.0-2.6.10 -> v2.7.x
```

## References

- [../ROADMAP.md](../ROADMAP.md)
- [../CHANGELOG.md](../CHANGELOG.md)
- [../UPGRADE.md](../UPGRADE.md)
