---
layout: content
title: Japanese Line Breaks
tags: japanese
---
Regardless of spaces ([latin](https://unicode-table.com/en/0020/) or [ideographic](https://unicode-table.com/en/3000/)) or punctuation, [word-break: keep-all](https://www.w3schools.com/cssref/css3_pr_word-break.asp) is a necessary CSS attribute to avoid Japanese words being split indiscriminately. <span class="italics">Note: the formatting on this page will depend on your browser and/or screen size, but the word-break examples might yield something of a trainwreck.</span>

## Line Break on Japanese Punctuation
Most browsers and platforms don't preferentially break lines on standard Japanese punctuation, but even those that do will still leave large blocks of text escaping their containers.
<table>
    <tr>
        <td class="bold text-align-center" colspan="5">Break on JP Punctuation<br />
        <span class="xsmall">(text will overstep containers)</span>
        </td>
    </tr>
    <tr>
        <td></td>
        <td><i class="fab fa-chrome" aria-hidden="true"></i></td>
        <td><i class="fab fa-firefox" aria-hidden="true"></i></td>
        <td><i class="fab fa-safari" aria-hidden="true"></i></td>
        <td><i class="fab fa-edge" aria-hidden="true"></i></td>
    </tr>
    <tr>
        <td class="bold">Mac</td>
        <td><i class="far fa-check-circle" aria-hidden="true"></i></td>
        <td><i class="fa fa-times" aria-hidden="true"></i></td>
        <td><i class="fa fa-times" aria-hidden="true"></i></td>
        <td class="bold larger">--</td>
    </tr>
    <tr>
        <td class="bold">Win</td>
        <td><i class="far fa-check-circle" aria-hidden="true"></i></td>
        <td><i class="fa fa-times" aria-hidden="true"></i></td>
        <td class="bold larger">--</td>
        <td><i class="far fa-check-circle" aria-hidden="true"></i></td>
    </tr>
    <tr>
        <td class="bold">iOS</td>
        <td><i class="fa fa-times" aria-hidden="true"></i></td>
        <td><i class="fa fa-times" aria-hidden="true"></i></td>
        <td><i class="fa fa-times" aria-hidden="true"></i></td>
        <td class="bold larger">--</td>
    </tr>
</table>

<div class="space-table">
    no spaces<br />
    <a href="https://www.w3schools.com/cssref/css3_pr_word-break.asp">word-break: keep-all</a>
    <br />
    <div style="word-break:keep-all;">
    回路図とは電子回路、空気圧機器、油圧機器などの回路を記述するために用いられる図のことである。
    実体配線図と異なり、回路図での位置と実際に配置する場所は無関係であり、一種のグラフである。
    </div>
</div>

```html
<div style="word-break:keep-all;">
回路図とは電子回路、空気圧機器、油圧機器などの回路を記述するために用いられる図のことである。実体配線図と異なり、回路図での位置と実際に配置する場所は無関係であり、一種のグラフである。
</div>
```

## Line Break on Zero-Width Space
I tried using [zero-width spaces](https://unicode-table.com/en/200B/) to separate words -- unfortunately this doesn't work in all browsers. It seems iOS doesn't recognize the zero-width space. There are plenty of other [unicode whitespace options](https://en.wikipedia.org/wiki/Whitespace_character), but in my experience they vary widely in support and rendering, so I've largely avoided them here.
<table>
    <tr><td class="bold text-align-center" colspan="5">Break on <a href="https://unicode-table.com/en/200B/">Zero-Width Space</a></td></tr>
    <tr><td></td><td><i class="fab fa-chrome" aria-hidden="true"></i></td><td><i class="fab fa-firefox" aria-hidden="true"></i></td><td><i class="fab fa-safari" aria-hidden="true"></i></td><td><i class="fab fa-edge" aria-hidden="true"></i></td></tr>
    <tr><td class="bold">Mac</td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td><i class="fa fa-times" aria-hidden="true"></i></td><td class="bold larger">--</td></tr>
    <tr><td class="bold">Win</td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td class="bold larger">--</td><td><i class="far fa-check-circle" aria-hidden="true"></i></td></tr>
    <tr><td class="bold">iOS</td><td><i class="fa fa-times" aria-hidden="true"></i></td><td><i class="fa fa-times" aria-hidden="true"></i></td><td><i class="fa fa-times" aria-hidden="true"></i></td><td class="bold larger">--</td></tr>
</table>

<div class="space-table">
    <a href="https://unicode-table.com/en/200B/">zero-width spaces</a><br />
    <a href="https://www.w3schools.com/cssref/css3_pr_word-break.asp">word-break: keep-all</a>
    <br />
    <div style="word-break:keep-all;">
    回路図&#8203;とは&#8203;電子回路、&#8203;空気圧機器、&#8203;油圧機器&#8203;などの&#8203;回路&#8203;を&#8203;
    記述する&#8203;ために&#8203;用いられる&#8203;図のこと&#8203;で&#8203;ある。&#8203;実体配線図&#8203;と&#8203;
    異なり、&#8203;回路図&#8203;で&#8203;の&#8203;位置&#8203;と&#8203;実際&#8203;に&#8203;配置する&#8203;
    場所&#8203;は&#8203;無関係&#8203;で&#8203;あり、&#8203;一種&#8203;の&#8203;グラフ&#8203;で&#8203;ある。
    </div>
</div>

```html
<div style="word-break:keep-all;">
回路図&#8203;とは&#8203;電子回路、&#8203;空気圧機器、&#8203;油圧機器&#8203;などの&#8203;回路&#8203;を&#8203;記述する&#8203;ために&#8203;用いられる&#8203;図のこと&#8203;で&#8203;ある。&#8203;実体配線図&#8203;と&#8203;異なり、&#8203;回路図&#8203;で&#8203;の&#8203;位置&#8203;と&#8203;実際&#8203;に&#8203;配置する&#8203;場所&#8203;は&#8203;無関係&#8203;で&#8203;あり、&#8203;一種&#8203;の&#8203;グラフ&#8203;で&#8203;ある。
</div>
```

## Line Break on WBR Tag
The HTML [word break tag](https://www.w3schools.com/tags/tag_wbr.asp) (<code>&lt;wbr&gt;</code>) reliably breaks lines in every browser I tested. This is a cross-browser friendly solution, but it's pretty ugly to view pre-rendering.
<table>
    <tr><td class="bold text-align-center" colspan="5">Line Break on <a href="https://www.w3schools.com/tags/tag_wbr.asp"><code>&lt;wbr&gt;</code></a> Tag</td></tr>
    <tr><td></td><td><i class="fab fa-chrome" aria-hidden="true"></i></td><td><i class="fab fa-firefox" aria-hidden="true"></i></td><td><i class="fab fa-safari" aria-hidden="true"></i></td><td><i class="fab fa-edge" aria-hidden="true"></i></td></tr>
    <tr><td class="bold">Mac</td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td class="bold larger">--</td></tr>
    <tr><td class="bold">Win</td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td class="bold larger">--</td><td><i class="far fa-check-circle" aria-hidden="true"></i></td></tr>
    <tr><td class="bold">iOS</td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td class="bold larger">--</td></tr>
</table>

<div class="space-table">
    <a href="https://www.w3schools.com/tags/tag_wbr.asp">word break tag</a><br />
    <a href="https://www.w3schools.com/cssref/css3_pr_word-break.asp">word-break: keep-all</a>
    <br />
    <div style="word-break:keep-all;">
    回路図<wbr>とは<wbr>電子回路、<wbr>空気圧機器、<wbr>油圧機器<wbr>などの<wbr>回路<wbr>を<wbr>記述する<wbr>ために<wbr>
    用いられる<wbr>図のこと<wbr>で<wbr>ある。<wbr>実体配線図<wbr>と<wbr>異なり、<wbr>回路図<wbr>で<wbr>の<wbr>位置<wbr>と<wbr>
    実際<wbr>に<wbr>配置する<wbr>場所<wbr>は<wbr>無関係<wbr>で<wbr>あり、<wbr>一種<wbr>の<wbr>グラフ<wbr>で<wbr>ある。
    </div>
</div>

```html
<div style="word-break:keep-all;">
回路図<wbr>とは<wbr>電子回路、<wbr>空気圧機器、<wbr>油圧機器<wbr>などの<wbr>回路<wbr>を<wbr>記述する<wbr>ために<wbr>用いられる<wbr>図のこと<wbr>で<wbr>ある。<wbr>実体配線図<wbr>と<wbr>異なり、<wbr>回路図<wbr>で<wbr>の<wbr>位置<wbr>と<wbr>実際<wbr>に<wbr>配置する<wbr>場所<wbr>は<wbr>無関係<wbr>で<wbr>あり、<wbr>一種<wbr>の<wbr>グラフ<wbr>で<wbr>ある。
</div>
```

## Line Break on Ideographic Space
The first 8 chapters of Kairozu separate words with spaces for easier reading -- when there are no kanji, it's hard to parse sentences without spaces between words. I discovered the hard way that not all browsers break on [ideographic spaces](https://unicode-table.com/en/3000/).
<table>
    <tr><td class="bold text-align-center" colspan="5">Break on <a href="https://unicode-table.com/en/3000/">Ideographic Space</a></td></tr>
    <tr><td></td><td><i class="fab fa-chrome" aria-hidden="true"></i></td><td><i class="fab fa-firefox" aria-hidden="true"></i></td><td><i class="fab fa-safari" aria-hidden="true"></i></td><td><i class="fab fa-edge" aria-hidden="true"></i></td></tr>
    <tr><td class="bold">Mac</td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td><i class="fa fa-times" aria-hidden="true"></i></td><td><i class="fa fa-times" aria-hidden="true"></i></td><td class="bold larger">--</td></tr>
    <tr><td class="bold">Win</td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td><i class="fa fa-times" aria-hidden="true"></i></td><td class="bold larger">--</td><td><i class="far fa-check-circle" aria-hidden="true"></i></td></tr>
    <tr><td class="bold">iOS</td><td><i class="fa fa-times" aria-hidden="true"></i></td><td><i class="fa fa-times" aria-hidden="true"></i></td><td><i class="fa fa-times" aria-hidden="true"></i></td><td class="bold larger">--</td></tr>
</table>

<div class="space-table">
    <a href="https://unicode-table.com/en/3000/">ideographic spaces</a><br />
    <a href="https://www.w3schools.com/cssref/css3_pr_word-break.asp">word-break: keep-all</a>
    <br />
    <div style="word-break:keep-all;">
    回路図　とは　電子回路、　空気圧機器、　油圧機器　などの　回路　を　記述する　ために　用いられる　図のこと　で　ある。　
    実体配線図　と　異なり、　回路図　で　の　位置　と　実際　に　配置する　場所　は　無関係　で　あり、　一種　の　グラフ　で　ある。
    </div>
</div>

```html
<div style="word-break:keep-all;">
回路図　とは　電子回路、　空気圧機器、　油圧機器　などの　回路　を　記述する　ために　用いられる　図のこと　で　ある。　実体配線図　と　異なり、　回路図　で　の　位置　と　実際　に　配置する　場所　は　無関係　で　あり、　一種　の　グラフ　で　ある。
</div>
```

## Line Break on Latin Space
All browsers <span class="italics">will</span> break text on regular [latin spaces](https://unicode-table.com/en/0020/), but this doesn't add as much separation between the words as I'd like. I tried using two spaces, but most browsers will strip one of those spaces out. It's possible to use one normal space in addition to a [non-breaking space](https://unicode-table.com/en/00A0/), but that's.. ugly.

<table>
    <tr><td class="bold text-align-center" colspan="5">Break on <a href="https://unicode-table.com/en/0020/">Latin Space</a> (Single)<br /><span class="xsmall">(no mid-text span tags)</span></td></tr>
    <tr><td></td><td><i class="fab fa-chrome" aria-hidden="true"></i></td><td><i class="fab fa-firefox" aria-hidden="true"></i></td><td><i class="fab fa-safari" aria-hidden="true"></i></td><td><i class="fab fa-edge" aria-hidden="true"></i></td></tr>
    <tr><td class="bold">Mac</td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td class="bold larger">--</td></tr>
    <tr><td class="bold">Win</td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td class="bold larger">--</td><td><i class="far fa-check-circle" aria-hidden="true"></i></td></tr>
    <tr><td class="bold">iOS</td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td class="bold larger">--</td></tr>
</table>

<div class="space-table">
    <a href="https://unicode-table.com/en/0020/">latin spaces</a><br />
    <a href="https://www.w3schools.com/cssref/css3_pr_word-break.asp">word-break: keep-all</a>
    <br />
    <div style="word-break:keep-all;">
    回路図 とは 電子回路、 空気圧機器、 油圧機器 などの 回路 を 記述する ために 用いられる 図のこと で ある。 
    実体配線図 と 異なり、 回路図 で の 位置 と 実際 に 配置する 場所 は 無関係 で あり、 一種 の グラフ で ある。
    </div>
</div>

```html
<div style="word-break:keep-all;">
回路図 とは 電子回路、 空気圧機器、 油圧機器 などの 回路 を 記述する ために 用いられる 図のこと で ある。 実体配線図 と 異なり、 回路図 で の 位置 と 実際 に 配置する 場所 は 無関係 で あり、 一種 の グラフ で ある。
</div>
```

## Line Break on Latin Spaces & CSS Word Spacing
My eventual solution was to replace all <a href="https://unicode-table.com/en/3000/">ideographic spaces</a> with <a href="https://unicode-table.com/en/0020/">latin spaces</a>, all full-width Japanese punctuation with half-width Japanese punctuation, and then use <a href="https://www.w3schools.com/cssref/pr_text_word-spacing.asp">CSS to increase the spacing between words</a>. <span class="bold">This works well with regular text, but unfortunately there's something in Safari/WebKit which breaks the spacing around words when they're enclosed in span tags.</span>
<table>
    <tr><td class="bold text-align-center" colspan="5">Break on <a href="https://unicode-table.com/en/0020/">Latin Space</a> + <a href="https://www.w3schools.com/cssref/pr_text_word-spacing.asp">CSS</a><br /><span class="xsmall">(no mid-text span tags)</span></td></tr>
    <tr><td></td><td><i class="fab fa-chrome" aria-hidden="true"></i></td><td><i class="fab fa-firefox" aria-hidden="true"></i></td><td><i class="fab fa-safari" aria-hidden="true"></i></td><td><i class="fab fa-edge" aria-hidden="true"></i></td></tr>
    <tr><td class="bold">Mac</td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td class="bold larger">--</td></tr>
    <tr><td class="bold">Win</td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td class="bold larger">--</td><td><i class="far fa-check-circle" aria-hidden="true"></i></td></tr>
    <tr><td class="bold">iOS</td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td class="bold larger">--</td></tr>
</table>

<div class="space-table">
    <a href="https://unicode-table.com/en/0020/">latin spaces</a> + <a href="https://www.w3schools.com/cssref/pr_text_word-spacing.asp">word spacing</a><br />
    <a href="https://www.w3schools.com/cssref/css3_pr_word-break.asp">word-break: keep-all</a>
    <br />
    <div style="word-break:keep-all; word-spacing: 0.76em;">
    回路図 とは 電子回路､ 空気圧機器､ 油圧機器 などの 回路 を 記述する ために 用いられる 図のこと で ある｡ 
    実体配線図 と 異なり､ 回路図 で の 位置 と 実際 に 配置する 場所 は 無関係 で あり､ 一種 の グラフ で ある｡
    </div>
</div>

```html
<div style="word-break:keep-all; word-spacing: 0.76em;">
回路図 とは 電子回路､ 空気圧機器､ 油圧機器 などの 回路 を 記述する ために 用いられる 図のこと で ある｡ 実体配線図 と 異なり､ 回路図 で の 位置 と 実際 に 配置する 場所 は 無関係 で あり､ 一種 の グラフ で ある｡
</div>
```

This seems to work well with most text sizes; the following examples alternate between ideographic spaces and latin spaces w/CSS word-spacing.

<h1 style="word-break:keep-all;">いぬ　は　くろい　です。</h1>
<h1 style="word-break:keep-all; word-spacing: 0.76em;">いぬ は くろい です。</h1>
<h3 style="word-break:keep-all;">いぬ　は　いちばん　すきな　どうぶつ　です。</h3>
<h3 style="word-break:keep-all; word-spacing: 0.76em;">いぬ は いちばん すきな どうぶつ です。</h3>

```html
<h1 style="word-break:keep-all;">いぬ　は　くろい　です。</h1>
<h1 style="word-break:keep-all; word-spacing: 0.76em;">いぬ は くろい です。</h1>
<h3 style="word-break:keep-all;">いぬ　は　いちばん　すきな　どうぶつ　です。</h3>
<h3 style="word-break:keep-all; word-spacing: 0.76em;">いぬ は いちばん すきな どうぶつ です。</h3>
```

## Line Break on Latin Spaces & Monospaced Font
While this doesn't achieve the same degree of spacing, it does seem to be universally friendly as far as browsers go. The downside is that you can't specify another preferred Japanese font.

<table>
    <tr><td class="bold text-align-center" colspan="5">Break on <a href="https://unicode-table.com/en/0020/">Latin Space</a> + <a href="https://www.w3schools.com/cssref/pr_font_font-family.asp">Mono</a><br /><span class="xsmall">(no mid-text span tags)</span></td></tr>
    <tr><td></td><td><i class="fab fa-chrome" aria-hidden="true"></i></td><td><i class="fab fa-firefox" aria-hidden="true"></i></td><td><i class="fab fa-safari" aria-hidden="true"></i></td><td><i class="fab fa-edge" aria-hidden="true"></i></td></tr>
    <tr><td class="bold">Mac</td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td class="bold larger">--</td></tr>
    <tr><td class="bold">Win</td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td class="bold larger">--</td><td><i class="far fa-check-circle" aria-hidden="true"></i></td></tr>
    <tr><td class="bold">iOS</td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td><i class="far fa-check-circle" aria-hidden="true"></i></td><td class="bold larger">--</td></tr>
</table>

<div class="space-table">
    <a href="https://unicode-table.com/en/0020/">latin spaces</a> + <a href="https://www.w3schools.com/cssref/pr_font_font-family.asp">monospace</a><br />
    <a href="https://www.w3schools.com/cssref/css3_pr_word-break.asp">word-break: keep-all</a>
    <br />
    <div style="word-break:keep-all; font-family: monospace;">
    回路図 とは 電子回路､ 空気圧機器､ 油圧機器 などの 回路 を 記述する ために 用いられる 図のこと で ある｡ 
    実体配線図 と 異なり､ 回路図 で の 位置 と 実際 に 配置する 場所 は 無関係 で あり､ 一種 の グラフ で ある｡
    </div>
</div>

```html
<div style="word-break:keep-all; font-family:monospace;">
回路図 とは 電子回路､ 空気圧機器､ 油圧機器 などの 回路 を 記述する ために 用いられる 図のこと で ある｡ 実体配線図 と 異なり､ 回路図 で の 位置 と 実際 に 配置する 場所 は 無関係 で あり､ 一種 の グラフ で ある｡
</div>
```