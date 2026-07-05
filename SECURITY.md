# Security Policy

## ⚠️ Intended Vulnerabilities

**Zero-Day Legacy** is an intentionally vulnerable **Boot-to-Root CTF lab machine** designed for cybersecurity education.

The vulnerabilities included in this project are **intentional** and are required to complete the attack chain. They are **not security bugs**.

Please **do NOT report** the following as vulnerabilities:

* SQL Injection (`login.php`, `loginadmin.php`)
* Stored XSS (`nurse_messages.php`)
* Session Hijacking via cookie theft
* Missing CSRF protection on invoice deletion
* Credential exposure (`admin_backup.php`)
* Plaintext passwords stored in the database
* Weak MD5 password hashing
* Linux privilege escalation via **CVE-2021-3493**

These behaviors are part of the intended learning experience.

---

## Reportable Issues

Please report only issues that are **not intentionally vulnerable**, such as:

* VM boot failures
* Broken setup or deployment instructions
* Corrupted or missing files
* Reset script failures
* Documentation errors
* Any issue preventing the lab from functioning as intended

---

## Responsible Use

This machine must only be used in:

* Isolated VirtualBox environments
* Local networks
* Authorized educational or research environments

**Never deploy this machine on a public-facing server.**

---

## Contact

For questions about the project or to report non-intended issues, please contact the project team. Do not open a public GitHub issue for security vulnerabilities.

--

## ⏱ Response Time

We aim to respond to all valid security reports within 48 hours and will prioritize fixing confirmed issues as quickly as possible.
