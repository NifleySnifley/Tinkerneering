---
layout: project
title:  "Rocket Tracker"
projid: rtrk
date:   2023-08-8 00:00:00 -0500
wip: true
categories: project
description: A custom GPS tracking and telemetry device for use in high powered amateur rocketry using an ESP32 module and LoRa radio.
image: rocketracker/trackerv01.jpg
links:
 - "[Hw & Sw Github](https://github.com/NifleySnifley/RocketTracker)"
redirect_from:
  - /rockettracker
sysname: "PLACEHOLDER"
---

### The Rocket Tracker

Over the last few years, me and my dad have gotten more and more involved in the world of amateur high-power rocketry through our local branch of the Tripoli rocketry club. As we started working on bigger and more powerful rockets, we ended up having the same problem that so many others in the rocketry community have came across as well: when my rocket lands in a corn field, how do I find it? The most common solution is to equip the rocket with a long-range radio tracking device, and this can come in the form of small radio direction finding (RDF) beacons for falconry to GPS-based tracking devices that sometime require HAM licensing. I thought it would be a fun challenge to design my own tracking device to launch in our rockets, so here we are! It has certainly been an adventure designing my own tracking system and I've learned so much about PCB design, electronics, and RF along the way.

### Concept

The rocket tracking system consists of two components, the actual tracker that goes into the rocket, a nd a "receiver" or base station that stays on the ground and receives information from the tracker in the rocket. Originally I had planned to make the receiver a self-contained device using a Raspberry Pi with a screen, but after going down that path a bit I realized that it was unnecessarily complex and a Raspberry Pi was expensive and overpowered. Going forward, I plan on using a rp2040 microprocessor to create a base station "dongle" with its USB capability. For the actual tracker, my idea from the start was to use an ESP32 because of its bluetooth capabilities and powerful processor. The tracker would also include a GPS, magnetometer, gyro, barometer, and high-g accelerometer for gathering flight info and keeping track of the rocket. Aside from this, the most important component of the tracking system is the radio system that allows the tracker to send data back to the base station, for this I chose to use a HopeRF RFM97CW LoRa module because of it's high power and relatively low price.

<!-- 
## The PLACEHOLDER Tracking System
The PLACEHOLDER tracking system consists of two main components, the RECEIVER, and the tracker. Both the RECEIVER and the tracker are equipped with 915MHz (ISM band) HopeRF radio transceivers that allow live sending of telemetry information from the tracker to the RECEIVER. The data received from the tracker contains information on your rocket's position, altitude, orientation, and other information gathered from the onboard GPS and suite of sensors. The RECEIVER, when paired with the host software on a laptop or other portable computer provides a graphical interface displaying telemetry information.

## The Tracker
The tracker is the primary component of the tracking system, after all it is, of course, the thing you put in your rocket! The tracker can be powered by a variety of batteries (3.3 to 12 volts) and fits inside a standard 29mm body tube. The tracker contains a number of sensors (accelerometer, magnetometer, gyroscope, and barometer) for measuring the rocket's altitude, speed, and orientation in realtime during the flight. Last but not least, the most important components of the tracker are the GPS and radio module that tracks the location of your rocket and sends live telemetry information back to you on the ground over the air. The tracker also includes flash memory that stores information logged throughout the duration of your rocket's flight, these logs can be downloaded over bluetooth from the tracker.

## The RECEIVER
The RECEIVER is the only other essential component of the tracking system. The RECEIVER can send and receive data to and from the tracker. As a USB dongle it can be used with dedicated software to show live telemetry information from your tracker, but it can also be used without additional software, emulating a standard serial-port GPS. As a emulated GPS, applications such as MapSphere or google maps can be used to show and record your rocket's position received using the RECEIVER dongle.


TODO:
- Decide on names and logos!
- Write dedicated pages about the tracker and RECEIVER with more technical information and documentation
- Add images, gallery maybe? -->