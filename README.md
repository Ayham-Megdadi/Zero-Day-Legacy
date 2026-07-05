<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=30&pause=1000&color=FF0000&center=true&vCenter=true&width=800&lines=Zero-Day+Legacy;Boot-to-Root+CTF+Lab+Machine;Royal+Health+Hospital+%E2%80%94+Vulnerable+Web+App;Graduation+Project+%7C+Grade%3A+97%25+%F0%9F%8F%86" alt="Typing SVG" />

<br/>

![CTF](https://img.shields.io/badge/Type-Boot--to--Root%20CTF-red?style=for-the-badge&logo=hackthebox)
![Platform](https://img.shields.io/badge/Platform-VirtualBox-blue?style=for-the-badge&logo=virtualbox)
![OS](https://img.shields.io/badge/OS-Ubuntu%2020.04%20LTS-orange?style=for-the-badge&logo=ubuntu)
![Stack](https://img.shields.io/badge/Stack-Apache%20%2B%20PHP%20%2B%20MySQL-green?style=for-the-badge&logo=php)
![Grade](https://img.shields.io/badge/Grade-97%25%20%F0%9F%8F%86-gold?style=for-the-badge)
![University](https://img.shields.io/badge/ANU-Graduation%20Project-purple?style=for-the-badge)
![Bilingual](https://img.shields.io/badge/Bilingual-AR%20%2F%20EN-teal?style=for-the-badge)
![Ethical](https://img.shields.io/badge/Use-Educational%20%26%20Ethical%20Only-lightgrey?style=for-the-badge)

<br/>

> **Graduation Project — Ajloun National University (ANU)**  
> Faculty of IT — Cybersecurity and Cloud Computing | Academic Year 2025–2026  
> **🏆 Highest Grade in the University: 97%**

</div>

---

## 📖 Overview

**Zero-Day Legacy** is a realistic, intentionally vulnerable **Boot-to-Root CTF (Capture The Flag)** lab machine developed as a graduation project at **Ajloun National University**. It simulates a hospital management system — **Royal Health Hospital** — containing a complete real-world attack chain across multiple vulnerability classes.

The attacker takes the role of a patient who cannot afford a hospital bill and decides to hack the system to delete the invoice. Starting from the internal network, the attacker must chain 17 steps from reconnaissance to full root compromise.

> ⚠️ **This system is intentionally vulnerable for cybersecurity education. All vulnerabilities are by design. For academic use only. Never deploy on a public-facing server.**

---

## 🎯 Attack Scenario

> *A patient at Royal Health Hospital receives an invoice he cannot afford. Instead of paying, he connects to the hospital's internal network and begins hacking the system — escalating from a web vulnerability to full root access.*

### Attack Chain (17 Steps)

| # | Action | Tool / Method | Outcome |
|---|--------|--------------|---------|
| 1 | Network Discovery | `netdiscover` | Find hospital VM IP |
| 2 | Port Scan | `nmap -sV <IP>` | Port 80 (HTTP) + Port 22 (SSH) open |
| 3 | Web Recon | `dirb` / `gobuster` | Find `admin.php` (403), `robots.txt` |
| 4 | Login as Patient | Browser | See unpaid invoice → motivation |
| 5 | SQL Injection | `' OR role='nurse' --` on `login.php` | Login as nurse account |
| 6 | XSS Injection | `nurse_messages.php` → JS payload | Stored XSS in messages |
| 7 | Auto-Reply Trigger | PHP auto-inserts admin reply | XSS echoed back to nurse page |
| 8 | Cookie Theft | `document.cookie` → netcat listener | Steal admin session cookie |
| 9 | Session Hijack | Set cookie in browser | Access admin dashboard |
| 10 | Delete Invoice | `admin_invoices.php` (GET, no CSRF) | Invoice deleted from DB |
| 11 | Find SSH Credentials | `admin_backup.php` | `user1 / Adm1n#H0sp` |
| 12 | SSH Login | `ssh user1@<IP>` | Low-privilege shell |
| 13 | Find Hash File | `/home/user1/crack-user2-hash.txt` | MD5 hash of user2 password |
| 14 | Crack Hash | `hashcat` / `john` / CrackStation | user2 plaintext password |
| 15 | Switch User | `su - user2` | Shell as user2 |
| 16 | Privilege Escalation | **CVE-2021-3493** (EDB-49655) | Root shell |
| 17 | Delete Target File | `rm /var/backups/hospital/invoices_backup.sql` | **🚩 CTF SOLVED** |

---

## 🔓 Vulnerability Specifications

| # | Vulnerability | Location | CWE / CVE |
|---|--------------|----------|-----------|
| V1 | SQL Injection | `login.php` + `loginadmin.php` | CWE-89 |
| V2 | Stored XSS | `nurse_messages.php` → `admin_messages.php` | CWE-79 |
| V3 | Session Hijacking | Admin cookie theft via XSS | CWE-384 |
| V4 | Missing CSRF Protection | `admin_invoices.php` delete via GET | CWE-352 |
| V5 | Credential Exposure | `admin_backup.php` SSH creds in UI | CWE-312 |
| V6 | Plaintext Passwords | MySQL `users` table | CWE-256 |
| V7 | Privilege Escalation | Linux kernel — Ubuntu OverlayFS | CVE-2021-3493 |
| V8 | Weak Hash (MD5) | `/home/user1/crack-user2-hash.txt` | CWE-328 |

> All vulnerabilities are **intentional and serve a specific educational purpose** in the CTF attack chain.

---

## 🛠️ Technology Stack

| Layer | Technology | Version |
|-------|-----------|---------|
| OS | Ubuntu LTS | 20.04.5 |
| Web Server | Apache | 2.4.x |
| Language | PHP (no frameworks) | 7.4 |
| Database | MySQL | 8.0.x |
| Frontend | HTML / CSS / JS (custom) | — |
| VM Platform | VirtualBox | — |
| Network | Bridged Adapter (Static IP) | — |
| Auto-Reset | Cron job every 90 minutes | — |

---

## 🖥️ VM Specifications

```
OS:        Ubuntu 20.04.5 LTS
vCPU:      1
RAM:       1 GB
Storage:   2 GB
Network:   Bridged Adapter (gets real LAN IP)
Services:  Apache (80) + OpenSSH (22) + MySQL (3306 local only)
Auto-Reset: Every 90 minutes (cron job restores DB + target file)
```

---

## ⬇️ Download

<div align="center">

[![Download VM](https://img.shields.io/badge/⬇️%20Download%20VM%20(.ova)-Google%20Drive-blue?style=for-the-badge&logo=google-drive)](https://drive.google.com/file/d/1l3ycTob6W0LsjWuNfo0qi7RwDJh32q8J/view?usp=sharing)

</div>

**Setup Instructions:**
1. Download the `.ova` file from the link above
2. Import into VirtualBox: `File → Import Appliance`
3. Set Network to **Bridged Adapter**
4. Start the VM — Apache and MySQL auto-start on boot
5. Run `netdiscover` from your attacker machine to find the IP
6. Begin your attack from `http://<IP>`

---

## 📁 Documentation

All project documentation is available in the [`/docs`](./docs/) folder:

| Document | Description |
|----------|-------------|
| [`PRD — Zero-Day Legacy v2.pdf`](./docs/) | Full Project Requirements Document |
| [`Penetration Test Report.pdf`](./docs/) | Complete pentest report of the machine |

---

## 👥 Development Team

<div align="center">

| # | Name | ID | Role |
|---|------|----|------|
| 1 | **Ayham Megdadi** | 202220116 | Project Lead — Web App & Attack Chain Design |
| 2 | **Ibrahim Onizat** | 202220363 | Web Development & Vulnerability Integration |
| 3 | **Manar Hussein** | 202220241 | Database Design & Seed Data |
| 4 | **Amira Freihat** | 202220520 | ERD + Schema + VM Deployment |
| 5 | **Salsabeel Abu Hawwa** | 202220148 | LAMP Stack Setup & Auto-Reset Mechanism |

**Supervisor:** Dr. Mohammad Al-Sawah  
**University:** Ajloun National University (ANU)  
**Faculty:** IT — Cybersecurity and Cloud Computing  
**Academic Year:** 2025–2026

</div>

---

## 🏆 Academic Achievement

<div align="center">

```
╔══════════════════════════════════════════════════════╗
║      🏆 HIGHEST GRADE IN THE UNIVERSITY: 97%        ║
║                                                      ║
║   Ajloun National University — Graduation Project    ║
║   Faculty: IT / Cybersecurity & Cloud Computing      ║
║   Academic Year: 2025–2026                           ║
╚══════════════════════════════════════════════════════╝
```

</div>

---

## ⚖️ Ethical & Legal Disclaimer

> This project is developed **exclusively for academic and educational purposes** as a graduation project at Ajloun National University.

- All vulnerabilities are **intentional and controlled**
- The system is designed to run in an **isolated VirtualBox environment on a local network**
- **NEVER deploy on a public internet-facing server**
- All patient data is **fictional and generated for the CTF**
- By using this machine, you agree to use it only in **authorized, controlled environments for educational purposes**

---

<div align="center">

*Developed with ❤️ by the Zero-Day Legacy Team — ANU 2025–2026*  
*⭐ Star this repo if you found it useful!*

</div>
