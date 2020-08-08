---
id: 899
title: Monte Carlo Petals
date: 2017-05-19T21:42:50+00:00
author: Alex Z.
layout: post
guid: https://www.physicstomato.com/?p=899
permalink: /monte-carlo-petals/
views:
  - 260
wp_featherlight_disable:
  - 
categories:
  - Executables
  - Idea Space
---
<div style="position: relative; padding-bottom: 100%;">
</div>

<p style="text-align: left;">
  <span style="font-weight: 400;">I finished finals today, and I’m pretty glad; it’s been a long, grueling spring semester and summer should prove one hell of a reward this time around.</span>
</p>

<span style="font-weight: 400;">After submitting my last assignment of the 2016-2017 school year, a finicky problem set for a thermodynamics course, I walked to my bus stop past a tree boasting a great deal of flowering buds—not uncommon for the season. And as I strolled by, its petals floated down and were carried by the wind, which made for a pleasant scene.</span>

<span style="font-weight: 400;">So I moved in to get a closer look and to take a picture of it. Here it is.</span><figure id="attachment_900" aria-describedby="caption-attachment-900" style="width: 576px" class="wp-caption alignnone">

<img class="wp-image-900" src="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/05/tree.jpg?resize=576%2C432&#038;ssl=1" alt="" width="576" height="432" srcset="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/05/tree.jpg?resize=300%2C225&ssl=1 300w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/05/tree.jpg?resize=768%2C576&ssl=1 768w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/05/tree.jpg?resize=1024%2C768&ssl=1 1024w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/05/tree.jpg?resize=1200%2C900&ssl=1 1200w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/05/tree.jpg?w=1680&ssl=1 1680w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/05/tree.jpg?w=2520&ssl=1 2520w" sizes="(max-width: 576px) 85vw, 576px" data-recalc-dims="1" /> <figcaption id="caption-attachment-900" class="wp-caption-text">It doesn&#8217;t do it justice. I know people always say this, but you really had to be there.</figcaption></figure> 

<p style="text-align: left;">
  <span style="font-weight: 400;">I also ended up noticing that they landed in a very particular pattern on the ground. Basically, as you got closer to the tree, there were more petals. </span>
</p>

<p style="text-align: left;">
  <span style="font-weight: 400;">And that makes sense: wind can only carry the petals so far from where they start on their branches. But there were so many petals that have been falling for so long that, as a whole, they formed a remarkably clear map of their falling distribution. </span>
</p>

<p style="text-align: left;">
  <span style="font-weight: 400;">Incredibly, you could easily make out something that resembled a sort of gradient towards the center, kind of like the charge distribution of a point charge in 2D: heavy in the middle, and lighter as you get further out.</span>
</p>

<span style="font-weight: 400;">But it wasn&#8217;t this pattern the entire way through: nearing the center of the tree, the petal density only got higher </span>_<span style="font-weight: 400;">up to a point</span>_<span style="font-weight: 400;">, after which it started decreasing again. This also makes sense because, well, tree trunks don&#8217;t grow petals. </span>

<span style="font-weight: 400;">But it was undeniable that the pattern had a nice unique beauty to it, and so I wanted to see if I could remake it myself. I also figured that simulating the random falling of petals to get a sense of the end distribution was similar to a Monte Carlo method, which uses random sampling to solve problems in statistics. </span>

<span style="font-weight: 400;">It ended up looking pretty awesome, and it was actually a relatively simple and short method. Here&#8217;s what I did:</span>

### **Part Zero: The Game Plan**

* * *

<span style="font-weight: 400;">“Monte Carlo Petals” should consist of three main steps. First, we have to set the petal starting positions. Then, we need an algorithm to generate a random wind vector for each petal. Finally, we add each wind vector to the starting position and plot the results.</span>

<span style="font-weight: 400;">Let&#8217;s get this big one out of the way first: how do we generate random vector directions? If you think about it, that&#8217;s basically the backbone of this whole project. We need some way to make a set of equal-length (preferably unit-length) vectors that are distributed randomly with respect to direction. After that, we can scale the magnitudes using any probability distribution we like.</span>

<span style="font-weight: 400;">I found this online for Python, which seems to do the trick:</span>

<pre class="prettyprint">import numpy as np

def random_vec(dims, number):
    vecs = np.random.normal(size = (number,dims))
    mags = np.linalg.norm(vecs, axis=-1)
    return(vecs/mags[...,np.newaxis])</pre>

