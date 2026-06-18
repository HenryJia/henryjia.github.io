---
layout: page
title: A Mathematically Designed and Precision Machined Irish Flute
description: Some people trusted me with a lathe, so I made a flute.
img: assets/img/flute/flute0.jpg
importance: 1
#category: work
related_publications: true
---
# Background

Around late 2024, I finally got access to the Warco lathe and mill at the Birmingham Makerspace. I'd been asking for a little while. The original reason I wanted access was to make one of the tools for making a violin. Specifically, I wanted one of those bending irons for making the ribs of a violin. But, they were quite expensive, and like any cheapskate engineer, I wanted to try making one myself for a fraction of the cost.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
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
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/flute/high_whistle0.jpg" title="High Whistle Mk0" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The first high whistle I fabricated, in the key of D with just intonation.
</div>

This design was OK in all honesty. It worked well and was in tune, though it was somewhat overcomplicated. It also wasn't tunable, which wasn't ideal. This was tolerable though since I'd tuned it reasonably accurately in the manufacturing process, and high whistles seemed less sensitive to factors like temperature (forshadowing what would happen later with the low whistle design). I think the biggest issue with it however was that I didn't have good precision metrology tools at the time. I had a set of Mitutoyo calipers, but as any good machinist will know, you need micrometers. Calipers are only good for ballpark measurements.

This meant that the assembly process relied heavily on me abusing a key property of aluminium, which is that it's soft and had a substantial thermal expansion coefficient (23um/m/K). I could machine things to a lower tolerance, and force parts together with a blowtorch and hammer. This worked, but it was definitely not pretty. It left a lot of marks and scars on the flute. I suppose it added character though.


<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    This image can also have a caption. It's like magic.
</div>

You can also put regular text between your rows of images, even citations {% cite einstein1950meaning %}.
Say you wanted to write a bit about your project before you posted the rest of the images.
You describe how you toiled, sweated, _bled_ for your project, and then... you reveal its glory in the next row of images.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>

The code is simple.
Just wrap your images with `<div class="col-sm">` and place them inside `<div class="row">` (read more about the <a href="https://getbootstrap.com/docs/4.4/layout/grid/">Bootstrap Grid</a> system).
To make images responsive, add `img-fluid` class to each; for rounded corners and shadows use `rounded` and `z-depth-1` classes.
Here's the code for the last row of images above:

{% raw %}

```html
<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
```

{% endraw %}
