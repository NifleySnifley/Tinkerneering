---
layout: project
projid: bldc_v2
title:  "BLDC Motor Controller V2"
date:   2025-11-1 00:00:00 -0500
wip: true
categories: project
description: A second BLDC motor controller design aiming to fix some of the issues with my last design with more conservative specs and a more thorough design process. Using a similar [DRV8320](https://www.ti.com/lit/ds/symlink/drv8320.pdf?ts=1766885080688&ref_url=https%253A%252F%252Fwww.ti.com%252Fproduct%252FDRV8320), [NTTFSSCH1D3N04XL](https://www.mouser.com/datasheet/3/101/1/NTTFSSCH1D3N04XL-D.PDF) FETs, [INA241](https://www.ti.com/lit/ds/symlink/ina241a.pdf) for inline current sensing, and a [STM32G474](https://www.st.com/resource/en/datasheet/stm32g474cb.pdf) MCU. Aiming for operation at up to 24V 30A.
image: bldc_v2/render_transparent.png
links:
 - "[OnShape Document](https://cad.onshape.com/documents/66454a2c76b67f165972157e/w/2ecf8158066ea2686bd52c27/e/387c4969608941a8ec5404ff?renderMode=0&uiState=6950870ab189a2b25f07a95e)"
---

### Specifications & Design Targets:
- Up to 24V operation
- 30A continuous current at stall, 50A+ peak phase current (transiently)
- Three-phase inline current sensing
- Phase voltage sensing for sensorless commutation
- On board encoder ([MA702](https://www.monolithicpower.com/en/ma702.html)) to enable sensored FOC operation without any external components
- RS485 interface for sensor communication (capable of SSI over RS485 for external absolute encoder)
- CAN and serial interfaces for control
- 5V tolerant GPIO for interfacing with hall effect sensors
- Convenient form factor for mounting into a compact BLDC actuator design
- FETs located specifically for ease of cooling
- XT60 for power and MR60 for phase connections
- Specifically tuned for low ripple at a switching frequency of 24kHz

### Development
- [Rough switching calculations](https://www.desmos.com/calculator/n7nzazmwdy)
- [Bulk capacitance/ripple calculations](https://www.desmos.com/calculator/aimarnhdmt)

### Gallery

{% include image.html file="bldc_v2/pcb_cad.png" astyle="width:65%" caption="PCB CAD Mmdel" %}

{% include image.html file="bldc_v2/trace_internals.png" astyle="width:65%" caption="PCB internal routing (planes hidden)" %}

{% include image.html file="bldc_v2/heat_spreader.png" astyle="width:65%" caption="PCB mounted to aluminum heat spreader (CAD)" %}

{% include image.html file="bldc_v2/layout_v1.png" astyle="width:65%" caption="Version 1 of power stage routing for a single phase - current iteration is version 5 :)" %}