---
layout: content
title: Tizen Dev Adventures
hasgithub: https://github.com/kairozu/Gear-S2-AWatch
hasimg: /images/awatchface.png
tags: project code
---
## Summary
The Samsung Gear S2 Smartwatch runs Tizen (Android Wear is more common on Android-compatible smartwatches) -- it's a project within the Linux Foundation (based on the Linux kernel/GNU C library implementing the Linux API), but is "governed" by a "technical steering group" composed of Samsung, Intel, and others. There's a native C++ framework and a web application framework that allows for HTML5/JS apps to run without a browser.

There are pros and cons of the Gear S2, but I like the round interface/bezel navigation and I have the 4G version that allows for a cellular connection without tethering my phone (meaning I can go for a run w/just the watch and have it track GPS/receive messages/play music through bluetooth headphones). The battery life is great and charging is fast, but the Gear app store leaves a lot to be desired if you're looking for anything beyond email/messaging/watch functionality/fitness.

This watch face is programmed using the JavaScript/HTML5 web app method, and it features: current time +10 min, second time zone, day of the week + date, local weather, daily step count, and battery status. This is a collection of the resources I used & the issues I encountered: some solved, others circumvented, and a handful which remain a mystery.

## Development Sandbox
1. Download the Tizen SDK: [https://developer.tizen.org/development/tools/download](https://developer.tizen.org/development/tools/download)
2. Register for Samsung dev certificates: [http://developer.samsung.com/gear/guide-registering-certificates](http://developer.samsung.com/gear/guide-registering-certificates)
3. Enable debugging on your Gear (Settings > Gear Info > Debugging)
4. Connect the Gear S2 to your development environment:
    1. Turn bluetooth off so the watch will connect to a wifi network -- if you don't have settings synced between your phone and the watch, you'll have to enter the wifi settings manually.
    2. Make sure your watch and your development machine are on the same network.
    3. Open the Tizen IDE (not required for connecting the watch to the SDB, but necessary if you'll be sending code from the IDE to the watch).
    4. Connect SDB (serial debugger) via command prompt: C:\tizen-ide\tools\sdb.exe connect ip-of-the-watch
        * Note: The SDB connection can be unreliable -- I find that it helps if you try connecting immediately after the watch connects to a wifi network (or disabling/enabling wifi).
    5. The watch should show up in the Tizen IDE.
    6. Right click on your Gear in the Connection Explorer and select "Permit to Install Applications"
* This guide is helpful w/more details about getting things set up correctly: [http://www.tizenexperts.com/.../gear-s2-smartwatch/](http://www.tizenexperts.com/2015/12/how-to-deploy-to-gear-s2-smartwatch/)

## Tizen Development Resources
* Tizen API Reference: [https://developer.tizen.org/dev-guide/2.4/org.tizen.web.apireference/html/cover_page.htm](https://developer.tizen.org/dev-guide/2.4/org.tizen.web.apireference/html/cover_page.htm)
* Tizen CodeSnippets: [https://developer.tizen.org/community/code-snippet](https://developer.tizen.org/community/code-snippet)
* Samsung Developer Portal: [http://developer.samsung.com/gear](http://developer.samsung.com/gear)
* StackOverflow Tizen Tag: [https://stackoverflow.com/questions/tagged/tizen](https://stackoverflow.com/questions/tagged/tizen)
* Tizen Experts Developer: [http://www.tizenexperts.com/category/developer/](http://www.tizenexperts.com/category/developer/)
* Weather API Options: [http://www.programmableweb.com/news/top-10-weather-apis/analysis/2014/11/13](http://www.programmableweb.com/news/top-10-weather-apis/analysis/2014/11/13)
* HumanActivityMonitor API: [https://developer.tizen.org/dev-guide/.../tizen/humanactivitymonitor.html](https://developer.tizen.org/dev-guide/2.4/org.tizen.web.apireference/html/device_api/mobile/tizen/humanactivitymonitor.html)
* Exporting SHealth Data: [http://forums.androidcentral.com/.../export-save-s-health-data-file.html](http://forums.androidcentral.com/samsung-galaxy-note-5/606733-there-way-export-save-s-health-data-file.html)

## Progress (Concept->Build 1->Build 2)
<div class="flexBox">
    <img height="250" src="/images/awatch_template.png" />
    <img height="250" src="/images/awatch_build1.png" />
    <img height="250" src="/images/awatchface.png" />
</div>

## Current Frustrations
* There's a disparity between what is clearly possible based on other apps (customization of watch faces from the watch face selection screen, calling default s-health and weather apps to query for step count & current conditions) and what Samsung has documented. It seems some features are restricted to Samsung "Partners" (service alarms! grrr!): [https://stackoverflow.com/.../styles-in-gear-s2-on-tizen-sdk](https://stackoverflow.com/questions/33100769/watch-face-with-additional-styles-in-gear-s2-on-tizen-sdk)
* I'm surprised by the bizarre lack of developer support (on Samsung's own forums!), questions like these go unanswered: [http://developer.samsung.com/forum/board/thread/view.do?boardName=SDK&messageId=279858](http://developer.samsung.com/forum/board/thread/view.do?boardName=SDK&messageId=279858)

## AWatch Custom Watch Face Notes
* **Weather**  
Without an easy way to call for weather data from the built in app, I'm pulling the current location and querying Weather Underground w/the latitude/longitude for current conditions.
1. Get the current position: *navigator.geolocation.getCurrentPosition(success, failure, options);*
2. Create a new *XMLHttpRequest* to grab the data from WUnderground: http://api.wunderground.com/api/your-api-key-here/conditions/q/latitude,longitude.xml
    * Note: you'll need to apply for your own API key; the free version has a limited # of requests per minute/hour/month iirc.
3. Parse out the data you want from the returned XML tags (temp_f and weather in my case).
4. Create a routine to update as desired; since alarm services aren't currently available unless you have a Samsung Partner certificate (shaking my head at you, Samsung), in my *updateTime()* function I update the weather once an hour (if minutes <= 30 and weather hasn't already been checked that hour).
* **Pedometer**  
The HumanActivityMonitor API allows you query the total # of steps taken since the application (watch face widget in this case) was loaded, or the total # of steps taken FOR ALL TIME. I have no idea who decided why those were more important than "daily steps" which is something that the S-Health pedometer can do. There's a function to ask for differences in step count based on timestamps, but the documentation wasn't sufficient for me figuring out how to use that in my favor. End result: a dirty hack. Every night at midnight I save the total # of steps taken FOR ALLLLL TIMEEEE to local storage.
1. I call the AccumulativePedometerListener whenever new steps are detected: *tizen.humanactivitymonitor.setAccumulativePedometerListener(onStepChange);*
2. I grab the last saved total step count: *step_diff = localStorage['com.dendriticspine.awatch.stepcount'];*
3. If step_diff is 0, that means it's probably the first time the watch face has been loaded, so I save the current total step count to local storage: *localStorage.setItem('com.dendriticspine.awatch.stepcount', step_ts);*
4. I subtract the current total step count from *step_diff*.
5. At midnight I save the current total step count to *step_diff* again.
The end result is that for the first day, before midnight, the count is inaccurate. Once the first midnight occurs, and the proper "total # of steps taken since you've had the device" is saved, the daily step count should be accurate. This is really ugly, I know, I'd love a better way to accomplish this.
* **Battery**  
Battery monitoring is straightforward, make the following calls and update your display accordingly in the *getBatteryState()* function:
*battery.addEventListener('chargingchange', getBatteryState);*  
*battery.addEventListener('chargingtimechange', getBatteryState);*  
*battery.addEventListener('dischargingtimechange', getBatteryState);*  
*battery.addEventListener('levelchange', getBatteryState);*
* **Time/Time Zones**  
    * Use *date = tizen.time.getCurrentDateTime()* to call the current date/time, and pull your desired info from the resulting date object.
    * Display a time other than the reported one, e.g. I want my watch to be 10 minutes fast: *date.setMinutes(date.getMinutes() + 10)*
    * Switch time zones: *date2 = date.toTimezone('Asia/Tokyo')*
* **Watch Ambient Mode**  
The Watch Face has two different display states: “active” and “always-on.” The name “active state” is very self-explanatory. In the active state, the Watch Face displays in full color. On the other hand, the always-on state (aka "ambient mode") uses limited colors and brightness. Ambient mode can use up to 10 percent of the total screen pixels in low brightness, doesn't support anti-aliasing or "second" information (due to the lower screen refresh rates), and the background must be in black. Allowed colors are: cyan, magenta, yellow, red, green, blue, and white (no greyscale).  I use the canvas HTML element to draw an analog watch w/the day/date display. Right now I'm hiding/showing HTML elements to switch between the canvas layout and the regular HTML layout, which seems ugly, but works well enough.

    Because the ambient mode watch face is displayed at all times unless users decide to turn it off, a screen burn-in protection is required -- the system slightly changes the positions of the on-screen elements at a specific rate (I spent a solid hour thinking this was an error in the trig I'd used to calculate where the hour/minute hands would be).  

    The ambient_tick event is triggered every minute while the device is in the ambient mode. You can use the callback to update the time on your watch application in the ambient mode. In this callback, do not perform time-consuming task and always update the UI as fast as possible. The platform can put the device to sleep shortly after the ambient tick expires.

## Submitting to the Samsung Application Store
Submitting an app to the Google Play Store is a painless and one might almost say.. pleasant process. Submitting an app to the Samsung store is the opposite. Unless you have a "partner" license, your options are limited, there are no private/beta streams available for publishing, and the time between hitting "submit" and being able to download your app via store is.. <del>I can't say just yet, but it has been 2 days so far</del>. I understand why everyone wants to have their own walled garden of an app store, but it surely won't succeed with such limited developer support/delays in publishing.

Update: After 7 days, my watch face widget was approved.. but the partner configuration app was denied with the report below. While the issue they point out is real, and I absolutely don't mind being held to their design quality standards, I'm absolutely floored that someone is actually going through QA for all of the submitted apps. THEY EVEN INCLUDED A CUSTOM VIDEO OF MY APP RUNNING ON A DEV KIT TO HIGHLIGHT THE ISSUE THEY WERE HAVING. Absolutely crazy!! No wonder it took 7 days!

<img class="image_center" width="775" src="/images/samsungdenied.png" />

Update 2: I fixed the text formatting issue and re-submitted.. and waited another 7 days. This time it was rejected because configuration changes made from the AWConfig app aren't immediately reflected in the AWatch watchface. Unfortunately this is intentional; the watchface must be reloaded manually. I don't have partner-level API access (and lack the business license/desire needed to apply) so I cannot force the watchface to reload from within the AWConfig app (tizen.application.kill is partner-level). I don't want to query the filesystem for configuration changes from AWatch because that'd be an unreasonable and unnecessary drain on resources. I suppose I'll give them credit for conveying the issue without using words? Images below are screenshots from the video that Samsung sent me w/the rejection. I submitted a question through their "one on one developer support" (?) asking for recommendations. We'll see.

<img class="image_center" width="775" src="/images/watch_failure.png" />

<b>Update 3: Success! Both AWatch and AWConfig are both listed on the Samsung Gear Store. There are updates I'd like to make on both apps, but the lengthy process involved w/updating apps puts any minor updates I'd like to make at the absolute bottom of my todo list. </b>

Update 4: I pushed a few updates with additional functions (temperature unit display, 24 hour mode, retaining saved data in AWConfig), but unless some magnificent bug is discovered, I'm no longer working on this project. Pushing updates to the Samsung store is too frustrating, nearly every update was met with an initial rejection for absurd reasons (eg, 1: displayed weather data on my watchface doesn't match the weather data on the official weather app; this is because my data updates every hour from weather underground while their app only updates every 6 hours from weather.com, 2: displayed step count doesn't match SHealth step count for the first 24 hours; this is because they don't allow access to the SHealth daily step count!). Turnaround time between submission and first rejection was usually ~7 days, plus re-submission and certification adding another ~7 days. 2 weeks for a simple update that had no problems to begin with makes for a miserable experience.
