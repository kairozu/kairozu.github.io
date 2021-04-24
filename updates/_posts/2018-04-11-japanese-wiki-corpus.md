---
layout: content
title: Wikipedia JP Corpus
tags: japanese code 
---
This outlines the process of downloading a Japanese Wikipedia database snapshot, extracting the plain text content, and performing some pretty heavy filtering to clean up the resulting data. This focuses on building a collection of sentences without regard for the original articles; the end result is ~1.2GB of text (nearly 10 million sentences).

Database dumps of the Japanese language Wikipedia are available here: [https://dumps.wikimedia.org/jawiki/](https://dumps.wikimedia.org/jawiki/) -- I used the files from March 30, 2018 ([jawiki-20180301-pages-articles-multistream.xml.bz2](https://dumps.wikimedia.org/jawiki/20180301/jawiki-20180301-pages-articles-multistream.xml.bz2), [jawiki-20180301-pages-articles-multistream-index.txt.bz2](https://dumps.wikimedia.org/jawiki/20180301/jawiki-20180301-pages-articles-multistream-index.txt.bz2)). Most of the files mentioned below are also available in the [Japanese-Text-Analysis GitHub repo](https://github.com/cryptogramber/Japanese-Text-Analysis/tree/master/wiki-jp-corpus).

I used [this Wikipedia extractor tool](https://github.com/bwbaugh/wikipedia-extractor) to pull plain text from the database dump -- this will discard image references, tables, lists, and other annotations usually present in Wikipedia pages. The command below uses the default output file size of 500K (-b 500K), and took ~84 minutes to extract the full 1503793 articles.

```terminal
$ bzcat jawiki-20180301-pages-articles-multistream.xml.bz2 | python WikiExtractor.py -o texts -
```

This will create a directory <code>texts/</code> with 28 subdirectories (named AA, AB, AC, etc through BB), each containing ~100 text files. Each file has a number of Wikipedia articles grouped by doc tags, e.g. the article for [地理 (geography)](https://ja.wikipedia.org/wiki?curid=56) would be reduced to the following -- note that the lists of information have already been removed:

```html
<doc id="56" url="https://ja.wikipedia.org/wiki?curid=56" title="地理"\>
地理

地理（ちり、英: Geography）
「地理」という表現は古くからあり、有名なところでは漢書の『地理志』がある。 
地理学とは、地球の表面と住民の状態、その相互関係を研究する学問である。
「地理」は、日本の学校で設置されている、「人間の生活に影響を与える地域的、社会的な構造」を学ぶための科目である。 
自然環境や産業環境などを含む環境を学習対象としている。
小学校および中学校においては、歴史や公民と並び、社会科の一分野である。
高等学校においては、最近は「地理歴史科」という教科の中の一科目となっており、「地理A」「地理B」に細分されている。
</doc>
```

I use [wikiclean.py](https://github.com/cryptogramber/Japanese-Text-Analysis/blob/master/wiki-jp-corpus/wikiclean.py) to (0) normalize latin parentheses to full-width parentheses, (1) remove full articles with doc tags for internal Wikipedia stuff, subject categories, etc, (2) remove the opening doc tag for other articles, as well as the article name which generally isolated text on the line following, (3) remove the closing doc tags, (4) remove line breaks, (5) remove all parentheticals, (6) remove other content between tags, (7) remove all lines w/o ending punctuation.

```python
wikitext = punctuation(wikitext)
wikitext = re.sub(r'&lt;doc.*?title=.*?:.*?&gt;([\s\S]*?)&lt;/doc&gt;', '', wikitext)   # (1) remove cat/wiki/img entries
wikitext = re.sub(r'&lt;doc.*?&gt;\n.*\n', '', wikitext)      # (2) remove opening doc tags & title on next line
wikitext = re.sub(r'&lt;[ / ]?doc[ / ]?&gt;', '', wikitext)   # (3) remove closing doc tags
wikitext = re.sub(r'&lt;[ / ]?br[ / ]?&gt;', '', wikitext)    # (4) remove all variation of linebreaks
wikitext = re.sub(r'[\(\uff08][^\(\uff08\)\uff09]*[\)\uff09]', '', wikitext) # (5) remove parentheticals
wikitext = re.sub(r'&lt;.*?&gt;([\s\S]*?)&lt;/.*?&gt;', '', wikitext)   # (6) remove other content between tags
wikitext = re.sub(r'.+(?&lt;![。！？])\n', '', wikitext)        # (7) remove all lines w/o ending punctuation
```

I save the text processed above to a single text file, <code>wikiclean.txt</code> -- this file is ~2.4GB. The next processing step uses [wikisentences.py](https://github.com/cryptogramber/Japanese-Text-Analysis/blob/master/wiki-jp-corpus/wikisentences.py) to read that file and sort sentences based on some pretty heavy filters -- if you don't want a collection of sentences split by newlines, this step is counterproductive. This step will remove A LOT of data -- it's always tempting to try and save as much as possible, but the cost is usually the cleanliness of your results. If you need to preserve more data, the most significant changes would be removing the blanket filter on left and right corner brackets, and not filtering out the latin alphabet. With the current filters, there are 9266337 sentences that survive.

```python
if (re.search('[,「」（）［］《》＜＞{}@&＆#＃※=＝+＋/／；;：:…]', sentence)     # dismiss brackets, etc
    or re.search('[a-zA-Z]', sentence)                  # dismiss any latin alphabet characters
    or re.search('[\u2150-\u218F\u2190-\u21FF\u2460-\u26FF]', sentence)     # shapes, icons, etc
    or re.search('[\u3003-\u300B\u300E-\u301B\u301D-\u303F]', sentence)     # shapes, icons, etc
    or re.search('、{2,}', sentence)                    # dismiss if more than 2 、in a row
    or re.search('、。', sentence)                      # dismiss if the pattern 、。 is found
    or sentence.count('・') > 2                         # dismiss if there are more than 2 dots
    or sentence.endswith('、')                          # dismiss if the line ends with 、
    or len(sentence) > 150                              # dismiss if the line is more than 150 chars
    or len(sentence) < 3                                # dismiss if the line is less than 3 chars
    or not re.search('[\u3040-\u309F]+$', sentence)):   # dismiss if the line doesn't end w/kana
```

Running [wikisentences.py](https://github.com/cryptogramber/Japanese-Text-Analysis/blob/master/wiki-jp-corpus/wikisentences.py) will discard anything shorter than 2 characters, ending in a comma, or without a '。' somewhere in the line. Anything caught in the statement above will be sorted into a <code>wikiclean_dismissed.txt</code> file, with everything else going into <code>wikiclean-sentences.txt</code> -- both files are ~1.2GB. If you want to see a subset of these sentences, change <code>start_at_sentence</code> and <code>end_at_sentence</code> below to your desired values, and run the following:

```python
start_at_sentence = 1000
end_at_sentence = 5000
with open('wikiclean-sentences.txt') as f:
    sentences = f.readlines()

article_sample = open('wikiclean-sample-set.txt', 'w')
for sentence in sentences[start_at_sentence:end_at_sentence]:
    article_sample.write(sentence)
article_sample.close()
```

The instructions above should be sufficient for replicating the filtered subset of sentences in <code>wikiclean-sentences.txt</code>, but I'm happy to share mine if your interest is non-commercial in nature (I assume since the data comes from Wikipedia, the non-commercial aspect is a necessity). Email me at a@cryptogramber.com and let me know what you'd be using it for. :)