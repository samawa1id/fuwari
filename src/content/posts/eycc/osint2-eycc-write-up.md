---
title: EYCC 2025 — OSINT Challenges (onsite-round)
published: 2025-09-20
pinned: false
description: a write-up for EYCC's onsite-round OSINT challenges
tags: [OSINT, CTF, Write-up, EYCC]
category: Write-ups
author: 0xSky
draft: false
---
# EYCC 2025 — OSINT Challenges (onsite-round)

![Header Image](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*rrHdnRdlfcZ7VgVT.jpg)

Hey! In this write-up, I’ll cover the *Egyptian Youth Cybersecurity Competition (EYCC)* OSINT challenges of the final onsite round.

Let’s get started!

---

## **First Challenge**

We were given this picture:

![Challenge Image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*kKfyj-0BmbGxzQN8-iozfg.png)

We had to locate where this photo was taken and extract the blurred timestamp, then combine them with the string **“echo site”** to form the password of a Pastebin link that contains the flag.

Zooming into the photo, I immediately noticed the timestamp: **2025-8-24**  
I also recognized the place — Longyearbyen.

I searched for Longyearbyen on Google Earth and found the exact spot:

![Google Earth Image](https://miro.medium.com/v2/resize:fit:2000/format:webp/1*CXWP6QxXmg1u4xXqcguNaA.png)

The challenge hinted that the location starts with **“S”**, so after clicking the location we see:

![Svalbard Image](https://miro.medium.com/v2/resize:fit:790/format:webp/1*lbTgZhxBjNnbCkFlStjLew.png)

The required part was **Svalbard**.

So the final password was:

```

Svalbard echo site 2025-8-24

```

Entering it into Pastebin revealed the flag:

![Flag Image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*vs49EYtoKB0ir13ZGgGoqw.png)

---

## **Second Challenge**

We were given a username: **InsaneHunterCTF**  
We needed to trace it and find the flag.

Searching for the username across platforms, I found a GitHub account:

![GitHub](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*J9jJ658Y6YyTDtrGJoZpsw.png)

Inside the `HunterCTF` repo there was an HTML file:

![Repo](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*FY1Zq-Pj85TBLe16K0vNUw.png)

And inside it — an interesting comment:

![Comment](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*hWYjoz6Osb_7Lr2CQ1Sovg.png)

Opening the link gave:

![Link Page](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*dOihURqvDGmAaLyfCKWZ6A.png)

Appending `/secure.zip` downloaded a protected ZIP file.

I produced a hash:

```

zip2john secure.zip > hash.txt

```

Then cracked it:

```

john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt

```

John outputted something like:

```

!LUVDKR!..*7¡Vamos!

```

…but the password didn’t work.

The challenge also hinted at fuzzing `/hidden_FUZZ`.

I used ffuf:

```

ffuf -u [http://13.62.48.186/hidden_FUZZ](http://13.62.48.186/hidden_FUZZ) -w wordlist.txt

```

It found:

```

/hidden_data

```

![ffuf](https://miro.medium.com/v2/resize:fit:1034/format:webp/1*Njvpt5FnTg9FuMzWmEPRSg.png)

Inside were two PDF files.

`leak.pdf` looked corrupted, so I used `strings leak.pdf`:

![Strings Output](https://miro.medium.com/v2/resize:fit:652/format:webp/1*W_3hDBFTaDmjF269803-8Q.png)

It wasn’t the correct flag.

The second file, `leak2.pdf`, also showed a wrong flag:

![Leak2](https://miro.medium.com/v2/resize:fit:906/format:webp/1*HIf8LTdtn6MbotD1psub2Q.png)

So I ran strings on it:

![Strings Output](https://miro.medium.com/v2/resize:fit:1092/format:webp/1*RA73sDtIqTZWGAm9l7Jmyw.png)

This time it revealed the correct ZIP password.

After unzipping, `flag.zip.txt` contained:

![Final Flag](https://miro.medium.com/v2/resize:fit:778/format:webp/1*_khyDCbHb68sLwbserZcPA.png)

And voilà!

---

That was all! Don’t forget to check my other write-ups~
