---
layout: content
title: Intracellular Recording
tags: science
hasimg: /images/helixa_ganglia.png
imgwidth: 240
---
The nervous system of Helix aspersa consists of a small number of large neurons (motor, sensory, and interneurons) grouped into discrete ganglia located throughout the snail (vs one cephalized structure in the head). Exposing the subesophageal ganglia, part of a ring of ganglia surrounding the esophagus, allows for intracellular recordings from neurons in the left parietal and right parietal ganglia -- these neurons carry signals to and from the gut, head, and foot of the snail. The recordings below are from a neuron in the right parietal ganglia (circled in green on the right).

Glass microelectrodes are used for intracellular recording. 1.5mm diameter glass tubes are heated/pulled until they extend to a very fine point (less than 0.5um -- small enough that it can be inserted across the cell's plasma membrane without severe damage). The microelectrode is filled w/3M potassium chloride, which forms a conductive path through the electrode into the cell. This was done in a laboratory setting using a vibration isolation table ("air table") to protect the preparation from mechanical disturbances. Impaling the neuron with a microelectrode causes damage to the cell, often eliciting an erratic response of spontaneous activity and causing a depolarization in the cell membrane; hyperpolarizing DC current can be used to stabilize the cell if needed.

## Equipment Used
* A-M Systems Humbug Noise Eliminator, 110V, 60Hz
* WPI Model 767-B Intra Electrometer
* AD Instruments PowerLab 26T
* Sutter Instruments MP-285/T Micromanipulator
* AmScope 40x-2000x B580B
* MATLAB, LabChart, LabScope

## Intracellular Recording
<a href="/images/ic_fig1.png"><img class="imageCenter" alt="Intracellular Recording" src="/images/ic_fig1.png" /></a>

Spontaneous bursting of action potentials following impalement of a neuron in the right parietal ganglia. Impalement at t = 6:18 (A) -- showed initial bursts of action potentials 3-8 spikes long which occurred both spontaneous and as an apparent reaction to a brief depolarizing pulse of 10nA current at t = 6:35 (B). Time between bursts increased from 3 seconds, to 5 seconds, to 10 seconds. The resting potential was unstable between -29.02mV and -34mV for the first minute, with an average action potential amplitude of 73.22mV (C) from rest, an average overshoot of 42.09mV (D), and an average undershoot of 20.62mV (E) below resting.

## Hyper & Depolarizing Current
<a href="/images/ic_fig2.png"><img class="imageCenter" alt="Hyper & Depolarizing Current" src="/images/ic_fig2.png" /></a>

The neuron ceased spontaneous activity without any external stimulus and the resting potential continued to decrease, reaching -46.04mV (A). Whether the three hyperpolarizing DC current pulses applied at t = 1:27 (B), t = 1:33 (C), and t = 1:40 (D) contributed to the continuing stabilization of the resting potential is unknown. A 3ms pulse of 4.21nA current triggered a burst of action potentials (E).

## Short Pulse Stimulation
<a href="/images/ic_fig3.png"><img class="imageCenter" alt="Short Pulse Stimulation" src="/images/ic_fig3.png" /></a>

Thirteen 10ms pulses of depolarizing current ranging in amplitude from 3.01nA to 5.01nA were injected into the neuron. Action potentials were achieved with depolarizing current as low as 4.30nA, but only pulses above 4.71nA resulted in an action potential with every pulse. 4.51nA was the lowest amplitude pulse that could produce an action potential greater than 50% of the time. Neuron responses are listed by number with associated current injection. The resting potential of the cell was -47.50mV, with the action potential caused by 4.51nA of current reaching threshold at -36.38mV and having an amplitude of 80.31mV, an overshoot of 33.29mV, and an undershoot of 18.03 below resting. The duration of the action potential using the half amplitude method was 14.98ms (A). The spikes in membrane voltage at the onset and cessation of stimulus result from the bridge being unbalanced.

## Summation Response 
<a href="/images/ic_fig4.png"><img class="imageCenter" alt="Summation Response" src="/images/ic_fig4.png" /></a>

Eight 2.81nA pulses of depolarizing current, 3ms in duration with 5ms intervals, were injected into the neuron. The membrane potential continued to depolarize more and more w/the summed response to each additional pulse. The neuron was sufficiently depolarized to threshold at -35.50mV (A), triggering an action potential.

## Membrane RC Properties
<a href="/images/ic_fig5.png"><img class="imageCenter" alt="Membrane RC Properties" src="/images/ic_fig5.png" /></a>

A single 1s duration 0.20nA amplitude stimulus caused the neuron to depolarize along an RC curve, representing the passive properties of the cell. Vmax (A) is -41.12mV, 63% of Vmax (B) = -44.82mV, and tau (C) = 170ms.

<a href="/images/ic_fig6.png"><img class="imageCenter" alt="Membrane RC Properties" src="/images/ic_fig6.png" /></a>

Next, five hyperpolarizing pulses were injected, ranging from -0.80nA to -4.00nA. Vm at (A) is -139.58mV, 63% of Vm at A (from rest) is -106.43mV (B), tau is 70ms (C). Using Vm at (A) adjusted for resting potential and the -4.00nA of injected current to calculate the passive resistance value of this neuron yields R = 22.40MOhm, and using tau to calculate the capacitance yields C = 3.13nF.

## Post-Inhibitory Rebound
<a href="/images/ic_fig7.png"><img class="imageCenter" alt="Post-Inhibitory Rebound" src="/images/ic_fig7.png" /></a>

Hyperpolarizing pulses of -2.51nA and -3.01nA for a duration of 1s each hyperpolarized the cell sufficiently to trigger an action potential following the cessation of stimulus; the post inhibitory rebound response. Only one action potential was triggered for each hyperpolarization, and no action potentials were triggered for hyperpolarizing stimuli between 0-2.5nA.