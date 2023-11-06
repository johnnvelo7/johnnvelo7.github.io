---
title: Bad Memory - Forensics (MEDIUM) Huntress CTF Writeup
date: 2023-11-06
author: John Velo
description: Bad Memroy
---

# Bad Memory - Writeup

The task wants us to recover the password that the user has forgotten. I immediately thought of using ***Volatility 3*** since we are working with an image or memory dump. 

```file image.bin```

![indrect payload 1](/bad_memory/Picture1.png)

So straight to action, I decided to get the ***NTLM*** hashes from this image.

```vol -f image.bin windows.hashdump```

![indrect payload 2](/bad_memory/Picture2.png)

I saveed these hashes into a text file and fire up my favourite password cracker, ***John The Ripper*** to crack these hashes.

```john --format=NT -w=/usr/share/wordlists/rockyou.txt hash.txt```

![indrect payload 3](/bad_memory/Picture3.png)

The only thing I have left is make the ***md5sum*** of this string to sumit as the flag format.

```echo -n "goldfish#" | md5sum```

![indrect payload 4](/bad_memory/Picture4.png)

flag{2eb53da441962150ae7d3840444dfdde}