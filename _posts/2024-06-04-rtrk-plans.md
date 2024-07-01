---
layout: post
title:  "Rocket Tracker Part 9: Plans for the Summer"
date:   2024-06-04 12:09:00 -0500
categories: blog
project: rtrk
---
Now that school and robotics is over, I’m starting to start working on some of my projects again! The one project that I really want to get done this summer is my rocket tracker, and I’ve started putting together a design for a new hardware revision of the tracker as well as rethinking the system architecture and software components of the tracker.

## Hardware Redesign
For this new revision of the tracker I’ve decided to focus less on cost-savings and more on using higher quality sensors and hardware. Pretty much every component has been either replaced or upgraded from the last version including:

- New [ESP32-S3](https://www.digikey.com/en/products/detail/espressif-systems/ESP32-S3-WROOM-1U-N16/16162649) (USB!)
- [BNO085](https://www.digikey.com/en/products/detail/ceva-technologies-inc/BNO085/9445940) 9-Axis IMU (built-in sensor fusion)
- [TPS63031](https://www.digikey.com/en/products/detail/texas-instruments/TPS63031DSKR/2048021) Buck converter (the same buck that I used for the receiver)
- [ADXL375BCCZ](https://www.digikey.com/en/products/detail/analog-devices-inc/ADXL375BCCZ/4376342) 200g accelerometer (hoping to capture engine performance data from super fast launches)
- [CAM-M8C](https://www.digikey.com/en/products/detail/u-blox/CAM-M8C-0/6150647) GPS Module (smaller, omnidirectional antenna)
  
In addition to these new components, another important change is moving the sensors from I2C (400kHz) to SPI (~8Mhz). This 20-fold increase in speed will hopefully allow faster sensor data acquisition for improved log resolution and better sensor fusion. For the power system, I’ve also added a [BQ24073](https://www.digikey.com/en/products/detail/texas-instruments/BQ24073RGTR/2047265) 1S LiPo charger IC (one of the cool TI ones with power passthrough) that will charge the tracker’s battery (I’m planning for about 1500mAh given a rough estimate of the current consumption of the components)

## Tracker Firmware
In addition to upgraded hardware for the tracker, I’m planning on making some major improvements to the firmware and adding a bunch of much-needed features. One issue with the tracker that I had last year was noisy altimetry data, which was derived from the raw output of the pressure sensor I was using (LPS25). I recently prototyped using a Kalman filter to combine noisy pressure sensor readings with data from the tracker’s accelerometer to get smoother, and more accurate altitude measurements at a higher rate. One of the crucial features that was missing from the tracker firmware last year was logging, this version of the tracker will have a dedicated memory chip for logging. In addition to more log storage, the ESP32-S3 has USB hardware which I plan on using for log downloading to a computer either with a custom protocol or with the tracker appearing as a USB storage device. 

## Receiver Software
The receiver “base station” software I wrote for last year’s iteration of the tracker was pretty “sketchy” by my standards - a fairly crude `pyqt` GUI that I put together in a short period of time for the first launch of the tracker. One of the lower priority but still important things that I plan to do is to upgrade this software to a more feature-complete, well-written, and nicer looking GUI (Ideally using C#, but I’m not sure exactly how I’ll get offline maps working - that’s the major complexity of the software)

I’m excited to get back to working on this project! I’ll be away for most of June, but my goal is to get the board designed, ordered, and assembled by the middle of July. Thanks for reading!
