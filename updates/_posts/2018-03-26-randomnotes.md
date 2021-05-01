---
layout: content
title: Random Notes
tags: update
---
I collect lots of one-off notes, sometimes technical (e.g. how to compress a series of files following a specific pattern), sometimes not (e.g. best way to hard boil eggs, or random insightful quote from random insightful person), and I've started collecting some of them here. 

## Clear the MBR on Microsoft Surface when stuck on the UEFI screen
```terminal
dd if=/dev/zero of=/dev/sda bs=512 count=1
efibootmgr -b 0000 -B
```

## DRV2065L + Precision Microdrives
SCL = A5 = pin closer to FTDI connect = green<br />
SDA = A4 = pin closer to cpu = yellow
- Connect Vin to the power supply, 3-5V is fine
- Connect GND to common power/data ground
- Connect the SCL pin to the I2C clock SCL (A5) pin on the Arduino (UNO & 328 based Arduino = A5, Mega = digital 21, Leonardo/Micro = digital 3)
- Connect the SDA pin to the I2C data SDA (A4) pin on the Arduino (UNO & 328 based Arduino =  A4, Mega = digital 20, Leonardo/Micro = digital 2)

## Python Slicing Summary
```python
# a[start:end:step] # from start, but not past end, by step
# the :end value represents the first value that is not in the selected slice

# start or end may be a negative number, which counts from the end of the array instead of the beginning
a[-1]    # last item in the array
a[-2:]   # last two items in the array
a[:-2]   # everything except the last two items

# step may be a negative number:
a[::-1]    # all items in the array, reversed
a[1::-1]   # the first two items, reversed
a[:-3:-1]  # the last two items, reversed
a[-3::-1]  # everything except the last two items, reversed

alphabet = "abcdefghijklmnopqrstuvwxyz"

# first 7 characters (abcdefg)
alphabet[0:7:]  # or [0:7]
alphabet[:7:]   # or [:7]

alphabet[3::]       # starting after character 3 (first char will be 'd')
alphabet[-1::]      # last character (z)
alphabet[-2::]      # last two characters (yz)
alphabet[::-1]      # reverse the array (z-a)
alphabet[1::-1]     # the first two items, reversed (ba)
alphabet[:-3:-1]    # the last two items, reversed (zy)
alphabet[-3::-1]    # everything except the last two items, reversed (x-a)
```

## Authenticate on GitHub with a secondary user
- Create a dedicated SSH config with IdentityFile and IdentitiesOnly
- Update the origin URL of every repo to use the SSH config: github-user:user/repo

```
~/.ssh/config:

Host github.com-username1
        HostName github.com
        User git
        IdentitiesOnly yes
        IdentityFile ~/.ssh/username1_rsa

Host github.com-username2
        HostName github.com
        User git
        IdentitiesOnly yes
        IdentityFile ~/.ssh/username2_rsa
```

## Superior Hard Boiled Eggs
Lower your eggs straight from the fridge into already-boiling water. If boiling, lower the heat to a simmer. Cook the eggs for 11.5 minutes for hard or 6 minutes for soft. Shock them in ice water immediately. Let them chill in that water for at least 15 minutes, or in the fridge overnight. Peel under cool running water.


