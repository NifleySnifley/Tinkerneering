For this project, from the start I had planned on using a Beaglebone Blue SBC to serve as the brain of the robot, but as I dug deeper into the intricacies of how I would program this board, I came across numerous difficulties that arose from using this board.

### The initial idea:

My initial idea was to program the robot using completely custom software written for (and on) the beaglebone running it's default Debian-based OS. I got pretty far into this and by the time I realized that it might not be the best idea, I had already partially written a library to handle communication between robot and driver station, (very basic) custom driver station software, and had planned out how to do multi-component IPC and a HAL for the beaglebone. During the mechanical design and construction of the robot, I took a break from developing this software and started to realize how unsustainable this ecosystem and workflow was. The major pitfalls of this approach were focused on the development workflow, which involved remote development and compilation on the (not very powerful) beaglebone which was a cumbersome and time consuming process: just compiling the C++ software on the beaglebone took about a minute, which made it very difficult to test things and start making meaningful progress on fiddly components like the HAL. 

### Brainstorming a new approach

In my time not spend working on the mechanical aspects of the robot (which are detailed in my previous post) I researched alternative frameworks, ecosystems, and workflows that would hopefully make my life easier in the future. After spending some time looking, I came up with a short list of frameworks that I would investigate further:

- [ROS2](https://www.ros.org/) (Robot Operating System)

- YARP (Yet Another Robot Platform)

- A custom-built system using a prebuilt communication system like [ZeroMQ](https://zeromq.org/) and problably using a serialization system like [protobufs](https://protobuf.dev/).

Looking over this selection, my primary concern is portability and the ease/ability to cross compile and deploy programs using a given framework. Secondarily, I obviously would prefer a mature and fully-featured library that has a reasonable community. 

For the second criteria, ROS would be my obvious choice since is a massive and mature ecosystem with a huge userbase. Unfortunately, after extensive research, ROS doesn't really seem to fulfill my first criterion: ROS is a massive project with *many* dependencies that seems (at lest to me) to be a ordeal to cross-compile and it's Yocto support, `meta-ros` is outdated and no longer maintained.

Building a custom system using a messaging framework (gRPC, ZeroMQ, etc.) would fulfill my first criterion because in my case, it would be designed and tailored to meet these constraints. On another note, building a custom library would just be another hurdle to get over because I would need to custom-build everything neccesary.

Lastly, YARP. YARP is a relatively lightweight (compared to ROS) robotics middleware, with a similar set of features to ROS at a basic level (pseudo-port based IPC, interface description language, etc.) and is even compatible with ROS. The major selling point for me is that YARP is quite easy to cross compile, it's almost entirely self-contained (it's single dependency, `libace-dev` is also CMake based and easily cross compiled). Although YARP doesn't have as large of a userbase as ROS, YARP is quite mature (20+ years old now!) and has been used in a few notable robots such as [iCub](https://icub.iit.it/) (which it was developed for!) 

### System Setup:

**THIS IS CURRENTLY WIP**







# OLD :point_down:

### A new idea:

After this “failed” approach, I needed to find another solution that would be continually workable, and allow for meaningful software development on the (space and processing constrained) beaglebone. I had been looking at using ROS (specifically ROS2) for a while, but last year I eventually gave up when trying to get it up and running on a beaglebone after trying many different ways of installing it to no avail. According to the ROS docs, the ARM architecture of the Beaglebone is not officially supported by ROS, which means that there aren't any binary releases via a package manager. Additionally, the beaglebone is too space and speed constrained to build ROS from source. I was too lazy to try and compile ros for armhf on another computer using a cross-compilation toolchain (crosstool-ng), so I just gave up. By that point I had lost 90% of my motivation to learn ROS, and I didn’t have any other ROS-supported hardware that I could practically use on a robot (I have Raspberry Pis, but they aren’t officially supported either, and RPIs aren’t cool). When looking for how to possibly get ROS working on a beaglebone again I came across the Yocto project, a tool designed to build custom embedded linux distributions and the accompanying SDKs. In addition to providing a cross-development SDK (which would allow more efficient development and deployment of my initial software), ROS provides a Yocto/OpenEmbedded “layer” called meta-ros that is supposed to allow ROS to be added into a Yocto build. This looked pretty promising, but the first step was to get Yocto to build an image for the Beaglebone.

### A rough start with Yocto

As I got started with using Yocto for the first time

**
