---
id: 2266
title: Chasing Clouds – An Airborne Radar Live Visualization System
date: 2019-08-30T19:25:00+00:00
author: Alex Z.
layout: post
guid: https://www.physicstomato.com/?p=2266
permalink: /cloud-chaser/
views:
  - 103
wp_featherlight_disable:
  - 
image: /wp-content/uploads/2020/03/Pictureapr2.jpg
categories:
  - Idea Space
---
<hr class="wp-block-separator" />

Last summer, I moved into a cramped Airbnb in Pasadena with two roommates to work at Caltech&#8217;s amazing [Jet Propulsion Laboratory (JPL)](https://www.jpl.nasa.gov/). I tinkered with an [airborne radar system](https://airbornescience.jpl.nasa.gov/instruments/apr2apr3)&#8216;s visualization system, taking it from slow and static to streamlined and dynamic with a custom built Python-based data pipeline and GUI. I thought the whole project was pretty interesting, so here’s what went into it.

## Some Background

The JPL research site, a joint venture between NASA and Caltech, is mostly known for its combination of cutting-edge space exploration and robotics technology. The intern experience at this site is famous for being interactive, memorable, and not like any other internship. <figure class="wp-block-image is-resized">

<img src="https://i0.wp.com/www.jpl.nasa.gov/images/technology/20190319/timelapse-16.jpg?resize=806%2C453&#038;ssl=1" alt="Image result for jet propulsion laboratory" width="806" height="453" data-recalc-dims="1" /> <figcaption>Source: [JPL website](https://www.jpl.nasa.gov/news/news.php?feature=7353)</figcaption></figure> 

The team I worked with, the folks responsible for the Airborne Third Generation Precipitation Radar ([APR3](https://airbornescience.nasa.gov/instrument/APR-3)), loads big and complicated radar systems onto research aircraft and sends them to far away places. They measure cloud precipitation and study things like extreme weather, the effects of slash-and-burn agriculture and other polluting land uses on precipitation, and the general impact of aerosols on climate.&nbsp;

In previous missions, the APR3 radar was simply “along for the ride.” The actual direction of the aircraft was decided by a different research team working with a different tool. Essentially, the APR3 team just requested when the radar be turned on/off and took a look at the data using in-house code after each trip.

However, APR3&#8217;s next trip would be at the end of summer 2019 over the Philippines shortly after my internship; this time it would be the principal instrument and could direct the plane as it flew. 

Furthermore, for this experiment, they wouldn’t have a plan of where to fly until the radar went live and was in the air. They only knew _what_ precipitation patterns they were looking for. Basically, they had to go cloud chasing.

## The Cloud Chaser<figure class="wp-block-image size-large is-resized">

<img src="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2020/03/IMG_20181102_122747.jpeg?resize=774%2C580&#038;ssl=1" alt="" class="wp-image-2313" width="774" height="580" srcset="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2020/03/IMG_20181102_122747.jpeg?resize=1024%2C768&ssl=1 1024w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2020/03/IMG_20181102_122747.jpeg?resize=300%2C225&ssl=1 300w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2020/03/IMG_20181102_122747.jpeg?resize=768%2C576&ssl=1 768w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2020/03/IMG_20181102_122747.jpeg?resize=1536%2C1152&ssl=1 1536w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2020/03/IMG_20181102_122747.jpeg?resize=1200%2C900&ssl=1 1200w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2020/03/IMG_20181102_122747.jpeg?w=2016&ssl=1 2016w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2020/03/IMG_20181102_122747.jpeg?w=1680&ssl=1 1680w" sizes="(max-width: 709px) 85vw, (max-width: 909px) 67vw, (max-width: 984px) 61vw, (max-width: 1362px) 45vw, 600px" data-recalc-dims="1" /> <figcaption>Taken on my first visit to the lab, around 2018</figcaption></figure> 

When I was at JPL, we called my homegrown visualization software “APR-3 Meta”, which sounds really sophisticated and let me submit an official-looking report to government employees. Now that we’re in own blog, I can call it whatever I want. I’m going with _Clou_d _Chaser_, because the idea of going through so much trouble to chase down clouds is funny to me. 

Cloud Chaser was intended to be a comprehensive Python-based upgrade to their current viz system, which was done in MATLAB. The downsides to MATLAB (and the onboard viz program generally) were numerous:

  1. It needs a license! The license is [crazy expensive](https://www.mathworks.com/pricing-licensing.html) and we couldn’t rely on the JPL site-wide license since that needed to be verified online. There’s no guarantee of internet halfway across the world and 80,000 feet in the air.
  2. The scripts had loads of confusing cross-referencing and redundancies. It was built over countless iterations to satisfy all sorts of functions that it didn’t need for the new mission. Lots of scripts were separated for no clear reason (little reusability, tons of redundant lines).
  3. Critically, the program lacked live-update features for many relevant parameters and the feed it did have was difficult to read for non-experts.

To solve these problems, we decided that it would be best if I just rewrote the entire thing in Python, which is open-source and has advantages in its wide range of free visualization packages. 

I only had about two months to learn MATLAB, rewrite the code that translated the binary feed from APR3 to usable data, and figure out how to make a pretty GUI in Python that gave critical info to airplane operators in potentially extreme weather situations.

Luckily, I also had access to a great team of mentors in [Dr. Raquel Rodriguez-Monje](https://www.researchgate.net/profile/Raquel_Monje), [Dr. Simone Tanelli](https://www.researchgate.net/profile/Simone_Tanelli), [Dr. Ousmane Sy](https://www.researchgate.net/profile/Ousmane_Sy5), and [Dr. Steve Durden](https://www.researchgate.net/scientific-contributions/5413009_SL_Durden) from the APR3 team, who offered advice and direction along the way. Ultimately, I was able to hack together a pretty competent solution before the end of summer.

## Interpreting Radar Data

I looked at several Python modules that could make data viz GUIs, but none provided the robustness and depth of customization of [PyQt](https://riverbankcomputing.com/software/pyqt/intro), a popular Python binding for the cross-platform widget toolkit [Qt](https://www.qt.io/). PyQt also has support for embedding Matplotlib plots, which I planned to use for graphing the radar data.

When designing, I quickly realized that the original method for reading binary data in the MATLAB code took too long and, for especially large input files, actually overloaded my computer. 

Since the data was arranged into packets, each varying in format along a single packet, it initially seemed necessary to iterate individually through each packet to correctly apply the read procedure. After all, this was essentially the method that APR3&#8217;s original code implemented.

However, I devised a workaround that leveraged the massive (3-4 orders of magnitude) speedup associated with vectorizing code in Numpy while losing no precision in the analysis step. 

To simplify, my code reads an entire file at once using a Numpy “[memmap](https://docs.scipy.org/doc/numpy/reference/generated/numpy.memmap.html)”, a method of mapping a binary file as a NumPy array, and sets it to read as the smallest byte size that the radar&#8217;s files used, an 8-bit unsigned integer. 

<div class="wp-block-image">
  <figure class="aligncenter size-large"><img src="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2020/02/example.png?w=840&#038;ssl=1" alt="" class="wp-image-2274" srcset="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2020/02/example.png?w=1006&ssl=1 1006w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2020/02/example.png?resize=300%2C93&ssl=1 300w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2020/02/example.png?resize=768%2C238&ssl=1 768w" sizes="(max-width: 709px) 85vw, (max-width: 909px) 67vw, (max-width: 1362px) 62vw, 840px" data-recalc-dims="1" /><figcaption>Diagram of how APR3 packets were generally formatted – the two headers provided critical metadata about what was contained inside (i.e. you need to read them to interpret the raw data correctly), but they were in a different bit format than each other and the raw data.</figcaption></figure>
</div>

For the rest of the formats, I simply used vectorized operations in NumPy to convert multiple 8-bit columns to higher orders, e.g. two 8-bits could become a 16, and four 8-bits could be converted to 32. In case you didn&#8217;t know, vectorizing Python code makes it nutty [fast](https://www.pythonlikeyoumeanit.com/Module3_IntroducingNumpy/VectorizedOperations.html).

I quickly found it was important our code worked fast so that the system could actually be used for live visualization. This method took parsing times for even the largest files we worked with from several minutes (at least on my dinky laptop) to consistently _less than a second._ That&#8217;s step one done.

## Design

APR3 is made up of [three](https://en.wikipedia.org/wiki/Ku_band) [constituent](https://en.wikipedia.org/wiki/Ka_band) [frequency](https://en.wikipedia.org/wiki/W_band) [bands](https://en.wikipedia.org/wiki/Radio_spectrum) and we wanted to track two important metrics for each, meaning six plots could capture everything we needed. In PyQt, you just have write the correct horizontal and vertical containers into the window and populate them with [Matplotlib widgets](https://matplotlib.org/3.1.3/gallery/user_interfaces/embedding_in_qt_sgskip.html). The support for Matplotlib is basically already built into PyQt.

<div class="wp-block-image">
  <figure class="aligncenter size-large"><img src="https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2020/03/Pictureapr2-3.jpg?w=840&#038;ssl=1" alt="" class="wp-image-2301" srcset="https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2020/03/Pictureapr2-3.jpg?w=684&ssl=1 684w, https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2020/03/Pictureapr2-3.jpg?resize=300%2C273&ssl=1 300w" sizes="(max-width: 709px) 85vw, (max-width: 909px) 67vw, (max-width: 984px) 61vw, (max-width: 1362px) 45vw, 600px" data-recalc-dims="1" /><figcaption>The six plots I needed to represent ongoing data. Note that W Band is grayed out, indicating that there was no available data for that band in the given time interval. It is possible to plot &#8220;partial&#8221; data if one band was turned off for some of the time.</figcaption></figure>
</div>

One interesting design requirement was that the plots needed to be &#8220;file agnostic&#8221;. In other words, the team wanted to specify what gets plotted by time interval and not by file. Some files don&#8217;t totally overlap, meaning it had to be able to handle &#8220;empty&#8221; time on some intervals when plotted. 

Luckily, if you populate a Matplotlib mesh chart with multiple data arrays spaced apart, the space between will just be filled with the background color. I changed it to gray to symbolize that there was no data available for that time.

## Live Update

The final and main challenge of this project was to make the interface update live as the radar picked up new data. At first, this issue seemed insurmountable—how could I learn how to combine GUI programming

But the nature of the project also meant I had an easy place to start. APR3 automatically updates its target directory periodically as it finds new data. This meant the challenge could be reduced to simply detecting when there were changes to the data inside the directory and updating the plots accordingly.

I settled on a package called fsmonitor to watch the filesystem after the program was initialized. The program now opened a directory instead of a single file, read all of the data inside it (including some metadata files included alongside each), and then continued to watch for changes. Every new change would redraw the graph with new data.

There are some logical operations specific to continuously graphing data. For instance, I had to keep track of the most &#8220;extreme&#8221; x-values so that I could continuously update the bounds of the graph. Also, each time new data was added to the Matplotlib graph, it added another color legend bar to represent only that new data! I settled on a system that just ignores new color bar updates after the first.

## Final Notes

There are a number of features that future implementations of the program may want to consider adding. First, the time-based paradigm of the plots has some limitations. The y-axis is not bounded like the x-axis, since the y-axes for the w-band were different from the ku- and ka-bands. This could potentially be resolved by linking only the ku- and ka- bands or by scaling the changes in those types to changes in the w-band dynamically.

Second, the color bars for the power and doppler velocity plots are not properly scaled to the entirety of the plot. Rather, it simply creates a color bar that is representative of the first file and refuses to add any more. When implementing the color bar originally, I found that asking it to update the color bar simply adds another color bar to the left of what is already stored. However, there is probably a workaround that I was not able to find given the time constraints.

Lastly, it would be nice to have a way to change the color scheme and plot style inside the program to prepare plots for publication and see changes immediately. Currently, it is necessary to change the internal code, restart the program, reselect the directory, and then wait for the plots to generate if you want to change the style. This implementation greatly restricts the lead time for plot-making.