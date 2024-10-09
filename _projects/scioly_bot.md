---
layout: project
projid: scioly_bot
title:  "Science Olympiad Robot Tour"
date:   2024-03-2 00:00:00 -0500
categories: project
description: This is the robot I built and programmed for my high school's Science Olympiad team to compete in the Robot Tour event. We won second place in the state using this robot.
image: sciolybot/robotbackside.jpg
links:
 - "[2024 Robot Tour Code (Github)](https://github.com/NifleySnifley/SciOly2023)"
 - "[Robot CAD (OnShape)](https://cad.onshape.com/documents/bbe5a32963d41ceffe6e68f4/w/005e6fb0a999a6c69223d441/e/f9fa478bb65171ffda30b501)"
---

I was build captain on my high school's Science Olympiad team for the 2024 season. One of the events that I took lead on was [Robot Tour](https://www.soinc.org/robot-tour-c). Unfortunately the science olympiad season overlaps with robotics, so I didn't get to spend as much time perfecting this robot as I wanted too - it could certainly have been better in many ways, but oh well.

The robot consists of two [micro metal gearmotors](https://www.pololu.com/category/60/micro-metal-gearmotors) with encoders (used for odometry) attached to a CNC-machined polycarbonate chassis plate. A [Raspberry Pi Pico](https://www.raspberrypi.com/products/raspberry-pi-pico/) is used to control the robot which is powered with 4 AAA batteries. I originally planned to use the two [VL6180X](https://www.dfrobot.com/product-2287.html) distance sensors mounted on the front of the robot for odometry correction using the obstacles in the maze, but due to time constraints, I never got around to doing this. 

<br/>
{% include image.html file="sciolybot/robotcad.png" astyle="width:65%" caption="Robot CAD" %}


On the software side, the robot takes a text-based representation of the maze as input, finds the most efficient path around tha maze, and then generates a smooth B-Spline path to drive. Using the wheel encoders, the robot keeps track of it's translation and rotation relative to it's starting point. Using this information, the robot follows the B-Spline path using an optimized pure pursuit controller and feedforward control for the wheel motors. I created a rudimentary but functional simulator for debugging the robot's control algorithms using [raylib](https://www.raylib.com/) which greatly sped up the development process.

<br/>
{% include image.html file="sciolybot/simulator.png" astyle="width:65%" caption="Robot simulator simulating a maze solution" %}

Here's a video of the robot in action!

<iframe width="100%" height="512" src="https://www.youtube.com/embed/l-RjTHcnKug" title="2024 Science Olympiad Robot Tour" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
<br/>

Aaand... some more photos!

{% include image.html file="sciolybot/robotfull.jpg" astyle="width:65%" caption="Fully assembled robot" %}
{% include image.html file="sciolybot/robotside.jpg" astyle="width:65%" caption="Side view" %}
{% include image.html file="sciolybot/robotbackside.jpg" astyle="width:65%" caption="Back & electronics" %}
{% include image.html file="sciolybot/robotbottom.jpg" astyle="width:65%" caption="Bottom" %}
