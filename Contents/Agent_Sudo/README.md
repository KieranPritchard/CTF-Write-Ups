# 📌 Challenge Info

- **CTF Name: Try Hack Me**
- **Challenge Name: Agent Sudo**
- **Category: Web Application**
- **Points: 150**
- **Difficulty: Easy**

# 🧠 Challenge Description

Exploit a Windows machine in this beginner level challenge.

# 🗃️ Files Provided

None

# 🌐 Challenge Setup

## **Tools Used:**

- **Nmap** — Port scanning & service enumeration
- **Gobuster** — Directory enumeration
- **Burp Suite** — Intercepting and modifying HTTP requests
- **Hydra** — Brute forcing login credentials
- **Steghide** — Extracting hidden data from images
- **John the Ripper** — Cracking password-protected archives
- **scp** — Securely copying files from remote host to local machine

## **Environment:**

- TryHackMe hosted target machine
- Kali Linux (attacker machine)

# 🔍 Initial Recon

I first deployed the machine to get the IP address that i then scanned and found three services running on them. I found on the IP address: FTP on port 21; SSH on port 22; and apache on port 80.

# 🛠️ Exploitation / Solution

## 1. First Look Through The Website

I opened the webpage on the provided IP address and was greeted with a message from a person called “Agent R”. In response, I fired up Gobuster on the webpage, as there was nothing else I could use.

I then searched Google for information on changing user agents, as the question mentions redirecting. I used Burp Suite to catch a request from the website and rename the user agent header to another agent’s message. I deduced that “Agent R” was called because the agents were all letters of the alphabet, limiting me to at least 25 tries before I should try something else.

I tried it a couple of times before coming across an interesting header in the HTTP response pointing to a PHP page with a possible message. I went to the page and found out that the real name of Agent C is Chris. It also mentions that he needs to change his password.

## 2. Finding Credentials:

I used Hydra with the username chris and the rockyou.txt wordlist to crack the password. After cracking, it revealed the password was crystal. I logged in and downloaded three files from the FTP server.

The text file I downloaded referenced steganography being used to hide something in another file. This led me to a hidden zip file in one of the photos. I converted the password-locked zip file to a format John the Ripper could crack. I cracked the password and got the word alien. I obtained the steganography password from the file and converted it from base 64, giving me arena51. I used it to extract J’s name and password from Steghide Agent.

## 3. Accessing the remote computer

I used the credentials to sign into SSH and easily found the user flag. I noticed a photo file. I used secure copy to transfer the photo to my Kali Linux virtual machine. I opened it and found it was a photo of the Roswell alien autospy.
I listed the sudo privileges and first checked gtfoblins, but they didn’t have anything I could use. I then found an exploit on exploit-db that I could use under CVE-2019-14287. I used the exploit to get root privileges and then found the root flag.

# 🏴 Flag

```
User Flag: b03d975e8c92a7c04146cfa7a5a313c7
Root Flag: b53a02f55b57d4439e3341834d70c062
```

# 🧪 Tools Used

- **Nmap** — Network scanning and service enumeration
- **Gobuster** — Directory brute forcing
- **Burp Suite** — Intercepting/modifying HTTP requests
- **Hydra** — Brute-forcing login credentials
- **Steghide** — Extracting hidden data from images
- **John the Ripper** — Cracking password-protected archives
- **scp** — Transferring files securely
- **Exploit-DB** — Finding privilege escalation exploits

# 📝 Notes / Lessons Learned

- Always check HTTP headers — sometimes the key is hidden in plain sight.
- Steganography is a common technique in CTFs; always inspect images for hidden files.
- Brute force attacks can be efficient if the username is known and password lists are small.
- Privilege escalation often comes down to misconfigurations, not just kernel exploits.

# 📷 Screenshots (Optional)
<img src="https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/Agent_Sudo/Agent_Sudo_Screenshot_1.png">
<img src="https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/Agent_Sudo/Agent_Sudo_Screenshot_2.png">
<img src="https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/Agent_Sudo/Agent_Sudo_Screenshot_3.png">
<img src="https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/Agent_Sudo/Agent_Sudo_Screenshot_4.png">
<img src="https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/Agent_Sudo/Agent_Sudo_Screenshot_5.png">
<img src="https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/Agent_Sudo/Agent_Sudo_Screenshot_6.png">
<img src="https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/Agent_Sudo/Agent_Sudo_Screenshot_7.png">
<img src="https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/Agent_Sudo/Agent_Sudo_Screenshot_8.png">
<img src="https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/Agent_Sudo/Agent_Sudo_Screenshot_9.png">
<img src="https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/Agent_Sudo/Agent_Sudo_Screenshot_10.png">
<img src="https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/Agent_Sudo/Agent_Sudo_Screenshot_11.png">
<img src="https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/Agent_Sudo/Agent_Sudo_Screenshot_12.png">
