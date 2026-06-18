---
layout: page
title: A Mathematically Designed and Precision Machined Irish Flute
description: Some people trusted me with a lathe, so I made a flute.
img: assets/img/flute/flute0.jpg
importance: 1
#category: work
related_publications: false
---
# Background

Around late 2024, I finally got access to the Warco lathe and mill at the Birmingham Makerspace. I'd been asking for a little while. The original reason I wanted access was to make one of the tools for making a violin. Specifically, I wanted one of those bending irons for making the ribs of a violin. But, they were quite expensive, and like any cheapskate engineer, I wanted to try making one myself for a fraction of the cost.

<div class="row justify-content-center">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/flute/bending_iron.jpg" title="Violin Bending Iron" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    An example of a violin bending iron sold by El Coda for around 255 Euros
</div>

I'd 3D printed violins before in the past, both based on the [Hovalin Design](https://www.hovalabs.com/work/hovalin) by Hova Labs and the [Modular Fiddle](https://openfabpdx.com/modular-fiddle/) by OpenFab-PDX. However, I found they were both lacking in various ways compared to a traditional wood violin. I kind of wanted to make a violin for a long time, but I knew this was quite a complex project. So I kind of put it off and never got round to it.

Parallel to this, I got roped into learning the Irish high whistle/penny flute by various friends in the University of Warwick's folk group. I kind of realised both that the Irish high whistle was both exceptionally easy to learn, and should be relatively straightforward to manufacture on a lathe and mill. After a little bit of searching on how to calculate the tunings, I discovered that an old retired flutemaker had published a [calculator](https://music.bracker.uk/pub/html/Workshop/Whistle-Calculator.html) for working out the hole positions, for given key and set of hole sizes.

# The Mk0 High Whistle

So, with OnShape as my CAD software of choice, as they were basically the only CAD package that had a free hobbyist tier and ran on Linux, I drew together the initial designs for a high whistle. I decided to go with the high whistle initially as I felt this might be easier than the larger low whistle. This wasn't true in hindsight. They're similarish in difficulty to manufacture.

<div class="row">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/flute/high_whistle0.jpg" title="High Whistle Mk0" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include video.liquid path="assets/video/flute/high_whistle0.mp4" title="High Whistle Mk0" class="img-fluid rounded z-depth-1" controls=true %}
    </div>
</div>
<div class="caption">
    On the left, the first high whistle I fabricated, in the key of D with just intonation. On the right, a video of me playing "The Foggy Dew" on it. My playing is not that good as I'm mainly a violinist, but I think the sound quality is pretty good.
</div>

This design was OK in all honesty. It sounded well and was in tune, though it was somewhat overcomplicated. It also wasn't tunable, which wasn't ideal. This was tolerable though since I'd tuned it reasonably accurately in the manufacturing process, and high whistles seemed less sensitive to factors like temperature (forshadowing what would happen later with the low whistle design). I think the biggest issue with it however was that I didn't have good precision metrology tools at the time. I had a set of Mitutoyo calipers, but as any good machinist will know, you need micrometers. Calipers are only good for ballpark measurements.

This meant that the assembly process relied heavily on me abusing a key property of aluminium, which is that it's soft and had a substantial thermal expansion coefficient (23um/m/K). I could machine things to a lower tolerance, and force parts together with a blowtorch and hammer. This worked, but it was definitely not pretty. It left a lot of marks and scars on the flute. I suppose it added character though. That being said, it was quite funny when musicians asked me how I made it. I told them "Precision's not real. You just need a bigger hammer."

# Mk0, Mk1 and Mk2 Low Whistle

Eventually though, I did finally get round to obtaining some precision snap gauges, along with a set of old Mitutoyo micrometers for cheap on eBay. The snap gauges were a little bit broken, and I actually had to machine a part or 2 to get them working. But, they were enough. I also procured some nicer carbide tooling for better machining quality.

After iterating on the design of the high whistle a bit and simplifying it, I produced more for friends who were professional musicians. I was then confident enough to scale it up to a low whistle. The first attempt (Mk0) kind of failed disastrously, and ended up in the scrap box of shame. This then lead to the second attempt with the Mk1, which was quite successful, and remains my main low whistle to this day.

<div class="row">
    <div class="col-sm-5 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/flute/low_whistle0.jpg" title="Low Whistle Mk1" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-7 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/flute/low_whistle1.jpg" title="Low Whistle Mk0 & Mk1" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    On the left, the Mk1 low whistle. On the right, the failed Mk0 low whistle in multiple pieces after being cut up for scrap, next to the Mk1 low whistle.
