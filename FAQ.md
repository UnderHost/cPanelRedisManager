# Frequently Asked Questions

---

## General

### What is cPanel Redis Manager?

cPanel Redis Manager is a commercial plugin by UnderHost that integrates Redis directly into cPanel and WHM.

It provides fully managed Redis instances per account, including installation, configuration, monitoring, health checks, and process management - all without requiring command line access.

---

### Who is this for?

- **Hosting providers** offering Redis to cPanel customers
- **System administrators** managing multi-tenant cPanel servers
- **Developers** using Redis for caching, sessions, or queues

---

## Source Code and Repository

### Why is the plugin source code not in this repository?

cPanel Redis Manager is a commercial, proprietary product. The source code is not publicly distributed.

This repository exists to:
- Provide product documentation
- Publish the development roadmap
- Track issues and feature requests

The installation package is delivered privately after purchase.

---

### Can I inspect the code before buying?

Documentation, feature breakdowns, and screenshots are available at:

👉 https://cpanelredismanager.com

You can also review:
- FEATURES.md
- HOW_IT_WORKS.md

For technical questions, contact support@underhost.com.

---

## Compatibility

### What operating systems are supported?

cPanel Redis Manager follows the official cPanel-supported operating system lifecycle.

Supported platforms include:
- AlmaLinux 8, 9, 10
- CloudLinux 8, 9, 10
- Rocky Linux 8, 9
- Ubuntu LTS (22.04, 24.04)

Legacy systems may work but are not guaranteed.

---

### What cPanel versions are supported?

Any actively supported version of cPanel & WHM using the Jupiter theme.

---

### Does it work with CloudLinux and CageFS?

Yes.

- Automatic CageFS integration
- Alt-PHP support
- Compatible with PHP Selector

---

### What Redis versions are supported?

Redis 6.x and 7.x using system packages.

---

### What PHP versions are supported?

All PHP versions available on the server, including:
- EasyApache 4
- CloudLinux alt-PHP

The Redis PHP extension must be installed separately.

---

### Do I need root access?

Yes, root SSH access is required for installation.

End users do not need root access to use Redis.

---

## Licensing

### How does the license work?

Each license is tied to a single server (by IP).

- Validation is performed against the license server
- Results are cached locally
- Both WHM and cPanel contexts use the same validation system

---

### What happens if the license server is unavailable?

A grace period is built in.

If the license server cannot be reached:
- the system continues operating normally
- no interruption to production services
- grace period lasts up to 72 hours

---

### Can I use the license on multiple servers?

No. Each license covers one server.

---

### What if I migrate to a new server?

You can update the licensed IP address from your client area.

---

### Does the license expire?

No. The current license is a one-time purchase with lifetime updates.

---

## Technical

### How are Redis instances isolated between accounts?

Each cPanel account runs its own Redis process:

- runs under the account system user
- bound to `127.0.0.1`
- assigned a unique port
- separate config, data, and log files

Accounts cannot access each other’s instances.

---

### How is the system secured against user tampering?

Critical data is managed by a root-owned control system.

- Metadata stored outside user directories
- User files are not trusted for privileged operations
- No user-controlled PID or config is used for WHM actions

This prevents cross-account interference and privilege escalation.

---

### What happens if Redis crashes?

The system detects failure and restarts the instance automatically.

- per-user monitoring
- state-aware restart logic
- prevents restart if intentionally stopped

---

### How is Redis health checked?

The system performs active checks:

- authenticated `PING`
- response validation
- process verification

Health state is tracked separately from running state.

---

### Can users break the Redis configuration?

No.

Only safe configuration options are allowed:
- memory limits
- eviction policy
- timeout
- persistence toggle

All other directives are blocked.

---

### Does this work with WordPress, Magento, or other CMS platforms?

Yes.

Any application that supports Redis can connect using:
- host (localhost)
- port
- authentication key

---

### Does installing Redis affect other services?

No.

- Redis instances are localhost-only
- no public ports are exposed
- system Redis is isolated

---

## Support

### How do I get support?

- Email: support@underhost.com
- Client area: https://customerpanel.ca
- GitHub Issues (documentation only)

Typical response time is within 24 hours.

---

> cPanel® is a registered trademark of cPanel, L.L.C. This project is not affiliated with or endorsed by cPanel, L.L.C.
