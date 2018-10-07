---
layout: content
title: Insect Flight Lab
hasgithub: https://github.com/kairozu/Insect-Flight-Lab
hasimg: /images/torque_render.png
tags: project science code
---
Series of tools designed for observing and experimenting with the mechanics of insect flight. Includes a tethered insect flight simulator which combines a closed loop visual feedback system with an optical transducer that records torque produced by yaw motions -- this allows for (soft) real time external control of the relationship between insect yaw motions and resulting movement of the insect's visual field. I was interested in the extent to which feedback gain between torque (yaw) and image motion determines an animal's ability to track a visual stimulus, along with the ability of an animal to adapt to different gains (including negative gain) applied to the feedback loop.  The latter investigates the potential for natural plasticity in the visual flight control circuit. 

## Torque Sensor Components
* 1x Tungsten Wire/Rod
* 5x Miniature Screws (2x top, 2x bottom, 1x mount)
* 2x Precision Ball Bearings (SD 3mm, OD 10mm, Width 4mm) ([http://www.mcmaster.com/#7804k128/=cypl5s](http://www.mcmaster.com/#7804k128/=cypl5s))
* 1x Brass Rod (1/4, 6.35mm diameter) ([http://www.acehardwareoutlet.com...SKU=5391016](http://www.acehardwareoutlet.com/ProductDetails.aspx?SKU=5391016))
* 1x OSI Optoelectronics Dual Photodiode
* 1x 940nm IR LED ([http://www.radioshack.com...2062565](http://www.radioshack.com/product/index.jsp?productId=2062565))
* 1x AD734 (10MHz, 4-Quadrant Multiplier/Divider) ([http://www.analog.com...product.html](http://www.analog.com/en/special-linear-functions/analog-multipliersdividers/ad734/products/product.html))
* 1x OP467 (Quad Op-Amp) ([http://www.analog.com...product.html](http://www.analog.com/en/all-operational-amplifiers-op-amps/operational-amplifiers-op-amps/op467/products/product.html))
* AD827 (Dual Op-Amp) ([http://www.analog.com...product.html](http://www.analog.com/en/other-products/militaryaerospace/ad827/products/product.html))
* 2x 100k resistors
* 2x 5k resistors
* 2x capacitors
* +/-12V Voltage Source

## Insect Virtual Flight Arena/Rear Projection System Components
* Curved rear projection screen (sheet of mylar from your local art store works fine)
* VSL Software (Win & OSX Versions)
	* Version 1: Torque Sensor Alpha &rarr; Level Shifter &rarr; Arduino &rarr; VSL v1.0 in Processing
	* Version 2: Torque Sensor Alpha &rarr; Level Shifter &rarr; Teensy &rarr; VSL v2.0 in OpenGL/C
	* Version 3: Torque Sensor Beta &rarr; NI DAQ Board Input A &rarr; MATLAB &rarr; Torque Sensor Beta &rarr; NI DAQ Board Input B &rarr; VSL v3.0 in OpenGL/C
	* Version 4: Torque Sensor Beta &rarr; NI DAQ Board &rarr; VSL v4.0 in OpenGL/C with (optional) MATLAB export
* EAGLE (only necessary if you want to produce the Torque Sensor interface PCB)
* (optional, for data processing) MATLAB
* [80-20](http://www.8020.net/) was used to construct the arena frame, with a curved sheet of mylar acting as the rear projection screen
* TI pico projector ([http://www.ti.com/tool/dlp1picokit](http://www.ti.com/tool/dlp1picokit)) was used to project the visual stimulus onto the convex surface of the curved mylar
* (optional, but awesome) low-pass filter/instrumentation amp from [Alligator Technologies]( http://www.alligatortech.com/USBPGF-S1_USB_programmable_instrumentation_amplifier_low_pass_anti_alias_filter.htm) to filter out the wingbeat frequency
* NI-DAQ board for data collection (in my experience, the more expensive the DAQ board, the more issues you will have -- be wary)

<div class="flexBox">
	<div class="innerImg" style="background-image: url('/images/torquearena.png');"></div>
	<div class="innerImg" style="background-image: url('/images/testing_torque.jpg');"></div>
</div>

## Notes
This system was used to gather data for the following papers:
 
* [Abdicating power for control: a precision timing strategy to modulate function of flight power muscles](/images/abdicating.pdf) (Sponberg S, Daniel TL)
* [Autostabilizing airframe articulation: Animal inspired air vehicle control](/images/autostabilizing.pdf) (Dyhr JP, et al.)

<div class="flexBox">
	<img class="image_center" src="/images/torque2.0.png" /> 
	<img class="image_center" src="/images/torque2.0board.png" />
</div>

The torque sensor and associated divider circuit allow us to measure the yaw motions of tethered insects mid-flight. 

Upgrades from previous builds:

* Switched to a tungsten torsion wire (stainless steel torsion wire had terrible hysteresis effects, wasn't strong enough)
* Used an wavelength matched LED for the dual photodiode (~940nm)
* Used low impedance wire (also: used the same wire for all connections)
* Added capacitors to the photodiode splitter circuit
* Upgraded the crossbar (see pictures)

<img class="image_center" src="/images/torqueTest_sinusoidalGrating2Hz.png" />

The top plot is representative of how the pattern presented to the insect was moving -- in this case a single horizontal bar moving back and forth across the insect's visual field. The bottom plot is the torque recorded during this time; you can see the insect attempting to follow the horizontal bar. 
	
Delay is an issue, in circuits and in visual refresh rates. Most projectors don't actually refresh the display image as often as the refresh rate would imply, and documentation on this is lacking. Ideally this entire system would be implemented in a RT OS.
