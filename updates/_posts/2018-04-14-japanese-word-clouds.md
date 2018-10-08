---
layout: content
title: Word Clouds in Japanese
hasgithub: https://github.com/kairozu/Japanese-Word-Cloud
tags: japanese code
---
Word clouds are kinda cliche; trying to interpret word frequency -- or really any other functional information -- from a smoothie of words and color will only take you so far. That said, they're cool looking, so hey. These are a few of my favorites -- a brief introduction to generating word clouds using the story of ももたろう, a Kairozu word cloud shaped like an orange version of Kai the Koi, and a [JAXA](http://global.jaxa.jp/) [logo](https://commons.wikimedia.org/wiki/File:Jaxa_logo.svg) with words mined from the [@JAXA_jp](https://twitter.com/JAXA_jp) Twitter account.

## ももたろう Word Cloud
First, the most basic of word clouds using the story of [ももたろう](http://hukumusume.com/douwa/pc/jap/08/01.htm). The general order for creating these word clouds is as follows: (1) Load the text file with the story, (2) tokenize the text, (3) remove words I don't want to include, (4) indicate desired colors and/or shape, and then finally (5) create the word cloud. These steps are numbered in each code excerpt below.

<a href="hhttps://raw.githubusercontent.com/kairozu/Japanese-Word-Cloud/master/momo_word_cloud.png"><img class="imageCenter" src="https://raw.githubusercontent.com/kairozu/Japanese-Word-Cloud/master/momo_word_cloud.png" alt="word cloud using words from momotaro"/></a>

<ul>
<li>Momotaro Word Cloud Code: <a href="https://github.com/kairozu/Japanese-Word-Cloud/blob/master/momotaro_wordcloud.py">momotaro_wordcloud.py</a></li>
<li>Source Text: <a href="https://github.com/kairozu/Japanese-Word-Cloud/blob/master/momotaro.txt">momotaro.txt</a></li>
<li>Font (Google Noto CJKjp-Light): <a href="https://www.google.com/get/noto/">https://www.google.com/get/noto/</a></li>
<li>Options: Basic Word Cloud, Stopwords</li>
</ul>

```
import MeCab
from os import path
from wordcloud import WordCloud, STOPWORDS

# (1) load the text file with the story
d = path.dirname(__file__)          # directory interface for file access
with open(path.join(d, 'momotaro.txt')) as f:
    momotaro = f.readlines()

# (2) tokenize the text
mct = MeCab.Tagger("-O chasen -d /usr/local/lib/mecab/dic/mecab-ipadic-neologd/")
momo_text = ''
for sentence in momotaro:
    jparse = mct.parseToNode(sentence)
    while jparse:
        mct_split = jparse.feature.split(',')
        momo_text = momo_text + mct_split[6] + ' '  # keep dictionary form
        jparse = jparse.next

# (3) indicate words I don't want to include in the word cloud
stopwords = set(STOPWORDS)
stopwords.add("です")
stopwords.add("する")

# (4) this word cloud uses the default colors and doesn't indicate a shape
# (5) create the word cloud
font_path = d + '~/Library/Fonts/NotoSansCJKjp-Light.otf'
wordcloud = WordCloud(background_color="white", stopwords=stopwords, font_path=font_path).generate(momo_text)

image = wordcloud.to_image()
image.show()                    # display generated wordcloud
```

## Kairozu Word Cloud
For the [Kairozu.com](https://kairozu.com) word cloud, I dumped sentences from Kairozu's first few chapters into a CSV file and ran that text through MeCab to pull out worthwhile bits of grammar (nouns, verbs, and adjectives). For more background on MeCab, check out: [Tokenization of Japanese Text](https://kairozu.github.io/updates/japanese-tokenization) and [Simple Japanese Text Analysis](https://kairozu.github.io/updates/simple-jp-text-analysis). This Python library does most of the word cloud heavy lifting: [https://github.com/amueller/word_cloud](https://github.com/amueller/word_cloud) (thanks Andreas Mueller!).

<a href="https://github.com/kairozu/Japanese-Word-Cloud/raw/master/kairozu_word_cloud.png"><img class="imageCenter" src="https://github.com/kairozu/Japanese-Word-Cloud/raw/master/kairozu_word_cloud_small.png" alt="kairozu.com word cloud" /></a>

<ul>
<li>Kairozu Word Cloud Code: <a href="https://github.com/kairozu/Japanese-Word-Cloud/blob/master/kairozu_wordcloud.py">kairozu_wordcloud.py</a></li>
<li>Source Text: Sentences & practices from <a href="https://kairozu.com">Kairozu.com</a></li>
<li>Color/Mask Image: <a href="https://github.com/kairozu/Japanese-Word-Cloud/blob/master/kaikoiorange.jpg">orangekaithekoi.jpg</a></li>
<li>Font (Google Noto CJKjp-Light): <a href="https://www.google.com/get/noto/">https://www.google.com/get/noto/</a></li>
<li>Options: Colors via ImageColorGenerator, Shape via Image Mask, High Resolution</li>
</ul>

```
# (4) generate the colors used in the word cloud from orange Kai the Koi
kai_coloring = imread(path.join(d, 'kaikoiorange.jpg'))
image_colors = ImageColorGenerator(kai_coloring)    # generate image colors

# (4) create the Koi shape of the word cloud from Kai the Koi
mask = np.array(Image.open(path.join(d, 'kaikoiorange.jpg')))

# (5) generate the word cloud using the following options:
# collocations: whether to include collocations (bigrams) of two words
# mask: the shape of the word cloud -- taken from Kai the Koi above
# scale: scaling between computation and drawing, lower=faster, higher=better resolution
# relative_scaling: importance of relative word frequencies for font size
# color_func: use the colors generated above w/ImageColorGenerator
wordcloud = WordCloud(collocations=False, mask=mask, background_color="white", font_path=font_path, \
            contour_width=1, max_words=4000, max_font_size=110, min_font_size=10, scale=5, \
            relative_scaling=0.5, color_func=image_colors, random_state=3).generate(kaifull)
```

## JAXA Word Cloud (Blue)
The JAXA word cloud is my favorite.. in part because I learned so many new kanji + words. :) The source text for this was pulled from the [@JAXA_jp](https://twitter.com/jaxa_jp) Twitter feed. To recreate this, you'll need to make your own Twitter API keys.

<ol>
<li>Go to <a href="https://apps.twitter.com/">https://apps.twitter.com/</a></li>
<li>Click "Create New App"</li>
<li>Give your app a name, description, and website -- a placeholder URL is fine for the website. Assuming you're only doing this for personal use, the values here don't matter much. Leave the Callback URL blank.</li>
<li>Check the box that says you've read the developer agreement (you should, in theory, read this agreement) & click "Create your Twitter application"</li>
<li>In the Twitter Application Management interface, go to "Keys and Access Tokens"</li>
<li>Under Application Settings, you'll see your Consumer Key (API Key) and Consumer Secret (API Secret) -- copy these values to consumer_key and consumer_secret respectively.</li>
<li>Under Your Access Token, click "Create my access token" -- the resulting Access Token and Access Token Secret should be copied to access_token and access_token_secret respectively.</li>
<li>For more information, see the Twitter API Docs: <a href="https://developer.twitter.com/en/docs/api-reference-index">Twitter API Reference Index</a></li>
</ol>

<a href="https://github.com/kairozu/Japanese-Word-Cloud/raw/master/jaxa_word_blue.png"><img class="imageCenter" src="https://github.com/kairozu/Japanese-Word-Cloud/raw/master/jaxa_word_blue_small.png" alt="JAXA word cloud blue" /></a>

<ul>
<li>JAXA Twitter Word Cloud Code: <a href="https://github.com/kairozu/Japanese-Word-Cloud/blob/master/jaxa_wordcloud.py">jaxa_wordcloud.py</a> <span class="smaller">(first half generates the image above; latter half generates the image with red highlight words below)</span></li>
<li>Source Text: <a href="https://twitter.com/JAXA_jp">@JAXA_jp Twitter</a></li>
<li>Mask Image: <a href="https://commons.wikimedia.org/wiki/File:Jaxa_logo.svg">https://commons.wikimedia.org/wiki/File:Jaxa_logo.svg</a></li>
<li>Font (Google Noto CJKjp-Light): <a href="https://www.google.com/get/noto/">https://www.google.com/get/noto/</a></li>
<li>Options: Custom Colors, Shape via Image Mask, High Resolution, Twitter Source</li>
</ul>

[Tweepy](http://www.tweepy.org/) is a Python library for accessing the Twitter API. The code below pulls full tweets from the account [@JAXA_jp](https://twitter.com/jaxa_jp), discards all retweets, and then removes URLs and references to YouTube.

```
# tweet_mode='extended' pulls the full text of a tweet (the default is truncated after 140)
for status in tweepy.Cursor(api.user_timeline, screen_name='@jaxa_jp', tweet_mode='extended').items():
    if (not status.retweeted) and ('RT @' not in status._json['full_text']):    # remove retweets
        cleantweet = re.sub(r'https://t.co/[a-zA-Z0-9]{10}', '', status._json['full_text'])
        cleantweet = re.sub(r'、@YouTube がアップロード', '', cleantweet)
        cleantweet = re.sub(r'@YouTube', '', cleantweet)
        jaxatweets_clean.append(cleantweet)                 # save clean tweets
```

Similar to the Kairozu word cloud, I tokenize the text with MeCab and keep desired parts of speech -- adjectives, verbs, and nouns in this case. I used the [JAXA logo from Wikipedia](https://commons.wikimedia.org/wiki/File:Jaxa_logo.svg) for the mask (shape) of the word cloud and the function below to vary the shades of blue used to color individual words. The following will return a HSL color value between HSL(207, 100%, 20%) -- a darker blue, and HSL(207, 100%, 65%) -- a lighter blue. The JAXA blue that I pulled from the SVG logo was HSL(207, 100%, 35%). The other settings for generating the word cloud are largely the same as those above.

```
# (4) word-cloud color range
def jaxa_color_func(word, font_size, position, orientation, random_state=None, **kwargs):
    return "hsl(207, 100%%, %d%%)" % random.randint(20, 65)
```
## JAXA Word Cloud (Highlights)
<a href="https://github.com/kairozu/Japanese-Word-Cloud/raw/master/jaxa_word_highlight.png"><img class="imageCenter" src="https://github.com/kairozu/Japanese-Word-Cloud/raw/master/jaxa_word_highlight_small.png" alt="JAXA word cloud with highlights"/></a>

<ul>
<li>JAXA Twitter Word Cloud Code w/Highlights: <a href="https://github.com/kairozu/Japanese-Word-Cloud/blob/master/jaxa_wordcloud.py">jaxa_wordcloud.py</a> <span class="smaller">(this code will create two versions -- the blue one shown previously, and this one with the red highlight words)</span></li>
<li>Source text, mask image, font, etc are identical to those above.</li>
<li>Options: Word Highlights!</li>
</ul>

Building on the previous code for the blue JAXA word cloud, this will highlight the listed words with the indicated shade of red (#d92425). <code>SimpleGroupedColorFunc()</code> takes two arguments; a dictionary with words to highlight and the color to highlight them with, and a default color for all other words.

```
# (4) create additional version with red highlight for defined words (aka words I liked)
class SimpleGroupedColorFunc(object):
    def __init__(self, color_to_words, default_color):
        self.word_to_color = {word: color
                              for (color, words) in color_to_words.items()
                              for word in words}
        self.default_color = default_color

    def __call__(self, word, **kwargs):
        return self.word_to_color.get(word, self.default_color)

default_color = "#0062b3"       # words without highlight
color_to_words = {
    '#d92425': ['宇宙での実験', '火星', '長期滞在', '宇宙服', '国際宇宙ステーション', '打ち上げる', 'はぶやさ',
    'はぶやさ2', 'きぼう', '大西', 'ファン', '衛星', '観測', '宇宙飛行士', '実験', '宇宙科学研究所', '技術'] }

# (4) create new color function to highlight words above in red
grouped_color_func = SimpleGroupedColorFunc(color_to_words, default_color)
wordcloud.recolor(color_func=grouped_color_func)
```

I picked words I thought were interesting, some of which were new to me. I learned all sorts of things about JAXA missions while looking a few of these up. :)

<div class="divResponsive">
<table class="smaller">
    <tr><td>きぼう</td><td>きぼう</td><td>Kibo! The Japanese Experiment Module (JEM) is a human-rated space facility & JAXA contribution to the ISS.</td><td><a href="http://iss.jaxa.jp/en/kibo/">http://iss.jaxa.jp/en/kibo/</a></td></tr>
    <tr><td>宇宙科学研究所</td><td>うちゅうかがくけんきゅうしょ</td><td>Institute of Space and Astronautical Science (ISAS), a division of JAXA.</td><td><a href="http://www.isas.jaxa.jp/en/">http://www.isas.jaxa.jp/en/</a></td></tr>
    <tr><td>宇宙での実験</td><td>うちゅうでのじっけん</td><td>experiments in space</td><td></td></tr>
    <tr><td>宇宙飛行士</td><td>うちゅうひこうし</td><td>astronaut</td><td><a href="http://iss.jaxa.jp/en/astro/biographies/">http://iss.jaxa.jp/en/astro/biographies/</a></td></tr>
    <tr><td>宇宙服</td><td>うちゅうふく</td><td>spacesuit</td><td></td></tr>
    <tr><td>火星</td><td>かせい</td><td>Mars</td><td><a href="http://mmx.isas.jaxa.jp/en/">http://mmx.isas.jaxa.jp/en/</a></td></tr>
    <tr><td>長期滞在</td><td>ちょうきたいざい</td><td>long-term stay</td><td></td></tr>
    <tr><td>打ち上げる</td><td>うちあげる</td><td>to launch!</td><td></td></tr>
    <tr><td>はぶやさ（２）</td><td>はぶやさ（２）</td><td>Asteroid sample return missions; Habuyasa 2 is currently heading toward the asteroid "162173 Ryugu."</td><td><a href="http://global.jaxa.jp/projects/sat/hayabusa2/">http://global.jaxa.jp/projects/sat/hayabusa2/</a></td></tr>
    <tr><td>大西</td><td>おおにし</td><td>Family name of JAXA astronaut Takuya Onishi; spent 4 mos on the ISS in 2016.</td><td><a href="http://iss.jaxa.jp/en/astro/biographies/onishi/">http://iss.jaxa.jp/en/astro/biographies/onishi/</a></td></tr>
    <tr><td>ファン</td><td>ふぁん</td><td>Reference to fan!fun!JAXA -- educational site.</td><td><a href="http://fanfun.jaxa.jp/">http://fanfun.jaxa.jp/</a></td></tr>
    <tr><td>衛星</td><td>えいせい</td><td>satellite</td><td></td></tr>
    <tr><td>観測</td><td>かんそく</td><td>observation</td><td></td></tr>
    <tr><td>実験</td><td>じっけん</td><td>experiment</td><td></td></tr>
    <tr><td>技術</td><td>ぎじゅつ</td><td>technology</td><td></td></tr>
    <tr><td>国際宇宙ステーション</td><td>こくさいうちゅうすてーしょん</td><td>International Space Station</td><td><a href="http://iss.jaxa.jp/en/">http://iss.jaxa.jp/en/</a></td></tr>
</table>