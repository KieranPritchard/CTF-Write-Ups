# 📌 Challenge Info

- **CTF Name: Try Hack Me**
- **Challenge Name:** Bounty Hunter
- **Category: Web App**
- **Points: 150**
- **Difficulty: Easy**

# 🧠 Challenge Description

You talked a big game about being the most elite hacker in the solar system. Prove it and claim your right to the status of Elite Bounty Hacker!

# 🗃️ Files Provided

No files were provided.

# 🌐 Challenge Setup

## **Tools Used:**

- **nmap** — Port scanning and service detection
- **gobuster** — Directory brute-forcing on the web server
- **hydra** — Brute-force login credentials
- **ftp / ssh** — File access and remote login
- **GTFOBins** — Privilege escalation reference

## **Environment:**

- Local Kali linux virtual machine.

# 🔍 Initial Recon

Firstly, I scanned for services with nmap. doing this found three services: ftp on port 21; ssh on port 20; and http on port 80.

# 🛠️ Exploitation / Solution

## 1. Exploration

- I went to the website on the network and was meet with a landing page.
- There were no links to other pages so, i decided to use gobuster to find any more pages. i found a page called home and another page.
- After this i thought to look at what is on the ftp server. I opened the ftp server to a login form. I tried name as the user name and a message saying “only for anonymous”.
- I signed into ftp with anonymous as my user name and listed files, i found two files and downloaded them.

## 2. Exploitation

- Found out one was a message written by someone called lin.
- The other contained a list of passwords.
- I then used hydra with the password list and “lin” as the username to find out the password to the ssh client.
- the password was “RedDragonSyndicate” and i signed onto ssh using it.

## 3. Privilege escalation.

- I listed sudo privileges and then looked on gtoblins for privilege escalation commands.
- Used command to escalate privalges and gain root.
- found the user flag and navigated to root to find the root flag.

# 🏴 Flag

```
THM{CR1M3_SyNd1C4T3}
THM{80UN7Y_h4cK3r}
```

# 🧪 Tools Used

- **nmap** — Discovered open ports and running services
- **gobuster** — Enumerated hidden web directories
- **hydra** — Brute-forced SSH password
- **ftp/ssh** — Connected to services and navigated the file system
- **GTFOBins** — Found privilege escalation vectors

# 📝 Notes / Lessons Learned

- Anonymous FTP access can expose sensitive information.
- Always check for reused usernames in file contents — they often become SSH usernames.
- Directory brute-forcing is essential when a website has little to no navigation.
- GTFOBins is a key resource for privilege escalation when you have limited sudo rights.

# 📷 Screenshots (Optional)
![Screenshot of the challenge soloution](https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/RootMe/Bounty_Hunter_Screenshot_1.png)
![Screenshot of the challenge soloution](https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/RootMe/Bounty_Hunter_Screenshot_2.png)
![Screenshot of the challenge soloution](https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/RootMe/Bounty_Hunter_Screenshot_3.png)
![Screenshot of the challenge soloution](https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/RootMe/Bounty_Hunter_Screenshot_4.png)
![Screenshot of the challenge soloution](https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/RootMe/Bounty_Hunter_Screenshot_5.png)
![Screenshot of the challenge soloution](https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/RootMe/Bounty_Hunter_Screenshot_6.png)
![Screenshot of the challenge soloution](https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/RootMe/Bounty_Hunter_Screenshot_7.png)
![Screenshot of the challenge soloution](https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/RootMe/Bounty_Hunter_Screenshot_8.png)
![Screenshot of the challenge soloution](https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/RootMe/Bounty_Hunter_Screenshot_9.png)
