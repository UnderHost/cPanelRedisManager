# Installation Overview

This document describes the installation process for cPanel Redis Manager at a high level.

> The installation package is delivered privately after purchase. It is not publicly distributed. This protects the licensed software and ensures every deployment is authorized. You will receive your installation instructions by email after completing your purchase.

---

## Prerequisites

Before installing, confirm the following:

| Requirement | Detail |
|---|---|
| Valid license | Purchase at [customerpanel.ca](https://customerpanel.ca/client/store/addons-license-script/redis-manager) |
| Root SSH access | Required — the installer must run as root |
| cPanel & WHM | Installed and running |
| Operating system | AlmaLinux 8/9, CentOS 7/8, CloudLinux 7/8/9, or Ubuntu |
| RAM | Minimum 2 GB (4 GB recommended) |
| Package manager | `dnf`, `yum`, or `apt-get` available |
| curl + unzip | Available on the server |

---

## Installation Process

### Step 1 — Purchase and Receive Your License

Complete your purchase at the UnderHost client portal. You will receive an email containing:
- Your license key
- Your installation instructions

### Step 2 — Connect to Your Server

Connect via SSH as root (or use `sudo -i` to switch to root).

### Step 3 — Run the Installer

Follow the instructions in your activation email to run the installer. You will be prompted to enter your license key during installation.

The installer automatically:
- Validates your license key against the UnderHost license server
- Detects your operating system
- Installs the Redis server package if not already present
- Secures the system Redis service to localhost only
- Deploys the cPanel plugin to the Jupiter theme directory
- Registers the plugin with cPanel
- Configures CloudLinux / CageFS if applicable
- Stores your license key securely

### Step 4 — Access in cPanel

After successful installation, Redis Manager appears under **Software** in the cPanel interface for all accounts on the server.

Users click **Initialize Server** on first visit to provision their Redis instance.

---

## Upgrading

Upgrades use the same installation process. When the installer detects an existing installation, it automatically enters upgrade mode:

1. Detects the installed version from the `VERSION` file
2. Backs up current plugin files to `/var/backups/redis-plugin/`
3. Deploys the new plugin files
4. Preserves the existing license key — no re-entry required
5. Runs any pending migration scripts
6. Cleans up

**User Redis instances are not interrupted during an upgrade.** All running instances continue operating. User data, configs, and logs are never modified by the upgrade process.

---

## Uninstalling

To remove the plugin interface only (preserves all user Redis data):

```bash
/usr/local/cpanel/scripts/uninstall_plugin \
  /usr/local/cpanel/base/frontend/jupiter/redis_plugin \
  --theme=jupiter

rm -rf /usr/local/cpanel/base/frontend/jupiter/redis_plugin
```

To also remove the Redis server and all data (destructive — removes all user Redis data):

```bash
yum remove redis -y
rm -rf /etc/redis /var/lib/redis
```

> ⚠️ The second set of commands permanently removes Redis and all cached data from the server. Use only if you are certain this is intended.

---

## PHP Redis Extension

The cPanel Redis Manager plugin handles Redis server management. For PHP applications to connect to Redis, the PHP Redis extension must be installed separately.

**Via WHM EasyApache (non-CloudLinux):**
1. Log in to WHM as root
2. Navigate to Software → Module Installers
3. Click Manage next to PHP Pecl
4. Search for `redis` and click Install
5. Restart services

**Via CloudLinux (alt-PHP):**
```bash
yum install alt-php-redis
systemctl restart alt-php<version>-php-fpm
```

**Via PECL:**
```bash
/usr/local/cpanel/bin/pecl install redis
```

---

## CloudLinux and CageFS

The installer detects CloudLinux automatically and runs:

```bash
cagefsctl --addrpm redis
cagefsctl --force-update
```

This ensures Redis is accessible within CageFS environments. Alt-PHP support for the Redis extension is available through the standard CloudLinux package repositories.

---

## Support

For installation assistance, contact [support@underhost.com](mailto:support@underhost.com) or open a ticket through your [UnderHost client area](https://customerpanel.ca).

Full documentation: [cpanelredismanager.com/documentation.php](https://cpanelredismanager.com/documentation.php)

---

> cPanel® is a registered trademark of cPanel, L.L.C. This project is not affiliated with or endorsed by cPanel, L.L.C.
