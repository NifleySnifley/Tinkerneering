---
layout: post
title:  "Rocket Tracker Part 7: Base Station Improvements & Fixes"
date:   2023-09-08 18:09:00 -0500
categories: blog
project: rtrk
---

Between last post and now, I've been testing the tracker in various different ways, walking around, etc. and smoothing out some wrinkles and bugs in the software and the communication between the tracker and the basestation software.

## Some Issues

With this basic setup, I could see the location of the tracker as I walked, great! Well, sort-of, occasionally the track would display seemingly random spikes, varying in amplitude, sometimes even to invalid GPS coordinates (like 450 degrees...), something must be seriously wrong. Unfortunately for me, the GPS data flows through no less than ***8*** different "pathways" (conversions) to get all the way to the user:

- GPS UART
- NMEA sequence parsing
- Protobuf serialization, 
- Tracker radio
- Receiver radio
- Intermediary format
- Protobuf deserialization
- Map display

There are so many things that could go wrong in this system! Fortunately I've developed tested many of the components independently so I could preemptively take protobuf serialization, deserialization, map display and the intermediary format off of the list. Hmm... I checked the UART signals and there didn't seem to be any obvious corruption or noise. Well, that left the source of the error down to the NMEA parser ([LWGPS](https://github.com/MaJerle/lwgps)) or something in the radio communications. Well, I tested the GPS parser overnight without any errors or missed NMEA sequences, so I assumed that it must be something in the radio communications. It made sense because the spikes only seemed to happen when the tracker was either far away, or in a self-propelled faraday cage (car). But that shouldn't be a problem... the LoRa module already does CRC checking (and it's enabled in the driver I wrote), so shouldn't that catch spurious messages and corrupt data? *Apparently not*. 

## Fixes!

The simplest and most effective solution I could think of was to simply add another (16-bit) CRC to the LoRa packets being sent, and ignore packets with invalid CRCs when received. After doing [a bit of reading about CRCs](http://www.sunshine2k.de/articles/coding/crc/understanding_crc.html) I implemented a table-based 16-bit CRC and added it into the "frame manager" structure that is in charge of serializing and deserializing packet data on both the receiver and tracker/transmitter. Better yet, it works! I'm still not entirely sure why the LoRa error checking doesn't catch some errant messages, but at least it was a pretty easy problem to solve.

## More Sensors

The tracker was tracking, but thats not all it can do! Even though the order of of the I2C signals on the connector on the PCB was inverted (stupid me), I managed to solder the connector on backwards in a way that spanned two different connector footprints and had the correct pinout. Since I had a way of attaching I2C peripherals to the board, I could attach any of a plethora of different sensors to the board, but I had one in particular that I planned on testing: a barometer, for altimetry. Although I plan to use the BMP390 pressure sensor in future revisions of the PCB, I had a LPS25 breakout board from Adafruit handy so I used it instead. After making sure the I2C communication was working well, I wrote a simple driver for the LPS25 and tada: pressure data! After a little bit, I had the averaged pressure readings converted to altitude thanks to the BMP390's datasheet, and it was time to send the data over the air! Luckily I had already created a message type for altitude data that was just waiting to be implemented, so sending the additional altitude data over the LoRa radio in addition to the GPS data was super easy.

## Graphs and More!

Pressure data was now flowing in to the user-end software, but I wasn't doing anything with it yet... time to change that! I had been planning on graphing this altitude data for the user to see, and lucky for me, the Matplotlib package conveniently has a Qt backend that makes it quite easy to add into an existing Qt app. Unfortunately updating the live plot with data seems to take a bit longer than I would like, but it's OK for now, I'll find a solution later... Having a working live plot is great, but one thing that I thought I could improve would be to increase the update rate of the barometer info. During a rocket launch, measuring altitude information once per second isn't really enough to get a full picture of what's going on. Improving the update rate of the telemetry information required some more significant structural changes to the receiver firmware. My solution in the end was to send LoRa messages as fast as possible (with 50ms in between messages so as not to overwhelm the receiver), and only send the (longer) GPS information when the GPS updates. This allows pressure data to be transmitted with an update rate of approximately 14hz, while the GPS data is updated at 1hz (the update rate of the GPS itself), conserving bandwidth.

The one last feature that I needed before I would be ready to send this thing up on a rocket was logging, what good would all of this data be if I couldn't analyze it! I chose to log each "datum" (a single piece of information, altitude, GPS data, etc.) as a JSON object (by using python-protobuf's `MessageToJson`) in a logfile along with a timestamp relative to the start of the logging session in the user-software. This way, the log data is both human readable, and trivially parsed by most any programming language which will make it easy for future users of this tracking system to do their own analysis.

After a little bit more testing I worked out a few more bugs and it was ready to go! Thanks for reading and I'm looking forward to flight-testing this thing for the first time in my next blog post!