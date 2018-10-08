---
layout: content
title: Simple JP Text Analysis
tags: japanese code
---

This is a quick tutorial on using Python to 1) load a simple text file with some Japanese text, 2) perform word tokenization on individual sentences using MeCab, 3) count the most frequently used nouns in the text, 4) perform a quick-and-dirty conversion of past-tense sentences to present-tense. The files mentioned below are also available in the [Japanese-Text-Analysis GitHub repo](https://github.com/kairozu/Japanese-Text-Analysis).

We'll use a simplified version of the [Ant and the Grasshopper](http://read.gov/aesop/052.html), in the file [grasshopper.txt](https://github.com/kairozu/Japanese-Text-Analysis/blob/master/simple-jp-text-analysis/grasshopper.txt).

```
夏は暑いです。螽斯が木の下にいます。螽斯は歌を歌います。楽しいです。蟻が来ました。
蟻は食べ物を運びます。螽斯が言いました。蟻さん、一緒に歌を歌いましょう。
蟻は言いました。いいえ、歌いません。私達は働きます。螽斯は聞きました。
どうしてですか。冬は食べ物がありませんから。今は夏ですよ。螽斯は笑いました。
それから毎日、螽斯は歌を歌いました。働きませんでした。冬です。雪が降ります。
とても寒いです。螽斯の家には、食べ物がありません。蟻の家には、食べ物がたくさんあります。 
螽斯は、蟻の家へ行きました。螽斯は言いました。蟻さん、お願いです。食べ物を下さい。
蟻は言いました。私達は、夏、働きました。だから、食べ物があります。あなたは夏、何をしましたか。
```

And the following Python script: [grasshopper_analysis.py](https://github.com/kairozu/Japanese-Text-Analysis/blob/master/simple-jp-text-analysis/grasshopper_analysis.py).
```
import MeCab
from collections import Counter                             # for counting most common elements

# load MeCab and the mecab-ipadic-neologd dictionary
# https://github.com/neologd/mecab-ipadic-neologd
# mct = MeCab.Tagger("-O chasen -d /usr/lib/x86_64-linux-gnu/mecab/dic/mecab-ipadic-neologd")
mct = MeCab.Tagger("-O chasen -d /usr/local/lib/mecab/dic/mecab-ipadic-neologd/")

# simple recreation of previous MeCab command line tests; parse and tokenize sentence
print(mct.parse('今日はいい天気ですね。'))

gh_text = open('grasshopper.txt', 'r').read()               # open text file and read it into gh_text

# split text into sentences on '。' character, and then replace the ending '。' on all sentences
gh_lines = gh_text.split('。')
gh_lines = [x + '。' for x in gh_lines if len(x) > 0]

nouns = []                                                  # create empty lists for nouns, verbs, adj
verbs = []
adjectives = []

for sentence in gh_lines:                                   # loop through each sentence in gh_lines
    jparse_bug = mct.parse(sentence)
    jparse = mct.parseToNode(sentence)

    while jparse:
        mct_split = jparse.feature.split(',')               # split features up by commas
        if mct_split[0] == '名詞':
            nouns.append(jparse.surface)                    # if word is a noun, add the element to nouns
        elif mct_split[0] == '動詞':
            verbs.append(jparse.surface)                    # if word is a verb, add the element to verbs
        elif mct_split[0] == '形容詞':
            adjectives.append(jparse.surface)               # if word is an adj, add the element to adj
        jparse = jparse.next                                # move on to the next word-token

noun_counts = str(Counter(nouns).most_common(3))            # count 3 most common nouns (convert to str)
verb_counts = str(Counter(verbs).most_common(3))            # count 3 most common verbs (convert to str)
adjective_counts = str(Counter(adjectives).most_common(3))  # count  3 most common adjectives (convert to str)

print(noun_counts)                                          # print the 3 most comon nouns
print(adjective_counts)                                     # print the 3 most common adjectives
print(verb_counts)                                          # print the 3 most common verbs
```

Running [grasshopper_analysis.py](https://github.com/kairozu/Japanese-Text-Analysis/blob/master/simple-jp-text-analysis/grasshopper_analysis.py) from the command line will (should?) print a breakdown of the example sentence「今日はいい天気ですね」and a list of the 3 most common nouns, adjectives, and verbs.

```
$ python3 ./grasshopper_analysis.py
今日	キョウ	今日	名詞-副詞可能
は	ハ	は	助詞-係助詞
いい	イイ	いい	形容詞-自立	形容詞・イイ	基本形
天気	テンキ	天気	名詞-一般
です	デス	です	助動詞		特殊・デス	基本形
ね	ネ	ね	助詞-終助詞
。	。	。	記号-句点

[('螽斯', 9), 	('蟻', 8), 	('食べ物', 6)]
[('暑い', 1), 	('楽しい', 1), 	('寒い', 1)]
[('歌い', 4), 	('あり', 4), 	('言い', 4)]
```

Looking at the bottom three lines of text above:
<ul>
<li>The three most common nouns are: grasshopper (螽斯・キリギリス), ant (蟻・アリ), and food (食べ物・たべもの).</li>
<li>The three most common adjectives are: hot (暑い・あつい), fun (楽しい・たのしい), and cold (寒い・さむい).</li>
<li>The three most common verbs are (in dictionary form): to sing (歌う・うたう), to exist (ある), to say (言う・いう).</li>
</ul>

Next, [grasshopper_past_present.py](https://github.com/kairozu/Japanese-Text-Analysis/blob/master/simple-jp-text-analysis/grasshopper_past_present.py) will print all of the sentences which are in present tense, followed by the sentences in past-tense, followed by the sentences in past-tense converted into present-tense. Changing 'した' to 'す' is a pretty messy strategy for changing past-tense to present, but in this case we only have one edge case with a negative-past sentence (〜ませんでした).

```
import MeCab, re                                                    # regex library (for finding tense)

# load MeCab and the mecab-ipadic-neologd dictionary
# https://github.com/neologd/mecab-ipadic-neologd
# mct = MeCab.Tagger("-O chasen -d /usr/lib/x86_64-linux-gnu/mecab/dic/mecab-ipadic-neologd")
mct = MeCab.Tagger("-O chasen -d /usr/local/lib/mecab/dic/mecab-ipadic-neologd/")

gh_text = open('grasshopper.txt', 'r').read()                       # open text file, read into gh_text

# split text into sentences on '。' character, and then replace the ending '。' on all sentences
gh_lines = gh_text.split('。')
gh_lines = [x + '。' for x in gh_lines if len(x) > 0]

past = set()                                                        # create empty set for past-tense lines

for sentence in gh_lines:                                           # loop through sentences in gh_lines
    jparse_bug = mct.parse(sentence)
    jparse = mct.parseToNode(sentence)

    while jparse:                                                   # while there are word-tokens in sentence
        if jparse.posid == 25:                                      # catches verb conjugations
            # in this case, past-tense conj. have 'た'
            if jparse.surface == 'た':
                past.add(sentence)                                  # if 'た' was found, add to past-tense
        jparse = jparse.next                                        # move to the next word-token

present = set(gh_lines) - past                                      # remove lines in past from gh_lines

print("Grasshopper and the Ant sentences in present-tense:")
[print(x) for x in present]                                         # "for every x in present, print x"
print("\nGrasshopper and the Ant sentences in past-tense:")
[print(x) for x in past]                                            # "for every x in past, print x"

new_present = []                                                    # empty list for past-tense-to-present

# change all of the sentences in past-tense, to present-tense
for past_sentence in list(past):
    # change negative-past to negative, and postive-past to present
    now_present = re.sub('ませんでした', 'ません', past_sentence)
    now_present = re.sub('した', 'す', past_sentence)
    new_present.append(now_present)                                 # add to list new_present sentences

print("\nGrasshopper and the Ant sentences, past-to-present:")
[print(x) for x in new_present]                                     # "for every x in new_present, print x"
```
```
$ python3 ./grasshopper_past_present.py
Grasshopper and the Ant sentences in present-tense:
どうしてですか。
楽しいです。
螽斯が木の下にいます。
だから、食べ物があります。
蟻さん、お願いです。
とても寒いです。
蟻の家には、食べ物がたくさんあります。
蟻は食べ物を運びます。
蟻さん、一緒に歌を歌いましょう。
今は夏ですよ。
私達は働きます。
食べ物を下さい。
夏は暑いです。
いいえ、歌いません。
螽斯は歌を歌います。
冬です。
螽斯の家には、食べ物がありません。
冬は食べ物がありませんから。
雪が降ります。

Grasshopper and the Ant sentences in the past-tense:
私達は、夏、働きました。
蟻が来ました。
螽斯が言いました。
螽斯は、蟻の家へ行きました。
あなたは夏、何をしましたか。
それから毎日、螽斯は歌を歌いました。
螽斯は聞きました。
蟻は言いました。
働きませんでした。
螽斯は言いました。
螽斯は笑いました。

Grasshopper and the Ant sentences, once past, now present-tense:
私達は、夏、働きます。
蟻が来ます。
螽斯が言います。
螽斯は、蟻の家へ行きます。
あなたは夏、何をしますか。
それから毎日、螽斯は歌を歌います。
螽斯は聞きます。
蟻は言います。
働きませんです。
螽斯は言います。
螽斯は笑います。
```