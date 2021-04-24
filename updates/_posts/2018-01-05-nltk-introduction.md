---
layout: content
title: NLTK Basics
tags: japanese code
---
NLTK, or the Natural Language Toolkit, is a Python-based series of libraries and other tools for symbolic and statistical natural language processing. This is a short introduction to some of the basic functions and how they apply with Japanese text. All code snippets below are combined into a single file for download here: [japanese_nltk_basics.py](https://github.com/cryptogramber/Japanese-Text-Analysis/blob/master/nltk-basics/japanese_nltk_basics.py).

The online book [Natural Language Processing with Python](http://www.nltk.org/book/) is a wonderful overview of NLTK (in English), and the author of the [Japanese translation](https://www.oreilly.co.jp/books/9784873114705/), [Masato Hagiwara](http://masatohagiwara.net/), has written an excellent addition to [Japanese-specific applications](http://www.nltk.org/book-jp/ch12.html).

If you haven't already: [install NLTK](https://www.nltk.org/install.html) and then [install the NLTK data](https://www.nltk.org/data.html).

These examples use the JEITA Public Morphologically Tagged Corpus and the KNB Corpus. First, we'll print all of the file identifiers in both corpuses, and then focusing on the JEITA corpus, compare the average word length, average sentence length, and lexical diversity for each fileid.

```python
import nltk
from nltk.corpus import jeita
from nltk.corpus import knbc

print("file identifiers in the jeita and knbc corpuses:")
print(jeita.fileids())
print(knbc.fileids())

print("avg word length, avg sentence length, and lexical diversity for each fileid in JEITA:")
for fileid in jeita.fileids():
    num_chars = len(jeita.raw(fileid))
    num_words = len(jeita.words(fileid))
    num_sents = len(jeita.sents(fileid))
    num_vocab = len(set(w.lower() for w in jeita.words(fileid)))
    print(round(num_chars/num_words), round(num_words/num_sents), round(num_words/num_vocab), fileid)
```

A quick look at some of the access methods for the JEITA corpus -- the first ten words, the following five words with their part-of-speech tags, and the full list of methods available.

```python
print(jeita.words()[0:10])          # first ten words in the JEITA corpus
print(jeita.tagged_words()[10:20])  # next ten words with their part-of-speech tags in the JEITA corpus
print(dir(jeita))                   # methods available in the JEITA corpus
```

The part-of-speech tags are returned as a tuple with the word itself -- the pronunciation of the word, its unconjugated form, and the part-of-speech tags are separated by tab (<code>\t</code>) breaks. Part-of-speech tags can be found at the bottom of this post: [Japanese Tokenization](https://cryptogramber.github.io/updates/japanese-tokenization). The table below is expanded for easier reading:

<div class="divResponsive">
<table>
    <tr><td>('から',&nbsp;&nbsp;</td><td>&nbsp;'カラ&nbsp;</td><td>&nbsp;\t&nbsp;</td><td>から </td><td>&nbsp;\t&nbsp;</td><td>助詞</td><td>格助詞&nbsp;</td><td>一般'),</td><td>      </td><td>   </td><td>        </td></tr>
    <tr><td>('まけ',</td><td>'マケ</td><td>\t</td><td>まける&nbsp;&nbsp;</td><td>\t</td><td>動詞</td><td>自立</td><td>\t     </td><td>一段   </td><td>\t&nbsp;&nbsp;</td><td>連用形'), </td></tr>
    <tr><td>('出さ',</td><td>'ダサ</td><td>\t</td><td>出す </td><td>\t</td><td>動詞</td><td>自立</td><td>\t     </td><td>五段・サ行&nbsp;&nbsp;</td><td>\t&nbsp;&nbsp;</td><td>未然形'),</td></tr>
    <tr><td>('れ',</td><td>'レ   </td><td>\t</td><td>れる </td><td>\t</td><td>動詞</td><td>接尾</td><td>\t     </td><td>一段    </td><td>\t&nbsp;&nbsp;</td><td>連用形'),  </td></tr>
    <tr><td>('た',</td><td>'タ   </td><td>\t</td><td>た </td><td>\t</td><td>助動詞</td><td>      </td><td>\t</td><td>特殊・タ</td><td>\t&nbsp;&nbsp;</td><td>基本形')</td></tr>
</table>
</div>

Next, let's load a single file from the JEITA corpus as an NLTK Text (offers more functionality for text analysis, e.g. concordance, collocation discovery, regular expression search over tokenized strings, etc) and look at the data.

```python
jsingle_t = nltk.Text(jeita.words('a0010.chasen'))  # load 'a0010.chasen' as an NLTK Text
print(len(jsingle_t))                               # total number of words/symbols ("tokens")
print(len(set(jsingle_t)))                          # unique number of words/symbols ("tokens")
print(jsingle_t.count("夜"))                         # number of times '夜' occurs in the text
```

A dispersion plot shows the locations of a word in the text; each stripe represents an instance of a word, and each row represents the entire text. A frequency distribution tells us the frequency of each vocabulary item in the text, from which we can pull the most common elements.

```python
jsingle_t.dispersion_plot(["見る", "地", "時間", "今", "高い"])    # location of words in text
fdist_j = nltk.FreqDist(jsingle_t)                              # frequency distribution
print(fdist_j.most_common(50))                                  # 50 most common elements
```

More fun with words and patterns:

```python
jsingle_ts = set(jsingle_t)      # remove duplicates

print(sorted(w for w in jsingle_ts if w.endswith('しい')))      # words in a0010 ending in しい
print(sorted(w for w in jsingle_ts if w.startswith('見')))      # words in a0010 starting with 見
print(sorted(w for w in jsingle_ts if '山' in w))               # words in a0010 which contain 山
print(sorted(w for w in jsingle_ts if '上' in w or '下' in w))  # words in a0010 which contain 上 or 下

# for each word w in the vocabulary jsingle_ts, check whether len(w) is > or = 3
print(sorted(w for w in jsingle_ts if len(w) >= 3))

# for each word w in jsingle_ts, check if length is >= 3, and if it occurs >= 3 times
print(sorted(w for w in jsingle_ts if len(w) >= 3 and fdist_j[w] >= 3))
```

Examples above rely on a single piece of the JEITA corpus, now let's create NLTK Texts for each corpus in full. Again, we use frequency distributions to see the 50 most common words from each corpus. Collocations show sequences of words which appear together unusually often in the text -- e.g. "science fiction"  or "teddy bear" might be collocations in an English text. Concordances show occurrences of a token (in the case below, '人') with the context in which it appears. Using similar(token) returns a list of words that appear in the same context (with the same words on either side) as the token (this doesn't mean the words themselves are similar).

```python
jfull_t = nltk.Text(jeita.words())           # create NLTK Text from JEITA Corpus
kfull_t = nltk.Text(knbc.words())            # create NLTK Text from KNB Corpus

fdist_jfull = nltk.FreqDist(jfull_t)         # create frequency dist from JEITA Corpus
print(fdist_jfull.most_common(50))           # 50 most common words in JEITA Corpus
fdist_kfull = nltk.FreqDist(kfull_t)         # create frequency dist from KNB Corpus
print(fdist_kfull.most_common(50))           # 50 most common words in KNB Corpus

# a collocation is a sequence of words that occur together unusually often
print(jfull_t.collocations())
print(kfull_t.collocations())

# occurrences of '人' in the text with surrounding context
print(jfull_t.concordance("人"))
print(kfull_t.concordance("人"))

# words that appear in the same context (same words on either side) as '人'
print(jfull_t.similar("人"))
print(kfull_t.similar("人"))
```