---
layout: content
title: Random Notes
tags: update code science japan japanese space travel project
---
I collect lots of one-off notes, sometimes technical (e.g. how to compress a series of files following a specific pattern), sometimes not (e.g. best way to hard boil eggs, or random insightful quote from random insightful person), and I've started collecting some of them here. 

## Clear the MBR on Microsoft Surface when stuck on the UEFI screen
```terminal
dd if=/dev/zero of=/dev/sda bs=512 count=1
efibootmgr -b 0000 -B
```

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