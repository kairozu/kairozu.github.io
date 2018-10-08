---
layout: content
title: Progressive Web Apps
tags: project code
hasgithub: https://github.com/kairozu/Progressive-Web-Apps/
---
I've been fascinated by Progressive Web Applications (PWA) lately. I've largely been using Angular to build things, but with every new PWA comes a few odds and ends that I've learned, and as such, I'll try to keep track of them here. The general repository for these PWA experiments is here: [https://github.com/kairozu/Progressive-Web-Apps/](https://github.com/kairozu/Progressive-Web-Apps/).

## Spike Train Calculator (October 2018)
<img class="imageR" height="150" alt="weather" src="/images/spiketrain.png" />
https://github.com/kairozu/Progressive-Web-Apps/ephys-calc

Converts between inter-pulse intervals/train burst widths and frequency/number of pulses & plots an example waveform (also my first foray into JS/jQuery). Mostly useful for visualizing spike trains in discussions or double checking your math when hopping between ephys equipment.

Once you begin entering values, the example waveform will not plot until all values have been entered. You can choose between calculating your waveform from the inter-pulse period and the train burst width, or from the # of pulses and the frequency of those pulses -- the alternate option will be displayed automatically.  Scientific notation is displayed on the right for reference if you're using a system that requires SN (AM Systems, yay).

<div class="spacerClear"></div>

## Mathotron (October 2018)
<img class="imageL" height="160" alt="mathotron" src="/images/mathotron.png" />
https://github.com/kairozu/Progressive-Web-Apps/mathotron

Simple calculator that keeps a ticker tape history of mathematical operations. It's pretty simple and lacking in aesthetic quality, but I wanted to test hosting PWAs on GitHub Pages.

It was generated via the standard: <code>$ ng new mathotron</code>
Angular material design elements were added via <code>$ npm install --save @angular/material @angular/cdk</code>
Angular 6 makes adding dependencies for PWA support & creating a default service worker/manifest.json pretty easy with:
<code>$ ng add @angular/pwa --project mathotron</code>

Create the production copy with <code>$ ng build --prod</code> and then copy the project name folder from within the new dist folder to wherever you want to host your PWA. When serving PWAs from GitHub pages, make sure to change your paths relative to the current folder, the base URL should be ./ instead of just / (the default) -- check your index.html, manifest.json, ngsw.json.

Configuring a PWA for iOS takes a few extra steps, [outlined here by Apple](https://developer.apple.com/library/archive/documentation/AppleApplications/Reference/SafariWebContent/ConfiguringWebApplications/ConfiguringWebApplications.html). Note that any transparency (alpha channel) in your app icon png files will be made black. On iOS, PWAs need to be installed through Safari -- there's no "add to desktop" option within Chrome at the moment.
