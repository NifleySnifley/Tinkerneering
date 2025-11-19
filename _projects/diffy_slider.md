---
layout: project
projid: diffy-slider
title:  "Differential Slider-Arm"
date:   2025-06-1 00:00:00 -0500
wip: true
categories: project
description: A lightweight differential mechanism I built to learn more about optimal control and system identification.
image: diffyslider/IMG_1971.png
links:
 - "[OnShape](https://cad.onshape.com/documents/06eba940ba88e9d4b1a03ccb/w/5bae78d6217bce97356096fe/e/b3570365d257c890cd529b45?renderMode=0&uiState=691e2aaf01f092eb821547a7)"
---

The mechanism is driven by two Kraken X44 brushless motors in a differential configuration where spinning both motors the same direction rotates the arm, and spinning them in opposite directions slides the gantry. This is accomplished with two 2-meter long HTD belts directly driven by the motors. For more rotational torque on the arm, the gantry integrates a low backlash 3D printed single stage planetary gearbox. The slider bearing blocks and ring gear are integrated resulting in a very low part count.

### Gallery

<br/>
{% include image.html file="diffyslider/full_cad.png" astyle="width:65%" caption="Full mechanism CAD" %}

{% include image.html file="diffyslider/exploded.png" astyle="width:65%" caption="Gantry exploded view" %}

{% include image.html file="diffyslider/IMG_1973.png" astyle="width:65%" caption="Motor mounting" %}

{% include image.html file="diffyslider/IMG_1992.png" astyle="width:65%" caption="Gantry belt routing" %}

### Videos

<iframe width="100%" height="512" src="https://www.youtube.com/embed/jd06Zb-_0CQ" title="DiffySlider Belt Demo" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

<br/>
System identification - a great showcase of how terrifyingly fast this thing can accelerate, this is only stepping at 5V rather than the 12V or 24V I run it at...
<iframe width="100%" height="512" src="https://www.youtube.com/embed/459f19hf8Qs" title="DiffySlider SysID" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>