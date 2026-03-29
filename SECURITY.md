# Security Policy

## Supported Versions

Security updates are applied to actively maintained release lines.

We strongly recommend keeping your installation up to date.

| Version | Supported |
|---|---|
| Latest stable (current production) | ✅ Fully supported |
| Active release line (e.g. 2.1.x, 2.2.x) | ✅ Supported |
| Older versions | ⚠️ Upgrade required |

> ⚠️ Security fixes are not backported to outdated versions.

---

## Reporting a Vulnerability

UnderHost takes security seriously. If you discover a vulnerability in cPanel Redis Manager, please report it responsibly.

**Do not report security vulnerabilities through public GitHub issues.**

### Responsible Disclosure Process

1. **Email your report to:** security@underhost.com

2. **Include in your report:**
   - Clear description of the vulnerability
   - Steps to reproduce
   - Potential impact
   - Proof-of-concept (if applicable)
   - Your name/handle for credit (optional)

3. **What to expect:**
   - Acknowledgment within 48 hours
   - Initial assessment within 5 business days
   - Ongoing updates during remediation
   - Credit in release notes (optional)

4. **Please do not:**
   - Publicly disclose before a fix is released
   - Access or modify data that is not yours
   - Perform denial-of-service testing

---

## Security Scope

The following are considered in-scope:

- cPanel and WHM plugin interfaces
- API endpoints (WHM and cPanel)
- Authentication and authorization controls
- Redis instance isolation between users
- File permissions and privilege boundaries
- Command execution and input validation

Out-of-scope:

- Misconfiguration by server administrators
- Unsupported operating systems
- Third-party software not maintained by this project

---

## Security Architecture

cPanel Redis Manager is designed for **multi-tenant hosting environments** and enforces strict isolation and privilege separation.

### Instance Isolation

Each Redis instance runs under the cPanel account user and binds only to `127.0.0.1`.

- No public exposure
- No cross-account access
- No shared Redis processes

---

### Root-Owned Control Plane

All authoritative metadata is stored in:
/var/lib/redis-manager/


- Owned by root
- Permission `0700`
- Contains port, password, and config references

User home directories are never trusted for privileged operations.

---

### Process Validation

Before any operation is performed, the process is verified:

- `/proc/<pid>/exe` must match Redis binary
- Process owner must match the cPanel account
- Command line must reference expected config file

Stale or invalid PID files are automatically detected and cleaned.

---

### Safe Configuration System

Redis configuration is generated from a strict allowlist:

- `maxmemory`
- `maxmemory-policy`
- `timeout`
- persistence toggle

Arbitrary directives are never accepted from user input.

---

### CSRF Protection

All state-changing actions:

- Require POST requests
- Require valid CSRF tokens
- WHM tokens are session-bound

---

### Command Execution Safety

- No shell string concatenation
- All commands executed via `proc_open()` with argument arrays
- Redis CLI restricted to allowlisted commands

---

### File Safety

- No world-writable files
- Config files: `0640`
- Secrets and license files: `0600`
- Atomic file writes used for all sensitive data

---

### License System

- License keys stored outside source code
- Validation results cached locally
- Grace period allows continued operation during temporary outages
- License checks enforced in both WHM and cPanel contexts

---

### Audit Logging

Administrative actions are logged with:

- timestamp
- actor (WHM/cPanel user)
- action performed
- target account
- result status

---

## Contact

For support: support@underhost.com  
For security disclosures: security@underhost.com
