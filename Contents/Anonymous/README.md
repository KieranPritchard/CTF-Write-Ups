# 📌 Challenge Info

- **CTF Name: TryHackMe**
- **Challenge Name:** Anonymous
- **Category:** Linux
- **Points: 210**
- **Difficulty: Medium**

# 🧠 Challenge Description

Not the hacking group

# 🗃️ Files Provided

None

# 🌐 Challenge Setup

## Tools Used:
- nmap — port scanning & service/version enumeration
- ftp — interact with the FTP server
- nc (netcat) — listener / networking
- find — search filesystem for SUID binaries
- GTFOBins — SUID exploitation reference
- PentestMonkey reverse-shell cheat sheet

## Environment:
TryHackMe virtual machine (via VPN connection)

# 🔍 Initial Recon

I deployed the machine to obtain the target IP, then ran nmap to identify open services. The scan showed:

- FTP on port 21
- SSH on port 22
- NetBIOS-SSN on port 139
- Microsoft-DS on port 445

A version scan confirmed SMB-related services on 139/445. 


# 🛠️ Exploitation / Solution

## Step One — FTP Enumeration
- Connected to FTP and tried the common anonymous login: username: anonymous, password: password. The login succeeded.
- In the FTP root there was a folder “scripts” containing:
  - clean.sh — cleanup script
  - removed_files.log — empty log file but timestamp updated
  - to-do.txt — hinting SSH credentials are not safe
- Tried the FTP credentials on SSH. unfortunately they did not work.

## Step Two — Abusing a Cron Job

- Noticed removed_files.log timestamp changed often → suspected a cron job executes clean.sh.
- At this point I was stuck because i knew there must of been a way to spawn a shell here, so I checked a write-up which introduced me to PentestMonkey’s reverse shell one-liners.
- I edited clean.sh locally to include a reverse-shell payload, uploaded it back to FTP (so the cron job would run it).
- Started a netcat listener on my attacking machine and waited. When the cron job executed the modified clean.sh, I received a reverse shell as the target user which i intercepted with nmap.

Step Three — Privilege Escalation
- Found the user flag in the user home directory.
- Enumerated for SUID binaries using this script: `find / -type f -perm -04000 -ls 2>/dev/null`
- Identified env as SUID and checked GTFOBins for exploitation methods.
- Used the GTFOBins technique to spawn a root shell: `./env /bin/sh -p`
- With the root shell, read the root flag in /root.

# 🏴 Flag

> User Flag: 90d6f992585815ff991e68748c414740
> Root Flag: 4d930091c31a622a7ed10f27999af363

# 🧪 Tools Used

- nmap
- ftp / lftp (optional)
- nc (netcat)
- find
- GTFOBins (https://gtfobins.github.io)
- PentestMonkey reverse shell cheat sheet (http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet)

# 📝 Notes / Lessons Learned

- File timestamps and logs often reveal scheduled tasks (cron jobs).
- When a script is run by a scheduled task, modifying that script can allow command execution (if you have write access).
- I got stuck initially but referencing a write-up pointed me towards PentestMonkey reverse shells, which are now a go-to resource.

# 📷 Screenshots

<img src="https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/Anonymous/Anoymous_Screenshot_1.png">
<img src="https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/Anonymous/Anoymous_Screenshot_2.png">
<img src="https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/Anonymous/Anoymous_Screenshot_3.png">
<img src="https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/Anonymous/Anoymous_Screenshot_4.png">
<img src="https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/Anonymous/Anoymous_Screenshot_5.png">
<img src="https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/Anonymous/Anoymous_Screenshot_6.png">
<img src="https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/Anonymous/Anoymous_Screenshot_7.png">
<img src="https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/Anonymous/Anoymous_Screenshot_8.png">
<img src="https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/Anonymous/Anoymous_Screenshot_9.png">
<img src="https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/Anonymous/Anoymous_Screenshot_10.png">
