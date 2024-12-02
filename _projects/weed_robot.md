---
layout: project
title:  "Weed Spraying Rover"
projid: wrbt
date:   2024-06-12 00:00:00 -0500
wip: false
categories: project
description: An off-road capable mobile robot with accessories for weedwacking and dispensing liquid weed killer controlled with ROS2.
image: weedrover/squirt.jpg
links:
 - "[Software GitHub Repo](https://github.com/NifleySnifley/Rover2024)"
 - "[Arm/Accessory Controller Firmware GitHub](https://github.com/NifleySnifley/PicoRobotArm)"
---

## Specifications

### Robot:

- 4 AndyMark PG71 gearmotors for propulsion (top speed of about 0.3m/s)
- 4 Brute® 7103500YP 8" x 2" Lawn Mower Drive Wheels for off-road traction and horrible squealing noises when turning on pavement...
- 20mm Aluminum extrusion frame
- Raspberry Pi 5 for robot control with ROS2 Iron Irwini.
- Dual Jaguar (MDL-BDC24) motor controllers with a custom ROS2 driver using a usb to RS232 adapter
- 4 onboard cameras with a Raspberry Pi 5 for video streaming.
- Dedicated Raspberry Pi Pico for arm, weedwacker, and accessory control. (interfaced over USB)

### Sprayer:

- 4-DOF robotic arm with 60Kg/cm servos and stepper driven turntable
- Raspberry Pi Pico based arm & accesory controller
- Nozzle, pump, and hose repurposed from a broken battery powered weed spraying wand
- 3D inverse kinematics for precise and intuitive positioning
- Microsoft LifeCam mounted on the end of the arm for sprayer targeting

### Weed Wacker:

- Weed wacker mounted on a 40cm folding arm
- Winch deployment
- Direct drive CIM motor for weedwacking with a [RYOBI 2-in-1 bladed head](https://www.amazon.com/RYOBI-Fixed-Line-Bladed-AC052N1/dp/B087Z99HHR) on a 3D printed adapter for cutting
- Capable of cutting weeds, grass, small shrubs (and if you aren't careful, your ankles).

## Photo Gallery

<br/>

{% include image.html file="weedrover/electronicsproto.jpg" astyle="width:75%" caption="Prototype control system mockup with different motors" %}

{% include image.html file="weedrover/drivetrain.jpg" astyle="width:75%" caption="Drivetrain before accessories were installed" %}

{% include image.html file="weedrover/oldarm.jpg" astyle="width:75%" caption="3DOF arm originally designed for Triangle Bot, before being repurposed for weed spraying" %}

{% include image.html file="weedrover/wheelgears.jpg" astyle="width:75%" caption="PG71 motor with 3D printed gear to interface with the wheels" %}

{% include image.html file="weedrover/armbasic.jpg" astyle="width:75%" caption="Basic arm & turntable mounted" %}

{% include image.html file="weedrover/front_electronics.jpg" astyle="width:75%" caption="Front electronics closeup" %}

{% include image.html file="weedrover/electronics.jpg" astyle="width:75%" caption="Rear electronics closeup" %}

{% include image.html file="weedrover/v1_driving.jpg" astyle="width:75%" caption="First version of operational rover driving around" %}

{% include image.html file="weedrover/v1_spraying.jpg" astyle="width:75%" caption="Initial spraying test" %}

{% include image.html file="weedrover/v2_arm.jpg" astyle="width:75%" caption="Upgraded arm with camera" %}

{% include image.html file="weedrover/weeding.jpg" astyle="width:75%" caption="Camera mast" %}

{% include image.html file="weedrover/pov_camera.jpg" astyle="width:75%" caption="View from the drive camera" %}

{% include image.html file="weedrover/teleop_view_v1.jpg" astyle="width:75%" caption="Views from all of the cameras on the teleoperation computer" %}

{% include image.html file="weedrover/whacker_deployed.jpg" astyle="width:75%" caption="Weedwacker attachment deployed" %}

{% include image.html file="weedrover/whacker_retracted.jpg" astyle="width:75%" caption="Weedwacker attachment retracted" %}

{% include image.html file="weedrover/deployed.jpg" astyle="width:75%" caption="Completed V2 robot with all accessories deployed" %}
