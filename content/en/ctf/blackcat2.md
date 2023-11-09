---
title: BlackCat2 - Malware (HARD) Huntress CTF Writeup
date: 2023-11-09
author: John Velo
description: Black Cat 2
---

# Black Cat 2  - Writeup

This task was about decrypting the encrypted files and try to get the flag back from the user’s files.

![Black Cat 2](/blackcat2/Picture1.png)

I was given these files to play around with, pretty much the same as the first black cat task just without the NOTE.png.

![Black Cat 2](/blackcat2/Picture2.png)

These are the encrypted files inside the victim folder.

![Black Cat 2](/blackcat2/Picture3.png)

I figured that it might have the same solution as the last task, so I decided to check the file description, as well the strings from the decryptor.exe

```strings Decryptor.exe```

![Black Cat 2](/blackcat2/Picture4.png)

I didn’t anything useful rather than random strings and codes, but looking at the file description, we can see that it is an unusual executable compiled through ***.NET***

```file Decryptor.exe```

![Black Cat 2](/blackcat2/Picture5.png)

Just to be sure, I decided to dynamically run the decryptor.exe through ***promon*** in windows to see what the application is doing, but still found nothing useful.

![Black Cat 2](/blackcat2/Picture6.png)

**TIME TO DECOMPILE THE PROGRAM**

Since it was compiled with .NET I then decided to use ***dnSpy*** to look through the original code. 

![Black Cat 2](/blackcat2/Picture7.png)

FINALLY SOMETHING USEFUL. I realized that the code was made for ***32bit*** and was written in ***C#***.

![Black Cat 2](/blackcat2/Picture8.png)

More interesting part was this ***decryption function*** I found which explains the decryption ***algorithm***.

![Black Cat 2](/blackcat2/Picture9.png)

**ZOOMED IN**

Basically the program searches for files ending in .encry extension, and does the decryption. For the first file to be decrypted, it uses the provided decryption key, while to decrypt the rest of the files, it needs the ***sha256sum*** of the first decrypted file. Kinda crazy right? I mean who would even do that.

![Black Cat 2](/blackcat2/Picture10.png)

*Function that calculates the sha256sum of the first decrypted file.*

![Black Cat 2](/blackcat2/Picture11.png)

This function means that if I have the original password, then I’ll be able to generate the decryption key, but the problem here is that I was not able to find the ***password***.

![Black Cat 2](/blackcat2/Picture12.png)

*Decryption function*

![Black Cat 2](/blackcat2/Picture13.png)

*Hard coded IV value for AES decryption*

![Black Cat 2](/blackcat2/Picture14.png)

**IN SUMMARY**

*I would be able to decrypt the files If had the original password used, but since reading about how the program works, I got an idea to just do the same as the previous challenge. What if I find the first original picture? Then I will be able to calculate the sha256sum of that right? Well let’s test it out!*

**Finding the picture**

This was harder than I thought. I wasted a lot of time searching for the original website used to match the file name and extension, but luckily, I got a hint that the extension doesn’t need to be exact match!

![Black Cat 2](/blackcat2/Picture15.png)

Searching the exact file in ***google images*** with parenthesis gave me this result with consistent url. Could be the website used to download the images?


![Black Cat 2](/blackcat2/Picture16.png)

*https://www.atxfinearts.com/blogs/news/100-most-famous-paintings-in-the-world*

![Black Cat 2](/blackcat2/Picture17.png)

I found the picture I was looking so I decided to save it as a picture.

![Black Cat 2](/blackcat2/Picture18.png)

THERE IT WAS!!! Just with a different extension. I also made sure that it was the exact same size as the decrypted file.

![Black Cat 2](/blackcat2/Picture19.png)

Only one thing left to do. I decided to go back to kali and take the sha256sum of this file and got:

***80d60bddb3b57a28d7c7259103a514cc05507c7b9cf0c42d709bdc93ffc69191***

![Black Cat 2](/blackcat2/Picture20.png)


After trying different python scripts to reverse the encryption using this hash, I failed. It was then I realized ***“WHAT IF”*** I just use the hash as the key using the Decryption.exe? So I went back to windows and tried just that. 

![Black Cat 2](/blackcat2/Picture21.png)

**VIOLAAA**, I did not expect that to work, but hey, a flag is a flag! :D

![Black Cat 2](/blackcat2/Picture22.png)