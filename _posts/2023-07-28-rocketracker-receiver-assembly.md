---
layout: post
title:  "Rocket Tracker Part 4: Receiver Assembly"
date:   2023-07-28 15:00:00 -0500
categories: blog
project: rtrk
---


The PCBs for my receiver finally arrived! After almost exactly a week, my boards from JLCPCB were ready to be assembled!
<br/>
<br/>
<div style="width: 100%; height: fit-content, display: block; overflow: auto;">
{% include image.html file="rocketracker/pcb_assy/boardfront.jpg" astyle="width:40%; float: left; margin-left: 5%" %}
{% include image.html file="rocketracker/pcb_assy/boardback.jpg" astyle="width:40%; float: right; margin-right: 5%" %}
</div>


### Paste Stenciling

Due to the use of 0402 components, a USB-C connector and a QFN-packaged microcontroller in my deshaving a stencil was pretty much a neccessity. I made a makeshift jig to hold the PCB to be assembled by taping the other 4 pcbs down to the stencil's wood packaging and smeared my solder paste onto the PCB with a metal scraper.

<br/>
<div style="width: 100%; height: fit-content, display: block; overflow: auto;">
{% include image.html file="rocketracker/pcb_assy/stencil1.jpg" astyle="width:40%; float: left; margin-left: 5%" caption="The stencil, quite reflective!" %}
{% include image.html file="rocketracker/pcb_assy/paste_jig.jpg" astyle="width:40%; float: right; margin-right: 5%" caption="Using PCBs to hold PCBs" %}
</div>

{% include image.html file="rocketracker/pcb_assy/boardpasted.jpg" astyle="width:65%" caption="The board with solder paste applied" %}

### Pick and Place, Manually

The most laborious part of assembling the board was placing all of the 22 diferent types of components which were each in their own bags from DigiKey, I ended up just taking bags out of the box one by one, opening them, and placing the components. Thanks to the awesome interactive BOM plugin for KiCAD which made it really easy to locate each component, assembly took me only about 20 minutes. Placing the 0402 components was much easier than I expected and I'm pretty confident I could have hand soldered them if I had needed to. After all of the components were placed (except the one DNF pullup resistor) the board was ready to be reflowed!.

<br/>
{% include image.html file="rocketracker/pcb_assy/boardpopulated.jpg" astyle="width:65%" caption="All SMD components placed!" %}

### Final Touches

After reflowing the rp2040 and USB connector were left with a few solder bridges but I managed to remove them with some solder wick and it wasn't nearly as much of a nightmare as I had expected! I soldered on a couple of THT components such as the expansion headers and the SMA connector for the antenna and it was done! When I plugged it into my computer Windows made a happy noise and it showed up as a USB drive! Success! but not quite yet... I tried to program it with a simple blink program but the board seemed to fail programming. Using `picotool` I confirmed that the flash wasn't being programmed properly and set off to find a solution. I used my hot air gun to re-reflow the rp2040 and its flash chip just to make sure there weren't any bad connections and I also had to flip around the LEDs that I realized I had placed backwards. Well, one of these things seemed to fix the issue and I was able to get it to program!

<br/>
<div style="width: 100%; height: fit-content, display: block; overflow: auto;">
{% include image.html file="rocketracker/pcb_assy/blobsdetail.jpg" astyle="width:40%; float: left; margin-left: 5%" caption="Annoying solder blobs" %}
{% include image.html file="rocketracker/pcb_assy/blobsfixed.jpg" astyle="width:40%; float: right; margin-right: 5%" caption="Fixed!" %}
</div>

<br/>
{% include image.html file="rocketracker/pcb_assy/blinking.jpg" astyle="width:65%" caption="Happily blinking" %}

Thanks for reading! Keep posted for the future of this board, hopefully it will get some firmware soon!