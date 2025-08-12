# 📌 Challenge Info

- **CTF Name: Try Hack Me**
- **Challenge Name: Agent Sudo**
- **Category: Web Application, Windows, Privalge Escalation**
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

- I opened the web page on the ip address and was greeted with a message from a person called: “Agent R”.
- In response to this i then fired up gobuster on the webpage. There was nothing else i could use
- I then googled about changing user agents because the question says about redirecting.
- I then used burp suite to catch a request from the website to rename the user agent header to another agents messages. I detucted that if agent r was called that because the agents were all letters of the alphabet. limiting me to at least 25 tries before i should try something else.
- I tryed it a couple of times before coming a across a interesting header in the http response pointing to a php page with a possible message.
- I went to the page and found out that the real name of agent c is chris. it also mentions he needs to change his password.

## 2. Finding Credentials:

- i then used hydra with the username chris and the rockyou.txt wordlist to crack the password. after the cracking was completed it revealed the password was crystal.
- I logged in and downloaded three files from the FTP server.
- The text file i downloaded made refrence to stegongraphy being used to hide things in another one of the files.
- This was where i found a hidden zip file in one of the photos. i converted the zip file which was password locked to a format john the ripper could crack. I cracked the password and got the word alien.
- I got the steg password from the file and converted it from base 64 and got arena51. I used it to extract with steghide agent J’s name and password.

## 3. Accessing the remote computer

- I used the credentials to sign into SSH. I then went and found the user flag quite easily and noticed a photo file.
- I used secure copy to transfer the photo to my kali linux virtual machine. I opened it and found it was a photo of the roswell alien autospy.
- I then listed the sudo privailages and first checked gtfoblins but they didnt have anything i could use. I then found on exploit db a exploit that i could use under: CVE-2019-14287
- I then used it to get root privalages and then i found the root flag

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

