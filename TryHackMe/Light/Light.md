# 📌 Challenge Info

- **CTF Name:** TryHackMe
- **Challenge Name:** Light
- **Category:** Database Exploit
- **Points: 90**
- **Difficulty:** Beginner

# 🧠 Challenge Description

Light is a beginner-friendly room on TryHackMe that introduces users to basic SQL injection techniques. Through a simple login challenge, you'll explore how improper input handling can expose vulnerabilities in web applications. Great for those starting out in web exploitation!

# 🗃️ Files Provided

- **Port:** 1337
- **Username:** smokey

# 🌐 Challenge Setup

## **Tools Used:**

- nmap (port scanning)
- netcat (connecting to service)
- john the ripper (password cracking)
- CyberChef (decoding attempts)

## **Environment:**

- Local Kali Linux VM and THM target machine.

# 🔍 Initial Recon

Before starting the challenge, I was given the machine's IP address, the service port (1337), and a username (smokey). I scanned the IP address with `nmap` to check for any other services — only SSH was found, which wasn’t needed for this challenge. After that, I connected directly to the service using `netcat`, and found a login prompt.

# 🛠️ Exploitation / Solution

## 1. First Login

- I connected to the machine on try hack me via netcat.
- I was presented with a login portal on my command line to the database.
- I then entered the given username `smokey`, which produced a value on the screen.
- At first I suspected some sort of encoding, so I tried decoding it with CyberChef but no luck.

## 2. Finding out the Encoded Value

- I saved the given "password" into a text file named `password.txt` to come back to if i had any light bulbs go off.
- Decided to use John the Ripper on the file but, it hinted that the content could be UTF-8 encoding.
- I then attempted further decoding with CyberChef, but still didn't retrieve anything useful so, i stopped that there.

## 3. Trying SQL Injection

- Attempted SQL queries manually through netcat:
    - Basic inputs like `select from *` caused errors (bad syntax).
    - Tried using `' OR 1=1` and variations, leading to different errors.
    - Experimented with `' OR 1=1 --` which gave new error messages.
    - After researching SQL payloads, I found a working query:

```sql
' UNION SELECT null, table_name FROM information_schema.tables --
```

- Initially struggled because the server restricted certain characters, but after testing different versions, I retrieved the admin's username and part of the flag.

## 4. Finding the Username's Password

- I explored the database schema further and its columns to see if there was any other data.
- I found an `id` column and retrieved its data.
- I made a query to filter the password table based on the `id`, which finally revealed the complete password for `smokey` and allowed me to get the final flag.

# 🏴 Flag

> THM{SQLit3_InJ3cTion_is_SimplE_nO?}
> 

# 🧪 Tools Used

- **nmap** — Scanned IP address to discover open ports/services.
- **netcat** — Connected to the service manually.
- **john the ripper** — Analyzed the provided encoded password.
- **CyberChef** — Attempted various decoding methods.
- **SQL Injection payload lists** — Helped craft injections.

# 📝 Notes / Lessons Learned

- SQL Injection requires creativity, especially when the environment restricts certain characters.
- It's good practice to save any outputs like hashes or encoded data immediately into a file.
- Testing payloads manually teaches a lot more than just copy-pasting.
- Always explore the database structure (information schema) carefully if you have injection access.

# 📷 Screenshots (Optional)
