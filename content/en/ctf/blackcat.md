---
title: BlackCat - Malware (EASY - not really) Huntress CTF Writeup
date: 2023-11-06
author: John Velo
description: Black Cat
---

# Black Cat - Writeup

In this challenge, I was given a zip file containing the malware. 

![Black Cat 1](/blackcat/Picture1.png)

I could already see that the challenge was about decrypting the encrypted files inside the victim-files along with the ***NOTE.png*** that tells me what to do in order to get the files back. 

![Black Cat 2](/blackcat/Picture2.png)



![Black Cat 3](/blackcat/Picture3.png)

I also saw the encrypted ***flag.txt*** along with some random files inside the ***“victim-files”*** folder.

Since this is a CTF challenge, I thought about investing this pictures as well using ***Aperi'Solve***, a really good website to automate stenography. 


![Black Cat 4](/blackcat/Picture4.png)


![Black Cat 5](/blackcat/Picture5.png)

The picture seems pretty normal and nothing inside. 
Next, I opened the ***DecryptMyFiles.exe*** in ***Ghidra*** to inspect the file furthermore.

![Black Cat 6](/blackcat/Picture6.png)

After inspecting the main function, I found out that the program was written in Go Lang, and also found the culprit and explanation to what kind of encryption the program is using. The program is accepting any key more than 8 characters.

![Black Cat 13](/blackcat/Picture13.png)

This is the part of the program where it is manipulating byte orders, a.k.a **XOR**’ing the files. The next step for me was to find a known original file and try to XOR the two files, to get the original decryption key.

Remembering that there was an encrypted file called “the-entire-text-of-hamlet.txt.encry”, I then decided to find the original text and compare both files. 

https://gist.github.com/provpup/2fc41686eab7400b796b

I then saved the file into hamlet.txt, and then ran **“diff”** command to compare both files. 

![Black Cat 7](/blackcat/Picture7.png)

*End of encrypted hamlet using xxd.* ```xxd encryptedhamlet.txt```

![Black Cat 8](/blackcat/Picture8.png)

*End of decrypted hamlet using xxd.* ```xxd hamlet.txt```

## WAIT A SECOND
Hmm….. could it be that the decryption key is **“COSMOBOI”**?
To be sure, I used this python script to XOR two files.

![Black Cat 9](/blackcat/Picture9.png)

After running this script, I got to see that my susipicions were correct. The decryption key was **“cosmoboi”** which is 8 characters long. 

![Black Cat 10](/blackcat/Picture10.png)

I then decided to run **wine** for the decryption tool, and then put “cosmoboi” as the key, successfully helping me get the user’s files back!

![Black Cat 11](/blackcat/Picture11.png)

![Black Cat 12](/blackcat/Picture12.png)

