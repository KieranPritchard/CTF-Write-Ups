# 📌 Challenge Info

- **CTF Name: TryHackMe**
- **Challenge Name: OhSINT**
- **Category: OSINT**
- **Points: 0**
- **Difficulty: Easy**

# 🧠 Challenge Description

What information can you possible get with just one image file?

**Note:** This challenge was updated on 2024-02-01. If you are following any older walkthroughs, expect a small change. Additionally, the file is also available on the AttackBox, under the `/Rooms/OhSINT` directory.

# 🗃️ Files Provided

- An image of the Windows XP wallpaper

# 🌐 Challenge Setup

## **Tools Used:**

- **ExifTool** — for extracting metadata from images
- **Google** — for OSINT investigations and lookups
- **Wigle.net** — for BSSID/SSID lookup and geolocation

## **Environment:**

- TryHackMe AttackBox

# 🔍 Initial Recon

I first downloaded the image to take a closer look at it. on its own it looks like a random image of the windows wallpaper for windows XP. although as i have learned from watching films and stuff theres probably something more to it so thats what i did. 

# 🛠️ Exploitation / Solution

## 1. Looking At the photo

- I used **ExifTool** to extract metadata from the image. This revealed useful information such as GPS data and copyright information.
- A key piece of data found was a copyright tag: **"OWoodflint"**.
- I Googled this name, which led me to a **GitHub repository** containing a project called *People Finder*. The repository also contained a **WordPress website link** and an **email address**, answering two questions in the TryHackMe challenge.

## 2. Exploring Further

- Visiting the WordPress site revealed that the individual was located in **New York**, which answered another question on TryHackMe.
- While browsing the site, I also noted a few potential clues hidden in the HTML source code (more on that later).

## 3. Looking on x

- A Google search for "OWoodflint" revealed an **X (Twitter)** account.
- The profile image (avatar) was a **cat**, which answered the corresponding challenge question.
- One of the tweets from the account mentioned a **BSSID**.
- I used **wigle.net** to search for the BSSID and successfully obtained the corresponding **SSID** and **location name**.

## 4. Finding the password

- I returned to the WordPress site and viewed the **page source**.
- Hidden in the HTML was a paragraph element that didn’t appear in the rendered page.
- Copying and pasting that hidden text into TryHackMe revealed it to be the **final flag**, successfully completing the challenge.

# 🏴 Flag

```
None
```

# 🧪 Tools Used

- **ExifTool** — For extracting metadata from the image
- **CyberChef** — (if used for decoding any hidden strings)
- **Wigle.net** — To identify SSID/location from BSSID
- **Google/X** — For OSINT sleuthing and locating online accounts

# 📝 Notes / Lessons Learned

- Always check image metadata — you never know what's hidden in plain sight.
- GitHub and social media can leak a lot more personal info than you'd expect.
- Even seemingly harmless sites can contain hidden content in the source code.
- OSINT is powerful — and sometimes terrifying.

# 📷 Screenshots (Optional)
![Screenshot of the challenge soloution](https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/OhSINT/OhSINT_1.png)
![Screenshot of the challenge soloution](https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/OhSINT/OhSINT_2.png)
![Screenshot of the challenge soloution](https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/OhSINT/OhSINT_3.png)
![Screenshot of the challenge soloution](https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/OhSINT/OhSINT_4.png)
![Screenshot of the challenge soloution](https://github.com/KieranPritchard/CTF-Write-Ups/blob/main/TryHackMe/OhSINT/OhSINT_5.png)