</div>

Whilst the Mk1 low whistle worked very well, it still ran into some issues left over from the old high whistle design. The big one was that it was not tunable. This was a much bigger problem for the low whistle than the high whistle, as the low whistle appeared to be much more sensitive to temperature changes. This was compounded by the fact that I tuned the low whistle as it was being made in the workshop, during summer. The whistle was still reasonably warm from the machining process. As it got to autumn and winter, the whistle naturally got colder, and became about half to a full semitone flat towards the upper end of the first octave.

This problem wasn't the end of the world though, but it was annoying. You could compensate by warming up the whistle thoroughly before playing, as well as blowing harder on the upper end of the first octave. But, it already needed quite a lot of air anyway. My lung capacity was very much being stretched by it.

This then lead to the Mk2 design, which was actually tunable. I'd noticed there was a lot of ways traditional flutemakers made their flutes tunable. Some used a piece of lubricated cork to seal the end of the tuning slide. Others relied on teflon tape (also known as plumber's tape) to create an airtight seal.

I thought about all of these methods, and I decided to go with neither of them. I realised that I now had a precision lathe, and micrometers. I could just machine the tuning slide to a 20 micron tolerance. Using my machining skills, I could make it so the tuning slide just about slides with some friction. With a little bit of PTFE lubricant, this would work perfectly. I then wouldn't need to worry about figuring out anything more complicated.

This led to the Mk2 design, which was my best design yet. It still needed a lot of air, but it was tunable. The tuning however still is a tiny bit on the flatter side, as I underestimated how far the tuning slide needed to move in winter to compensate for the colder termperatures. But it was still a major improvement, and my best flute to date. I gave it to a good friend who is a much more professional musician than I am. By all accounts, they seem to be impressed by it. My whistles so far have been rated as comparable to professionally made flutes.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include video.liquid path="assets/video/flute/low_whistle0.mp4" title="Low Whistle Mk0" class="img-fluid rounded z-depth-1" controls=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/flute/low_whistle2.jpg" title="Low Whistle Mk2" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    On the left, a video of me playing "McKechnie's Farewell" on the Mk1 low whistle. On the right, the Mk2 low whistle, on which you can see the tuning slide. I unfortunately gave the Mk2 away to a friend before I recorded myself playing it, so I have no video of it. I might eventually ask him to record himself playing it, and add it here.
</div>

# Future Work

So, I guess there's a relatively clear roadmap, for when I have time to continue this, and for the Mk3 low whistle design. The first is of course a longer tuning slide. This will help it deal with fluctuating temperatures better. The second is to figure out how to reduce the air requirements. I'm honestly uncertain about this, as my understanding now of the physics of the flute is that it's a set of tradeoffs. Reducing air with a narrower window would probably make it quieter, which we don't want. We want it to project well for performances and sessions. We may be able to get around that by making the window longer, but that might ruin the sound quality due to increased turbulence. This is something I'll have to experiment with.

The other thing I want to do is to get access to a suitable CNC machine. Machining is very time intensive. Each whistle is approximately 20 hours of manual machining time. With automation, that could be cut down a lot. I can't say how much exactly, but CNCs can run somewhat unsupervised, though not fully unsupervised due to safety concerns. Even if it was only 10 hours of manual time, that would be a huge improvement.

Getting hold of a CNC would also allow me to better design the mouthpiece. The mouthpiece shape isn't that important, as long as it's comfortable enough. But it is currently a pain in the arse to make, as I kind of have to do it freehand with a belt sander, It just about works, but it's very inefficient. A CNC would make this much easier.

# Design Files

The full parametric design files are available via OnShape's link sharing [here](https://cad.onshape.com/documents/18124ad9576687ebc5343565/w/ccef50f699a04516c4a3e6be/e/0a9c0a59844e99352745eedb?renderMode=0&uiState=6a34132af7594a72582dee80).

You can export the designs to a format of your choosing and use them to manufacture your own flutes.

However, please note that these designs should be used as a reference. Unlike 3D printing, machining depends very heavily on the specific tooling you have access to, and the methods you use with them. Tolerances are **not** modelled into the CAD designs. I figured them out as I went along machining.

Also note that these designs are based around common tube sizes I had access to. If the materials you have access to are different, you may need to adjust the designs accordingly. Use the calculator I referenced to work out exact hole positions you need/

And of course, obligatory disclaimer: I am not responsible for anything you do with these designs. If you hurt yourself, or someone else, or break something, that's on you. You are meant to exercise your own skills and expertise when using these designs. I am not responsible for your actions.