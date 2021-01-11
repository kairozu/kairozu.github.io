---
layout: content
title: Kairozu Overview
hasimg: /images/kairozu-lesson.png
hasgithub: https://github.com/kairozu/Kairozu-Backup
imgwidth: 240
tags: japanese project code
---
I find Socratic and programmed methods of inquiry to be particularly effective when it comes to retaining information -- my two favorite examples are <a href="https://www.amazon.com/Sidmans-Neuroanatomy-Programmed-Learning-Lippincott/dp/0781765684/">Sidman's Neuroanatomy: A Programmed Learning Tool</a> and <a href="https://www.amazon.com/Little-Schemer-Daniel-P-Friedman/dp/0262560992/">The Little Schemer</a>. After completing the former for a class in college, the process really struck me as a potentially amazing way to learn a language. If I give someone a list of vocabulary words in a new language, and then teach them how to say “the dog is black” and then “the cat is black”, chances are good they’ll be able to say “the bird is black” on their own -- if they can say the bird is black, they can probably also say “the turtle is green.”

Kairozu introduces grammatical constructs using these small, logical steps, which are organized by chapter around groups of new vocabulary words. I tried to minimize wordy grammar explanations and maximize immediate application of small grammar templates, which are then built upon word by word (or particle by particle). The lessons are an attempt to organize the grammar into an easily-referenced format.

<span class="italics">Note: Kairozu is no longer public, but the source is available <a href="https://github.com/kairozu/Kairozu-Backup">here</a>. I've made full database dumps available to previous users and helped them set up their own instances. Thanks everyone for playing with my language-learning system!</span>

<div class="spacerClear"></div>

I pulled data from a variety of Japanese language sources, e.g. <a href="https://kairozu.github.io/updates/nhk-easy-corpus">NHK Easy News (+a Google BigQuery of Reddit posts)</a> and <a href="https://kairozu.github.io/updates/japanese-wiki-corpus">Wikipedia</a>, and wrote a bunch of code to break down the most common words and grammatical constructs -- these are what the computer-generated sentences used in lesson practices and quizzes are drawn from. I've written about some of the basics for getting started with the analysis of Japanese text:
<ul>
<li><a href="https://kairozu.github.io/updates/japanese-tokenization">Japanese Tokenization</a></li>
<li><a href="https://kairozu.github.io/updates/simple-jp-text-analysis">Simple Japanese Text Analysis</a></li>
<li><a href="https://kairozu.github.io/updates/nltk-introduction">An Introduction to NLTK w/Japanese</a></li>
<li><a href="https://kairozu.github.io/updates/cleaning-jp-text">Cleaning Japanese Text Sources</a></li>
</ul>

## Sentences (Practice & クイズ)
If I have a flashcard which only requires the visual recognition of an answer, I won't retain as much as if I need to type, or speak, the answer myself. Kairozu uses English-to-Japanese prompts -- if I know how to say what I want in Japanese, that is, I can come up with the words myself, I can assumedly understand those same words if I read or heard them elsewhere. For practice material, two sentences are presented in English, with textbox prompts to enter the equivalent in Japanese. At first, the full Japanese sentence is visible, meaning I can copy it word for word, but following a correct submission, those hints disappear, reappearing only after an incorrect answer. Quiz sentences are similar to practice sentences, but are only presented one at a time. All sentences have a "literal" reading to assist with translation, e.g. 犬は黒いです would have the literal reading of "as for dog, black is."

## Input Modes
The fringe (?) benefit of requiring the input of full answers is getting used to the Japanese IME on both regular keyboard and phone. While the input fields do accept romaji autoconversion via <a href="https://wanakana.com/">WanaKana.js</a>, I think the additional practice with using a flick-input keyboard on my phone has been useful. All quizzes accept both kanji or kana as input, but you can't pick or choose within a sentence -- e.g. for the sentence "the grapes are delicious" you could input ｢ぶどうはおいしいです｣ or ｢葡萄は美味しいです｣ but not ｢葡萄はおいしいです｣. Most words commonly written as kana are maintained in their kanji forms (e.g. りんご／林檎 and かわいい／可愛い) with a few exceptions, e.g. いい. Users with accounts on Kairozu can have hints/answers shown in their kanji forms via the "Prefer Kanji" setting under Account > Kairozu Settings. Enabling kanji input had the additional benefit of making voice/dictation input (I use Google Keyboard, but iOS's voice dictation also works well) possible with the auto-conversation that occurs. It's good practice as far as pronunciation goes.

Japanese often allows for lots of leeway when it comes to ordering the words in a sentence. Unless a sentence is internally marked as strict (this is invisible to the user), in which case the sentence entered must match Kairozu's exactly, an answer will be accepted as correct so long as all of the words are present, regardless of order. Users with accounts can enable an "Always Strict" mode which removes this leniency by going to Account > Kairozu Settings.

## User Accounts
Previously an account was required to access most of the lesson/quiz material, as progress through the material was tracked and limited to require mastering previous content before continuing on. While all of the material is accessible now without an account, using non-default options (e.g. displaying hints in kanji) and creating custom flashcards requires an account to be created. The public view of Kairozu is no longer active, and most users have been transitioned to local instances maintained by other people, but I don't mind adding new people to my private instance if they shoot me an e-mail: amber@kairozu.com.

## Flashcards
My personal usage of Kairozu is largely in the Flashcards system. You can import flashcards from the vocabulary lists or lesson quizzes, or you can upload a CSV file to batch-import flashcards from elsewhere. The review system follows a general spaced-review algorithm, with two possible input modes -- text reviews require entering the sentence in Japanese following an English prompt, and quick reviews are more akin to a typical flashcard system where you declare whether you knew the material or not once the answer is shown. Of course entering the text is better for memory retention, but when on a mobile device, the quick system is far more convenient. You can hop between them, or access text-entry mode for extra practice after answering a quick review question incorrectly.

<div class="flexBox">
	<a href="/images/flashcard-quick.png"><img width="300" src="/images/flashcard-quick.png" alt="flashcard quick prompt" /></a>
	<a href="/images/flashcard-quick-ans.png"><img width="300" src="/images/flashcard-quick-ans.png" alt="flashcard quick answer" /></a>
    <a href="/images/flashcard-quick-text.png"><img width="300" src="/images/flashcard-quick-text.png" alt="flashcard text mode" /></a>
</div>

## Screenshots
These are various screenshots from a number of pages on the previously hosted nihongo.kairozu.com.

<div class="flexBox">
	<a href="/images/nihongo_kai1.png"><img width="300" src="/images/nihongo_kai1.png" alt="front page" /></a>
	<a href="/images/nihongo_kai2.png"><img width="300" src="/images/nihongo_kai2.png" alt="lesson1" /></a>
    <a href="/images/nihongo_kai3.png"><img width="300" src="/images/nihongo_kai3.png" alt="lesson2" /></a>
</div>

<div class="spacerClear"></div>

<div class="flexBox">
	<a href="/images/nihongo_kai4.png"><img width="300" src="/images/nihongo_kai4.png" alt="hiragana practice" /></a>
	<a href="/images/nihongo_kai5.png"><img width="300" src="/images/nihongo_kai5.png" alt="counter practice" /></a>
    <a href="/images/nihongo_kai6.png"><img width="300" src="/images/nihongo_kai6.png" alt="lesson selection" /></a>
</div>