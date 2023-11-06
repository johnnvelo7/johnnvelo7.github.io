---
title: Snake Eater - Malware (EASY) Huntress CTF Writeup
date: 2023-11-06
author: John Velo
description: Snake Eater
---

# Snake Eater - Writeup

First things first, to analyze this malware, I had to examine what kind of file it was. Using  ***file*** and ***strings*** command in Kali, gave me a view of what this file was doing. 

```file snake_eater.exe```

![Snake Eater 1](/snake_eaterI/Picture1.png)

After analyzing the malware structure and description, I realied that the file was encrypted in some ways so I stopped and had to brainstorm a bit. 

```strings snake_eater.exe```

![Snake Eater 2](/snake_eaterI/Picture2.png)

![Snake Eater 3](/snake_eaterI/Picture3.png)

In order to get more information, I used the ***binwalk*** command in Kali to see more what it was doing. 

```binwalk -e snake_eater.exe```

![Snake Eater 4](/snake_eaterI/Picture4.png)

I found nothing useful because the data was encrypted. 

**Time to boot up Windows VM**

Using windows, I saw this weird fie icon, just like the challenge description says.

![Snake Eater 5](/snake_eaterI/Picture5.png)

Some google research later, I found that it was a python executable. 

Back in Kali, I tried to decompile this file using this python executable script called ***PyInstaller Extractor v2.0***. 

![Snake Eater 6](/snake_eaterI/Picture6.png)

https://github.com/extremecoders-re/pyinstxtractor

After running the script, I got the extracted folders, and was able to see inside the structure of the malware. 

```extractor.py snake_eater.exe```

![Snake Eater 7](/snake_eaterI/Picture7.png)

![Snake Eater 8](/snake_eaterI/Picture8.png)

## BAD NEWS: 
I realized that the file was encrypted using pyarmor. 

![Snake Eater 9](/snake_eaterI/Picture9.png)

Running out of hope, I decided to run it dynamically in Windows using ***procmon***. 

![Snake Eater 10](/snake_eaterI/Picture10.png)

I could already see that the malware was doing A LOT. I wanted to see more so I had to filter the event logs using the filter option. Add this filter and apply. 

![Snake Eater 11](/snake_eaterI/Picture11.png)

Just scrolling through the logs I was shocked because I could already see the ***flag*** in plaintext. :D

![Snake Eater 12](/snake_eaterI/Picture12.png)

![Snake Eater 13](/snake_eaterI/Picture13.png)