---
layout: project
projid: fpga-cpu
title:  "FPGA RISC-V SoC"
date:   2024-10-9 00:00:00 -0500
categories: project
description: I'm currently designing a SoC based on my own RISC-V rv32IM-compatible processor core with VGA graphics and other miscellaneous IO functionality TBD. Currently, I'm targeting the amazing [Upduino](https://tinyvision.ai/products/fpga-development-board-upduino-v3-1)'s [ICE40UP5K](https://www.latticesemi.com/en/Products/FPGAandCPLD/iCE40UltraPlus) FPGA, but I'm planning to move to a [ECP5](https://www.latticesemi.com/Products/FPGAandCPLD/ECP5) soon to enable adding more advanced functionality & increase speed.
image: fpga_cpu/fpeega.jpg
---

<br/>
Here's a pinout diagram of my most recent Upduino-based carrier board
{% include image.html file="fpga_cpu/pinout.png" astyle="width:65%" caption="Pinout" %}
<!-- 
<br/>
It also runs on a iceFUN board! (faster, but with less memory)
{% include image.html file="fpga_cpu/pinout.png" astyle="width:65%" caption="iceFUN blinky!" %} -->