# Security Policy

## Supported Versions

Security updates are applied to the current stable release. We strongly recommend keeping your installation current by running the upgrade installer when new versions are released.

| Version | Supported |
|---|---|
| Latest stable | ✅ Yes |
| Previous releases | ⚠️ Update recommended |

---

## Reporting a Vulnerability

UnderHost takes security seriously. If you discover a vulnerability in cPanel Redis Manager, please report it responsibly.

**Do not report security vulnerabilities through public GitHub issues.**

### Responsible Disclosure Process

1. **Email your report to:** [security@underhost.com](mailto:security@underhost.com)

2. **Include in your report:**
   - A clear description of the vulnerability
   - Steps to reproduce the issue
   - The potential impact in your assessment
   - Any proof-of-concept code (if applicable)
   - Your name or handle if you would like to be credited

3. **What to expect:**
   - Acknowledgment of your report within 48 hours
   - An initial assessment within 5 business days
   - Regular updates as we investigate and remediate
   - Credit in the release notes if you wish, once the issue is resolved and disclosed

4. **Please do not:**
   - Publicly disclose the vulnerability before we have had a reasonable opportunity to address it
   - Attempt to access, modify, or delete data that does not belong to you during testing
   - Perform denial-of-service testing

---

## Security Architecture

The following security principles are applied throughout cPanel Redis Manager:

**Instance isolation**
Each Redis instance runs as the cPanel account user and binds exclusively to `127.0.0.1`. Instances are never exposed to public network interfaces. Cross-account access is not possible by design.

**No world-writable files**
Config files are created with `chmod 0640`. License files are `chmod 600` and owned by root. No plugin files are world-writable.

**No PID file trust for privileged operations**
WHM-level stop and shutdown operations use authenticated `redis-cli SHUTDOWN` against a root-owned metadata record — never by reading a user-writable PID file and sending a kill signal.

**Root-owned metadata store**
All authoritative instance metadata (port, password, config path) is stored in `/var/lib/redis-manager/` with `chmod 700` and owned by root. User-home config files are treated as display data only for privileged operations.

**CSRF protection**
All state-changing actions in both the cPanel and WHM interfaces require a valid CSRF token. WHM tokens are session-bound using the cPanel `cpsess` session identifier.

**Shell injection prevention**
The web-based Redis CLI uses `proc_open()` with an explicit argument array. No user input is ever concatenated into a shell command string. A strict allowlist of safe Redis verbs is enforced server-side.

**License key protection**
License keys are stored in a file separate from PHP source code, with restricted permissions. Keys are never embedded in source files, logged, or transmitted to end users.

**License validation caching**
License validation uses a local cache with a one-hour TTL to avoid external dependency on every page load. A grace period allows continued operation if the license server is temporarily unreachable.

---

## Contact

For non-security support inquiries: [support@underhost.com](mailto:support@underhost.com)

For security disclosures: [security@underhost.com](mailto:security@underhost.com)
