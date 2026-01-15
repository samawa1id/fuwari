---
title: EYCC 2025 — Forensics Challenges
published: 2025-09-07
pinned: false
description: a write-up for EYCC's Forensics challenges
tags: [DFIR, CTF, Write-up, EYCC]
category: Write-ups
author: 0xSky
draft: false
---
# EYCC 2025 — Forensics Challenges

![Forensics Banner](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*qQQA1m3ijnyEBYMm.jpg)

Hi there! This write-up covers the _Egyptian Youth Cybersecurity Competition (EYCC)_ Forensics challenges that I managed to solve, with the steps taken to find each flag.

Let’s get started!

---

## First Challenge: Paper Trail

We were given a PDF file named **secret.pdf**, which appeared completely blank.  
I checked its metadata using **exiftool** and immediately found the flag.

![Exiftool Output](https://miro.medium.com/v2/resize:fit:874/format:webp/1*1yjP8tz67E7BdityMucyEg.png)

---

## Second Challenge: Fractured Memory

We were given a password-protected ZIP file named **CUNTISSIMO**.

First, I created a hash of the ZIP password using `zip2john`:

```bash
zip2john CUNTISSIMO > hash.txt
````

Then I cracked the password using **JohnTheRipper**:

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

John successfully cracked the password: **123456789**

After unzipping the archive, a file named **CUNTISSIMO** was extracted.
I examined it with the `file` command and found that it was a JPEG, but opening it showed that it was corrupted.

To investigate, I checked the file in a hex editor and noticed the header was incorrect:

![Hex Header](https://miro.medium.com/v2/resize\:fit:1288/format\:webp/1*7KV4o-OsGUZqo-d5wsKWvQ.png)

The correct JPEG header should be:

```
FF D8 FF E0
```

I fixed the header manually, and the image was successfully repaired:

![Repaired Image](https://miro.medium.com/v2/resize\:fit:1400/format\:webp/1*iITLsb7Ns8ksZ0tk6OEd1Q.jpeg)

The patched image revealed an encoded string that looked like **Base32**, so I decoded it using [DCode](https://dcode.fr).

![Decoded Base32](https://miro.medium.com/v2/resize\:fit:1400/format\:webp/1*f8tgujW7cbCOBrw_jUJ8wQ.png)

And here’s the flag!

---

That was all! Don’t forget to check my other write-ups for the **Web, Crypto, and OSINT** challenges.
