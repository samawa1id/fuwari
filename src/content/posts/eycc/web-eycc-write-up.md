---
title: EYCC 2025 — Web Challenges
published: 2025-09-07
pinned: false
description: a write-up for EYCC's web challenges
tags: [Web, CTF, Write-up, EYCC]
category: Write-ups
author: 0xSky
draft: false
---
# EYCC 2025 — Web Challenges

![EYCC Banner](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*O-JH8o8NsFFKPVBZY9gTOg.jpeg)

Hello there! This write-up covers the _Egyptian Youth Cybersecurity Competition (EYCC)_ web challenges I solved, focusing on the methods and techniques used.

---

## First Challenge: Open Gate

The link redirected me to this login page:

![Open Gate Login](https://miro.medium.com/v2/resize:fit:1182/format:webp/1*V9Bw59V7wabExqPLfQdEgA.png)

My first thought was that it was probably vulnerable to **SQL injection**, so I tried injecting:

```text
a’ OR 1=1 --
````

And the flag appeared!

---

## Second Challenge: Secure Shop

This time it was a search page:

![Secure Shop Search](https://miro.medium.com/v2/resize\:fit:1400/format\:webp/1*3oet-kbKoU2VkMYeQzJWRw.png)

By inspecting the page with developer tools, I found the flag laying there:

![Flag in Source](https://miro.medium.com/v2/resize\:fit:2000/format\:webp/1*KeDRI655KZt0XjYEe05X_Q.png)

I suspected the challenge should be solved in another way. The JavaScript function was converting ASCII values to normal characters and saving it in a variable called **flag**.

Then I checked if the website was vulnerable to **XSS** by testing:

```html
<script>alert(1)</script>
```

It worked!

![XSS Test](https://miro.medium.com/v2/resize\:fit:1400/format\:webp/1*GyRzsq3U02ggM955wqivJA.png)

Next, I copied the JavaScript code from the page into the search bar, added an alert to reveal the flag:

```javascript
<script>
var codes = [101, 121, 99, 99, 123, 101, 102, 108, 99, 107, 102, 
             106, 101, 110, 99, 108, 97, 107, 101, 102, 125];
var flag = String.fromCharCode.apply(null, codes);
alert(flag);
</script>
```

The site blocked input on reload, so I ran the script locally to view the flag:

![Flag Revealed](https://miro.medium.com/v2/resize\:fit:2000/format\:webp/1*ezqJaWCnw9caubqj8SVbIg.png)

---

## Third Challenge: Whisper Box

The webpage itself had nothing special:

![Whisper Box](https://miro.medium.com/v2/resize\:fit:1224/format\:webp/1*hBU3QYKQIl8O0SxM8bmMBA.png)

I viewed the page source and found some credentials:

![Credentials](https://miro.medium.com/v2/resize\:fit:1274/format\:webp/1*B5vnR7FACrwZovqi7OiryQ.png)

My first thought was to send a POST request with these credentials using cURL:

![cURL Post](https://miro.medium.com/v2/resize\:fit:1400/format\:webp/1*BnHgtaUj3rRumPWkUyj9Jw.png)

And here’s the flag!

---

## Fourth Challenge: Secure Bank

To solve this challenge and get the flag, our mission was to make a CSRF PoC for the password changing page of a provided website.

The login page:

![Bank Login](https://miro.medium.com/v2/resize\:fit:1296/format\:webp/1*fSHi2n5v4lsB4Gm13GcO_g.png)

After logging in with provided credentials (*user & password*), the dashboard appeared:

![Dashboard](https://miro.medium.com/v2/resize\:fit:2000/format\:webp/1*HWU9Mt-UgaX61j6C3Vur0A.png)

I checked the password changing page and captured the request using Burp Suite:

![Burp Capture](https://miro.medium.com/v2/resize\:fit:1400/format\:webp/1*KjULITpAotY9OeWx8XR3lA.png)

Then I copied the request to CSRF Shark and created a CSRF PoC:

![CSRF PoC](https://miro.medium.com/v2/resize\:fit:2000/format\:webp/1*dBclxYvZrCxL20uQRS045Q.png)

Finally, I submitted the PoC after adding the `no-referrer` meta tag (mandatory for acceptance):

![PoC Submitted](https://miro.medium.com/v2/resize\:fit:1016/format\:webp/1*hkszD8hIsKmc6PoswPCfEg.png)

Et voila!

![Flag Success](https://miro.medium.com/v2/resize\:fit:1266/format\:webp/1*9Zal-fZLS3ei4GYyGm0iUw.png)

---

And that’s it! Don’t forget to check my other write-ups for the Crypto, Forensics, and OSINT challenges!
