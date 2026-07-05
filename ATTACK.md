<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=32&pause=1000&color=FF0000&center=true&vCenter=true&width=900&lines=Zero-Day+Legacy;Boot-to-Root+CTF+Lab+Machine;Royal+Health+Hospital+%E2%80%94+Hack+the+System;Graduation+Project+%7C+Grade%3A+97%25+%F0%9F%8F%86" alt="Typing SVG" />

--

### 🗺️ Attack Chain — 17 Steps

| # | Phase | Action | Tool | Outcome |
|---|-------|--------|------|---------|
| 1 | Recon | Network Discovery | `netdiscover` | Hospital VM IP found |
| 2 | Recon | Port Scan | `nmap -sV` | Port 80 + Port 22 open |
| 3 | Recon | Web Enumeration | `dirb` | `robots.txt` reveals admin paths |
| 4 | Recon | Login as Patient | Browser | Unpaid invoice → attack motivation |
| 5 | Exploit | SQL Injection | `' OR role='nurse' --` | Login as nurse **Amira** |
| 6 | Exploit | Stored XSS | JS payload via messages | XSS stored in database |
| 7 | Exploit | XSS Execution | Admin **AIMAS** opens messages | XSS fires in admin's browser |
| 8 | Exploit | Cookie Theft | `nc -lvnp 4444` | Admin session cookie captured |
| 9 | Exploit | Session Hijacking | Replace cookie in browser | Full admin access without password |
| 10 | Exploit | Delete Invoice | GET request (no CSRF) | Invoice deleted from DB |
| 11 | Pivot | Credential Exposure | `admin_backup.php` | `Ayham / Ibrahim@997` |
| 12 | Pivot | SSH Login | `ssh Ayham@<IP>` | Low-privilege shell |
| 13 | Pivot | Find Hash File | `/home/Ayham/crack-Manar-hash.txt` | MD5 hash of **Manar**'s password |
| 14 | Exploit | Crack the Hash | `hashcat` / CrackStation | Plaintext: `Salsbeel@2004` |
| 15 | Pivot | Switch User | `su - Manar` | Shell as **Manar** |
| 16 | PrivEsc | Privilege Escalation | CVE-2021-3493 (EDB-49655) | `root` shell — `uid=0` |
| 17 | Goal | Delete Target File | `rm /var/backups/hospital/invoices_backup.sql` | **🚩 CTF SOLVED** |

---

## 🔓 Vulnerability Specifications

| # | Vulnerability | Location | CWE / CVE | Severity |
|---|--------------|----------|-----------|----------|
| V1 | SQL Injection | `login.php` + `loginadmin.php` | CWE-89 | 🔴 Critical |
| V2 | Stored XSS | `nurse_messages.php` → `admin_messages.php` | CWE-79 | 🔴 High |
| V3 | Session Hijacking | Admin cookie theft via XSS | CWE-384 | 🔴 High |
| V4 | Missing CSRF Protection | `admin_invoices.php` delete via GET | CWE-352 | 🟠 Medium |
| V5 | Credential Exposure | `admin_backup.php` SSH creds in plaintext | CWE-312 | 🔴 High |
| V6 | Plaintext Passwords | MySQL `users` table — no hashing | CWE-256 | 🟠 Medium |
| V7 | Privilege Escalation | Linux kernel — Ubuntu OverlayFS | CVE-2021-3493 | 🔴 Critical |
| V8 | Weak Hash (MD5) | `/home/Ayham/crack-Manar-hash.txt` | CWE-328 | 🟠 Medium |

> All vulnerabilities are **intentional and serve a specific educational purpose** in the CTF attack chain.
