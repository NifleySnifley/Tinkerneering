---
layout: post
title:  "Rocket Tracker Part 12.1: Dual Deploy Hardware Testing"
date:   2024-08-18 12:09:00 -0500
categories: blog
project: rtrk
---

The latest hardware component of the rocket tracker that I have developed is a Dual Deploy (DD) board (I’ll go over more specific details in another post), the board hardware was kind of a flop. About half of it is actually functional as intended, which is better than some of the things I've designed, but still kind of disappointing.

The DD board was originally planned to have 4 analog input channels, 4 10 amp high current pyro channels for running E-matches (or other rocketry igniters), and 4 servo-PWM outputs, along with a 5V 3A power supply that I was aiming to be able to power a couple of little tiny SG90 servos with. The board also has some [super cool tiny addressable LEDs](https://mm.digikey.com/Volume0/opasdata/d220001/medias/docus/930/LTST-E263CEGBK_RevC_7-6-19.pdf) (compatible with the same protocol as the ubiquitous [‘neopixel’ WS2812](https://d2j2m4p6r3pg95.cloudfront.net/module_files/led-cube/assets/datasheets/WS2812B.pdf)) to be used as indicators for the pyro channels, those of course are daisy chained and at the end of the on-board indicator LEDs I added an expansion connector that would be able to run a longer external LED strip also powered by the same 5 volt 3 amp power supply as the servos.

Once I had the boards, after a couple of attempts I got the solder paste just right, I placed all the components, of course, and soldered the board up. All the solder joints looked pretty good. No bridging or anything nasty like that.

The first test that I wanted to do on the board was to test out the 5V power supply because although it's not *critical*, it's a pretty important component of the board. So I plugged it in and it seemed to work. The green power LED lit up. I was running if off a typical 3-cell 12V LiPo. I quickly measured it on my oscilloscope, and it seemed like it was working pretty well and producing a stable 5V.

So I went and I ate lunch. And when I got back from lunch, I plugged the board into the battery again. The LED flickered a couple times and then went out. That could not possibly be good. Well, turns out something must either be broken inside of the buck IC or there was something about my board that was just not quite right, because the board was no longer producing 5V at all. It was also getting pretty hot \- not good.

I was a bit flummoxed, so I checked between the battery positive and negative of the XT90 connector I had on the board and my multimeter said that it was a short circuit, about 0.3 ohms\! I didn't plug the battery in again (that could go badly) but I connected it to my power supply so I could try and see where the current it was drawing was going. I turned my power supply up to 7 volts and it was already pulling around 4A. Something was seriously wrong and I was determined to find the cause \- except for I left the power supply on for a little too long. I heard a little pop and the buck converter IC had developed a little glowing hole in it. Sadly, the magic smoke escaped and my power supply was no more. 

Unfortunately, I had only ordered one set of parts for this board, so there was no hope of fixing it. I managed to heat gun all the power supply components off for future use and bodge on a [LD1117](https://www.st.com/content/ccc/resource/technical/document/datasheet/99/3b/7d/91/91/51/4b/be/CD00000544.pdf/files/CD00000544.pdf/jcr:content/translations/en.CD00000544.pdf) linear regulator, which wouldn’t provide enough power for the servos, but would provide enough power to run the indicator LEDs, which is good enough.

Aside from that one epic fail, there weren't any (obvious) catastrophic failures of any of the other components on the board as far as I could tell. To find out if any of the other components were working, I'd need to start getting some firmware support for the various I2C devices on this board.

Thanks for reading\! In my next post, I’ll go over the firmware development aspect (and more testing) for the DD board.