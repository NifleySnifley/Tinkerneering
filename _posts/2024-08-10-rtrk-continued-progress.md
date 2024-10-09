---
layout: post
title:  "Rocket Tracker Part 11: Tracker Improvements & Progress"
date:   2024-08-10 12:09:00 -0500
categories: blog
project: rtrk
---

Since the last post, I've been working on many improvements and features for the tracker's firmware and support software. I was also able to fly the tracker on a few test flights at last month's Tripoli launch, but I'll talk about that in another post.

### New Features:

- Sensor calibration
- Onboard sensor fusion & filtering
- More versatile logging
- GPS improvements
- Configuration System

### Other Things:

- The start of a GUI interface?
- Dual-Deploy++ expansion board (WIP)

<br/>

## Configuration System

The configuration system was the first major addition to the tracker firmware after my initial testing, not because it was a feature I thought was really important, but because it's a prerequisite for some other functionalities (calibration). I wanted to make a framework for storing and accessing calibration values that would make it easy to use as a user, and also easy for me to use as the firmware/software developer. Thanks to ESP-IDF's convenient non-volatile storage (`nvs`) API, actually setting and getting values of different types (integers, strings, etc.) would be pretty easy, but that's only half the battle. The majority of the work I put into the configuration system was aimed towards making something that would be really easy for me to use as a developer. 

### Configuration Schema

The most important part of the configuration system I developed is the configuration schema. The configuration schema consists of a JSON file that describes the names, types, and other metadata pertaining to each settable configuration parameter. Using JSON, the configuration schema is structured hierarchically, which lends itself to easily being displayed in a GUI (I made a lot of considerations for how a configuration GUI would look when making this schema). Here's a little snippet of the configuration schema:

```json5
"freq_hz": {
    "!type": "int(903000000,927000000)",
    "!default": 914000000,
    "!name": "Frequency",
    "!suffix": "Hz",
    "!description": "Frequency of the LoRa radio. Valid frequencies are between 903 and 927 MHz (the ISM band)"
}
```

