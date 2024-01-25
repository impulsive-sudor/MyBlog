---
title: Palworld Corrupt File Save Fix
date: 2024-01-24T02:18:29.549Z
draft: true
featured_image: ""
type: ""
---

Notes:
Run the open source tool agaisnt the save.
Find player uid
    this is found in the exported JSON. If they are in a guild you can find it through there name
Search for the key value pal for the players missing. Move this missing data from the old save to the new save.

One of the ongoing issues in Palworld is charcter corruption. From a user propspective, when they try to login, they get stuck on the loading screen. I've noticed this typically happening after a server crash.

This guide is not for the someone looking for an easy fix. They easist way to fix this issue is either by creating a new server or restoring fully from a backup. We (my friends) couldn't do this since a handful of them already progressed hours ahead of the people that got corrupted.

## Assumptions

* You have a backup of the server somewhere, in particular, we need all the .sav files.
* You are somewhat technical and can deal with getting your hands dirty.
* You don't mind running unknown software from the internet.

## Pre-Requirements

* Install [WinSCP](https://winscp.net/eng/downloads.php)
    >This can be installed via Microsoft Store at a small cost. For this guide, I'm using the exe version of the program.
* Install [Python](https://www.python.org/downloads/windows/)
* Windows OS
* A Backup or Snapshot of the last good save
    >The saved files are located in the directory *Pal/Saved/SaveGames/ID/0/Level.sav*

## Pre-Requirements Install Guide

This will explain how to install WinSCP and Python.

### Python

Python is a popular programming language used by many developers across the world. Before you can run code on your device in Python, you need to install it.

1. Navigate to the Python downloads page on your Windows machine [https://www.python.org/downloads/windows/]
2. Select the "Windows installer (64-bit)" download
3. Click on the python installer package in your downloads folder to begin the install.
4. Make sure to enable the setting that configures your PATH in Windows for you
5. Click next on everything else
6. At the end, you can disable the file path limit if you like but it's not required for this guide.
7. Confirm that this is working by openning powershell and entering the command ```python```
8. You should now be in a python command prompt. To exit, enter ```exit()```

### WinSCP

WinSCP is a easy to use file transfer tool to move files over SSH. This is only really needed if you prefer to use a GUI over CLI and are using a Linux OS for your server.

1. Navigate to the WinSCP downloads page (try to ignore the ads) on your Windows machine [https://winscp.net/eng/download.php]
2. Select on the "DOWNLOAD WINSCP 6.1.2 (11 MB)" button to download the latest installer.
3. After downloaded, click on the installer file in your downloads folder.
4. Start by going through the steps required to install this tool.
5. During the install, additional install windows may come up. These are required tools that work alongside WinSCP
6. After install completion, run the WinSCP application to confirm it's working.

## Save Fix Steps

1. Let's start by centralizing everything we need in one location. We can create a folder on the desktop called "Save Fix".
2. Next, we need to gather the current save file
    >Due to the variability in each persons setup, I cannot go into detail on how to get your old save file. If you backed up your file before, you should known where it is. It doesn't matter how old it is, all we are looking for is some code to restore the corrupt player.
    1. Open up WinSCP
    2. Connect to your server via WinSCP
    3. Navigate to the save file *Pal/Saved/SaveGames/ID/0/Level.sav*
    4. Move this file to your local computer
3. Now find your old save file and download it onto your computer
4. Place these files in the "Save Fix" folder. I would rename the old save file to something like "level-old.sav"
5. Download [uesave-rs](https://github.com/trumank/uesave-rs/releases/download/v0.3.0/uesave-x86_64-pc-windows-msvc.zip) and place the uesave.exe into the same folder as the save files.
6. Download the python code from github [here](https://gist.github.com/cheahjs/300239464dd84fe6902893b6b9250fd0/archive/3a89097ce9a60946d68be320b0fa35fd20dd98ae.zip) and extract the files into the same save folder
7. Click and drag the current level.sav file onto the *convert-single-sav-to-json.bat* file. This will open a cmd prompt to convert the files from .sav to json.
    >This part will take some time to process and will generate a large json file. In my testing, the output json file is 7GB large.
8. Perform the same step on the old save file
9. Now is the fun part, we need to find the player UID. I did this by searching for the players name, which only works if the player is in a guild.
10. Once you have the UID, you need to find the block of JSON missing in the current save file by comparing it to the old save file. 
11. You will now copy that date from the old save file and move it to the current save file. Save these changes
12. Click and drag the corrected json file onto the *convert-single-json-to-sav.bat* script. This will convert the file back into a level.sav file.
13. Safely shutdown the current running server to prevent any corruption
14. Go onto the current server and backup the level.sav file again.
    >All of the progress made between you doing these changes and now will be lost in the game. The level.sav file is the server database.
15. Using WinSCP, move the newly created level.sav file from your computer into the *Pal/Saved/SaveGames/ID/0/* directory
16. Relaunch the server by running the pal server script.
17. If everything was done correctly, the corrupt users should now be able to login.

Congrats! I hope this guide worked for you as well as it worked for us. Happy Gaming!

### References

* [https://github.com/xNul/palworld-host-save-fix]
* [https://www.reddit.com/r/Palworld/comments/19cl66w/so_basically_for_those_with_broken_save_files/]
* [https://github.com/trumank/uesave-rs]