# Contributing

Thank you for your interest in Zero-Day Legacy!

## What We Welcome

- Bug fixes in the auto-reset mechanism
- Improvements to the setup documentation
- Additional CTF hints or walkthrough guides
- Translations or UI improvements to the hospital web app
- New difficulty levels or challenge variants

## What We Do NOT Accept

- Patches that fix the **intentional vulnerabilities** — they are the CTF challenge
- Changes that break the 17-step attack chain
- Any code that introduces real malware or harmful exploits

## How to Contribute

1. Fork the repository
2. Create a branch: `git checkout -b feature/your-feature`
3. Make your changes and test the full attack chain still works
4. Open a Pull Request with a clear description

## Code Style

- PHP: no prepared statements on intentionally vulnerable pages (by design)
- All pages must support both Arabic and English
- Session variables: `$_SESSION['user_id']`, `['username']`, `['role']`

---

*Zero-Day Legacy Team — Ajloun National University 2025–2026*
