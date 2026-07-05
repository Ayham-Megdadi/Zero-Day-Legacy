<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=32&pause=1000&color=FF0000&center=true&vCenter=true&width=900&lines=Zero-Day+Legacy;Boot-to-Root+CTF+Lab+Machine;Royal+Health+Hospital+%E2%80%94+Hack+the+System;Graduation+Project+%7C+Grade%3A+97%25+%F0%9F%8F%86" alt="Typing SVG" />

<br/>

![CTF](https://img.shields.io/badge/Type-Boot--to--Root%20CTF-red?style=for-the-badge&logo=hackthebox&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-VirtualBox-blue?style=for-the-badge&logo=virtualbox&logoColor=white)
![OS](https://img.shields.io/badge/OS-Ubuntu-server%2020.04%20LTS-orange?style=for-the-badge&logo=ubuntu&logoColor=white)
![Stack](https://img.shields.io/badge/Stack-Apache%20%2B%20PHP%20%2B%20MySQL-4F5D95?style=for-the-badge&logo=php&logoColor=white)
![Grade](https://img.shields.io/badge/Grade-97%25%20%F0%9F%8F%86-FFD700?style=for-the-badge)
![Bilingual](https://img.shields.io/badge/Bilingual-Arabic%20%2F%20English-teal?style=for-the-badge)
![Difficulty](https://img.shields.io/badge/Difficulty-Intermediate-yellow?style=for-the-badge)
![Ethical](https://img.shields.io/badge/Use-Educational%20Only-lightgrey?style=for-the-badge)

<br/>

> 🎓 **Graduation Project — Ajloun National University (ANU)**  
> Faculty of IT · Cybersecurity and Cloud Computing · Academic Year 2025–2026  
> **🏆 Highest Grade in the University: 97%**

</div>

---

## 📖 Overview

**Zero-Day Legacy** is a realistic, intentionally vulnerable **Boot-to-Root CTF (Capture The Flag)** lab machine built as a graduation project at **Ajloun National University**. It simulates a complete hospital management system — **Royal Health Hospital** — containing a full real-world attack chain across multiple vulnerability classes.

The attacker plays the role of a **patient who cannot afford a hospital bill** and decides to hack the system from within the internal network. Starting with basic reconnaissance, the attacker must chain 17 steps from initial web access to full root compromise — mirroring a real-world penetration test.

> ⚠️ **This machine is intentionally vulnerable for cybersecurity education. All vulnerabilities are by design. Run only in an isolated local network. Never deploy on a public-facing server.**

---

## ⬇️ Download the Machine

<div align="center">

[![Download VM](https://img.shields.io/badge/⬇️%20Download%20VM%20(.ova)%20—%20Google%20Drive-4285F4?style=for-the-badge&logo=google-drive&logoColor=white)](https://drive.google.com/file/d/1l3ycTob6W0LsjWuNfo0qi7RwDJh32q8J/view?usp=sharing)

</div>

### Setup in 3 Steps

```bash
# 1. Import into VirtualBox
File → Import Appliance → select the .ova file

# 2. Set Network Adapter
Settings → Network → Adapter 1 → Bridged Adapter

# 3. Discover the machine IP from Kali Linux
sudo netdiscover
```

Open `http://<machine-IP>` in your browser and begin your attack.

---

## 🏥 The Target — Royal Health Hospital

A fully functional bilingual (Arabic/English) hospital management system with three user roles and a complete attack surface.

### Homepage

![Hospital Homepage](photos/01_hospital_homepage.png)

### Patient Portal — The Starting Point

![Patient Portal](photos/03_patient_portal.png)
*The attacker logs in as patient **Cyber** and finds an unpaid invoice of $300,000 — the motivation begins.*

### Nurse Dashboard

![Nurse Dashboard](photos/04_nurse_dashboard.png)
*Accessed via SQL Injection — full patient management, messaging, and scheduling.*

### Admin Control Panel

![Admin Dashboard](photos/05_admin_dashboard.png)
*Accessed via XSS → Session Hijacking — full control over invoices, nurses, patients, and backups.*

### Admin Invoices

![Admin Invoices](photos/06_admin_invoices.png)
*Invoice management with no CSRF protection — deletion via a simple GET request.*

### Backup Page — Credential Exposure

![Backup Page](photos/09_admin_backup.png)
*SSH credentials exposed in plaintext — a key pivot point in the attack chain.*

### Arabic Interface (RTL Support)

![Arabic UI](photos/02_hospital_homepage_ar.png)
*Full Arabic interface with RTL layout — all pages support both languages.*

### CTF Flag — Mission Complete

![CTF Flag](photos/15_ctf_flag.png)
*The final message after deleting `invoices_backup.sql` and achieving full root access.*

---

> 📄 **Full attack chain with all technical screenshots is documented in the Pentest Report → [`/docs/`](./docs/)**

---

## 🎯 Attack Scenario

> *A patient at Royal Health Hospital receives an invoice he cannot afford.*  
> *He's connected to the hospital's internal network and decides to hack the system.*  
> *From there — the clock is ticking.*

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

---

## 🛠️ Technology Stack

| Layer | Technology | Version |
|-------|-----------|---------|
| OS | Ubuntu LTS (Focal Fossa) | 20.04.5 |
| Web Server | Apache | 2.4.x |
| Language | PHP (no frameworks — intentional) | 7.4 |
| Database | MySQL | 8.0.x |
| Frontend | HTML / CSS / JS — custom, no Bootstrap | — |
| VM Platform | VirtualBox | — |
| Network Mode | Bridged Adapter (real LAN IP) | — |
| Auto-Reset | Cron job every 90 minutes | — |
| Bilingual | Full Arabic + English with RTL | — |

---

## 🖥️ VM Specifications

```
OS:          Ubuntu 20.04.5 LTS — kernel 5.4.x (vulnerable to CVE-2021-3493)
vCPU:        1
RAM:         1 GB
Storage:     2 GB
Network:     Bridged Adapter — gets real IP from local router
Services:    Apache (80) · OpenSSH (22) · MySQL (3306 — local only)
Auto-Reset:  Every 90 minutes — restores DB + target file automatically
Bilingual:   Arabic + English on all pages
```

---

## 📁 Documentation

| Document | Description |
|----------|-------------|
| [`Zero-Day-Legacy-PRD-v2.docx`](./docs/Zero-Day-Legacy-PRD-v2.docx) | Full Project Requirements Document — attack chain, DB design, VM config, vulnerability specs |
| [`Penetration-Test-Report.pdf`](./docs/Penetration-Test-Report.pdf) | Complete penetration test report by Cyber Company AIMAS — full technical findings with screenshots |

---

## 👥 Development Team

<div align="center">

| Name | LinkedIn |
|------|----------|
| **Ayham Megdadi** | [![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat&logo=linkedin)](https://www.linkedin.com/in/ayham-megdadi) |
| **Ibrahim Onizat** | [![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat&logo=linkedin)](https://www.linkedin.com/in/ibrahim-onizat) |
| **Manar Hussein** | [![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat&logo=linkedin)](https://www.linkedin.com/in/manar-hussein) |
| **Amira Freihat** | [![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat&logo=linkedin)](https://www.linkedin.com/in/amira-freihat) |
| **Salsabeel Abu Hawwa** | [![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat&logo=linkedin)](https://www.linkedin.com/in/salsabeel-abu-hawwa) |

**Supervisor:** Dr. Mohammad Al-Sawah  
**University:** Ajloun National University (ANU)  
**Faculty:** IT — Cybersecurity and Cloud Computing  
**Academic Year:** 2025–2026

</div>

---

## 🏆 Academic Achievement

<div align="center">

```
╔═══════════════════════════════════════════════════════════╗
║       🏆  HIGHEST GRADE IN THE UNIVERSITY: 97%           ║
║                                                           ║
║    Ajloun National University — Graduation Project        ║
║    Faculty of IT — Cybersecurity & Cloud Computing        ║
║    Academic Year: 2025–2026                               ║
╚═══════════════════════════════════════════════════════════╝
```

</div>

---

## ⚖️ Ethical & Legal Disclaimer

> This project was developed **exclusively for academic and educational purposes** at Ajloun National University.

- All vulnerabilities are **intentional and controlled by design**
- Run only in an **isolated VirtualBox environment on a local network**
- **NEVER deploy on a public internet-facing server**
- All patient data is **fictional and generated for the CTF**
- By using this machine, you agree to use it only in **authorized, controlled environments for educational purposes**

---

<div align="center">

*Built with ❤️ by the Zero-Day Legacy Team — ANU 2025–2026*  
*⭐ Star this repo if it helped you learn something new!*

</div>
