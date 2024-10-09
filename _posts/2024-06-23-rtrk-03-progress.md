---
layout: post
title:  "Rocket Tracker Part 9.5: v0.3 PCB Progress Update"
date:   2024-06-23 12:09:00 -0500
categories: blog
project: rtrk
---

For the past week I've been on vacation with my family, but that doesn't mean I haven't been making any progress on my projects! In the time not spent biking, hiking, and traveling, I've been putting together the third revision of the tracker PCB that I mentioned in my last blog post.

### Changes

A few things about the design have changed since my last post, including the sensor suite and power system:

- No more `BNO085`! For both cost savings, and avoiding potential SPI issues, I've switched from the `BNO085` to the `LIS3MDL` 3-axis magnetometer and `LSM6DSM` 6-axis Accelerometer + Gyro.
- Decided on using the `LPS22` barometer
- Added a `MAX17048G` battery guage IC

### More details

In addition to making a few component changes, the design of the v0.3 tracker has a few notable differences from the previous version. First of all, instead of having 3 Qwiic I2C expansions, the v0.3 tracker has just one I2C expansion port but also a 6-pin GPIO expansion port that could be used for pyro channels, PWM output, etc. The v0.3 version will also be using a 4-layer PCB, I've found that it makes routing power to all of the components **much** easier and allows for tighter component placement. This version will also have a (de-facto standard) JST-PH connector for the LiPo battery and the same USB-C port that I used in my receiver PCB. Since the ESP32 can be programmed through it's built-in USB interface, I got rid of the programming and JTAG headers and added a basic programming header with BOOTSEL and reset pins. 

### Plans

The first rocket launch of the year is on July 13, I'm hoping to have the board functional at that time to get some launch data from the sensors recorded so I can prototype sensor fusion algorithms and other functionality of the tracking system. Ideally, I'll order the board as soon as I can which would be on the first of July, but that's cutting it close because getting the boards manufactured and shipped from china can take up to 8 days.

Thanks for reading!