---
layout: content
title: MS Band Utilities
hasgithub: https://github.com/kairozu/Microsoft-Band-Utils
hasimg: /images/bandsandbox.png
imgwidth: 240
tags: project code
---
This is a summary of the various utilities I made for interacting with the Microsoft Band: a simple Android app for polling the sensor data, and a windows app for downloading data from Microsoft Health Cloud w/a few simple Python scripts for parsing/analyzing data. 

The Microsoft Band isn't a perfect device, but I find it to be comfortable and non-intrusive. The haptic alerts are great, I use the run tracking whenever I'm not racing against a PR, I like the structured workouts, and the constant heart rate/skin temperature readings are really interesting to me. The battery life is sufficient for my usage patterns (usually lasts about 3 days w/o watch mode, just over a day w/watch mode), and it's not a fragile piece of hardware. 

## Android App (BandStat)
<img class="image_l" height="135" alt="bandstat" src="/images/bandstat.png" />

Bare-bones Android app which interfaces with the Microsoft Band (using the newly released SDK) -- the app displays band version, firmware version, and real-time readings from the heart rate, skin temperature, uv index, accelerometer, and gyroscope sensors.

I pair the Band with a Samsung Galaxy S5. The Android interface is well-developed, but lacks the keyboard functionality that Windows Phone 8.1 has. For viewing data, the web interface is best: [https://dashboard.microsofthealth.com](https://dashboard.microsofthealth.com).

The first SDK release offers access to the device sensors (accelerometer, gyrometer, UV index, skin temperature, heart rate), a way to change the colors/theme of the Band interface, the ability to create your own tile, access to the haptic motor for sending alerts, and the ability to send messages to the Band itself. Hoping for keyboard functionality outside of the Windows Phone universe in the next release -- would be nice to take/store quick notes on the Band itself.

Update 2015.06.29: You can download the example app here: [https://play.google.com/store/apps/details?id=com.dendriticspine.msbandstat](https://play.google.com/store/apps/details?id=com.dendriticspine.msbandstat)

It's not anything resembling pretty (read: currently there is no actual "design" involved with this app), but it's functional.

In [Android Studio](http://developer.android.com/sdk/index.html), include the [Microsoft Band SDK](http://developer.microsoftband.com) jar file in your Android project:
1. Go to your Android project's application directory and locate the libs folders (you can create it if it does not already exist), and copy the jar file to this location.
2. Open the Project Structure window from the File menu
3. Select the application module from the Modules list on the left
4. Select the Dependencies tab on the right
5. Click the + button on the right and select File dependency
6. Expand the libs folder, select the jar file, and click OK

In addition to adding the jar file to your Android project, you will also need to declare the following uses-permission tags in the AndroidManifest.xml:

<span class="mono">
&lt;uses-permission android: name="android.permission .BLUETOOTH"/&gt;<br />
&lt;uses-permission android: name="com.microsoft.band.service.access .BIND_BAND_SERVICE"/&gt;
</span>

The Band SDK documentation can be found here: [http://developer.microsoftband.com/docs/MicrosoftBandSDKPreview.pdf](http://developer.microsoftband.com/docs/MicrosoftBandSDKPreview.pdf)

A few changes to the documentation examples:<br />
<span class="mono">
Fails: import com.microsoft.band.BandConnectionResult;<br />
Works: import com.microsoft.band.ConnectionResult;<br />
<br />
Fails: BandClient bandClient = BandClientManager.getInstance() .create(getActivity(), pairedBands[0]);<br />
Works: BandClient bandClient = BandClientManager.getInstance() .create(getApplicationContext(), pairedBands[0]);<br />
<br />
Fails: BandPendingResult&lt;BandConnectionResult&gt; pendingResult = bandClient.connect();<br />
Works: BandPendingResult&lt;ConnectionResult&gt; pendingResult = bandClient.connect();<br />
</span>

Leaving this running on the phone drains the battery of the Band pretty quickly (constantly reading from the sensors + transmitting via bluetooth), but it's good for brief usage to see how the sensors work. There's also an option to determine whether the band is currently in contact with skin, and how "stable" the heart rate reading is.

The temperature reading (in degrees Celsius!) skews lower than your internal temperature, but it is pretty consistent. I used the paper "[Uncovering Different Masking Factors on Wrist Skin Temperature Rhythm in Free-Living Subjects](http://journals.plos.org/plosone/article?id=10.1371/journal.pone.0061142)" as a basis for comparison (side note: there's some really interesting research out there on correlation between wrist temperature and circadian rhythm).

<img class="centerImg" alt="microsoft band orientation" src="/images/bandaxes.PNG" />

The accelerometer and gyroscope/angular velocity x/y/z orientation (image taken from Microsoft's SDK documentation) is easy enough to discern by watching the values change as you move your arm in various directions, but I'm intrigued by how consistent the readings were with my attempts at making identical repetitive motions. Could be useful for identifying arm/wrist based gestures for controlling other things.

## BandSandbox (Download Health Data)
The download/export option offered by Microsoft in their Health Dashboard doesn't give you the full set of data collected by the Microsoft Band. This is a quick (and dirty) program to download _everything_ (or what you choose) using their Health Cloud API. The code is really ugly, and it errs on the slow side to avoid server-side rate limiting, but it works.

I also threw together (again, really ugly) some Python scripts to help parse/display the data:
[https://github.com/kairozu/Microsoft-Band-Utils/tree/master/Band-Data-Analysis](https://github.com/kairozu/Microsoft-Band-Utils/tree/master/Band-Data-Analysis)

**Relevant Resources**
* Microsoft Health Cloud: [https://developer.microsoftband.com/cloudAPI](https://developer.microsoftband.com/cloudAPI)
* Microsoft Health Dashboard: [https://dashboard.microsofthealth.com/](https://dashboard.microsofthealth.com/)
* MS Developer Center: [https://account.live.com/developers/applications](https://account.live.com/developers/applications)

Connecting to the Microsoft Health Cloud API requires a Microsoft account w/a registered application. You can register an application at the developer center link above -- the Client ID & Client Secret are both necessary.

The Health Cloud API will remove your access if you pummel their servers with requests, so I added 10-30 seconds between requests -- this means it can take a while to download large data sets. Time for requesting 1 year+5 days (572 activities) worth of...

- Hourly Summary Data: 8 min, 31 sec
- Daily Summary Data: 28 sec
- All Activities: Basic Activity Summary Data: 19 sec
- All Activities: GPS Data & Segment Details: 6 min, 34 sec
- All Activities: Minute Interval Summaries: 18 min, 42 sec <- required additional delays between requests to avoid being throttled for going over the bandwidth limits. 

## Compiling a Custom BandSandbox
A surprising number of people have e-mailed me for help with using or modifying the utility I wrote for extracting data from Microsoft Health (usually data collected via the now-discontinued Microsoft Band). I’ve pushed a few updates for others (bug fixes, adding future dates, etc), but I’m putting this detailed guide for building your own executable here.

Note: This assumes you’re running Windows 10.

### Create a Microsoft Application ID
Go to <a href="https://account.live.com/developers/applications">https://account.live.com/developers/applications</a> and log in to your Microsoft Account. Under Live SDK applications, click the button to **Add an App**. Enter whatever name you’d like, e.g. “MyBandSandboxApp” and click **Create Application**.

<img class="centerImg" src="/images/vs_install_a.png" />

Under Platforms, click **Add Platform** and select the **Native Application** option. A new “Native Application” section will appear in the Platforms section (already shown in the image below). Scroll down to the bottom of the page and click the **Save** button.

The **Application ID** (purple highlight below) is your *ClientId*, and the string under **Application Secrets** (orange highlight below) is your *ClientSecret*. Copy these two strings to a text file, an e-mail, or somewhere else you’ll be able to access them later. The ClientId and the ClientSecret shown in these images won't work for you.

<img class="centerImg" src="/images/vs_install_b.png" />

### Download and Extract BandSandbox Code
Download and unzip (right click the downloaded file and select “Extract All…”) the current GitHub repository for MS-Band-DataSandbox: <a href="https://github.com/kairozu/Microsoft-Band-Utils/archive/master.zip">https://github.com/kairozu/Microsoft-Band-Utils/archive/master.zip</a>

### Download and Install Visual Studio Community
Download and run the Visual Studio Community installer: <a href="https://www.visualstudio.com/vs/community/">https://www.visualstudio.com/vs/community/</a>

When you’re presented with the installation options window shown below, select **.NET desktop environment**. You can ignore the tabs for individual components and language packs. Click the **Install** button.

<img class="centerImg" src="/images/vs_install1.png" />

After installation, click the **Launch** button.

<img class="centerImg" src="/images/vs_install2.png" />

Signing in to your Microsoft account isn’t required -- for now, select *Not now, maybe later.* on the welcome screen. Leave the defaults for Development Settings/Color Theme, and click the **Start Visual Studio** button.

<div class="flexBox">
	<a href="/images/vs_install3.png"><div class="innerImg" style="background-image: url('/images/vs_install3.png');"></div></a>
	<a href="/images/vs_install4.png"><div class="innerImg" style="background-image: url('/images/vs_install4.png');"></div></a>
</div>

### Open, Modify, and Build BandSandbox
On the Start Page, click **Open Project / Solution** (or go to File > Open Project or Solution), and navigate to where you unzipped the BandSandbox GitHub repository (the default path is: *Downloads/Microsoft-Band-Utils-master/BandSandbox-Data-Extract/*). Select the Microsoft Visual Studio Solution file named **BandSandbox(.sln)** to open it. A security warning will pop up, click the **OK** button to continue.

<img class="centerImg" src="/images/vs_install5.png" />

In the Solution Explorer window, right click **BandSandbox** and select *Properties* to open the project properties window.

<img class="centerImg" src="/images/vs_install6.png" />

Go to the *Signing* tab, click the dropdown menu where it says *Choose a strong name key file:* and select **<New…>**. Type in a new name for your key file (e.g. “new_band_sandbox_key”), then enter a new password and click the **OK** button.

<img class="centerImg" src="/images/vs_install7.png" />

Click the **small arrow indicator** next to MainWindow.xaml to reveal **MainWindow.xaml.cs**. Double-click on **MainWindow.xaml.cs** to open the file.

<img class="centerImg" src="/images/vs_install8.png" />

Replace the text that says *replace-with-your-own-application-id* with the **Application ID** you created earlier, and replace the text that says *replace-with-your-own-client-secret* with the **Application Secret** you created earlier. Keep the quotation marks. The two lines should look something like this when you’re done, but with your own values.

<span style="color: #0000FF;">private const string</span> ClientId = <span style="color: #800000;">"00000000345EDA6E"</span>;  
<span style="color: #0000FF;">private const string</span> ClientSecret = <span style="color: #800000;">"ODqzkdp7bAKNA6uDIkHfsle"</span>;

At the top of the window, click the dropdown menu where it says Debug and select **Release**. Next, go to the File menu, and select Save All. Last, go to the Build menu, and select Build Solution.

<img class="centerImg" src="/images/vs_install9.png" />

Assuming that the build completes successfully, go back to the folder where you unzipped the GitHub repository, go into the **BandSandbox** directory, then the **bin** directory, and finally the **Release** directory. The **BandSandbox(.exe)** file is the program you will run to download your data. 

<img class="centerImg" src="/images/vs_install10.png" />

This folder (Release) can be copied and used from another computer; the **Newtonsoft.json** and **Newtonsoft.json.dll** files (orange highlight in the image below) must be kept in the same folder as the BandSandbox executable for it to run properly.

<img class="centerImg" src="/images/vs_install11.png" />
