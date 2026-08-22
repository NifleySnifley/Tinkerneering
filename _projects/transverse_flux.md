---
layout: project
projid: tfm_v1
title:  "Transverse Flux Motor"
date:   2026-8-22 00:00:00 -0500
wip: true
categories: project
description: Falling down the rabbit hole of motor design and magnetics
image: tfm/v1_cad.png
---

A while ago while reading about motor topologies and thinking about the implications of the analysis in [this amazing blog post](https://robot-daycare.com/posts/actuation_series_1/), I came across transverse flux motors (TFMs). TFMs are an interesting motor topology that enables (at least partial) decoupling of the magnetic and electrical circuits in the motor assembly by (usually) wrapping a single  coil around the inside of a multi-pole (sometimes called "flux modulating") stator core to link (transverse) flux between adjacent poles of a rotor assembly through the (axial) stator coil. The paper "Transverse Flux Machine—A Review" gives a great overview of various stator and rotor structures and archetypes, but what I'm most interested in is the TFM's ability to radically increase the pole count (and thus the torque constant) of a small motor without the need to wind a billion tiny stator teeth with their own coil. In theory, increasing the torque constant by adding more poles is one way to increase the motor constant (Km, Nm/sqrt(W)) of a motor to (hopefully) increase torque density. Honestly, I just was curious about how "good" of a motor I might be able to build using this design without any super fancy materials.



### First Design Iteration
For my first shot at designing a TFM, I decided to pursue a flux-concentrating rotor design with thin magnets to get as fine of a pole pitch as possible. With some [0.5mm thick magnets](https://www.jc-magnetics.com/Magnet-Blocks/N52-10mmx3mmx05mm-thin-Block-Rare-Earth-Neodymium-Magnet) and "faux-SMC" consisting of a mix of low viscosity casting resin and carbonyl iron powder I figured it might be possibly to fit 40 poles onto a 27mm diameter rotor. Unfortunately, after thinking about it for a long while, the manufacturing process for constructing just one of these rotors would be quite the undertaking (needing very fine 3D prints to hold magnets on the rotors, a three-piece modular jig to glue each phase's ring of magnets onto the stator, constructing a mold & vacuum chamber for casting the magnetic resin, etc.). Unfortunately, too much tooling and setup for a one-off in my view. The stator of this motor I planned to get manufactured out of 0.76mm 1008 low-carbon steel sheet from SendCutSend - certainly not as good of an option as electrical steel laminations, but *much* cheaper. I was willing to accept that even at medium speeds the motor's performance would probably be drastically reduced by eddy current losses, but at least I could probably get some good torque production at stall/low speeds with the reasonable magnetic permeability of 1008 steel.

{% include image.html file="tfm/v1/cad_front.png" astyle="width:65%" caption="Axial section view" %}

{% include image.html file="tfm/v1/cad_section.png" astyle="width:65%" caption="Side section view" %}

Although I haven't (and likely won't) manufacture this design, I ran many 2D and 3D magnetostatic simulations and did a bunch of magnetic circuit calculations to estimate performance and motor characteristics. With some tweaks to the design (including a not-really-printable plastic magnet backing to prevent inter-magnet flux leakage) I was able to get the tooth flux density up to about 1T! With this pole count it looks like there would be ~130μWb of flux linked and a rough Km of 0.09Nm/sqrt(W) which isn't bad at all for the size (~0.25kg). Unfortunately, the only way to get this good of torque density is to space the magnets closer together than I'd be able to 3D print the plastic backer for. With my next iteration I'm aiming to scale the design up a bit to not have to deal with 0.5mm thick magnets and be able to actually 3D print and machine parts at the scale I'll need.

{% include image.html file="tfm/v1/femm_mock.png" astyle="width:65%" caption="2D FEMM simulation of flux concentrating rotor with mock stator" %}

{% include image.html file="tfm/v1/flux_vectors_bad.png" astyle="width:65%" caption="Ansys Maxwell simulation of flux before addition of anti-leakage plastic magnet backing" %}

{% include image.html file="tfm/v1/density_good.png" astyle="width:65%" caption="Simulation of flux after addition of anti-leakage plastic magnet backing (much increased tooth density)" %}

{% include image.html file="tfm/v1/flux_tooth_close.png" astyle="width:65%" caption="Flux distribution of a single tooth face" %}


### Current Status:
At this point I'm on my second design iteration aiming to improve manufacturability of the motor while still vying for respectable torque density. More updates coming soon!


Resources:
- [Transverse Flux Machine—A Review](https://ieeexplore.ieee.org/document/9709772)
- [OneWheel TFM Teardown](https://forum.esk8.news/t/v1-onewheel-og-vesc-little-focer-24s1p-87v-upgrades-shredwheel/52984/85)
- [Design of an In-Slot Cooled Air-Core Flux-Focusing Permanent Magnet Synchronous Machine for Electric Aircraft Applications](https://ntrs.nasa.gov/api/citations/20240003659/downloads/TM-20240003659.pdf)
- [Flux Linkage in Transverse Flux Machines with Flux Concentration](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=4602381&tag=1)
- [Structural Dynamic Behaviour of a Linear Transverse Flux Machine](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=11014181)
- [US8395291B2: Transverse and/or commutated flux systems for electric bicycles ](https://patents.google.com/patent/US8395291B2/en?assignee=Electric+Torque+Machines%2c+Inc.&sort=new&page=3)
- [Rim driven thruster having transverse flux motor](https://patents.google.com/patent/US8299669B2/en?q=(transverse+flux+motor+thruster)&oq=transverse+flux+motor+thruster)
- [Transverse Flux Motor - Penn State Altoona \(Nicholas Kuhn\)](https://www.youtube.com/watch?v=AM3y6zRINdc&t=900s)
- [MDSM 2026: Reinventing the Motor: How Transverse Flux Technology is Transforming Industry](https://www.youtube.com/watch?v=66DywIYxGDM&source_ve_path=MjM4NTE&embeds_referring_euri=https%3A%2F%2Fetmpower.com%2F)
- [Design aspects on a transversal flux machine with SMC stator](https://research.chalmers.se/publication/535933/file/535933_AdditionalFile_4a3c6a2f.pdf)