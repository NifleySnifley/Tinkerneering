---
layout: project
projid: fpga-cpu
title:  "FPGA RISC-V SoC"
date:   2024-10-9 00:00:00 -0500
wip: true
categories: project
description: I'm currently designing a SoC based on my own RISC-V rv32IM-compatible processor core with VGA graphics and other miscellaneous IO functionality TBD. Initially, I targeted the amazing [Upduino](https://tinyvision.ai/products/fpga-development-board-upduino-v3-1)'s [ICE40UP5K](https://www.latticesemi.com/en/Products/FPGAandCPLD/iCE40UltraPlus) FPGA, but in search of higher performance, I have pipelined my initial design and switched to using a [ECP5](https://www.latticesemi.com/Products/FPGAandCPLD/ECP5) to allow for a more complex and optimized design with more FUNctionality.
image: fpga_cpu/fpeega.jpg
links:
 - "[GitHub](https://github.com/NifleySnifley/CPUDesign-IS)"
---

<br/>
## Current Achievements:

- Pipelined rv32im CPU and SoC capable of running on a ColorLight 5A-75B board (Lattice ECP5 LFE5U-25F) at 50MHz. 33.386 MIPS @ 50MHz, with the Dhrystone benchmark (1.5 CPI).

- Multi-cycle rv32im CPU and SoC capable of running on an Upduino board (Lattice ICE40UP5K) at 25MHz (overclocked). 4.7MIPS according @ 25MHz with the Dhrystone benchmark (5.32 CPI)

- 2-bit-color memory-mapped text mode VGA display adapter (640x480, 8x16 bitmap font, fg&bg color)

- Memory-mapped parallel IO and SPI host controller

- SPI Flash memory bootloader for Upduino SoC (flash memory->SPRAM)

- rv32im simulator written in C, side-by-side comparative verification by simulation of HDL designs (Verilator) alongside the software simulator. Running the official RISC-V rv32im test suite.

- SDL-based emulator for both SoCs with VGA and HUB75 LED matrix emulation.

<br/>

Here's a pinout diagram of my initial Upduino-based carrier board with 2-bit VGA graphics and a SPI controller for bootloading from flash memory.
{% include image.html file="fpga_cpu/pinout.png" astyle="width:65%" caption="Pinout" %}
<!-- 
<br/>
It also runs on a iceFUN board! (faster, but with less memory)
{% include image.html file="fpga_cpu/pinout.png" astyle="width:65%" caption="iceFUN blinky!" %} -->