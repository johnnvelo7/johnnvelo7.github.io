---
title: Snake Eater - Malware (EASY) Huntress CTF Writeup
date: 2023-11-06
author: John Velo
description: Snake Eater
---

SNAKE EATER WRITEUP

First things first, to analyze this malware, we need to examine what kind of file it is. Using the file and strings command in kali, it gave me a view of what this file is doing. 

![Snake Eater 1](/snake_eaterI/Picture1.png)

Here is just the beginning and end of the file. I already see that the file is encrypted in some ways. In order to find it out, we run the BINWALK -E command in kali to see more what it is doing. 

![Snake Eater 2](/snake_eaterI/Picture2.png)



![Snake Eater 3](/snake_eaterI/Picture3.png)



![Snake Eater 4](/snake_eaterI/Picture4.png)

I found nothing useful because the data is encrypted. 
Using windows, we see the weird file icon. 


![Snake Eater 5](/snake_eaterI/Picture5.png)

Some google research later, we find that it is a python executable. 
Back in Kali, I tried to decompile this file using this python executable script called PyInstaller Extractor v2.0. 


![Snake Eater 6](/snake_eaterI/Picture6.png)

https://github.com/extremecoders-re/pyinstxtractor

After running the file we get the extracted folders, and are able to see inside the structure of the malware. 


![Snake Eater 7](/snake_eaterI/Picture7.png)



![Snake Eater 8](/snake_eaterI/Picture8.png)

BAD NEWS: We see that the file Is encrypted using pyarmor. 

![Snake Eater 9](/snake_eaterI/Picture9.png)

Running out of hope, I decided to run it dynamically in windows using procmon. 

![Snake Eater 10](/snake_eaterI/Picture10.png)

We already see that it is doing A LOT. So what we need to do is to filter these event logs using the filter option.

![Snake Eater 11](/snake_eaterI/Picture11.png)

Add this filter and apply. 
Just scrolling through the logs we already see the flag. :D


![Snake Eater 12](/snake_eaterI/Picture12.png)



![Snake Eater 13](/snake_eaterI/Picture13.png)