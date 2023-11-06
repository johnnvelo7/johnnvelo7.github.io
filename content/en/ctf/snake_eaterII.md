---
title: Snake Eater II - Malware (MEDIUM) Huntress CTF Writeup
date: 2023-11-06
author: John Velo
description: Snake Eater II
---

SNAKE EATER II WRITEUP

After unzipping this file, I checked first what kind of file this malware is. 

![Snake Eater II 1](/snake_eaterII/Picture1.png)

Seems familiar to the previous challenge so I decided to check it in windows too. We see that It has the same icon as the previous challenge. 

![Snake Eater II 2](/snake_eaterII/Picture2.png)

I figured that this challenge will have the same thing as the previous challenge so I ran procmon to see what it is doing, perhaps on the same path directory as Snake Eater. 
We do get to see some interesting files that were created and deleted in microseconds. 


![Snake Eater II 3](/snake_eaterII/Picture3.png)

I tried to open the directory given to see if the flag is there, but it seems to be getting deleted really fast. I also found out that flag.txt is getting created on random folders after the /AppData/Roaming. This is a problem for me because I have multiple folders in that path, so catching the flag will be a bit difficult. That is when I decided that I will do everything in Linux since I only have 1 folder in that path in there. 
First, we use “inotifywait” program to see if it is catching the creation and deletion of file in the directory. (Install this first if you don’t have it)
Using wine, we can run some windows executables in Kali. And just as I thought, we were able to catch the creation of the flag.txt (Install wine first If you don’t have it)


![Snake Eater II 4](/snake_eaterII/Picture4.png)


![Snake Eater II 5](/snake_eaterII/Picture5.png)

Now just to make a python script that can read this file REALLY fast. This is when I decided to create a python script that can do just that.

![Snake Eater II 6](/snake_eaterII/Picture6.png)

After running the script on the same path, we were able to see the flag. 😊