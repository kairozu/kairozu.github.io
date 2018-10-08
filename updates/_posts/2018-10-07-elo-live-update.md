---
layout: content
title: Elo Live Update
hasgithub: https://github.com/kairozu/Elo-Live-Score
hasimg: /images/elolive.png
imgwidth: 240
tags: project code
---
## Elo Live Score
FiveThirtyEight made a system for [comparing your own NFL forecasts to those made by their Elo rating system](https://projects.fivethirtyeight.com/2018-nfl-forecasting-game/). On week 1, it is possible that I made at least one choice based on preferred mascot, but by week 4, I had cloned their [GitHub repository](https://github.com/fivethirtyeight/nfl-elo-game) and was trying to make my own model. I wish I could say that my week 4 was more accurate than my week 1, but, look, maybe my model just needs more work.

***I have no connection to FiveThirtyEight**. I didn't ask them for permission to make this. If they ask me to take it down, I am happy to do so. I'm a huge fan of the work they do. Nate, please don't sue me.*

When multiple games are being played concurrently, it's a bit of a hassle to track how the teams are doing relative to what my forecasts were.. so this Chrome extension was born. It pulls [current game data from the NFL](http://www.nfl.com/liveupdate/scorestrip/ss.xml), and when you're on [FiveThirtyEight's Elo game results page](https://projects.fivethirtyeight.com/2018-nfl-forecasting-game/results/), it uses some hacky javascript to insert the current quarter, time remaining, and score for each game that is currently live. When there is a live game, the page will refresh every minute. When there is no live game (and the page is still open for whatever reason), the page will refresh every hour.

The code is messy and doesn't have much in the way of error handling, but the risk of trying it out is slim to none (if it doesn't work, just remove the extension). If you have polite comments (or if you're FiveThirtyEight and you want me to take this down): amber@kairozu.com.

To install from Chrome Web Store: [https://chrome.google.com/webstore/detail/elo-live-score/hggppcbcehnkplgbhccfcnejkaaipafn](https://chrome.google.com/webstore/detail/elo-live-score/hggppcbcehnkplgbhccfcnejkaaipafn)

The extension is open source; you can download the code and modify it how you see fit. Chrome extensions can be installed locally with little effort if you don't want to go the Chrome Web Store route:
1. Go to Google Chrome Settings > Extensions
2. Click "Developer Mode" in the top right
3. Select "Load Unpacked Extension"
4. Navigate to & select the Elo-Live-Score folder on your drive
5. Load the page: [https://projects.fivethirtyeight.com/2018-nfl-forecasting-game/results/](https://projects.fivethirtyeight.com/2018-nfl-forecasting-game/results/)

Other live-update text sources of NFL data:
- [http://www.nfl.com/liveupdate/scorestrip/ss.xml](http://www.nfl.com/liveupdate/scorestrip/ss.xml)
- [http://www.nfl.com/liveupdate/scores/scores.json](http://www.nfl.com/liveupdate/scores/scores.json)
- [http://www.nfl.com/liveupdate/scorestrip/ss.xml](http://www.nfl.com/liveupdate/scorestrip/ss.xml)
- [http://www.nfl.com/liveupdate/scorestrip/ss.json](http://www.nfl.com/liveupdate/scorestrip/ss.json)

This guy does some cool open source work with NFL data: [http://blog.burntsushi.net/nfl-live-statistics-with-python/](http://blog.burntsushi.net/nfl-live-statistics-with-python/)
