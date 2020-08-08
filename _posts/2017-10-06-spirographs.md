---
id: 1372
title: Spirographs, Hypotrochoids, and Chaos
date: 2017-10-06T05:16:52+00:00
author: Alex Z.
layout: post
guid: https://www.physicstomato.com/?p=1372
permalink: /spirographs/
wp_featherlight_disable:
  - 
views:
  - 740
post_views_count:
  - 31
categories:
  - Executables
  - Idea Space
---
<div style='position:relative;padding-bottom: calc(75.0% + 44px)'>
</div>

<span class="wpsdc-drop-cap">E</span>arlier this week, in a course on ancient astronomy, I was introduced to the concept of “[epicycles](https://physics.weber.edu/schroeder/ua/Epicycle.png)” and their place in Ptolemy’s geocentric theory. In the domain of astronomy, epicycles are basically orbits on orbits, and you can have epicycles on epicycles, and so on&#8230;

For some reason, we as a species were stuck on the idea of having only ideal circles as the paths for planets, not realizing that they could also be ellipses. Oh, and we also thought the Earth was the center of the solar system.

<span style="font-weight: 400;">By the time humanity at large switched over to Kepler&#8217;s heliocentrism, the leading theory had some <em>84</em> <em>epicycles</em> in its full description. As it turns out, “adding epicycles” has since become eponymous with bad science—adding parameters in an attempt to get a fundamentally flawed theory to fit increasingly uncooperative data. Go figure.</span>

<span style="font-weight: 400;">While the science behind epicycle astronomy is very much false, they do draw out some frankly beautiful patterns if you follow their orbit. The patterns drawn reminded me of spirographs, and, as far as I can tell, for very good reason. A spirograph is really just a special case of an epicycle path, where the outer orbit perfectly matches up with the inner orbit’s rotation speed</span><figure id="attachment_1395" aria-describedby="caption-attachment-1395" style="width: 219px" class="wp-caption alignleft">

[<img class="size-full wp-image-1395" src="https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/epicycles.jpg?resize=219%2C216&#038;ssl=1" alt="" width="219" height="216" data-recalc-dims="1" />](https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/epicycles.jpg?ssl=1)<figcaption id="caption-attachment-1395" class="wp-caption-text">Spirograph-esque, no?</figcaption></figure> 

I was then wondering if it was possible to generate spirographs myself to mess around with. It turned out to be fairly straightforward: spirograph patterns are equivalent to a mathematical <a href="https://en.wikipedia.org/wiki/Hypotrochoid" target="_blank" rel="noopener noreferrer">hypotrochoid</a> with spinner distance equal or less than the inner radius, which is basically the shape you get following a point on a circle rotating inside a larger circle.

<span style="font-weight: 400;">Hypotrochoids are even more interesting though, since the spinner distance gets to be greater than the inner rotating circle if you want it to be. In fact, you can even set the radius of the inner rotating circle to be </span>_<span style="font-weight: 400;">larger</span>_<span style="font-weight: 400;"><em> than the outer radius</em> that it rotates in, or even </span>_<span style="font-weight: 400;">negative</span>_<span style="font-weight: 400;">! This isn’t something you could replicate with a real, physical spirograph, but since it’s just a mathematical model living inside my computer, we can do whatever we want with it.</span>

<span style="font-weight: 400;">In total, we have five parameters to work with—inner radius, outer radius, spinner radius, revolutions, and iterations. By messing around with the numbers, I’ve got it to produce some utterly insane graphs. I’d be lying if I said I fully understood the path behind some of these, but I’ll try my best to show and explain what I’ve found, and I’ll later propose a mathematical challenge behind the methods that I’m currently working on.</span>

<span style="font-weight: 400;">Anyways, let&#8217;s take a look at some spirographs (more accurately, hypotrochoids).</span>

### Proof Of Concept

* * *

The function for a hypotrochoid is traditionally defined parametrically—in terms of x and y. Python lets us define lambda functions easily to model these like so:

<pre class="prettyprint">x = lambda d,r,R,theta: (R-r)*np.cos(theta) + d*np.cos(((R-r)/r)*theta)
y = lambda d,r,R,theta: (R-r)*np.sin(theta) - d*np.sin(((R-r)/r)*theta)</pre>

Let&#8217;s set the theta to be in terms of a more intuitive quantity (revolutions):

<pre class="prettyprint">revs = 30
Niter = 9999
thetas = np.linspace(0,revs*2*np.pi,num=Niter)</pre>

Now, &#8220;revs&#8221; (revolutions) sets the amount of times the inner circle makes a complete rotation (2 pi radians each), while &#8220;Niter&#8221; (N iterations) is the amount of points we take along the path drawn (the &#8220;resolution&#8221; of our graph).

As an initial test, let&#8217;s set the relevant variables like so:

<pre class="prettyprint">d = 5 #Spinner distance from center of smaller circle
r = 3 #Smaller circle radius
R = 20 #Larger circle radius
revs = 6
Niter = 5000</pre><figure id="attachment_1373" aria-describedby="caption-attachment-1373" style="width: 600px" class="wp-caption alignnone">

<img class="wp-image-1373" title="Loop-a doop-a loop-a doop-a loop-a doop-a doop" src="https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-1.png?resize=600%2C588&#038;ssl=1" alt="" width="600" height="588" srcset="https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-1.png?w=603&ssl=1 603w, https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-1.png?resize=300%2C294&ssl=1 300w" sizes="(max-width: 709px) 85vw, (max-width: 909px) 67vw, (max-width: 984px) 61vw, (max-width: 1362px) 45vw, 600px" data-recalc-dims="1" /> <figcaption id="caption-attachment-1373" class="wp-caption-text">The first result of many</figcaption></figure> 

What do we have here? Looks pretty spirography to me.

We can change the amount and size of the &#8220;loops&#8221; by changing the ratios between the two radii and spinner distance. With different parameters:

<pre class="prettyprint">d = 3 #Spinner distance from center of smaller circle
r = 2 #Smaller circle radius
R = 5 #Larger circle radius
revs = 6
Niter = 5000</pre><figure id="attachment_1374" aria-describedby="caption-attachment-1374" style="width: 600px" class="wp-caption alignnone">

[<img class="wp-image-1374" src="https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-2.png?resize=600%2C597&#038;ssl=1" alt="" width="600" height="597" srcset="https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-2.png?w=594&ssl=1 594w, https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-2.png?resize=150%2C150&ssl=1 150w, https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-2.png?resize=300%2C298&ssl=1 300w" sizes="(max-width: 709px) 85vw, (max-width: 909px) 67vw, (max-width: 984px) 61vw, (max-width: 1362px) 45vw, 600px" data-recalc-dims="1" />](https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-2.png?ssl=1)<figcaption id="caption-attachment-1374" class="wp-caption-text">The ever-elusive 5-leaf clover</figcaption></figure> 

So this is fun and all, but I&#8217;ve found that we&#8217;re mostly limited to these loopy patterns (I call them &#8220;clovers&#8221;) if we don&#8217;t start messing with the iterations.

Lower the &#8220;resolution&#8221; of the graph, so we only take points every once in a while, and we can produce much more interesting plots.

<pre class="prettyprint">d = 5 #Spinner distance from center of smaller circle
r = 3 #Smaller circle radius
R = 20 #Larger circle radius
revs = 200
Niter = 1000</pre><figure id="attachment_1375" aria-describedby="caption-attachment-1375" style="width: 600px" class="wp-caption alignnone">

[<img class="wp-image-1375" src="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-3.png?resize=600%2C574&#038;ssl=1" alt="" width="600" height="574" srcset="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-3.png?w=604&ssl=1 604w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-3.png?resize=300%2C287&ssl=1 300w" sizes="(max-width: 709px) 85vw, (max-width: 909px) 67vw, (max-width: 984px) 61vw, (max-width: 1362px) 45vw, 600px" data-recalc-dims="1" />](https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-3.png?ssl=1)<figcaption id="caption-attachment-1375" class="wp-caption-text">All tangled up!</figcaption></figure> 

Cool, right? Check this out, though:

<pre class="prettyprint">d = 5 #Spinner distance from center of smaller circle 
r = 3 #Smaller circle radius 
R = 20 #Larger circle radius 
revs = 200 
Niter = 1020</pre><figure id="attachment_1383" aria-describedby="caption-attachment-1383" style="width: 600px" class="wp-caption alignnone">

<img class="wp-image-1383" src="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-4.png?resize=600%2C589&#038;ssl=1" alt="" width="600" height="589" srcset="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-4.png?w=597&ssl=1 597w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-4.png?resize=300%2C294&ssl=1 300w" sizes="(max-width: 709px) 85vw, (max-width: 909px) 67vw, (max-width: 984px) 61vw, (max-width: 1362px) 45vw, 600px" data-recalc-dims="1" /> <figcaption id="caption-attachment-1383" class="wp-caption-text">???</figcaption></figure> 

Holy smokes, what happened here?

Keep in mind that the parameters used for this one are nearly _identical_ to the one before it, differing only in iterations (1020 compared to 1000). That means that the only difference between them is a slight difference in angle spacing between the samples.

A small difference makes a big deal when we&#8217;re letting the difference fester over a few hundred rotations. Arguably, this makes the system a rather <a href="https://en.wikipedia.org/wiki/Chaos_theory" target="_blank" rel="noopener noreferrer">chaotic</a> one.

Here&#8217;s a few more examples of the low-resolution regular interval trick making insane graphs:

<pre class="prettyprint">d = 5 #Spinner distance from center of smaller circle
r = 17 #Smaller circle radius
R = 11 #Larger circle radius
revs = 160
Niter = 500</pre><figure id="attachment_1418" aria-describedby="caption-attachment-1418" style="width: 600px" class="wp-caption alignnone">

[<img class="wp-image-1418" src="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-5.png?resize=600%2C589&#038;ssl=1" alt="" width="600" height="589" srcset="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-5.png?w=715&ssl=1 715w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-5.png?resize=300%2C295&ssl=1 300w" sizes="(max-width: 709px) 85vw, (max-width: 909px) 67vw, (max-width: 984px) 61vw, (max-width: 1362px) 45vw, 600px" data-recalc-dims="1" />](https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-5.png?ssl=1)<figcaption id="caption-attachment-1418" class="wp-caption-text">This one&#8217;s my current personal favorite.</figcaption></figure> 

<pre class="prettyprint">d = 1 #Spinner distance from center of smaller circle
r = 11 #Smaller circle radius
R = 12 #Larger circle radius
revs = 121
Niter = 500</pre><figure id="attachment_1419" aria-describedby="caption-attachment-1419" style="width: 600px" class="wp-caption alignnone">

[<img class="wp-image-1419" src="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-7.png?resize=600%2C583&#038;ssl=1" alt="" width="600" height="583" srcset="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-7.png?w=608&ssl=1 608w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-7.png?resize=300%2C292&ssl=1 300w" sizes="(max-width: 709px) 85vw, (max-width: 909px) 67vw, (max-width: 984px) 61vw, (max-width: 1362px) 45vw, 600px" data-recalc-dims="1" />](https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-7.png?ssl=1)<figcaption id="caption-attachment-1419" class="wp-caption-text">This one has a certain elegance that I&#8217;m really digging.</figcaption></figure> 

<pre class="prettyprint">d = 3 #Spinner distance from center of smaller circle
r = 5 #Smaller circle radius
R = 7 #Larger circle radius
revs = 3598
Niter = 629</pre><figure id="attachment_1420" aria-describedby="caption-attachment-1420" style="width: 600px" class="wp-caption alignnone">

[<img class="wp-image-1420" src="https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-8.png?resize=600%2C595&#038;ssl=1" alt="" width="600" height="595" srcset="https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-8.png?w=591&ssl=1 591w, https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-8.png?resize=150%2C150&ssl=1 150w, https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-8.png?resize=300%2C297&ssl=1 300w" sizes="(max-width: 709px) 85vw, (max-width: 909px) 67vw, (max-width: 984px) 61vw, (max-width: 1362px) 45vw, 600px" data-recalc-dims="1" />](https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-8.png?ssl=1)<figcaption id="caption-attachment-1420" class="wp-caption-text">My friend picked five _random_ numbers for this one. She named it &#8220;byssustortafiguraphobia,&#8221; after searching for the latin roots that most closely translate to &#8220;fear of twisted shapes.&#8221;</figcaption></figure> 

<pre class="prettyprint">d = 3 #Spinner distance from center of smaller circle
r = 5 #Smaller circle radius
R = 7 #Larger circle radius
revs = 3598
Niter = 629</pre>

If I were to show every graph that I thought was interesting while messing around with this, this webpage would take a very, very long time to load (I&#8217;m probably already pushing it). But feel free to check all of them out in my public document <a href="https://docs.google.com/document/d/1RV8Gu_QjH_amULpLttihtLXYeTlZMMHQEXYIuhoAQDg/edit?usp=sharing" target="_blank" rel="noopener noreferrer">here</a>. It includes many that I didn&#8217;t find a place for in this post.

### Chaotic Systems

* * *

Remember that pair of completely different graphs we made earlier, where the only actual difference between the generation was a slight change in angle spacing between the samples? I actually found a lot of those, and the results are pretty wonderful.

But before we look at a few more examples of graphs changing wildly with small changes to their parameters (in my opinion, the coolest situations), here&#8217;s a more generic situation. Basically, I just wanted to point out that, most of the time, small changes can only make&#8230; well, _small changes_. See for yourself:<figure id="attachment_1417" aria-describedby="caption-attachment-1417" style="width: 600px" class="wp-caption alignnone">

[<img class="wp-image-1417" src="https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/Spiro-Capture.png?resize=600%2C595&#038;ssl=1" alt="" width="600" height="595" srcset="https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/Spiro-Capture.png?w=771&ssl=1 771w, https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/Spiro-Capture.png?resize=150%2C150&ssl=1 150w, https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/Spiro-Capture.png?resize=300%2C297&ssl=1 300w, https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/Spiro-Capture.png?resize=768%2C761&ssl=1 768w" sizes="(max-width: 709px) 85vw, (max-width: 909px) 67vw, (max-width: 984px) 61vw, (max-width: 1362px) 45vw, 600px" data-recalc-dims="1" />](https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/Spiro-Capture.png?ssl=1)<figcaption id="caption-attachment-1417" class="wp-caption-text">Yes, this is a screenshot of a Facebook Messenger album that was composed of photos of a computer screen that I took using my phone. Sorry, not sorry. It&#8217;s mayhem over here.</figcaption></figure> 

For reference, the parameters used for those 9 snapshots were:

<pre class="prettyprint">d = 6 #Spinner distance from center of smaller circle
r = 7 #Smaller circle radius
R = 8 #Larger circle radius
revs = 2000</pre>

—where Niter was 452-460. Just take my word for it that this boring sameness happens almost all of the time.

As for the times where it doesn&#8217;t happen&#8230;

<pre class="prettyprint">d = 5 #Spinner distance from center of smaller circle
r = 11 #Smaller circle radius
R = 12.6000 #Larger circle radius
revs = 1000</pre>

With these parameters, and 200 iterations we get:

[<img class="alignnone size-full wp-image-1421" src="https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-9.png?resize=594%2C591&#038;ssl=1" alt="" width="594" height="591" srcset="https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-9.png?w=594&ssl=1 594w, https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-9.png?resize=150%2C150&ssl=1 150w, https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-9.png?resize=300%2C298&ssl=1 300w" sizes="(max-width: 594px) 85vw, 594px" data-recalc-dims="1" />](https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-9.png?ssl=1)  
Okay, all good. With those same parameters and _201_ iterations, we get:

[<img class="alignnone size-full wp-image-1423" src="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-10.png?resize=594%2C591&#038;ssl=1" alt="" width="594" height="591" srcset="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-10.png?w=594&ssl=1 594w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-10.png?resize=150%2C150&ssl=1 150w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-10.png?resize=300%2C298&ssl=1 300w" sizes="(max-width: 594px) 85vw, 594px" data-recalc-dims="1" />  
](https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-10.png?ssl=1) Um, what happened? The simple explanation is that, at 200 divisions of the rotating angle of the inner circle, it happened to be offset slightly, and it created a (relatively) normal spirograph pattern that we&#8217;re used to. At 201 divisions though, it just happened to perfectly line up on the same points each time it sampled them around the function. Funky.

Okay, so here&#8217;s another, even more insane example. Prepare to have your mind blown.

<pre class="prettyprint">d = 5 #Spinner distance from center of smaller circle
r = 3 #Smaller circle radius
R = 8 #Larger circle radius
revs = 50050</pre>

In the following graphs, the iteration count runs from 997-1003:<figure id="attachment_1424" aria-describedby="caption-attachment-1424" style="width: 603px" class="wp-caption alignnone">

[<img class="wp-image-1424 size-full" src="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-11.png?resize=603%2C591&#038;ssl=1" alt="" width="603" height="591" srcset="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-11.png?w=603&ssl=1 603w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-11.png?resize=300%2C294&ssl=1 300w" sizes="(max-width: 709px) 85vw, (max-width: 909px) 67vw, (max-width: 984px) 61vw, (max-width: 1362px) 45vw, 600px" data-recalc-dims="1" />](https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-11.png?ssl=1)<figcaption id="caption-attachment-1424" class="wp-caption-text">Looks like&#8230; just some squares? Kinda lame.</figcaption></figure> <figure id="attachment_1426" aria-describedby="caption-attachment-1426" style="width: 603px" class="wp-caption alignnone">[<img class="wp-image-1426 size-full" src="https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-13.png?resize=603%2C591&#038;ssl=1" alt="" width="603" height="591" srcset="https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-13.png?w=603&ssl=1 603w, https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-13.png?resize=300%2C294&ssl=1 300w" sizes="(max-width: 709px) 85vw, (max-width: 909px) 67vw, (max-width: 984px) 61vw, (max-width: 1362px) 45vw, 600px" data-recalc-dims="1" />](https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-13.png?ssl=1)<figcaption id="caption-attachment-1426" class="wp-caption-text">Oh my.</figcaption></figure> <figure id="attachment_1427" aria-describedby="caption-attachment-1427" style="width: 603px" class="wp-caption alignnone">[<img class="wp-image-1427 size-full" src="https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-14.png?resize=603%2C591&#038;ssl=1" alt="" width="603" height="591" srcset="https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-14.png?w=603&ssl=1 603w, https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-14.png?resize=300%2C294&ssl=1 300w" sizes="(max-width: 709px) 85vw, (max-width: 909px) 67vw, (max-width: 984px) 61vw, (max-width: 1362px) 45vw, 600px" data-recalc-dims="1" />](https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-14.png?ssl=1)<figcaption id="caption-attachment-1427" class="wp-caption-text">The symmetry here makes NO sense. And how does this follow from what we just had?</figcaption></figure> <figure id="attachment_1428" aria-describedby="caption-attachment-1428" style="width: 603px" class="wp-caption alignnone">[<img class="wp-image-1428 size-full" src="https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-15.png?resize=603%2C591&#038;ssl=1" alt="" width="603" height="591" srcset="https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-15.png?w=603&ssl=1 603w, https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-15.png?resize=300%2C294&ssl=1 300w" sizes="(max-width: 709px) 85vw, (max-width: 909px) 67vw, (max-width: 984px) 61vw, (max-width: 1362px) 45vw, 600px" data-recalc-dims="1" />](https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-15.png?ssl=1)<figcaption id="caption-attachment-1428" class="wp-caption-text">Looking like a Picasso now.</figcaption></figure> <figure id="attachment_1429" aria-describedby="caption-attachment-1429" style="width: 597px" class="wp-caption alignnone">[<img class="wp-image-1429 size-full" src="https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-16.png?resize=597%2C586&#038;ssl=1" alt="" width="597" height="586" srcset="https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-16.png?w=597&ssl=1 597w, https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-16.png?resize=300%2C294&ssl=1 300w" sizes="(max-width: 597px) 85vw, 597px" data-recalc-dims="1" />](https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-16.png?ssl=1)<figcaption id="caption-attachment-1429" class="wp-caption-text">Yeah. Same function, I swear.</figcaption></figure> <figure id="attachment_1430" aria-describedby="caption-attachment-1430" style="width: 603px" class="wp-caption alignnone">[<img class="wp-image-1430 size-full" src="https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-17.png?resize=603%2C591&#038;ssl=1" alt="" width="603" height="591" srcset="https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-17.png?w=603&ssl=1 603w, https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-17.png?resize=300%2C294&ssl=1 300w" sizes="(max-width: 709px) 85vw, (max-width: 909px) 67vw, (max-width: 984px) 61vw, (max-width: 1362px) 45vw, 600px" data-recalc-dims="1" />](https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-17.png?ssl=1)<figcaption id="caption-attachment-1430" class="wp-caption-text">And we&#8217;re back to &#8220;normal.&#8221;</figcaption></figure> 

Crazy, right? I won&#8217;t pretend to know exactly what went down in this example; the extent of my knowledge is pretty much the combination of my earlier explanations on where the &#8220;chaos&#8221; of this system comes from and how that means that sometimes small changes make immense differences in the final graph.

### Extra Graphs

* * *

Before we cap things off, I wanted to show off a final few spirographs that I like a lot.

Here&#8217;s one that demonstrates how curved lines can be approximated using a series of straight ones:

<pre class="prettyprint">d = 1 #Spinner distance from center of smaller circle
r = 4 #Smaller circle radius
R = 5 #Larger circle radius
revs = 100
Niter = 325</pre>

[<img class="alignnone size-full wp-image-1431" src="https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-18.png?resize=608%2C591&#038;ssl=1" alt="" width="608" height="591" srcset="https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-18.png?w=608&ssl=1 608w, https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-18.png?resize=300%2C292&ssl=1 300w" sizes="(max-width: 709px) 85vw, (max-width: 909px) 67vw, (max-width: 984px) 61vw, (max-width: 1362px) 45vw, 600px" data-recalc-dims="1" />](https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-18.png?ssl=1)

The dark blue line is the generating function, and the cyan lines are the spirograph that it makes. As discussed earlier, the spirograph is really just a series of points connected from a generating function.

Curiously, it looks like the spirograph itself maps out _another generating function_, something that could be found under the same set of rules (a mathematical hypotrochoid)! I&#8217;ll leave it up to you to figure that one out.

Here&#8217;s another:

<pre class="prettyprint">d = 20 #Spinner distance from center of smaller circle
r = 69 #Smaller circle radius
R = 63.6 #Larger circle radius
revs = 740
Niter = 2030</pre><figure id="attachment_1432" aria-describedby="caption-attachment-1432" style="width: 603px" class="wp-caption alignnone">

[<img class="size-full wp-image-1432" src="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-19.png?resize=603%2C591&#038;ssl=1" alt="" width="603" height="591" srcset="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-19.png?w=603&ssl=1 603w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-19.png?resize=300%2C294&ssl=1 300w" sizes="(max-width: 709px) 85vw, (max-width: 909px) 67vw, (max-width: 984px) 61vw, (max-width: 1362px) 45vw, 600px" data-recalc-dims="1" />](https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-19.png?ssl=1)<figcaption id="caption-attachment-1432" class="wp-caption-text">Spooky.</figcaption></figure> 

I called that one &#8220;Doom Hands.&#8221; Pretty hellish, right?

Okay, last one.:

<pre class="prettyprint">d = 20 #Spinner distance from center of smaller circle
r = 69 #Smaller circle radius
R = 61.6 #Larger circle radius
revs = 10000
Niter = 10000</pre><figure id="attachment_1434" aria-describedby="caption-attachment-1434" style="width: 600px" class="wp-caption alignnone">

[<img class="wp-image-1434" src="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-20.png?resize=600%2C573&#038;ssl=1" alt="" width="600" height="573" srcset="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-20.png?w=605&ssl=1 605w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-20.png?resize=300%2C287&ssl=1 300w" sizes="(max-width: 709px) 85vw, (max-width: 909px) 67vw, (max-width: 984px) 61vw, (max-width: 1362px) 45vw, 600px" data-recalc-dims="1" />](https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-20.png?ssl=1)<figcaption id="caption-attachment-1434" class="wp-caption-text">The Homer Simpson curve.</figcaption></figure> 

I call that one the &#8220;Very Filling Donut&#8221; because, well, you know.

### Final Notes

* * *

So first off, I want to say that I did actually show this to the astronomy professor I mentioned at the beginning of my post. He&#8217;s an older fellow who mostly teaches required, main-series intro physics courses (read: uninterested engineering students), so I figured I could brighten his day up by showing him that someone made some pretty cool stuff mostly inspired by what he taught.

I showed it to a few other teachers and friends earlier who liked the idea, but without his approval in particular, the whole effort felt almost _incomplete_. Of course, being the guy that inspired it, I was expecting him to like it the most. I showed it to him with high hopes.

He didn&#8217;t seem all that interested. You win some.

Second, if you&#8217;re wondering how I created that cool animation at the top, I used <a href="https://www.desmos.com/calculator/" target="_blank" rel="noopener noreferrer">Desmos</a>, an online graphing calculator with surprisingly robust animation functions. <a href="https://www.desmos.com/calculator/tj11yk8gt6" target="_blank" rel="noopener noreferrer">Here&#8217;s the exact notebook</a> I used (complete with a bonus animation!).

Lastly, there&#8217;s actually an interesting class of problems that arises from hypotrochoids that I&#8217;ve been working on for a while now, and I&#8217;ve had a bit of progress. Take a look at this graph:

<pre class="prettyprint">d = 1 #Spinner distance from center of smaller circle
r = 11 #Smaller circle radius
R = 12 #Larger circle radius</pre>

(The exact numbers for revs/iterations aren&#8217;t really important if you just want generating functions/plain hypotrochoids—just make them really large relative to the other numbers. See the first two &#8220;clover&#8221; graphs at the beginning)

[<img class="alignnone size-full wp-image-1435" src="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-21.png?resize=608%2C591&#038;ssl=1" alt="" width="608" height="591" srcset="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-21.png?w=608&ssl=1 608w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-21.png?resize=300%2C292&ssl=1 300w" sizes="(max-width: 709px) 85vw, (max-width: 909px) 67vw, (max-width: 984px) 61vw, (max-width: 1362px) 45vw, 600px" data-recalc-dims="1" />](https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/10/spiro-21.png?ssl=1)

Here&#8217;s an interesting question: how many closed regions are in that graph? It&#8217;s kind of a lot (P.S. I don&#8217;t actually know, since counting them seems like a dry exercise, but have at it if you want to kill a few minutes).

I thought the total amount of regions in this graph was an interesting problem, in the sense that trying to figure it out analytically would be a lot of fun. In clear terms, the challenge would be as follows:

> Find a function of the three relevant parameters of a hypotrochoid (i.e. inner radius, outer radius, and spinner distance) for the amount of closed regions that its graph will form.

The problem is stated simply but it&#8217;s not trivial to solve (at least for me, strictly a non-mathematician). So far, I&#8217;ve figured out that the amount of &#8220;loops&#8221; L (i.e. the amount of revolutions the inner circle performs before it returns to its exact original state) can be consistently found with this formula:

<p style="text-align: center;">
  <img src="//s0.wp.com/latex.php?latex=L+%3D+%5Cfrac%7Blcm%28r%2CR%29%7D%7Br%7D&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="L = &#92;frac{lcm(r,R)}{r}" title="L = &#92;frac{lcm(r,R)}{r}" class="latex" />
</p>

—where r and R are the inner and outer radius, respectively, and lcm() finds the least common multiple of its inputs. For certain ideal situations, the amount of loops or the amount plus one is the same as the amount of closed regions, but most don&#8217;t follow that trend. They usually cross over each other (like the situation in the graph above), immensely complicating the problem.

What do you think? Have at it, and tell me how it goes.