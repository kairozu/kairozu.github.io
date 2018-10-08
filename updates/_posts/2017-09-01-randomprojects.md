---
layout: content
title: Random Projects
project-github-link: https://github.com/kairozu/
hasimg: /images/randomprojects.png
imgwidth: 240
tags: project code science japanese update
---
These are various snippets of projects ranging from completed smaller projects to abandoned larger ones (most recent listed first). Use them at your own risk.. most of them are one off novelties or attempts at doing something a certain way (that may or may not have worked), or even more terrifying, an attempt to learn/figure something out.

## WaniAnki-Python
<i class="fab fa-github fa-fw"></i> [https://github.com/kairozu/WaniAnki-Python](https://github.com/kairozu/WaniAnki-Python)

Python scripts to parse WaniKani kanji & vocabulary JSON dumps into Anki decks w/kanji stroke orders. See WaniKani's API documentation for pulling kanji/vocabulary data: [https://www.wanikani.com/api](https://www.wanikani.com/api) (a WaniKani account API key is required). WaniKani is great and you should support them with a subscription. This is for extra practice, especially with regard to writing kanji w/a stroke order reference. Please don't use this to avoid supporting WaniKani.

## Spike Train Calculator
<img class="imageR" height="150" alt="weather" src="/images/spiketrain.png" />
<i class="fab fa-github fa-fw"></i> [https://github.com/kairozu/Ephys-Stimulation](https://github.com/kairozu/Ephys-Stimulation)

Converts between inter-pulse intervals/train burst widths and frequency/number of pulses & plots an example waveform (also my first foray into JS/jQuery). Mostly useful for visualizing spike trains in discussions or double checking your math when hopping between ephys equipment.

Once you begin entering values, the example waveform will not plot until all values have been entered. You can choose between calculating your waveform from the inter-pulse period and the train burst width, or from the # of pulses and the frequency of those pulses -- the alternate option will be displayed automatically.  Scientific notation is displayed on the right for reference if you're using a system that requires SN (AM Systems, yay).

<div class="spacerClear"></div>

## 4-Letter Word Generator
<i class="fab fa-github fa-fw"></i> [https://github.com/kairozu/Kairozu-Sandbox/blob/master/lockcombo.py](https://github.com/kairozu/Kairozu-Sandbox/blob/master/lockcombo.py)

Did you also forget the word combination for your master 643DWD lock? Maybe these words will jog your memory! This generates all combinations of letters (both backward and forward) and screens them for being actual dictionary words. I'm sad to say that I had indeed set the lock to a dictionary word, and that yes, this actually worked for me.

## Chrome NewTab Color Extension
<img class="imageL" height="135" alt="weather" src="/images/newtab_chromestore.png" />
<i class="fab fa-github fa-fw"></i> [https://github.com/kairozu/NewTab-Color-Void](https://github.com/kairozu/NewTab-Color-Void)

NewTab Color Void is a bare-bones Chrome extension that replaces the default new tab window with a single-color (customizable in options) screen. Requires no permissions from the user; doesn't have access to browsing information, Chrome tabs, or anything else.

To install from Chrome Web Store: [https://chrome.google.com/webstore/detail/newtab-color-void/enbboabmkalnjjaciinmnjfbhajpejbl](https://chrome.google.com/webstore/detail/newtab-color-void/enbboabmkalnjjaciinmnjfbhajpejbl)

<div class="spacerClear"></div>

## Matplotlib Step/Weight/Date Plot
<i class="fab fa-github fa-fw"></i> [https://github.com/kairozu/Kairozu-Sandbox/blob/master/stepcount_weight_vs_date.py](https://github.com/kairozu/Kairozu-Sandbox/blob/master/stepcount_weight_vs_date.py)

I have years upon years of data collected from FitBits, Nike+ Watches, Microsoft Bands, Garmin Forerunners, etc. Quick script to read dates, step counts, and weight from a CSV file named stepcounts.csv 
(file contains header row which is discarded) & plots data for viz purposes. Easy to add other data (sleep, miles run, etc).

## Woodstock Amigurumi
<img class="imageR" height="130" alt="weather" src="/images/woodstock.png" />

It took a few lopsided scarves and squares to pick up the muscle memory for crochet, but it's like riding a bike after that. I didn't use a pattern for Woodstock, and his legs are more like a friendship bracelet than real crochet, but I'm pretty happy with how he turned out. There are some really crazy Amigurumi creations out there, but the return on time investment for crochet (to me) is rough unless you're looking to do something with your hands while otherwise occupied.

June Gilbank's channel on YouTube has a lot of great tutorials that range from (very patient) beginner crochet techniques to creating entire Amigurumi from scratch: [https://www.youtube.com/user/planetjune](https://www.youtube.com/user/planetjune).

<div class="spacerClear"></div>

## TuckerDavis Cable Tester
<img class="imageL" height="150" alt="weather" src="/images/tdtcabletester.jpg" />
<i class="fab fa-github fa-fw"></i> [https://github.com/kairozu/Tucker-Davis-Cable-Tester](https://github.com/kairozu/Tucker-Davis-Cable-Tester)

Extremely quick active/passive cable tester for TDT cables – useful when you have animals that view $1k+ cables as a fine delicacy. Project could be vastly improved without the overkill of a DAQ board that I used, but it was what I had sitting around at the time. Requires an Arduino Mega and a current LabVIEW installation.

<div class="spacerClear"></div>

## TuckerDavis Data Extractor
<img class="imageR" height="170" alt="weather" src="/images/tdtextract_1.png" />
<i class="fab fa-github fa-fw"></i> [https://github.com/kairozu/TDT-Extraction-Sandbox-GUI](https://github.com/kairozu/TDT-Extraction-Sandbox-GUI)

Data extraction tools / GUI in MATLAB for wrangling neuro/electrophys data stored in TDT (TuckerDavis Technologies) tank format.

Instructions for Data Extraction
1. This can be used to extract data saved in the Tucker Davis proprietary tank format -- you MUST have OpenDeveloper installed for this code to work. Tested with various MATLAB versions, including 2012/2013/2014 (Student Edition).
2. OpenDeveloper can be acquired from TDT: [http://www.tdt.com/downloads.html](http://www.tdt.com/downloads.html)
3. This works via ActiveX calls, so if you've disabled those on the operating system side, you'll have errors.
4. Data extracted relative to a specific tank is useful if you want Epoch Data to match recording data timestamps.
5. If you try to extract anything from an empty store (e.g. if you try to extract an epoch that was never triggered) the extraction will fail; this is a bug that will be fixed.. someday.
6. There are better and faster ways of doing this, but this was a quick hack that ended up seeing far more use than I expected.

<div class="spacerClear"></div>

## Silentium Est Aureum
<i class="fab fa-github fa-fw"></i> [https://github.com/kairozu/Silentium-Est-Aureum](https://github.com/kairozu/Silentium-Est-Aureum)

AN EXPERIMENT AND WILL MOST CERTAINLY BREAK SOME WEBSITE SOMEWHERE, USE AT YOUR OWN RISK. This is a Chrome extension that replaces the word "Comments" with "Regrets" and gives a title warning on associated links. It is very basic, will replace text you don't necessarily want replaced, and ultimately should not be used if you don't know what you're doing. That said, it was a fun experiment. To install, either pack the extension yourself, or drag the .crx file into your chrome://extensions window.

## TDT + Mindstorms NXT Connection
<i class="fab fa-github fa-fw"></i> [https://github.com/kairozu/TDT-NXT-Connection](https://github.com/kairozu/TDT-NXT-Connection)

Uses lever inputs on a Mindstorms NXT brick (the "button" NXT input is a simple contact circuit; you can rig your own lever system by halving an NXT accessory cable and creating an open circuit lever with whatever components you have sitting around) to cue a Tucker Davis system epoch while recording neural data. Requires TDT OpenDeveloper. This is absolutely overkill -- I recommend using an Arduino (or similar) instead, unless you'll be using the NXT for something else as well (e.g. conveyor belt).