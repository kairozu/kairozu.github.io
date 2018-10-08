---
layout: content
title: Simple Japanese Games
tags: japanese project code
---
A collection of JavaScript-based web tools for studying Japanese hiragana, katakana, particles, and counters. The former two are easily modified for other a/b-style sets of data. The tool for particles presents a sentence in Japanese with a particle missing, an English translation to clarify the meaning of the sentence, and four options for appropriate particles. The counter tool shows a set of 1-10 items and asks for the Japanese translation. 

## ひらがな と カタカナ
Arrow keys or W/A/S/D keys can be used to direct the center character to the matching "outer" character. If the answer is correct, a new question will be presented; if the answer is incorrect, the incorrect options will disappear to help identify the correct character. For every 20 points that the score increases, the level will increase, which introduces an additional 5 characters. Clicking "reset" will reset the level/score/streak. Clicking "mode" will swap between romaji/hiragana (or katakana) as the center character. Clicking "level" will increase the # of available characters (max: 10), sidestepping the score-based progression.

These are older versions of the Hiragana/Katakana swipe tools, adapted as Android games:
* Android version of the Hiragana tool: [https://play.google.com/store/apps/details?id=com.dendriticspine.tenkohiragana](https://play.google.com/store/apps/details?id=com.dendriticspine.tenkohiragana)
* Android version of the Katakana tool: [https://play.google.com/store/apps/details?id=com.dendriticspine.tenkokatakana](https://play.google.com/store/apps/details?id=com.dendriticspine.tenkokatakana)

## 助詞 (Particles)
A sentence with a missing particle (or missing particles) will be shown, along with 4 possible answers. Use either 1/2/3/4 (or A/S/D/F) keys to select the most correct particle, or select the particle by clicking w/the mouse. An English translation is shown to help with ambiguous cases where multiple particles might be grammatically correct. After the correct particle is chosen, it will take its rightful place in the sentence. Five seconds later, a new sentence will be shown.

I highly recommend the (vibrantly pink) book "All About Particles, A Handbook of Japanese Function Words" by Naoko Chino for studying particle usage. Good examples and a wide range of usage cases. Best particle reference I've seen.

## 助数詞 (Counters)
Most countable things in Japan have associated counter-words which are used to express numerical quantities. These are similar in function to the word “pieces” in “three pieces of paper” or “cup” in “four cups of tea,” but they cannot be used w/o an associated number. While only a fraction of these would be considered for common usage, there are many, many more:
[https://en.wikipedia.org/wiki/Japanese_counter_word#Extended_list_of_counters](https://en.wikipedia.org/wiki/Japanese_counter_word#Extended_list_of_counters)

I tried creating flashcards for the more common ones, but ultimately when a situation arose where I’d need a counter, I’d struggle to recall which counter would be appropriate. In an attempt to make my studying more effective, I made a page where a random number of objects is presented with a short description. You enter the number (phonetically) and the appropriate counter (don’t include the name of the object!) in the text box and hit “enter” to submit. 

Clicking 漢字 will change the input mode to kanji (instead of hiragana); clicking again will toggle back to hiragana. To use the kanji method, you'll need a Japanese input method. For Linux, I recommend IBus+Anthy, and for Windows, you can enable additional language input via the language control panel (charms -> settings -> change PC settings -> time and language -> region and language -> add a language). Clicking “?” under “GUIDE” will show you the objects available, the hiragana representations I’ve used, and the appropriate kanji.

The counters I’ve used are:

* 度　（ど）　degrees (e.g. degrees C/F)
* 杯　（はい）　cups of coffee, pints of beer
*  つ　（つ）　general counter.. or when you can’t remember
* 人　（り・にん）　people
* 錠　（じょう）　pills
* 個　（こ）　general counter for small objects
* 本　（ほん）　long, thin objects (pencils, bananas, dango)
* 枚　（まい）　flat, thin objects (paper, envelopes, t-shirts)
* 冊　（さつ）　bound objects (books)
* 台　（だい）　machines (cars, computers, bicycles)
* 匹　（ひき）　cats, mice, dogs, insects, bees, fish
* 羽　（わ）　birds and rabbits
* 箱　（はこ）　boxes
* 階　（かい）　floors in a building
* 名　（めい）　customers (people, but polite)
* 時間　（じかん）　hours (duration)

It seems that there is some leeway with certain objects (i.e. when using つ vs こ), which means there might be no perfect answer (or the answer might vary depending on where in Japan you are and whom you’re talking to). Hence the “guide” listing of where each object falls.  Some of the counters are.. tricky. I’m still not 100% sure for some of the categories I’ve put things in (e.g. pizza is in -まい right now because it is flat and thin.. but should it be -きれ because it’s a slice of something?).  

I relied heavily upon these pages for reference:

* [http://www.eigo21.com/jp/number/index.htm](http://www.eigo21.com/jp/number/index.htm)
* [http://www.guidetojapanese.org/learn/complete/counting](http://www.guidetojapanese.org/learn/complete/counting)
* [https://en.wikipedia.org/wiki/Japanese_counter_word](https://en.wikipedia.org/wiki/Japanese_counter_word)
