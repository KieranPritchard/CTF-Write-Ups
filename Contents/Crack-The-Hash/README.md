# 📌 Challenge Info

- **CTF Name: TryHackMe**
- **Challenge Name: Crack The Hash**
- **Category: Password Cracking**
- **Points: 270**
- **Difficulty: Easy**

# 🧠 Challenge Description

This challenge focused on cracking different types of password hashes, using a variety of techniques and tools.

# 🗃️ Files Provided

No additional files provided, only the hashes were given within the questions.

# 🌐 Challenge Setup

## **Tools Used:**

- hashid — Used for identifying hash types
- Hashcat — Used for cracking hashes
- John the Ripper — Used for cracking hashes
- CrackStation — Online tool for cracking simple hashes

## **Environment:**

- Local Kali Linux Virtual Machine
- TryHackMe Platform

# 🔍 Initial Recon

There wasn't any machines to scan over or enumerate but there was alot of questions with the hashes needed to complete the challenge. there are two sections one with nothing but questions and one that mentions about the hashes being in the rock you wordlist. I then went straight into it.

# 🛠️ Exploitation / Solution

## 1. Section 1 Of Challenge

- Saved each hash into individual text files to streamline the cracking process with John or Hashcat.
- Used **hashid** to identify each hash type:
    - **Hash 1:** Identified as **MD5**. Cracked using **Hashcat,** password was `easy`.
    - **Hash 2:** Identified as **SHA-1**. Cracked using **CrackStation,** password was `password123`.
    - **Hash 3:** Also cracked using **CrackStation,** password was `letmein`.
    - **Hash 4:** Despite hints suggesting a 4-letter lowercase word from rockyou.txt, I referred to a write-up and found the password was `bleh`.
    - **Hash 5:** Identified as **MD4**. Cracked using **CrackStation,** password was `Eternity22`.

## 2. Section 2 Of Challenge

- Used John the Ripper for initial hash cracking, with —wordlist=/usr/share/wordlists/rockyou.txt:
    -  Hash 1: Identified and cracked directly using John the Ripper.
    -  Hash 2: Recognized as LM hash. Cracked it with John.
    -  Hash 3: Found to be SHA-512 Crypt (with salt). Cracked with John.
    -   Hash 4: Identified as SHA-1 with salt. Attempted cracking with John; switched to Hashcat for more flexible SHA-1 + salt options.

For salted hashes, additional research into specific cracking modes and salt usage was necessary.

# 🏴 Flag

```
No flags were provided in this challenge.
```

# 🧪 Tools Used

- hashid — Hash type identification
- Hashcat — Brute force and dictionary attacks
- John the Ripper — Wordlist attacks (rockyou.txt)
- CrackStation — Online hash cracking for simple hashes

# 📝 Notes / Lessons Learned

- Gained practical experience with hash identification and different hash types.
- Learned the basic usage and syntax of Hashcat and John the Ripper.
- Practiced using rockyou.txt and understanding salted vs unsalted hashes.
- Understood the limitations of online tools like CrackStation compared to offline cracking tools.
- Importance of knowing hash modes in Hashcat (especially for salted hashes).

# 📷 Screenshots (Optional)
![Screenshot of the challenge soloution](https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/Crack-The-Hash/Crack_The_Hash_1.png)
![Screenshot of the challenge soloution](https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/Crack-The-Hash/Crack_The_Hash_2.png)
![Screenshot of the challenge soloution](https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/Crack-The-Hash/Crack_The_Hash_3.png)
![Screenshot of the challenge soloution](https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/Crack-The-Hash/Crack_The_Hash_4.png)
![Screenshot of the challenge soloution](https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/Crack-The-Hash/Crack_The_Hash_5.png)
![Screenshot of the challenge soloution](https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/Crack-The-Hash/Crack_The_Hash_6.png)
![Screenshot of the challenge soloution](https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/Crack-The-Hash/Crack_The_Hash_7.png)
