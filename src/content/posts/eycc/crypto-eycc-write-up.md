---
title: EYCC 2025 — Crypto Challenges
published: 2025-09-07
pinned: false
description: a write-up for EYCC's crypto challenges
tags: [Crypto, CTF, Write-up, EYCC]
category: Write-ups
author: 0xSky
draft: false
---
# EYCC 2025 — Crypto Challenges

![EYCC Crypto Banner](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*ivwxYactN1Yd596r.jpg)

Hey! This write-up covers the _Egyptian Youth Cybersecurity Competition (EYCC)_ Crypto challenges that I managed to solve with steps taken to reveal the final flag.

---

## First Challenge: Veiled Secret

This challenge was about decrypting a _secret message_:

```text
MKywL3gznaqhM2ghqzuxnzMvq-TulsD==TOR13
````

I noticed the `TOR13` at the end, which points to starting with ROT13.

So, I copied the secret message to my go-to decoder, [Dcode](http://dcode.fr), and checked the output:

![ROT13 Decoding](https://miro.medium.com/v2/resize\:fit:1400/format\:webp/1*qDRUvqTynwJhiEIz9VGldw.png)

Now we’re left with Base64 encoded text, so I decoded it in the same website and got the flag:

![Flag Revealed](https://miro.medium.com/v2/resize\:fit:1400/format\:webp/1*QLysdpI5ZSLjETBc08LYGQ.png)

---

## Second Challenge: Golden Spiral

We were given a file named `goldenSpiral`. It was not executable, so I made it executable:

```bash
chmod +x goldenSpiral
```

Then I tried executing it:

```bash
./goldenSpiral
```

But it threw an error:

```text
bash: ./goldenSpiral: cannot execute: required file not found
```

I checked the file type:

```bash
file goldenSpiral
```

It revealed that it was an ELF executable requiring this interpreter:

```text
/nix/store/lmn7lwydprqibdkghw7wgcn21yhllz13-glibc-2.40–66/lib/ld-linux-x86–64.so.2
```

After running the file with the required interpreter, an encrypted flag was returned:

```text
fzef{7i0fGcobhxzwr4j}
```

The challenge mentioned a sequence that “grows almost exponentially,” suggesting the **Fibonacci sequence**. Since the encrypted flag seemed alphabetically shifted, I used this [Fibonacci Cipher Decoder](https://wordsmithingtools.com/fibonacci-cipher) and started from 1 (because `e` comes right before `f` in the alphabet).

![Fibonacci Cipher](https://miro.medium.com/v2/resize\:fit:1400/format\:webp/1*OPzh4M5u8mqhQrZz61vXQQ.png)

And we got the flag!

---

## Third Challenge: Silent Keys

This challenge was an RSA decryption challenge.

We were given:

```text
n = 148304669693572711157725718049458731328582148078019
e = 65537
c = 35618364216358867907731764651946346081071748936005
```

The hint said:

> *n is the product of two primes; one of them is the integer part of pi multiplied by 10^5*

This challenge can be solved in two ways:

1. Directly inputting the values in [Dcode](http://dcode.fr) to get the flag:

![RSA Decryption via Dcode](https://miro.medium.com/v2/resize\:fit:1400/format\:webp/1*JFFR1H0ROtA0mtz8DL6mmg.png)

2. Or factorizing `n` using [factordb](https://factordb.com/) to get `p` and `q`:

![Factoring n](https://miro.medium.com/v2/resize\:fit:1400/format\:webp/1*9TBgGEpJ5BPvh6VpWemNug.png)

Then calculating `d` from `p, q, e`:

![Calculate d](https://miro.medium.com/v2/resize\:fit:1400/format\:webp/1*FB8ms9MFowzxn600WOATGQ.png)

Finally, decrypt the ciphertext `c` to reveal the flag:

![Decrypted Flag](https://miro.medium.com/v2/resize\:fit:1400/format\:webp/1*eAglyrLAZC89OUMOnwKV4A.png)

---

And that’s all! Don’t forget to check my other write-ups for the Web, Forensics, and OSINT challenges!

