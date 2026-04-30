<div align="center">

<img src="https://cdn4.iconfinder.com/data/icons/redis-2/1451/Untitled-2-512.png" width="80" alt="Redis Manager">

# cPanel Redis Manager

**Production-ready Redis management for cPanel & WHM servers.**

[![License](https://img.shields.io/badge/License-Proprietary-red.svg)](LICENSE.md)
[![Current](https://img.shields.io/badge/Current-2.3.10-blue.svg)](ROADMAP.md)
[![Internal Development](https://img.shields.io/badge/Internal%20Development-2.3.12-orange.svg)](ROADMAP.md)
[![Platform](https://img.shields.io/badge/Platform-cPanel%20%2F%20WHM-orange.svg)](docs/compatibility.md)
[![Price](https://img.shields.io/badge/Price-%244.95%20month-green.svg)](PRICING.md)

[Website](https://cpanelredismanager.com) · [Documentation](https://cpanelredismanager.com/documentation.php) · [Roadmap](ROADMAP.md)

</div>

---

## Overview

**cPanel Redis Manager** is a commercial plugin by [UnderHost](https://underhost.com) that brings fully managed Redis to cPanel and WHM environments.

It handles installation, configuration, process management, health monitoring, and per-account isolation - all through a native UI.

Designed for shared hosting environments, it allows each cPanel account to run its own Redis instance safely and predictably without requiring manual server administration.

---

## Key Capabilities

- **Per-account Redis instances** - fully isolated per cPanel user
- **One-click lifecycle management** (start, stop, restart)
- **Automatic port assignment** and secure AUTH key generation
- **WHM control panel** for server-wide monitoring and management
- **Per-account limits** (`maxmemory`, eviction policy, and more)
- **Health monitoring system** - detects broken or unresponsive instances
- **Automatic recovery via cron**
- **Backup and restore system** (per account)
- **Safe configuration system** - no dangerous directives allowed
- **CloudLinux & CageFS compatible**

---

## Designed for Hosting Environments

cPanel Redis Manager is built specifically for hosting providers:

- No shared Redis instance - **each account is isolated**
- No unsafe configuration exposure
- No manual CLI or root intervention required for daily use
- Predictable behavior across hundreds of accounts

---

## Supported Environments

cPanel Redis Manager follows the **official cPanel-supported operating system lifecycle** and remains compatible with all supported cPanel releases.

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

> ⚠️ Support for legacy systems is best-effort only. New features may not be backported.

---

## Current Status

| Item | Status |
|---|---|
| Current release | `v2.3.10` |
| Release line | `v2.3.x` |
| Next milestone | `v2.4.x - Hosting Control and Monetization` |

Recent update:

- `v2.3.11` - [BETA] Connection Helper Wizard, Application Detection, Setup Preflight, Diagnostics Bundle
- `v2.3.10` - CageFS network namespace handling update
- `v2.3.9` - Health Score and Smart Suggestions

  👉 See [ROADMAP.md](ROADMAP.md) for full details.

---

## Public Documentation

All installation, upgrade, and configuration steps are published on the official documentation website:

- https://cpanelredismanager.com/documentation.php
- https://cpanelredismanager.com/documentation.php#changelog
- https://cpanelredismanager.com/documentation.php#configuration
- https://cpanelredismanager.com/documentation.php#roadmap

---


## Screenshots

### cPanel Interface

<p align="center">
  <img src="screenshots/cpanel1.png" width="32%">
  <img src="screenshots/cpanel2.png" width="32%">
  <img src="screenshots/cpanel3.png" width="32%">
</p>

<p align="center">
  <em>Per-account Redis management directly inside cPanel</em>
</p>

---

### WHM Interface

<p align="center">
  <img src="screenshots/whm1.png" width="32%">
  <img src="screenshots/whm2.png" width="32%">
  <img src="screenshots/whm3.png" width="32%">
</p>

<p align="center">
  <img src="screenshots/whm4.png" width="32%">
  <img src="screenshots/whm5.png" width="32%">
  <img src="screenshots/whm6.png" width="32%">
</p>

<p align="center">
  <img src="screenshots/whm7.png" width="32%">
  <img src="screenshots/whm8.png" width="32%">
  <img src="screenshots/whm9.png" width="32%">
</p>

<p align="center">
  <em>Full WHM control panel with monitoring, limits, and management</em>
</p>

---

## About This Repository

This repository is the **public documentation and product information hub**.

The plugin source code is **proprietary** and not publicly distributed.

This repo exists to:
- Publish roadmap and product updates
- Provide compatibility and usage documentation
- Support users and customers

---

## Legal

cPanel® is a registered trademark of cPanel, L.L.C.  
This project is not affiliated with or endorsed by cPanel, L.L.C.

© 2026 UnderHost.com. All rights reserved.
