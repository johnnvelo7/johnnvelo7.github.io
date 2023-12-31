---
title: PATH_WATCHER
date: 2023-11-04
author: John Velo
description: CTF tool
---

![Path Watcher Example](/images/pathwatcher.png)

# path_watcher
**CTF TOOL:** 

https://github.com/johnnvelo7/path_watcher

Monitor a directory for files created and closed after writing events. It displays the contents of the file after it's written.
This is useful for CTF's where you need to dynamically analyse a malware especially if the malware is creating and deleting a file (flag.txt) in microseconds.

***TAKE NOTE:*** 

This program currently only works for Linux OS, but I'll add support for windows  soon.

## HOW TO USE:

Install the required package (pyinotify):
```pip install pyinotify```
or 
```pip3 install pyinotify```

RUN the program
```python3 monitor.py -h``` for help

or
```python3 monitor.py``` to run normally