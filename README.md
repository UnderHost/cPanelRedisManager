<div align="center">

<img src="https://cdn4.iconfinder.com/data/icons/redis-2/1451/Untitled-2-512.png" width="80" alt="Redis Manager">

# cPanel Redis Manager

**The easiest way to deploy and manage Redis on cPanel servers.**

[![License](https://img.shields.io/badge/License-Proprietary-red.svg)](LICENSE.md)
[![Version](https://img.shields.io/badge/Version-2.1.0-blue.svg)](ROADMAP.md)
[![Platform](https://img.shields.io/badge/Platform-cPanel%20%2F%20WHM-orange.svg)](docs/compatibility.md)
[![Price](https://img.shields.io/badge/Price-%2429.95%20one--time-green.svg)](PRICING.md)

[Website](https://cpanelredismanager.com) · [Documentation](https://cpanelredismanager.com/documentation.php) · [Purchase](https://customerpanel.ca/client/store/addons-license-script/redis-manager) · [Roadmap](ROADMAP.md)

</div>

---

## Overview

**cPanel Redis Manager** is a commercial plugin by [UnderHost](https://underhost.com) that integrates Redis directly into cPanel and WHM environments. It handles installation, configuration, health monitoring, process management, and per-account instance isolation — all without requiring manual server administration.

Redis is one of the most effective tools for improving web application performance. cPanel Redis Manager makes it deployable in minutes on any compatible cPanel server, with a clean UI accessible directly from the cPanel Software section.

---

## Key Capabilities

- **One-click Redis start/stop** from within cPanel
- **Per-user instance isolation** — each account runs its own Redis process
- **Automatic port assignment** and secure AUTH key generation
- **Health monitoring** with real-time status checks
- **Auto-restart via cron** — instances recover automatically after reboots
- **WHM admin panel** for server-wide monitoring and management
- **CloudLinux and CageFS compatible** — works with alt-PHP and selector environments
- **Secure by design** — bound to localhost only, no world-writable configs

See [FEATURES.md](FEATURES.md) for the complete feature list.

---

## Supported Environments

| Component | Requirement |
|---|---|
| Control Panel | cPanel & WHM |
| Operating System | AlmaLinux 8/9, CentOS 7/8, CloudLinux 7/8/9, Ubuntu |
| PHP | All versions including CloudLinux alt-PHP |
| Redis | 6.x / 7.x |
| Access | Root SSH required for installation |
| RAM | Minimum 2 GB (4 GB recommended) |

See [docs/compatibility.md](docs/compatibility.md) for full details.

---

## Current Status

| Version | Status |
|---|---|
| v2.0.4 | ✅ Released — stable production version |
| v2.1.0 | 🔄 In development — WHM plugin |
| v2.2.0 | 📋 Planned — cPanel custom config + monitoring |
| v2.3+ | 🔮 Future — hosting package integration, alerting, audit logs |

See [ROADMAP.md](ROADMAP.md) for the full development plan.

---

## Pricing

| License | Price | Scope |
|---|---|---|
| Single-Server | **$29.95 USD** one-time | One server, unlimited Redis instances |

- Free lifetime updates included
- IP address can be modified through the client area if you migrate servers
- Early adopters retain their lifetime license permanently
- A monthly subscription option may be introduced in the future — early adopters are protected

[→ Purchase a license](https://customerpanel.ca/client/store/addons-license-script/redis-manager)

See [PRICING.md](PRICING.md) for complete licensing details.

---

## Installation

Installation requires a valid license. After purchase, you will receive an activation email with your unique license key and installation instructions.

The installer handles:
- Redis server installation
- cPanel plugin registration
- Automatic configuration
- systemd / cron setup

> ⚠️ The installation package is delivered privately after purchase. It is not publicly distributed. This protects the integrity of the licensed software and ensures every deployment is properly authorized.

See [docs/installation-overview.md](docs/installation-overview.md) for a process walkthrough.

---

## Documentation

Full documentation is available at:

**[cpanelredismanager.com/documentation.php](https://cpanelredismanager.com/documentation.php)**

Topics covered:
- Installation and activation
- Uninstallation steps
- Configuration reference
- CloudLinux / CageFS setup
- PHP Redis extension installation
- Development roadmap

---

## About This Repository

This repository is the **public documentation and product information hub** for cPanel Redis Manager.

The plugin source code is **proprietary and not publicly distributed**. This repository exists to:

- Provide transparent product documentation
- Publish the development roadmap
- Offer a public reference for compatibility and feature information
- Support the open-source community through documentation

If you are a customer and need support, contact [support@underhost.com](mailto:support@underhost.com).

---

## Legal

cPanel® is a registered trademark of cPanel, L.L.C. This project is not affiliated with or endorsed by cPanel, L.L.C.

© 2025 UnderHost.com. All rights reserved. See [LICENSE.md](LICENSE.md).
