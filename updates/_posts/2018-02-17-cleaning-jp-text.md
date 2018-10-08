---
layout: content
title: Cleaning Japanese Text
tags: japanese code
---
Mining text sources from the web yields all sorts of textual oddities that'll destroy any morphological analysis and word-tokenization attempts. I remove residual formatting tags and other non-text data, and then try to dismiss text which falls outside of a normal sentence structure (contact information, headlines, etc). The files mentioned below are also available in the [jp-text-cleaning GitHub repo](https://github.com/kairozu/Japanese-Text-Analysis/tree/master/jp-text-cleaning).

## HTML Tags
I find it easiest to remove most HTML tags with a dedicated parser like [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/) -- this works for both extracting desired text from a larger document, and dismissing unwanted text within certain elements.

In the file [article.html](https://github.com/kairozu/Japanese-Text-Analysis/blob/master/jp-text-cleaning/article.html), my desired text is inside the "newsarticle" div. The text itself is also littered with other HTML tags. The script below removes most of the HTML with BeautifulSoup before stripping out excess whitespace and line breaks. There are a few different regex options for removing residual HTML tags; I use a catch-all for anything that's between angle brackets. [Regex101](https://regex101.com/) is a good site for testing patterns with various text examples (make sure to choose a language on the left).

```
from bs4 import BeautifulSoup
import re

with open('article.html') as f:
    text = f.read()                             # read in the article.html file
soup = BeautifulSoup(text, 'html.parser')       # run text through BeautifulSoup

# .decompose() removes tags specified and the text between them
# .unwrap() also removes the tags, but leaves the text inside untouched
for h2 in soup("h2"):               # remove h2 tags and everything between them
    h2.decompose()
for rt in soup("rt"):               # rt tags & text are furigana readings; remove these
    rt.decompose()
for ruby in soup("ruby"):           # remove ruby tags, but leave the text inside
    ruby.unwrap()

article = soup.find(id="newsarticle")           # the text I want is within the div w/id "newsarticle"
article = str(article).splitlines()             # convert to string
text = ''
for line in article:
    line = line.strip()                         # remove excess whitespace
    text = text + line                          # recombine text after removing whitespace

text = re.sub(r'<.*?>', '', text)                       # removes ALL HTML tags+attributes
# article = re.sub(r'<[ / ]?br[ / ]?>', '', article)    # removes all variations of br tags
# article = re.sub(r'<[/]?p.*?>', '', article)          # removes p tags and their attributes
# article = re.sub(r'<[/]?div.*?>', '', article)        # removes div tags and their attributes

article_clean = open('article_clean.txt', 'w')
article_clean.write(text)
article_clean.close()
```

Now I have a text file, [article_clean.txt](https://github.com/kairozu/Japanese-Text-Analysis/blob/master/jp-text-cleaning/article_clean.txt), with a "clean" paragraph of text. By clean, I mean free of HTML -- there might be other odds and ends mixed with the text (author names, phone numbers, text which originally served as a link, etc). 

## Japanese Unicode Ranges

I use [DecodeUnicode](http://www.decodeunicode.org) and [Unicode Table](https://unicode-table.com) for Unicode reference, and this [Library of Congress Site](https://memory.loc.gov/diglib/codetables/9.1.html) also has a table with 13,478 kanji character encodings. Using the unicode ranges for regex purposes is useful -- after some initial processing I tend to throw out every sentence with special characters. It takes too much time to go through these oddball sentences one by one, and they're decent indicators for imperfect sentence structures or otherwise undesirable text for eventual analysis.

<div class="divResponsive">
<table class="smaller">
<tbody>
<tr><td>Japanese Space</td><td>\u3000</td></tr>
<tr><td>Japanese Comma 、</td><td>\u3001</td></tr>
<tr><td>Japanese Period 。</td><td>\u3002</td></tr>
<tr><td>Vowel Elongation ー</td><td>\u30FC</td></tr>
<tr><td>Left Corner Bracket 「</td><td>\u300C</td></tr>
<tr><td>Right Corner Bracket 」</td><td>\u300D</td></tr>
<tr><td>JP Left Parenthesis （</td><td>\uFF08</td></tr>
<tr><td>JP Right Parenthesis ）</td><td>\uFF09</td></tr>
<tr><td>Japanese Exclamation ！</td><td>\uFF01</td></tr>
<tr><td>Japanese Question ？</td><td>\uFF1F</td></tr>
<tr><td>&nbsp;</td><td></td></tr>
<tr class="bold"><td>Hiragana</td><td>\u3040-\u309F</td></tr>
<tr class="bold"><td>Katakana</td><td>\u30A0-\u30FF</td></tr>
<tr><td>Japanese Symbols & Punctuation</td><td>\u3000-\u303F</td></tr>
<tr><td>Full-Width Punctuation, Numbers, Latin&#x3000;</td><td>\uFF01-\uFF60</td></tr>
<tr><td>Half-Width Punctuation & Katakana</td><td>\uFF61-\uFFEE</td></tr>
<tr class="bold"><td>Kanji</td><td>\u4E00-\u9FAF</td></tr>
<tr><td>Extended Kanji</td><td>\u3400-\u4DB5 \u4E00-\u9FCB \uF900-\uFA6A</td></tr>
<tr><td>Non-Punctuation Japanese</td><td>\u3040-\u9FAF</td></tr>
<tr><td>Kanji Radicals</td><td>\u2E80-\u2FD5</td></tr>
<tr><td>Other JP Symbols & Characters</td><td>\u31F0-\u31FF \u3220-\u3243 \u3280-\u337F</td></tr>
<tr><td>Enclosed Numbers (e.g. ①②③④)</td><td>\u2460-\u24FF</td></tr>
<tr><td>Shapes (e.g. ◉▶◩◿)</td><td>\u25A0-\u26FF</td></tr>
</tbody>
</table>
</div>

## Splitting Paragraphs into Sentences
Next, in [extract_sentences.py](https://github.com/kairozu/Japanese-Text-Analysis/blob/master/jp-text-cleaning/extract_sentences.py), I perform the following steps (some of which are functions in the file [spring_clean.py](https://github.com/kairozu/Japanese-Text-Analysis/blob/master/jp-text-cleaning/spring_clean.py)):
<ul>
<li>Change any Latin character set punctuation marks to their full-width Japanese equivalents, namely parentheses, question marks, and exclamation points. This makes for easier pattern matching.</li>
<li>Split the text on the Japanese period (。), then split the resulting strings on exclamation points and question marks (！？).</li>
<li>Dismiss any sentences without equal numbers of brackets/parentheses/etc, as it indicates the sentence was probably split improperly (e.g. it was split on a period which was inside a parenthetical, leaving one half of the statement with the prior sentence, and the other half with the latter) -- there are better ways to deal with this data if you want to preserve this text.</li>
<li>Dismiss sentences which have fewer than 4 characters, with more than a single set of parentheses/corner quotes, or with weird characters.</li>
</ul>

```
from spring_clean import punctuation, clean_text_check

sentence_collection = []            # hold the new list of sentences

def split_on_exclaim(text):         # see full file in github repo
    """splits text on！and adds results to sentence_collection"""

def split_on_question(text):        # see full file in github repo
    """splits on ？ and sends lines with ！ to split_on_exclaim"""

def split_to_sentences(text):       # see full file in github repo
    """splits on 。 and sends lines with ？ or ！ to their own split functions"""

with open('article_clean.txt') as f:
    paragraph = f.read()

sentences_clean = open("sentences_clean.txt", "w", encoding='utf-8')
paragraph = punctuation(paragraph)      # normalize punctuation
split_to_sentences(paragraph)           # split to sentences based on punctuation

for sentence in sentence_collection:
    if sentence.count('（') != sentence.count('）') or sentence.count('「') != sentence.count('」'):
        # bracket mismatches are dismissed
        pass
    else:
        if clean_text_check(sentence):          # check for weird characters and other deal breakers
            sentences_clean.write(sentence)     # write to file
            sentences_clean.write("\n")         # write line break to file

sentences_clean.close()
```

This yields a file of sentences, [sentences_clean.txt](https://github.com/kairozu/Japanese-Text-Analysis/blob/master/jp-text-cleaning/sentences_clean.txt), with one sentence per line.

## Bad Sentences
Unsurprisingly, when you scrape text from the internet, you end up with some weird edge cases. Unexpected characters. Paragraph headers and sub-headers. Lists. Dialogues. Phone numbers. Addresses. Typos. Odd spaces. Quizzes. Mixes of punctuation character types (e.g. roman character left parenthesis matched with a Japanese character right parenthesis). Song lyrics. The list goes on and on and on. While some amount of work is worthwhile for preserving useful text in a data set, the best strategy for cleaning data is similar to cleaning your fridge or your closet.. WHEN IN DOUBT, THROW IT OUT. It's not worth dealing with 100 sentence edge cases when you have 200,000 other sentences.