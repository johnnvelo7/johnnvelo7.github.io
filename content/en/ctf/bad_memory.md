---
title: Bad Memory - Forensics (MEDIUM) Huntress CTF Writeup
date: 2023-11-06
author: John Velo
description: Bad Memroy
---

# Bad Memory - Writeup

The task wants us to recover the password that the user has forgotten. I immediately thought of using **volatility** since we are working with an image or memory dump. 

```file image.bin```

![indrect payload 1](/bad_memory/Picture1.png)

So straight to action we need to get the **hashes**

```vol -f image.bin windows.hashdump```

![indrect payload 2](/bad_memory/Picture2.png)

We need to save these hashes into a text file and fire up **john the ripper** to crack these hashes.

```john --format=NT -w=/usr/share/wordlists/rockyou.txt hash.txt```

![indrect payload 3](/bad_memory/Picture3.png)

The only thing we need is make the **md5sum** of this string so we can get the flag.

```echo -n "goldfish#" | md5sum```

![indrect payload 4](/bad_memory/Picture4.png)

flag{2eb53da441962150ae7d3840444dfdde}