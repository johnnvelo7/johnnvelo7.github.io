---
title: Snake Eater II - Malware (MEDIUM) Huntress CTF Writeup
date: 2023-11-06
author: John Velo
description: Snake Eater II
---

# Snake Eater II - Writeup
After unzipping this file, I checked first what kind of file this malware is. 

```file snake_eaterII.exe```

![Snake Eater II 1](/snake_eaterII/Picture1.png)

Seems familiar to the previous challenge so I decided to check it in windows too. I saw that it had the same icon as the previous challenge. 

![Snake Eater II 2](/snake_eaterII/Picture2.png)

I figured that this challenge might have the same solution as the previous one so I ran ***procmon*** to see what it was doing, perhaps on the same path directory as Snake Eater. 

While dynamically analyzing the malware, I got to see some interesting files that were ***created*** and ***deleted*** in ***microseconds***. 

![Snake Eater II 3](/snake_eaterII/Picture3.png)

I tried to open the directory given to see if the flag is there, but it seems to be getting deleted really fast. I also found out that *flag.txt* is getting created on random folders after the /AppData/Roaming. This was a problem for me because I have multiple folders in that path, so catching the flag will be a bit difficult. That was when I decided that to do everything in *Kali Linux* since I only have 1 folder in that path through *wine*. 

First, I used ***“inotifywait”*** program to see if it was catching the creation and deletion of file in the directory. (Install this first if you don’t have it)

Using ***wine***, I was able to run some windows executables inside Kali. And just as I thought, I was able to catch the creation of the ***flag.txt*** (Install wine first If you don’t have it)

![Snake Eater II 4](/snake_eaterII/Picture4.png)

![Snake Eater II 5](/snake_eaterII/Picture5.png)

The only problem left now is to make a python script that can read this file REALLY fast. That was when I decided to create a python program called ***PATH_WATCHER*** that can do just that! (shameless plug).

![Path Watcher Example](/images/pathwatcher.png)

https://github.com/johnnvelo7/path_watcher

![Snake Eater II 6](/snake_eaterII/Picture6.png)

After running the script on the same path, I was able to retrieve the flag that was created. 😊