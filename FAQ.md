# Frequently Asked Questions

---

## General

### What is cPanel Redis Manager?

cPanel Redis Manager is a commercial plugin by UnderHost that integrates Redis directly into cPanel and WHM. It handles installation, configuration, per-account instance management, health monitoring, and process keep-alive — all without requiring end users to touch the command line.

### Who is this for?

- **Hosting providers** who want to offer Redis to their cPanel customers
- **System administrators** who manage cPanel servers and want an efficient way to deploy Redis at scale
- **Developers** who host on cPanel and need Redis for caching, sessions, or queuing

---

## Source Code and Repository

### Why is the plugin source code not in this repository?

cPanel Redis Manager is a commercial, proprietary product. The source code is not publicly distributed. This GitHub repository exists to provide transparent product documentation, publish the development roadmap, and give the community a place to track progress and report issues.

The installation package is delivered privately after purchase through the UnderHost client portal. This protects the integrity of the licensed software and ensures every deployment is authorized.

### Can I inspect the code before buying?

Screenshots of the cPanel and WHM interfaces are available on the product website at [cpanelredismanager.com](https://cpanelredismanager.com). The [FEATURES.md](FEATURES.md) and [HOW_IT_WORKS.md](HOW_IT_WORKS.md) files in this repository provide detailed technical descriptions of the implementation. If you have specific technical questions before purchasing, contact [support@underhost.com](mailto:support@underhost.com).

---

## Compatibility

### What operating systems are supported?

- AlmaLinux 8 and 9
- CentOS 7 and 8
- CloudLinux 7, 8, and 9
- Ubuntu (LTS releases)

### What cPanel versions are supported?

Any current release of cPanel & WHM with the Jupiter theme. The plugin registers with the Jupiter theme by default.

### Does it work with CloudLinux and CageFS?

Yes. The installer detects CloudLinux automatically and runs the necessary CageFS registration steps. Alt-PHP and the PHP Selector are supported. See [docs/compatibility.md](docs/compatibility.md) for details.

### What Redis versions are supported?

Redis 6.x and 7.x. The system Redis package installed by your distribution's package manager is used.

### What PHP versions are supported?

All PHP versions available on the server, including EasyApache 4 managed PHP and CloudLinux alt-PHP. The PHP Redis extension must be installed separately — instructions are in the [documentation](https://cpanelredismanager.com/documentation.php).

### Do I need root access?

Yes, root SSH access is required for installation. End users accessing Redis through cPanel do not need root access.

---

## Licensing

### How does the license work?

Each license covers one server identified by its IP address. The license is validated against the UnderHost license server. Responses are cached locally so validation does not impact page load performance.

### Can I use the license on multiple servers?

No. Each license covers one server. You can purchase additional licenses for additional servers at the same price.

### What happens if I migrate to a new server?

You can update the licensed IP address through your [UnderHost client area](https://customerpanel.ca) at any time.

### Does the license expire?

No. The current license model is a one-time purchase with no expiry.

### What if the UnderHost license server is unavailable?

A grace period is built in. If the license server cannot be reached after the local cache expires, the plugin continues to operate normally for up to 72 hours. This prevents a license server outage from affecting your production environment.

---

## Pricing

### What does the license cost?

$29.95 USD, one-time payment, per server.

### Are updates included?

Yes. Free lifetime updates are included with every license. This includes all future major and minor releases.

### Is there a monthly option?

Not currently. A monthly subscription option may be introduced in the future for enterprise features, but this would be optional. All existing one-time license holders retain their lifetime access permanently.

### Is there a refund policy?

For refund inquiries, contact [support@underhost.com](mailto:support@underhost.com) or visit your UnderHost client area.

---

## Technical

### How are Redis instances isolated between accounts?

Each cPanel account runs its own Redis process as that account's system user. Instances are bound to `127.0.0.1` and assigned a unique port. Config files, data directories, and logs are all stored in the account's home directory. Accounts cannot access each other's instances.

### What happens if Redis crashes?

A per-user cron job detects that the instance is no longer running on its assigned port and restarts it automatically. If the user intentionally stopped the instance, a state file prevents the cron from restarting it.

### Does this work with WordPress, Magento, or other CMS platforms?

Yes. Once a Redis instance is running, any application on that account that supports Redis can connect to it using the displayed host, port, and authentication key. Redis-specific configuration for popular CMS platforms is planned as presets in a future release.

### Does installing Redis affect other services on the server?

No. The system Redis service installed by the package manager is configured to bind to localhost only during installation. Per-user instances are similarly localhost-bound. No public ports are opened.

---

## Support

### How do I get support?

- **Email:** [support@underhost.com](mailto:support@underhost.com)
- **Client area:** [customerpanel.ca](https://customerpanel.ca)
- **GitHub Issues:** [github.com/UnderHost/cPanelRedisManager/issues](https://github.com/UnderHost/cPanelRedisManager/issues) (documentation and feature requests only)

Typical email response time is within 24 hours.

---

> cPanel® is a registered trademark of cPanel, L.L.C. This project is not affiliated with or endorsed by cPanel, L.L.C.
