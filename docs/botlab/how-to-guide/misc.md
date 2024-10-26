---
layout: default
title: Misc
parent: How-to Guide
grand_parent: Botlab
nav_order: 5
last_modified_at: 2024-10-25 13:37:48 -0500
---

> This guide provides instructions on miscellaneous how-to questions.

### Contents
* TOC
{:toc}

## How to charge the power bank
1. Push the switch of the power bank to position "I" to make the charging circuit breakout.
2. Connect the charger to the power bank
3. The LED indicator on the AC-DC charger head showing RED means the charging process is working.
4. The LED indicator on the AC-DC charger head showing GREEN means the charging process has completed.

## How to transfer file from MBot to your laptop - wormhole

There is a command-line tool, called [wormhole](https://magic-wormhole.readthedocs.io/en/latest/welcome.html) that comes in handy. It can safely and conveniently transfer things from one computer to another.

The scenario with the wormhole tool is as follows: If you've recorded a log file on the Pi, or just have some files need to transfer it to your laptop without uploading it to Github, you can use wormhole for this purpose. Below is an example of its usage:

<a class="image-link" href="/assets/images/botlab/how-to/wormhole-tool.png">
<img src="/assets/images/botlab/how-to/wormhole-tool.png" alt=" " style="max-width:600px;"/>
</a>

### Install
```bash
# On the Pi
$ sudo apt install magic-wormhole
```
```bash
# On your laptop
brew install magic-wormhole # for Mac
sudo apt install magic-wormhole # for Ubuntu
```
### Send and Receive
```bash
# on Pi, send the file:
wormhole send <path-to-file>
# then on your laptop, receive the file:
wormhole receive <code-wormhole-generated>
```

## Pi5 - Disk is full
1. Check how much space is left by running:
```bash
$ df -h
```
- Look for the line with `/` in the "Mounted on" column. This is your main storage. For example:
    ```bash
    Filesystem      Size  Used Avail Use% Mounted on
    /dev/mmcblk0p2   29G   11G   17G  40% /
    ```

2. You can identify large files by `du -h --max-depth=1 <Path> | sort -rh | head -n 10`:
```bash
$ du -h --max-depth=1 ~ | sort -rh | head -n 10
```
- This command lists the 10 largest items in your home directory. Example output:
    ```
    1.5G    /home/mbot
    410M    /home/mbot/.vscode-server
    342M    /home/mbot/.cache
    253M    /home/mbot/mbot_ws
    237M    /home/mbot/.config
    178M    /home/mbot/.vscode
    55M     /home/mbot/Bookshelf
    34M     /home/mbot/.envs
    8.2M    /home/mbot/.nx
    168K    /home/mbot/.dotnet
    ```
    - Here, `.vscode-server` can be safely deleted `$ rm -rf ~/.vscode-server`.
3. You can free up space by removing unnecessary package files:
    ```bash
    sudo apt clean
    ```