It seems fairly robust, too. Plotting:

<pre class="prettyprint">import matplotlib.pyplot as plt
from matplotlib import collections
def main():
    ends = random_vec(2,1000)
    vectors = np.insert(ends[:,np.newaxis], 0, 0, axis=1)
    figure,axis = plt.subplots()
    axis.add_collection(collections.LineCollection(vectors))
    axis.axis((-1,1,-1,1))
    plt.show()
main()
x = random_vec(2,200)
plt.scatter(x[:,0],x[:,1])
plt.show()</pre>

We get this graph:

<img class="size-medium wp-image-901 alignnone" src="https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/05/vector-generator.png?resize=300%2C199&#038;ssl=1" alt="" width="300" height="199" srcset="https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/05/vector-generator.png?resize=300%2C199&ssl=1 300w, https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/05/vector-generator.png?w=385&ssl=1 385w" sizes="(max-width: 300px) 85vw, 300px" data-recalc-dims="1" /> 

<span style="font-weight: 400;">So, we&#8217;ll just use that code. Why not? A little help can speed things up tremendously.</span>

### **Part One: Petal Ring**

* * *

<span style="font-weight: 400;">My model of petal starting positions was pretty basic; I just created a randomly distributed ring of them, modeling how the trunk and inner branches wouldn&#8217;t carry petals.</span>

<span style="font-weight: 400;">Take a random direction vector of length one and multiply it by some random value in between a larger number and a smaller number. Do this enough times, and you&#8217;ll map out a ring. The inner radius of your ring is the smaller number, and the outer radius is the larger one.</span>

<span style="font-weight: 400;">Using our random_vec() function:</span>

<pre class="prettyprint">Niter = 2000

startvecs = np.array(random_vec(2,Niter))
mags = np.random.uniform(low = 12, high = 15, size = Niter)
for i in range(Niter):
    startvecs[i] = startvecs[i]*mags[i]
plt.scatter(startvecs[:,0],startvecs[:,1])
plt.show()</pre>

<img class="size-medium wp-image-902 alignnone" src="https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/05/ring-generator.png?resize=300%2C202&#038;ssl=1" alt="" width="300" height="202" srcset="https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/05/ring-generator.png?resize=300%2C202&ssl=1 300w, https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/05/ring-generator.png?w=380&ssl=1 380w" sizes="(max-width: 300px) 85vw, 300px" data-recalc-dims="1" /> 

<span style="font-weight: 400;">Basically, we made 2000 “petals” in a ring with inner radius 12 and outer radius 15. It’s worth it to note that the outermost part of the ring has a lower density than the innermost, since there’s slightly more space to fill out there with essentially the same chance of a petal landing in any given place.</span>

### **Part Two: Some Wind Vectors**

* * *

<span style="font-weight: 400;">How strong is wind, on average? Its gotta be more than zero, if there&#8217;s any wind at all. The wind blowing near the tree when I first saw it was pretty strong, but not overwhelming.</span>

