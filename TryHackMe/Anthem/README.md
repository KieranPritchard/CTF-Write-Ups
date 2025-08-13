# 📌 Challenge Info

- **CTF Name:** Try Hack Me
- **Challenge Name:** Anthem
- **Category:** Web Application, Windows, Privilege Escalation
- **Points:** 150
- **Difficulty:** Easy

# 🧠 Challenge Description

Exploit a Windows machine in this beginner-level challenge.

# 🗃️ Files Provided

None

# 🌐 Challenge Setup

## **Tools Used:**

- **Nmap** — Network scanning to find open ports and services.
- **Gobuster** — Directory brute-forcing to find hidden paths.
- **Remmina** — RDP client to connect to the target’s desktop.

## **Environment:**

- **TryHackMe hosted VM** — Accessed through the provided IP address.

# 🔍 Initial Recon

I started the TryHackMe machine and performed an `nmap` scan:

- Port **80/tcp** — HTTP (Website)
- Port **3389/tcp** — RDP

Using `gobuster`, I discovered several interesting directories:

- `/sitemap`
- `/install` (potential CMS setup)

These immediately hinted at potential information disclosure and CMS exploitation opportunities.

# 🛠️ Exploitation / Solution

## 1. First Set of Tasks

- Checked `/robots.txt` and found a suspicious entry containing a password: **`UmbracoIsTheBest!`**
- The `/install` page revealed the CMS in use: **Umbraco**.
- The site’s main page showed the domain: **anthem.com**.
- On another page, I found a poem dedicated to the admin. Searching it on Google revealed it was “The Poem of Solomon Grundy,” giving me the probable admin username: **solomon**.

## 2. Searching for Flags

- Found the **first flag** on Jane Doe’s profile page.
- Discovered more flags in HTML source comments and `<meta>` tags.
- Attempted login to the Umbraco admin panel with `solomon:UmbracoIsTheBest!`, but no direct success on the CMS.
- Decided to attempt RDP login using the same credentials.

## 3. Remoting into the Desktop

- Used Remmina to RDP into the target as **solomon**.
- Found a text file on the desktop containing the **user flag**.
- Discovered an **Administrator** folder but could not access it with Solomon’s credentials.
- Located a hidden file named `backup`. Modified file permissions to grant myself read access.
- Inside was the **Administrator password**.
- Logged in via RDP as **Administrator**, navigated to the desktop, and retrieved the **root flag**.

# 🏴 Flags

```
THM{L0L_WH0_US3S_M3T4}
THM{G!T_G00D}
THM{L0L_WH0_D15}
THM{AN0TH3R_M3TA}
THM{N00T_NO0T}
THM{Y0U_4R3_1337}
```

# 🧪 Tools Used

- **Nmap** — Port scanning and service enumeration.
- **Gobuster** — Directory brute-forcing for hidden pages.
- **Remmina** — RDP access to the Windows desktop.

# 📝 Notes / Lessons Learned

- Always check `/robots.txt` — it can leak sensitive information like passwords.
- Poems, text, and other “fluff” content may be clues for usernames.
- Adjusting file permissions can be a quick privilege escalation method in misconfigured Windows systems.
- Even if a CMS login fails, credentials may still be valid for other services.

# 📷 Screenshots
