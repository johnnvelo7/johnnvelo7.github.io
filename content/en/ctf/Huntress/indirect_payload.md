---
title: Indirect Payload (Miscellaneous) Huntress CTF Writeup
date: 2023-11-04
author: John Velo
description: Indirect Payload
---



INDIRECT PAYLOAD WRITEUP
Visiting the website we get this page:
![indrect payload 1](/writeup-images/Picture1.png)


Clicking on the button will redirect us to another url: 

![indrect payload 2](/writeup-images/Picture2.png)

And then we get error message. 
 
![indrect payload 3](/writeup-images/Picture3.png)

I then decided to see what is happening using burpsuite. 

![indrect payload 4](/writeup-images/Picture4.png)
 
Here I see that we get a new site that we can follow, so I decided to follow it manually, and after 2 more redirections we see the first character of the flag. 

![indrect payload 5](/writeup-images/Picture5.png)
 
This is when I realized that the flag is scattered through all the URLs that we are forced to redirect to. Here is the python Script I ended up using to follow the urls and print the payload. 

![indrect payload 6](/writeup-images/Picture6.png)
 
After running the script, we can now see the whole picture.

![indrect payload 7](/writeup-images/Picture7.png)
 
We can then use this python script to parse the payload and print the flag. I first saved the output to a file called “flag.txt” and then ran it.

![indrect payload 8](/writeup-images/Picture8.png)

![indrect payload 9](/writeup-images/Picture9.png)