As you can see in this snippet, the schema also can (optionally) be used to store the description of a configuration, and has provisions for value validation (min/max bounds checking for integers&floats, length constraints for strings, etc.). Additionally, enum types can be defined and used in the schema. I made a python script that translates the schema into a flat data structure containing the types and metadata of each value (value "paths" are derived from the value's position in the hierarchical schema, much like filesystem paths). This translated representation of the configuration schema can be used directly (in the CLI tool for parsing and bounds-checking configuration values) and also for code generation.

### Codegen

To make the configuration schema easy to use from the C-based firmware of the tracker, I made another python script that generates C code from the configuration schema. Additionally, this tool hashes the names of every configuration value to produce a "key" that can be used to set/get the configuration value in `nvs`. I originally planned on just using the names of configuration values as `nvs` keys, but I found out that NVS only supports 16-character-long keys, so hashing was unfortunately neccesary. The generated C code, in addition to containing hashed keys, also contains a  list of the types, non-hashed names, and default values of every configuration value. This allows for another layer of type & name validation when setting configuration values, and also makes it really easy to dump all of the configuration values stored on the tracker. In addition to this, C enums and typedefs are generated for all custom enum types in the schema.

### Configuration Interfacing

Another neat feature of having default values built in to the firmware is that to store a default value, nothing needs to be stored in `nvs` at all! All configuration parameters not present in `nvs` are treated as default values, which also makes resetting the configuration as easy as erasing all stored values. I created a bunch of helper functions for setting/getting configuration values of all supported types (bool, int, string, float, enum) in the firmware, and made sure it was easy to access configuration values from anywhere in the firmware. I also implemented a new set of commands for setting, getting, and listing all current configuration values over the communication protocol and added functionality for this in the CLI tool.

<br/>

## Calibration

Now that the configuration system working, time to use it for calibration! All calibration parameters are stored using the same configuration system as everything else, which means they can be easily set, stored and accessed. On the tracker, there are three different types of sensors that need calibration:

- Magnetometer (hard and soft-iron calibration)

- Gyro (null offset calibration)

- Accelerometer (2-point calibration)

The information neccesary to apply each of these calibrations (scales and offsets) are all stored using the configuration schema. Actually applying the calibration is the easiest part.

### Calibration Interfacing

To calibrate these different sensors, I needed to be able to get a stream of raw sensor data from all of the sensors to the CLI tool. To accomplish this, I added a set of commands that can be used to request sensor data to be sent using the protocol (USB only) at a specific frequency, up to 256Hz (the rate at which the sensors are read from).

### Magnetometer Calibration

To calibrate a magnetometer, data needs to be collected from the magnetometer in many different orientations, then sphere fitting (or rough min-max fitting) can be applied that produces a uniform-length magnetic field vector from every measurement. I added an interactive tool (using `ncurses`) that collects data while the user rotates the tracker board to collect measurements in a bunch of different orientations, once data has been collected, the calibration parameters are calculated and can then be written to the tracker's configuration.

### Gyro Calibration

Gyro calibration is really simple, the CLI tool just collects daa, takes the average of each axis of the gyro to find the offsets, then writes the inverse of that offset value to the tracker's configuration

### Accelerometer calibration

Even though this is the most complicated calibration procedure, it's still pretty simple. I made a `ncurses`-based interactive tool that prompts the user to set the device in 3 different orientations (one per axis) and collects data for 1 second in each orientation, this data is then averaged to find the 0g and +1g point of each axis, which is used to calculate the scale and offset for two-point calibration. 

<br/>

## Sensor Fusion & Filtering

### AHRS

After getting all of the sensors calibrated, I continued with my plan of having real-time sensor fusion for altitude and orientation. For orientation, I used the amazing `Fusion` library that provides a simple-to-use Madgewick AHRS filter (the library is created by a company founded by Madgewick himself!). The filter is so easy to use that I spent most of the time working on getting all of the axes of the magnetometer and two accelerometers aligned, rather than on the filter itself. After some fiddling with different orientation conventions, the filter seemed to produce accurate orientation quaternions. I made a quick visualization tool using `vpython` and added it to the CLI to visualize the orientation of the device to confirm that the filter was working properly.

### Altitude Filtering

Another really nice feature of the `Fusion` library's `FusionAHRS` is that it conveniently can output acceleration values in world-space (North-East-Up convention) with gravity removed. Earlier, when I was doing some testing with a development board, I made a Kalman filter that uses world Z-axis acceleration and barometric altitude from the pressure sensor to produce filtered altimetry information. Using Espressif's ESP-IDF Eigen port, I adapted a Kalman filter implementation I found on github to be used for the altitude filter on the tracker. The altimetry filter is a pretty straightforward 2-state filter that's basically just a double-integrator (acceleration->velocity->position). To create the Q and R matrices for the filter, I used the standard deviations of data collected from the board sitting still on the table. I also added a function to the CLI that makes it easy to find these values and "calibrate" the altimetry filter. The altimetry filter has OK performance as-is, but I hope to improve it in the future with some filtering of the pressure sensor data, and better Q and R matrices.

## Logging Improvements

I've just made a couple of minor changes to the logging infrastructure. Mainly, instead of log frames comprised of only a timestamp and fixed-format sensor data, in this redesign, timestamp, a 16-bit datatype field, and then variable-length data are stored in each log frame. Not adding a datatype field to the logging frames was an oversight, but now having datatype fields, multiple different types of data can be logged. Using this data type field, now events and other information can be logged in addition to the standard sensor/flight data frames.

## GPS Improvements

Until now, I have been using GPS data from it's default 9600-baud NMEA output at 1Hz. One of the major selling points that convinced me to use this specific GPS was that it was purported to support 10Hz output. Since this GPS is a U-Blox M8 GPS, it also supports input and output with U-Blox's proprietary UBX protocol. U-Blox nicely provides a convenient library that support all of the functionality of their GNSS, Cellular and Bluetooth modules called `ubxlib`. `ubxlib` supports ESP-IDF natively, but when I got it integrated into the firmware, it caused conflicts with I2C because it uses a old (but still supported) I2C driver that conflicts with the modern ESP-IDF I2C driver. I managed to fix this in a sort-of hacky way by forking `ubxlib` and manually removing I2C support from the ESP-IDF port. With `ubxlib` working and using U-Blox's `u-center` tool, I was able to add functionality to change the GPS's update rate using the configuration system. During this testing, I inadvertently discovered that the LoRa connection allows telemetry up to 4Hz! How great!

# TODO: GUI and DD notes...

Well, that's it for this update! I'll make another post about the flight-tests later!
