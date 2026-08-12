---
layout: project
projid: bldc_v3
title:  "BLDC Motor Controller V3"
date:   2026-8-1 00:00:00 -0500
wip: true
categories: project
description: A third BLDC motor controller completely redesigned using [EPC23102 GaN power stages](https://epc-co.com/epc/products/gan-fets-and-ics/epc23102) and high-bandwidth hall-effect current sensors aiming to operate at higher voltages (48-65V) and be able to efficiently control low-electrical-time-constant motors in a small form factor
image: bldc_v3/kicad_board.png
links:
 - "[PCB Designs Codeberg](https://codeberg.org/Nifley/BLDC_V3)"
---

### Specifications & Design Targets:
- 48V (max 60V) operating voltage
- 500kHz switching frequency
- Fully ceramic bulk capacitance
- Two-phase inline current sensing with 1MHz bandwidth
- RS485 interface for commutation encoder
- Hall sensor/GPIO pins (48V bus fault protected)
- External thermistor for motor overtemp protection
- CAN for control and telemetry
- Half-credit-card form factor
- XT60 for power and MR60 for phase connections

<br/>
<br/>
<br/>

### More Information Coming Soon!