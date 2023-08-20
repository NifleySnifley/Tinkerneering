---
layout: post
title:  "Rocket Tracker Part 2: Receiver Architecture"
date:   2023-06-19 12:09:00 -0500
categories: blog
project: rtrk
---
(Don't be confused that I'm considering this post part two, I consider my initial designs and ideas last summer to be part 1 and I will write up a retrospective blog post about that sometime)

The last few days I've been working on designing a new version of the receiver for my tracking device for high-powered amateur rocketry. 

### Initial Designs

Last year during my initial brainstorming, development, and design of the rocket tracker my idea was to have a Raspberry Pi with a special HAT act as the receiver for the telemetry data from the rocket. As I started to develop and think about this idea more, I realized that maybe using a relatively expensive SBC to act as the receiver wasn't the best option and that led me to also rethink the architecture of the software between the user and the data coming in from the tracking device on the rocket. My original idea with the Raspberry Pi was to run a piece of "backend" software on the raspberry pi that would consist of a number of modules for managing the incoming telemetry data, downloading logs, and serving up a web-based user interface. The backend would process the incoming data and then pass it over a websocket to the frontend webapp. A diagram of the software and hardware architecture follows:

{% include image.html file="rocketracker/old_rx_sw.png" astyle="width:85%" caption="Software architecture" %}
{% include image.html file="rocketracker/old_rx_hw.png" astyle="width:85%" caption="Basic hardware block diagram" %}

<!-- TODO: Add image enlarge-on-click modal -->

Having a web-based UI makes supporting the end user experience consistently across different platforms easy, but the neccesary IPC between the backend server, the web UI, and the rocket tracker itself is a whole other level of (possibly) avoidable complexity on the software side of things. Using a Raspberry Pi as the backend server is also expensive, complex, and not very portable for a rocket tracker that's usually used while searching for a rocket in a field or (hopefully not) in the woods.

### A New Architecture

Seeking to reduce the cost and complexity of the software and hardware setup on the receiving end of the tracking setup, I devised a new and improved architecture for streamlining usage and software development for the receiver. A simple solution would be to interface the radio directly with a computer, but from my preliminary research and ideas of doing so, likely using something the likes of a FTDI USB-to-SPI inteface IC, it seems like it would be difficult to support across platforms and also add the possibility of missing messages from the tracker due to the non-realtime nature of userspace IO on personal computers. Another idea I came up with was to build a much simplified version of the previous "base station" that would incorporate a microcontroller-based USB device and the radio receiver. By doing this, the price of the  backend is greatly reduced and it also opens up another possibility - using the backend as a self-contained rocket-finding device! Instead of taking your phone along with a bulky gateway-like wifi-based base station, you can just unplug the receiver from your computer where you would have been looking at the realtime telemetry information coming back from the rocket, and use it to locate your rocket using a simple, minimal user interface. And better yet, I get to design another PCB and embedded device! Here's a simplified diagram of this new architecture from the software and hardware point of view:

{% include image.html file="rocketracker/new_rx_arch.png" astyle="width:85%" caption="New, in-development software/hardware architecture" %}

Thanks for reading! In the next post, I'll go over how I've started to design this new receiver! 
