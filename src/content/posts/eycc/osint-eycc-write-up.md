---
title: EYCC 2025 — OSINT Challenges
published: 2025-09-07
pinned: false
description: a write-up for EYCC's OSINT challenges
tags: [OSINT, CTF, Write-up, EYCC]
category: Write-ups
author: 0xSky
draft: false
---
# EYCC 2025 — OSINT Challenges

![EYCC OSINT Banner](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*JfcZMzKKaKu0xOS9.jpg)

Hola! This write-up covers the _Egyptian Youth Cybersecurity Competition (EYCC)_ OSINT challenges that I solved with steps taken to find the flag.  

This was my first time exploring OSINT challenges, and I definitely enjoyed them!

---

## First Challenge: Phantom Employee

Our mission was to find the name of a fired employee and check their digital footprint to find the flag.  

We were given a link to the company’s website, which had an **Our Team** page:

![Our Team Page](https://miro.medium.com/v2/resize:fit:2000/format:webp/1*LHQ_BwzmnD06A2NTee3big.png)

There was no clue about the fired employee either on the page itself or in the source code. So I copied the challenge’s link to the [WayBack Machine](https://web.archive.org/) and found an old version of the website that had the fired employee’s name:

![Archived Employee](https://miro.medium.com/v2/resize:fit:2000/format:webp/1*Ui7eAyZ6j2_m41lINpiHkQ.png)

Then I searched for this employee’s name across different platforms but initially found nothing. After some digging, I finally found a LinkedIn account with the same name and noticed the flag in the account’s info:

![LinkedIn Flag](https://miro.medium.com/v2/resize:fit:2000/format:webp/1*khG3NWWyb_95Zk8N_YIU8g.png)

---

## Second Challenge: Shadow Signal

This time, the goal was to track the digital footprint of an employee at a company called _TechSecure Inc._ to find the flag.  

A link to the company’s website was provided. I checked the site and noticed something interesting in the **Our Team** section:

![Team Section](https://miro.medium.com/v2/resize:fit:2000/format:webp/1*bpzSaIY3FSLTZs01kCxovg.png)

I searched for this username on different platforms and found an X account belonging to the same employee, which included a posted picture:

![X Account Photo](https://miro.medium.com/v2/resize:fit:902/format:webp/1*kAQGwATQ2qwNYeSu_6KoaA.png)

I first thought the flag was in the picture, so I tried extracting metadata and checking for steganography but found nothing. At this point, I almost lost hope.  

However, in the comment section, I found an old comment from someone named Mark, who was definitely not a contestant since the comment was made before the competition started:

![Old Comment](https://miro.medium.com/v2/resize:fit:876/format:webp/1*ZC9-4Ez6QU6wPQwFa2Wlzg.png)

Following that account led me to another picture:

![Linked Picture](https://miro.medium.com/v2/resize:fit:906/format:webp/1*y0bdEZFhz5U5wnV1XU9A_Q.png)  
![Full Picture](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*0-voJyz8BagMV0599-i4rA.png)

I downloaded this picture and examined it using `strings`:

```bash
strings coffee.jpg | head
````

The output hinted at a link to check:

![Strings Output](https://miro.medium.com/v2/resize\:fit:758/format\:webp/1*fiIU5cLP02qENiumlfW0QQ.png)

After checking the link, I found the flag directly:

![Flag Revealed](https://miro.medium.com/v2/resize\:fit:1400/format\:webp/1*AcVonKx8TLse9w3H0hcolg.png)

---

That’s it! Don’t forget to check my other write-ups for the Web, Crypto, and Forensics challenges.

