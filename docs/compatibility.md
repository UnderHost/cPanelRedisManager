# Compatibility

Supported environments and requirements for cPanel Redis Manager.

---

## Control Panel

| Software | Requirement |
|---|---|
| cPanel & WHM | Current supported releases (Jupiter theme) |
| WHM Plugin | Root access required |
| cPanel Plugin | Available to all accounts on licensed server |

---

## Operating Systems

cPanel Redis Manager follows the **official cPanel-supported operating system lifecycle** and is designed to remain compatible with all actively supported cPanel environments.

### Supported Operating Systems

| OS | Support Status |
|---|---|
| AlmaLinux 8 | Supported until March 1, 2029 |
| AlmaLinux 9 | Supported until May 31, 2032 |
| AlmaLinux 10 | Supported until May 31, 2035 |
| CloudLinux 8 | Supported until May 31, 2029 |
| CloudLinux 9 | Supported until May 31, 2032 |
| CloudLinux 10 | Supported until May 31, 2035 |
| Rocky Linux 8 | Supported until March 31, 2026 |
| Rocky Linux 9 | Supported until March 31, 2026 |
| Ubuntu 22.04 LTS | Supported until June 30, 2027 |
| Ubuntu 24.04 LTS | Supported until April 2029 |

### Legacy / Extended Support

| OS | Status |
|---|---|
| CentOS 7 / RHEL 7 / CloudLinux 6 | End of life (July 31, 2024) |
| CloudLinux 7 (ELS) | Critical updates until January 1, 2027 |
| CentOS 7 (ELS) | Critical updates until January 1, 2027 |
| Ubuntu 20.04 LTS | End of life (April 30, 2025) |

> ⚠️ Legacy systems are supported on a best-effort basis. New features may not be backported.

---

## Redis

| Component | Versions |
|---|---|
| Redis Server | 6.x, 7.x |
| Source | System package manager (dnf / yum / apt-get) |

Redis is installed using the system package manager. The plugin does not compile Redis from source.

---

## PHP

| Environment | Support |
|---|---|
| EasyApache 4 | All managed PHP versions |
| CloudLinux alt-PHP | All versions (Redis extension included) |
| PHP Selector | Fully compatible |
| PHP-FPM | Supported |

The Redis PHP extension must be installed separately from the plugin. See [docs/installation-overview.md](installation-overview.md).

---

## CloudLinux

| Feature | Support |
|---|---|
| CageFS | Supported (auto-configured during install) |
| alt-PHP | Supported |
| PHP Selector | Supported |
| LVE (resource limits) | Compatible |

The installer detects CloudLinux automatically and configures CageFS integration.

---

## Server Requirements

| Resource | Minimum | Recommended |
|---|---|---|
| RAM | 2 GB | 4 GB |
| Root access | Required | Required |
| Package manager | dnf, yum, or apt-get | — |
| Tools | curl, unzip | — |
| Network | HTTPS access for licensing | — |

---

## Network Requirements

Outbound HTTPS access is required for license validation during installation and periodic checks.

- License responses are cached locally
- Temporary outages do not affect runtime operation (grace period supported)

Redis instances bind exclusively to `127.0.0.1`. No inbound firewall rules are required.

---

## Browser Compatibility (cPanel / WHM UI)

Compatible with modern browsers:

- Chrome / Chromium (current)
- Firefox (current)
- Safari (current)
- Edge (current)

Requires the Jupiter theme in cPanel and WHM.

---

## Known Limitations

- Designed for single-server deployments (cluster support planned in v3.0)
- Multi-instance per cPanel account planned for v2.5.0
- WHM plugin requires Jupiter theme

---

> cPanel® is a registered trademark of cPanel, L.L.C. This project is not affiliated with or endorsed by cPanel, L.L.C.
