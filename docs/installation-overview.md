# Installation Overview

This document describes the installation process for cPanel Redis Manager at a high level.

> The installation package is delivered privately to licensed users. It is not publicly distributed.

---

## Prerequisites

Before installing, confirm the following:

| Requirement | Detail |
|---|---|
| Valid license | Purchase through [customerpanel.ca](https://customerpanel.ca/client/store/addons-license-script/redis-manager) |
| Root SSH access | Required |
| cPanel & WHM | Installed and running |
| Operating system | Supported cPanel-compatible operating system |
| RAM | Minimum 2 GB, 4 GB recommended |
| Package manager | `dnf`, `yum`, or `apt-get` |
| Tools | `curl` and `unzip` available |

For supported operating systems, see [compatibility.md](compatibility.md).

---

## Installation Process

### Step 1 - Purchase and Receive License

After purchase, you receive:

- your license key
- installation instructions
- access to license management through the client area

### Step 2 - Connect to the Server

Connect by SSH as `root`, or escalate to root before running the installer.

### Step 3 - Run the Installer

The installer handles both fresh installs and upgrades.

At a high level, it:

- validates the license
- detects the operating system
- installs Redis if needed
- secures the Redis service for localhost-only use
- deploys the cPanel plugin
- registers the plugin
- configures CloudLinux / CageFS support where applicable
- stores license and metadata safely
- applies migrations if required

### Step 4 - Access in cPanel

After successful installation, Redis Manager appears in the **Software** section in cPanel for accounts on the licensed server.

On first use, users initialize their own Redis instance from the UI.

---

## Upgrade Behavior

Upgrades use the same installer flow.

When an existing installation is detected, the installer enters upgrade mode and:

1. detects the installed version
2. backs up current plugin files
3. deploys the new package
4. preserves existing license state
5. runs pending migrations
6. performs cleanup

User Redis data is preserved during normal upgrades.

### Current rollout status

- **v2.0.3** is the current public production release
- **v2.0.4** is available to early access users and new installations
- broader public release of **v2.0.4** is planned alongside updated documentation and website content

---

## Uninstalling

Removal behavior depends on whether you want to remove only the plugin interface or also remove Redis data from the server.

Because environments vary, follow the official uninstall instructions supplied with your licensed package or support guidance from UnderHost.

> Removing Redis data is destructive and should only be done intentionally with confirmed backups where needed.

---

## PHP Redis Extension

The plugin manages Redis server instances. PHP applications still require the Redis PHP extension separately.

Common environments include:

- EasyApache 4
- CloudLinux alt-PHP
- PECL-based installs where appropriate

Refer to the official product documentation for environment-specific steps:

[cpanelredismanager.com/documentation.php](https://cpanelredismanager.com/documentation.php)

---

## CloudLinux and CageFS

When CloudLinux is detected, the installer applies the required CageFS integration steps automatically.

This supports:

- CageFS environments
- PHP Selector
- alt-PHP deployments

---

## Support

For installation or upgrade assistance:

- Email: [support@underhost.com](mailto:support@underhost.com)
- Client area: [customerpanel.ca](https://customerpanel.ca)

Full documentation:
[cpanelredismanager.com/documentation.php](https://cpanelredismanager.com/documentation.php)

---

> cPanel® is a registered trademark of cPanel, L.L.C. This project is not affiliated with or endorsed by cPanel, L.L.C.