<span style="font-weight: 400;">How each petal is directionally affected by wind should be pretty random as well (even if the wind itself is quite biased, it&#8217;ll change over time). We’ll start with the same random_vec() function usage as last time to make 2000 random directions. Then, we’ll multiply each direction by a length determined by a normal distribution around some set average. </span>

<span style="font-weight: 400;">This should make for a better wind model than, say, a uniform distribution, like we used for the petal ring. A normal distribution lets us make most of the wind around a set average strength, with less likely deviations from that average.</span>

<span style="font-weight: 400;">Here’s what it looks like written down:</span>

<pre class="prettyprint">avgwind = 5.0
winddev = 3.0

windvecs = np.array(random_vec(2,Niter))
windmags = np.random.normal(loc=avgwind,scale=winddev,size=Niter)
for i in range(Niter):
    windvecs[i] = windvecs[i]*[windmags[i]]
plt.scatter(windvecs[:,0],windvecs[:,1])
plt.show()</pre>

<span style="font-weight: 400;">And the resulting graph:</span>

<img class="alignnone size-medium wp-image-903" src="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/05/wind-vectors.png?resize=300%2C202&#038;ssl=1" alt="" width="300" height="202" srcset="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/05/wind-vectors.png?resize=300%2C202&ssl=1 300w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/05/wind-vectors.png?w=380&ssl=1 380w" sizes="(max-width: 300px) 85vw, 300px" data-recalc-dims="1" /> 

<span style="font-weight: 400;">You’ll notice that our average wind is low enough so that there’s still a lot of distribution around the center, especially since negative wind strength will just reverse the vector. This is intentional. We want a good portion of the petals to not move a lot, so that our final plot recognizes the starting positions well. Still, we want a lot of petals to move some too, which is why we set our average above 0.</span>

### **Part Three: Putting It All Together**

* * *

<span style="font-weight: 400;">Now we just need to add the wind vectors to our petal ring. Since we started off using arrays, we can do this in one fell swoop, like so:</span>

<pre class="prettyprint">petalvecs = windvecs + startvecs
plt.scatter(petalvecs[:,0],petalvecs[:,1])
plt.show()</pre>

<span style="font-weight: 400;">This produces the following graph:</span>

<img class="alignnone size-medium wp-image-904" src="https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/05/petal-vector.png?resize=300%2C202&#038;ssl=1" alt="" width="300" height="202" srcset="https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/05/petal-vector.png?resize=300%2C202&ssl=1 300w, https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/05/petal-vector.png?w=380&ssl=1 380w" sizes="(max-width: 300px) 85vw, 300px" data-recalc-dims="1" /> 

<span style="font-weight: 400;">Finally, I messed around with the numbers (petal number, average wind strength, wind deviation, and inner/outer ring radii), made the graph a little bigger and more square, changed the marker color/size/type, and added a background for some finishing touches.</span>

<span style="font-weight: 400;">As promised, these are our Monte Carlo Petals:</span>

<span style="font-weight: 400;"><img class="alignnone wp-image-905" src="https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/05/monte-carlo-petals.png?resize=585%2C577&#038;ssl=1" alt="" width="585" height="577" srcset="https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/05/monte-carlo-petals.png?resize=300%2C296&ssl=1 300w, https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/05/monte-carlo-petals.png?resize=768%2C758&ssl=1 768w, https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/05/monte-carlo-petals.png?w=876&ssl=1 876w" sizes="(max-width: 585px) 85vw, 585px" data-recalc-dims="1" /></span>

<span style="font-weight: 400;">Nice</span><span style="font-weight: 400;">. They’re not quite as visually appealing as the real thing, but I think it has its own simple beauty.</span>

<span style="font-weight: 400;">There’s still a lot more we can play around with, too.</span>

<span style="font-weight: 400;">Here’s the graph imposed on top of the (darker) starting positions:</span>

<img class="alignnone wp-image-907" src="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/05/monte-carlo-petal-start.png?resize=585%2C577&#038;ssl=1" alt="" width="585" height="577" srcset="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/05/monte-carlo-petal-start.png?resize=300%2C296&ssl=1 300w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/05/monte-carlo-petal-start.png?resize=768%2C758&ssl=1 768w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/05/monte-carlo-petal-start.png?w=876&ssl=1 876w" sizes="(max-width: 585px) 85vw, 585px" data-recalc-dims="1" /> 

<span style="font-weight: 400;">And here’s a graph of each wind vector from its starting position to the final petal location (I reduced the petal amount, since it’s not really interesting in the form of a jumbled mass of white and magenta):</span>

<img class="alignnone wp-image-908" src="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/05/monte-carlo-petals-wind-vectors.png?resize=585%2C577&#038;ssl=1" alt="" width="585" height="577" srcset="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/05/monte-carlo-petals-wind-vectors.png?resize=300%2C296&ssl=1 300w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/05/monte-carlo-petals-wind-vectors.png?resize=768%2C758&ssl=1 768w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/05/monte-carlo-petals-wind-vectors.png?w=876&ssl=1 876w" sizes="(max-width: 585px) 85vw, 585px" data-recalc-dims="1" /> 

<span style="font-weight: 400;">What else? We could directly plot the density as the darkness of a color, and figure out a function for the expected density value based on the input parameters.</span>

<span style="font-weight: 400;">And we could also mess around more with the variables themselves—wind deviation, average wind, petal amount, and the inner/outer ring radii—to make other pretty graphs and figure out the patterns that emerge from changing those numbers. Needless to say, there&#8217;s a lot I left unexplored.</span>

<span style="font-weight: 400;">What do you think? Have at it, and tell me how it goes.</span>