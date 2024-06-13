---
layout: post
project: robotics
title:  "Adapting a StreamDeck for use in FRC"
---

<!-- During the past couple of weeks, I've been working with my robotics team to build an offseason swerve-drive robot. It has been really fun to finally be able to tap into the potential of a swerve drive base, especially the precision and ease of driving autonomously. After tuning and programming autonomous routines for the robot, we started working on adding more automation into the teleop period (auto scoring, automatically driving to the substation, etc). In doing this we realized how handy it would be to have a way to select which grid node we want to score - I've seen this done in a few different ways at competitions, mostly wood/polycarbonate panels with arcade buttons for each node. 

TODO: 
 - How I got the idea
 - How the bigger concept developed
 - Development process and current state
 - Future features, etc. -->

## Preface

For the last couple of weeks, I've been working with some other members of my robotics team to build a swerve-drive robot in an attempt to keep our team up to date with the latest FRC technology and increase our competitiveness for next year's season. We went all the way from having just built the modules (SDS Mk4is) to having a fully operational robot with a basic intake and versatile autonomous routines in about 5 weeks, which I think is pretty cool given the fact that we only worked on the robot one day a week! For autonomous we started out with just following predefined pathplanner trajectories, but lately we've been looking into incorporating autonomous routines into the control of the robot even during teleop period. Automating more of the driver's job, we believe, will lead to more efficient and faster acquisition and scoring of gamepieces. Automated scoring in this year's game has one major issue aside from the obvious: there are so many places to score! To usefully automate scoring, one would need an easy way to select which "node" to score during the match. At regionals, I saw a few teams taking this more automated approach, and the majority of these teams used a "button box" with large arcade-style buttons representing each node on the grid. I'm sure that this is pretty effective, but building a dedicated driver-station for each new game seems like a lot of work! Apologies for the lengthy intro - but I think it provides some good context for why using a [StreamDeck](https://www.elgato.com/us/en/s/welcome-to-stream-deck) (a fancy macro pad with a tiny screen on each button) is, in my opinion at least, a more versatile and configurable input device for the control of FRC robots.

## Getting Started

My idea from the start was to build a configurable framework that serves as an interface between the StreamDeck and the FRC ecosystem. Elgato, the company that makes the StreamDeck, has software that allows you to bind actions to each of the keys of the StreamDeck and even though its (allegedly) possible to create plugins that can give custom functionality to the keys, I tried to create a plugin, and I couldn't get it to work for the life of me. Whether the plugin development process is really finnicky, or I'm just stupid (the latter is *much* more likely), I wasn't able to get anything to work properly. After some looking around on GitHub for alternative ways to programmatically interface with the StreamDeck, I found [python-elgato-streamdeck](https://github.com/abcminiuser/python-elgato-streamdeck), a python library providing a third-party interface with the StreamDeck. It took me under an hour to throw together a basic script that turned the StreamDeck into a visual representation of 1/3 of the grid that posted the currently selected grid node to the robot's [NetworkTables](https://docs.wpilib.org/en/stable/docs/software/networktables/networktables-intro.html). It looked fine, and had the interactivity that I wanted, but it was a bit laggy, which was pretty noticeable. 

## A New Approach

Looking on GitHub again for an alternative way to use the StreamDeck, I found [code-deck](https://github.com/hagronnestad/code-deck), an open-source alternative to the software provided by Elgato. Better yet, it has a well documented and easy-to use plugin framework that supports configuration of the StreamDeck's keys with a JSON configuration file. As soon as I found this, I had to try it. The plugin configuration system works great, and I immediately forked it and started making some modifications. The first modification I made was to change what selected each key from an integer index to a coordinate pair. Code-deck was originally only designed to be used with the smallest StreamDeck, but I wanted to make it useable with the larger StreamDeck as well. Now that I had customized the base software to my liking, it was time to start working on a plugin interfacing it with the NetworkTables. My idea was that each button on the StreamDeck would be somehow connected to a certain NetworkTables entry, displaying it, changing it when presses, etc. Some of these buttons that I wanted to implement were:

- Push/toggle button
- Radio buttons
- Boolean indicator
- Generic text/value display
- Numeric dial/bar graph display
- Enum display (values mapped to images/colors/text of the indicator)
- Number increment/decrement button

Using the [C# NetworkTables library](https://github.com/robotdotnet/NetworkTables) I created a wrapper for NetworkTables entries and as of writing this blog post, I have implemented the majority of these widgets. Using and improving on the plugin and JSON configuration system of the original code-deck, I added support for typed configuration values and enabled the configuration of the FRC plugin providing NetworkTables widgets so that configuring the StreamDeck to be a grid node selector, robot dashboard, or stats display is easy.

Check out [my fork](https://github.com/NifleySnifley/code-deck-frc), and keep posted for more! Thanks for reading!
