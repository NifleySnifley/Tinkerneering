---
layout: project
projid: bldc_v1
title:  "BLDC Motor Controller V1"
date:   2025-8-1 00:00:00 -0500
wip: false
categories: project
description: My first BLDC motor controller design, targeting 12V nominal operation and 40A peak current. Using the DRV8323 gate driver with integrated low-side current sensing, NTMFS0D5N04XMT1G FETs, and a STM32H523 MCU.
image: bldc_v1/thumbnail.jpg
---

More information coming soon! For now, here's a gallery of photos from development and testing:

{% include image.html file="bldc_v1/layout_v1.png" astyle="width:65%" caption="Iteration 1 of layout" %}

{% include image.html file="bldc_v1/layout_v2.png" astyle="width:65%" caption="Iteration 2 of layout" %}

{% include image.html file="bldc_v1/layout_final.png" astyle="width:65%" caption="Final iteration of layout" %}

{% include image.html file="bldc_v1/bare_pcb.jpg" astyle="width:65%" caption="PCB for real" %}

{% include image.html file="bldc_v1/assembled_basic.jpg" astyle="width:65%" caption="Assembled board - ready for testing" %}

{% include image.html file="bldc_v1/all_leds.jpg" astyle="width:65%" caption="Blinky lights!" %}

{% include image.html file="bldc_v1/motor_setup.jpg" astyle="width:65%" caption="Modified NEO motor with encoder board installed" %}

{% include image.html file="bldc_v1/snubber_wiring.jpg" astyle="width:65%" caption="Oh no! ringing is exceeding the absolute maximum ratings of the gate driver. Time to try adding snubbers and test with one phase hooked to a dummy load" %}

{% include image.html file="bldc_v1/resistor_setup.jpg" astyle="width:65%" caption="Dummy load (and 8020 #2012 for cooling)" %}