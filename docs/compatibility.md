# Compatibility

Supported environments and requirements for cPanel Redis Manager.

---

## Control Panel

| Software | Requirement |
|---|---|
| cPanel & WHM | Current release, Jupiter theme |
| WHM Plugin | Root access required |
| cPanel Plugin | Available to all accounts on licensed server |

---

## Operating Systems

| OS | Versions |
|---|---|
| AlmaLinux | 8, 9 |
| CentOS | 7, 8 |
| CloudLinux | 7, 8, 9 |
| Ubuntu | LTS releases |

> Rocky Linux and other RHEL-compatible distributions may work but are not officially tested.

---

## Redis

| Component | Versions |
|---|---|
| Redis Server | 6.x, 7.x |
| Source | System package manager (dnf / yum / apt-get) |

Redis is installed from the distribution's standard repositories (with EPEL enabled on RHEL-based systems). The plugin does not compile Redis from source.

---

## PHP

| Environment | Support |
|---|---|
| EasyApache 4 | All managed PHP versions |
| CloudLinux alt-PHP | All versions (Redis extension included by default) |
| PHP Selector | Fully compatible |
| PHP-FPM | Supported |

The PHP Redis extension must be installed separately from the plugin. Installation instructions are in [docs/installation-overview.md](installation-overview.md).

---

## CloudLinux

| Feature | Support |
|---|---|
| CageFS | ✅ Supported — registered during installation |
| alt-PHP | ✅ Supported |
| PHP Selector | ✅ Supported |
| LVE (resource limits) | ✅ Compatible |

The installer detects CloudLinux automatically and runs the necessary CageFS registration commands.

---

## Server Requirements

| Resource | Minimum | Recommended |
|---|---|---|
| RAM | 2 GB | 4 GB |
| Root access | Required for installation | — |
| Package manager | dnf, yum, or apt-get | — |
| Tools | curl, unzip | — |
| Network | License server access during install | — |

---

## Network Requirements

The installer requires outbound HTTPS access to the UnderHost license server during installation and license validation. After the initial installation, license validation responses are cached locally. The server does not need continuous external connectivity to operate.

Redis instances bind exclusively to `127.0.0.1`. No inbound firewall rules are required for Redis to function.

---

## Browser Compatibility (cPanel / WHM UI)

The plugin UI uses standard HTML, CSS, and JavaScript compatible with all modern browsers. The Jupiter theme in cPanel and the WHM admin interface are supported in:

- Chrome / Chromium (current)
- Firefox (current)
- Safari (current)
- Edge (current)

---

## Known Limitations

- The plugin is designed for single-server deployments. Multi-server / cluster support is planned for a future release.
- Multi-instance per cPanel account (more than one Redis instance per user) is planned for v2.5.0.
- The WHM plugin requires the Jupiter cPanel theme. Other themes are not currently supported.

---

> cPanel® is a registered trademark of cPanel, L.L.C. This project is not affiliated with or endorsed by cPanel, L.L.C.
