---
layout: post
title:  "Rocket Tracker Part 8: First Launch!"
date:   2023-09-19 18:09:00 -0500
categories: blog
project: rtrk
---

The (postponed) september launch for Tripoli MN was last weekend, and by that time finally the tracker was ready for some actual testing!

## Preparing for the Launch

Well... most of the preparation was done the week before in anticipation of the launch that was cancelled, but you get the point. The tracker was done, but I still needed to mount it into the rocket. The rocket I was planning on testing it with was a 5" diameter rocket that my dad built for level-2 certification that had a quite spacious electronics bay. I mounted the tracker with standoffs onto the wood "sled" that fit inside of the electronics bay, zip-tied on the battery, and attached the barometer as well. To power the tracker I used a cable I made last year that contained an Adafruit 5v buck converter so I would get a little bit more efficiency than just running the tracker's linear regulator off of the 12v LiPo battery. Why a 12v LiPo? Well, because it had enough capacity to theoretically run the tracker for *hours* and fit nicely inside of the electronics bay. Why not a 1s LiPo to power the 3.3v tracker electronics? My fault - I made the bad decision to use a run-of-the-mill LDO for voltage regulation, so the tracker is under normal operating voltage when running off a 1s LiPo.

<br/>
<div style="width: 100%; height: fit-content, display: block; overflow: auto;">
{% include image.html file="rocketracker/testflight/ebay_all.jpg" astyle="width:40%; float:left;margin-left:5%" caption="Complete electronics sled" %}
{% include image.html file="rocketracker/testflight/ebay.jpg" astyle="width:40%; float: right; margin-right: 5%" caption="Electronics bay containing sled" %}
</div>
{% include image.html file="rocketracker/testflight/case_full.jpg" astyle="width:65%;" caption="All packed!" %}

## Launch Day!

Launch day finally came! After setting up our table and doing some unpacking, the first thing we did was to install the electronics bay in the rocket and attach it to the shock cord. I had removed the battery before we left so I could charge it, so I zip tied a new, charged battery onto the sled. 
<div style="width: 100%; height: fit-content, display: block; overflow: auto;">
{% include image.html file="rocketracker/testflight/rocketrytable.jpg" astyle="width:40%; float:left;margin-left:5%" caption="Complete electronics sled" %}
{% include image.html file="rocketracker/testflight/tracking.jpg" astyle="width:40%; float: right; margin-right: 5%" caption="Electronics bay containing sled" %}
</div>
In preparation for the first flight, I turned on the tracker and made sure it was working properly, it seemed to work fine, so everything was ready to go! On another note, the rocket I launched it in was a 5.5in diameter rocket with a 38mm engine mount and about 5ft tall flying with a I-284 engine (projected to peak at 1860ft). My dad had flown this rocket a number of times previously with success, including his level 1 and 2 Tripoli certification, so I felt pretty good about this rocket as a test platform the tracker. We armed the chute release, set it up on the launch rail, and it was ready to fly! I was receiving a steady stream of data from the tracker, that was good news as well.

{% include image.html file="rocketracker/testflight/rocket_ready.jpeg" astyle="width:65%;" caption="Ready to go" %}
{% include image.html file="rocketracker/testflight/liftoff.jpeg" astyle="width:65%;" caption="Liftoff!!" %}

## Liftoff!
As the rocket launched, I was, of course, looking at the altitude readout from the receiver and not at the rocket. To my delight I could see the half-parabola start to form as the rocket ascended... and then it kept on going, looking like a perfectly nice parabola... *wait*... thats not good! parabolas are for objects in freefall! The graph hit zero altitude and lost connection, ***great***... 

## Oops
Well, the parachute failed to deploy, sending the rocket plummeting into the ground causing it to "smoosh" (totally scientific terminology). Miraculously all of the electronics in the rocket survived: my tracker just self-unplugged on impact, and even though the entire front electronics bay was badly bent, the Eggfinder Mini mounted in it seemed to still be alive.
<div style="width: 100%; height: fit-content, display: block; overflow: auto;">
{% include image.html file="rocketracker/testflight/rocket_crashed.jpeg" astyle="width:40%; float:left;margin-left:5%" caption="Sad rocket" %}
{% include image.html file="rocketracker/testflight/ebaybroken.jpeg" astyle="width:40%; float: right; margin-right: 5%" caption="Front electronics bay (Eggfinder)" %}
</div>
We later found out that the likely culprit for this unfortunate event was the use of a stiff cord rather than an elastic band for the Jolly Logic chute release that was used to deploy the parachute which failed. Sadly, this event practically totalled the rocket, the tube was "zippered" (split by the shock cord), the nosecone was bent beyond repair, and one of the fins broke off on impact.

## Moving On
Even though the first launch was a total flop, it still generated useful flight data. One flight isn't really enough for rigorous testing of the tracker, so I managed to fit the tracker into a much smaller (29mm tube) rocket with some seriously sketchy modifications:

- Instead of mounting the tracker onto an electronics sled or bay, I simply shoved it into the empty cargo bay of the rocket and padded it using ejection charge wadding ("dog barf" as the Tripoli people like to say)
- Powering the tracker from a 1s LiPo (remember how I said it wasn't designed to use a 1s LiPo? Apparently all of the components can at least sort-of tolerate the undervoltage!), which is suboptimal even though it works.

<div style="width: 100%; height: fit-content, display: block; overflow: auto;">
{% include image.html file="rocketracker/testflight/trackerbundle_table.jpg" astyle="width:40%; float:left;margin-left:5%" caption="\"Bundle\" configuration" %}
{% include image.html file="rocketracker/testflight/trackerbundle_back.jpg" astyle="width:40%; float: right; margin-right: 5%" %}
</div>
Using this configuration, the tracker flew 3 more times for a grand total of **4** flight logs! I'm looking forward to doing more detailed analysis on the flight data, but overall, the tracking system worked well without any major issues and both successfully recorded altitude information, and kept track of where the rocket was with GPS. 

Thanks for reading!