---
layout: content
title: Animal Fluid Reward
hasgithub: https://github.com/kairozu/Peristaltic-Pump-Reward-System
hasimg: /images/pump_mini.jpg
imgwidth: 240
tags: project science code
---
Most commercial water/fluid reward systems used in research settings cost a few hundred dollars (or more) and aren't easily modified / are difficult to integrate with existing hardware. This is a series of fairly quick hacks, but they do the job well and won't cost you >$100.. much less if you already have some of the components sitting around. Using a peristaltic pump is preferred, as the motor never actually comes into contact with the fluid itself. There are three different versions here -- the one I personally use is built with a Raspberry Pi, the L293D quadruple half-H driver from TI, and a peristaltic pump from Adafruit. The other version uses an Arduino with a SeeedStudio motor shield, but any motor shield made for the Arduino would probably do fine. You could also build an Arduino-based version using an L293D.

<div class="spacerClear"></div>

## Components/Languages
* Peristaltic Liquid Pump (12VDC / 300mA) with Silicone Tubing (max flow 100mL/min): [http://www.adafruit.com/products/1150](http://www.adafruit.com/products/1150)
* 12VDC Adapter (old D-Link wall adapter in my case) to power the motor
* Programmable device to control motor activity:
	* [Option 1] Raspberry Pi Model B: [http://www.newark.com/jsp/search/productdetail.jsp?sku=43W5302](http://www.newark.com/jsp/search/productdetail.jsp?sku=43W5302)
	* [Option 2] Arduino Uno (Or Similar): [http://arduino.cc/en/Main/arduinoBoardUno](http://arduino.cc/en/Main/arduinoBoardUno)
* Some way of routing power to/driving the motor:
	* [Option 1] L293D: [http://www.ti.com/lit/ds/symlink/l293d.pdf](http://www.ti.com/lit/ds/symlink/l293d.pdf) / [http://www.adafruit.com/products/807](http://www.adafruit.com/products/807)
	* [Option 2] Arduino Only: Seeed Motor Shield (any motor shield that fits your Arduino) [http://www.seeedstudio.com/](http://www.seeedstudio.com/depot/motor-shield-p-913.html)
	* [Option 3] Power Transistor
* Various build-necessary components for connecting everything (wire, protoboard, etc)
* [Optional] Momentary Push Button/Switch + 10kOhm resistor for manual fluid delivery
* [Optional] Something to house the components (I like OpenBeam or MakerSlide)

## Notes
***Raspberry Pi (or Arduino) with L293D***

Git repo: [https://github.com/kairozu/Peristaltic-Pump-Reward-System/tree/master/raspberry\_L293D\_version](https://github.com/kairozu/Peristaltic-Pump-Reward-System/tree/master/raspberry\_L293D\_version)

* Wiring diagram can be found below, and the L293D pinout can be found here: [http://www.ti.com/lit/ds/symlink/l293d.pdf](http://www.ti.com/lit/ds/symlink/l293d.pdf) -- additionally the DC motor tutorials at Adafruit (for both Arduino and Raspberry Pi) might be useful as a secondary reference if you have any trouble getting the motor running.
* Update your Raspberry Pi & install WiringPi2 (Python port) from GitHub:

		> sudo apt-get update
		> sudo apt-get upgrade
		> sudo apt-get install git-core
		> git clone git://github.com/WiringPi/WiringPi2-Python.git
		> cd wiringPi2-Python
		> sudo python setup.py install

* Build everything! (Breadboard -> Final Version)
* Download and run my Python script to drive the motor (or write your own)
	* My code is here: [https://github.com/kairozu/Peristaltic-Pump.../raspberry\_L293D\_version/L293D\_pump\_code\_wiringPi.py](https://github.com/kairozu/Peristaltic-Pump-Reward-System/blob/master/raspberry\_L293D\_version/L293D\_pump\_code\_wiringPi.py)
	* ("startx" to enter the Raspberry Pi desktop environment before running this script -- if you wish to run everything from the console, cut out all of the pygame code)
	* Press "w" to run the pump briefly.
	* Press "esc" to quit the program.
	* This line controls both the motor step size (1000) and the length of time the motor runs (1 second): motor.motor_loop(1000,1) -- modify it to suit your needs.
* (Note: There's another Python script in the git repository which can be used w/the Adafruit Occidentalis distro that doesn't require wiringPi be installed.)


***Arduino & SeeedStudio Motor Shield***

Git repo: [https://github.com/kairozu/Peristaltic-Pump-Reward-System/tree/master/arduino\_version](https://github.com/kairozu/Peristaltic-Pump-Reward-System/tree/master/arduino\_version)

* If you use the Seeed motor shield you'll need a compatible Arduino pinout -- the duemilanova or the uno both work well. This motor shield is overkill, but it's cheap/simple & the wiki has good information: [http://www.seeedstudio.com/wiki/Motor\_Shield\_V1.0](http://www.seeedstudio.com/wiki/Motor\_Shield\_V1.0)
* Connect your DC power adapter to the motor shield Vs / Gnd pins, and connect the motor to the M1+ / M1- pins.
* Connect the motor shield to the Arduino.
* Upload Arduino code via USB: [https://github.com/kairozu/Peristaltic-Pump-Reward-System/.../arduino\_motor\_shield\_drive.ino](https://github.com/kairozu/Peristaltic-Pump-Reward-System/tree/master/arduino\_version/arduino\_motor\_shield\_drive.ino)
* If you leave the J6 jumper connected, you don't need to provide a separate power source to the Arduino (it will pull power from the motor shield).
* If you want a manual “push button to dispense fluid” feature, you can pick up a button module from Seeed and connect it via their Grove system to make life easy, but I used a 10kOhm resistor and an old button switch I had laying around.

		Switch
			|
			|------------
			|           |
			|           |
			|          / \
		    5V        /   \
				10kOhm   Arduino Pin #5
			   Resistor
					|
					|
				   Gnd

* The physical assembly was done using odd metal pieces I had laying around. I'm not particularly proud of it, but it works fine (it doesn't really need a physical assembly to be functional). 
