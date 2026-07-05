<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=32&pause=1000&color=FF0000&center=true&vCenter=true&width=900&lines=Zero-Day+Legacy;Boot-to-Root+CTF+Lab+Machine;Royal+Health+Hospital+%E2%80%94+Hack+the+System;Graduation+Project+%7C+Grade%3A+97%25+%F0%9F%8F%86" alt="Typing SVG" />

<br/>

![CTF](https://img.shields.io/badge/Type-Boot--to--Root%20CTF-red?style=for-the-badge&logo=hackthebox&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-VirtualBox-blue?style=for-the-badge&logo=virtualbox&logoColor=white)
![OS](https://img.shields.io/badge/OS-Ubuntu%2020.04%20LTS-orange?style=for-the-badge&logo=ubuntu&logoColor=white)
![Stack](https://img.shields.io/badge/Stack-Apache%20%2B%20PHP%20%2B%20MySQL-4F5D95?style=for-the-badge&logo=php&logoColor=white)
![Grade](https://img.shields.io/badge/Grade-97%25%20%F0%9F%8F%86-FFD700?style=for-the-badge)
![Bilingual](https://img.shields.io/badge/Bilingual-Arabic%20%2F%20English-teal?style=for-the-badge)
![Difficulty](https://img.shields.io/badge/Difficulty-Intermediate-yellow?style=for-the-badge)
![Ethical](https://img.shields.io/badge/Use-Educational%20Only-lightgrey?style=for-the-badge)

<br/>

> 🎓 **Graduation Project — Ajloun National University (ANU)**  
> Faculty of IT · Cybersecurity and Cloud Computing · Academic Year 2026  
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

---

## 🏥 The Target — Royal Health Hospital

A fully functional bilingual (Arabic/English) hospital management system with three user roles and a complete attack surface.

### Homepage

![Hospital Homepage](photos/01_hospital_homepage.png)

### Login page

![Login page](photos/02_patient_portal.png)

### Patient Portal

![Patient Portal](photos/02_patient_portal.png)

### Nurse Dashboard

![Nurse Dashboard](photos/03_nurse_dashboard.png)

### Admin Dashboard

![Admin Dashboard](photos/04_admin_dashboard.png)

### Admin Invoices

![Admin Invoices](photos/05_admin_invoices.png)

### Chat page

![Chat page](photos/09_admin_backup.png)

### Backup Page

![Backup Page](photos/09_admin_backup.png)

---

## 🎯 Attack Scenario

> *A patient at Royal Health Hospital receives an invoice he cannot afford.*  
> *He's connected to the hospital's internal network and decides to hack the system.*  
> *From there — the clock is ticking.*

---

## 🛠️ Technology Stack

| Layer | Technology | Version |
|-------|-----------|---------|
| OS | Ubuntu Server LTS (Focal Fossa) | 20.04.6 |
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
OS:          Ubuntu Server 20.04.6 LTS — kernel 5.4.x (vulnerable to CVE-2021-3493)
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
