---
layout: content
title: Progressive Web Apps
tags: project code
hasgithub: https://github.com/cryptogramber/Progressive-Web-Apps/
---
I've been fascinated by Progressive Web Applications (PWA) lately. I've largely been using Angular to build things, but with every new PWA comes a few odds and ends that I've learned, and as such, I'll try to keep track of them here. The general repository for these PWA experiments is here: [https://github.com/cryptogramber/Progressive-Web-Apps/](https://github.com/cryptogramber/Progressive-Web-Apps/).

<div class="spacerClear"></div>

## 助数詞 (October 2018)
<img class="imageL" height="160" alt="josuushi screenshot" src="/images/josuushi.png" />
<div class="listItem"><i class="fab fa-github fa-fw"></i>  <a href="https://github.com/cryptogramber/Progressive-Web-Apps/tree/master/josuushi">https://github.com/cryptogramber/Progressive-Web-Apps/tree/master/josuushi</a></div>
<div class="listItem"><i class="fas fa-paper-plane fa-fw"></i> <a href="https://cryptogramber.github.io/sandbox/josuushi">https://cryptogramber.github.io/sandbox/josuushi</a></div>

Japanese counters are plentiful. There is an excellent Tofugu article which orders them by frequency/general usefulness here: <a href="https://www.tofugu.com/japanese/japanese-counters-list/">350 Japanese Counters Grouped By Usefulness</a>. This cycles through various things which can be counted -- dogs, people, pencils, envelopes, boxes, slices of pizza, etc -- and prompts the user for the number+counter word in Japanese (kana or kanji). The images are cached as a prefetch, so if the app is "installed" ("add to home screen"), it can be used offline. It requires a Japanese IME for input; in the future I'll probably adapt <a href="https://wanakana.com/">wanakana</a> as an Angular service.

The following counters are included: 
<ul>
    <li>ど／度 degrees of temperature or angle</li>
    <li>はい／杯 liquids in cups or bowls</li>
    <li>つ generic or abstract things</li>
    <li>にん／人 people</li>
    <li>こ／個 generic things, often small and round</li>
    <li>ほん／本 long, cylindrical objects</li>
    <li>まい／枚 flat or thin objects</li>
    <li>さつ／冊 bound volumes (books, magazines)</li>
    <li>だい／台 machines and surfaces</li>
    <li>ひき／匹 small animals, insects</li>
    <li>わ／羽 birds, rabbits</li>
    <li>はこ／箱 boxes</li>
    <li>かい／階 floors (of a building)</li>
    <li>めい／名 people (honorific, e.g. customers)</li>
    <li>じかん／時間 hours as a period of time</li>
    <li>じょう／錠 pills</li>
    <li>とう／頭 large animals, livestock</li>
    <li>きれ／切れ slices (of pizza, bread, etc)</li>
</ul>

If you're testing an Angular app locally, serving the production code w/<a href="https://www.npmjs.com/package/http-server">http-server</a> is especially useful for debugging PWA cache issues:

```terminal
$ npm install http-server
$ ng build --prod
$ http-server -c-1 dist/<appname>/
```

<div class="spacerClear"></div>

## Mathotron (October 2018)
<img class="imageL" height="160" alt="mathotron screenshot" src="/images/mathotron.png" />
<div class="listItem"><i class="fab fa-github fa-fw"></i>  <a href="https://github.com/cryptogramber/Progressive-Web-Apps/tree/master/mathotron">https://github.com/cryptogramber/Progressive-Web-Apps/tree/master/mathotron</a></div>
<div class="listItem"><i class="fas fa-paper-plane fa-fw"></i> <a href="https://cryptogramber.github.io/sandbox/mathotron">https://cryptogramber.github.io/sandbox/mathotron</a></div>

Simple calculator that keeps a ticker tape history of mathematical operations. It's pretty simple and lacking in aesthetic quality, but I wanted to test hosting PWAs on GitHub Pages.

It was generated via the standard: <code>$ ng new mathotron</code>
Angular material design elements were added via <code>$ npm install --save @angular/material @angular/cdk</code>
Angular 6 makes adding dependencies for PWA support & creating a default service worker/manifest.json pretty easy with:
<code>$ ng add @angular/pwa --project mathotron</code>

Create the production copy with <code>$ ng build --prod</code> and then copy the project name folder from within the new dist folder to wherever you want to host your PWA. When serving PWAs from GitHub pages, make sure to change your paths relative to the current folder, the base URL should be ./ instead of just / (the default) -- check your index.html, manifest.json, ngsw.json.

Configuring a PWA for iOS takes a few extra steps, [outlined here by Apple](https://developer.apple.com/library/archive/documentation/AppleApplications/Reference/SafariWebContent/ConfiguringWebApplications/ConfiguringWebApplications.html). Note that any transparency (alpha channel) in your app icon png files will be made black. On iOS, PWAs need to be installed through Safari -- there's no "add to desktop" option within Chrome at the moment.

<div class="spacerClear"></div>