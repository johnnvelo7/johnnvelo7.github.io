---
title: Indirect Payload - Miscellaneous (MEDIUM) Huntress CTF Writeup
date: 2023-11-04
author: John Velo
description: Indirect Payload
---


# Indirect Payload - Writeup

Visiting the website we get this page:

![indrect payload 1](/indirect_payload/Picture1.png)


When I clickked on the button, it redirected me to another url, and got error message. Hmmm... It seems as clicking the button results in an endless loop of redirection.

![indrect payload 2](/indirect_payload/Picture2.png)

![indrect payload 3](/indirect_payload/Picture3.png)

I then decided to see what is happening using ***burpsuite***. 

![indrect payload 4](/indirect_payload/Picture4.png)
 
Everytime I sent a GET request to */flag.php* site, I got new URLs instead. This was when I decided to follow it manually, and after 2 more redirections I could finally see the first character of the flag. 

![indrect payload 5](/indirect_payload/Picture5.png)
 
This is when I realized that the flag is scattered through all the URLs that I was forced to redirect to. To save time, I used this python script that follows the urls and prints the payload whenever there is. 

![indrect payload 6](/indirect_payload/Picture6.png)
 
After running the script, I was able to see whole picture.

![indrect payload 7](/indirect_payload/Picture7.png)
 
I first saved the output to a file called ***“flag.txt”*** and then ran another python script that parses the output and prints the flag in the correct format. 

![indrect payload 8](/indirect_payload/Picture8.png)

![indrect payload 9](/indirect_payload/Picture9.png)

