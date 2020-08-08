---
id: 1939
title: Generating 3D Coordinates for Practically Any Crystal Lattice
date: 2018-04-13T00:06:09+00:00
author: Alex Z.
layout: post
guid: https://www.physicstomato.com/?p=1939
permalink: /crystal-lattice/
wp_featherlight_disable:
  - 
views:
  - 2628
categories:
  - Executables
  - Idea Space
---
<span style="font-weight: 400;">It’s generally pretty hard to find analytical solutions for properties of </span>_<span style="font-weight: 400;">complex </span>_<span style="font-weight: 400;">crystal lattices—by complex, I mean really anything outside the scope of your average CHEM 101 equivalent (i.e. simple cubic, bcc, fcc and hexagonal structures). To simulate certain properties of a rigid lattice, a good method to employ is a direct numerical sum on a computer generated lattice, which usually converges as you add more atoms. But, how do you generate complex crystal lattice coordinates (if they aren&#8217;t already available online in a crystallographic database)? By nature, shouldn’t they be, well, </span>_<span style="font-weight: 400;">complex</span>_<span style="font-weight: 400;">?</span>

<span style="font-weight: 400;">Good question! But before we get into that, here’s a quick Python script that will generate </span>_<span style="font-weight: 400;">simple</span>_ <span style="font-weight: 400;">cubic coordinates at increasing shell sizes S:</span>

<pre class="brush: python; title: ; notranslate" title="">import itertools 
S = 10 
S_range = list(range(-S,S+1)) 
triplets = list(itertools.product(S_range, repeat=3)) 
</pre>

<span class="" style="display:block;clear:both;height: 0px;padding-top: 20px;border-top-width:0px;border-bottom-width:0px;"></span> 

Plotting in 3D for S=1:

<pre class="brush: python; title: ; notranslate" title="">from mpl_toolkits.mplot3d import Axes3D 
import matplotlib.pyplot as plt 
import numpy as np 

triplets = np.array(triplets) 
fig = plt.figure() 
ax = fig.add_subplot(111, projection='3d') 
ax.scatter(triplets[:,0], triplets[:,1], triplets[:,2], s = 200) 
plt.show()
</pre>

[<img class="wp-image-1966 aligncenter" src="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/simple-cubic-2-1-e1523575323890.png?resize=471%2C382&#038;ssl=1" alt="" width="471" height="382" srcset="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/simple-cubic-2-1-e1523575323890.png?w=552&ssl=1 552w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/simple-cubic-2-1-e1523575323890.png?resize=300%2C243&ssl=1 300w" sizes="(max-width: 471px) 85vw, 471px" data-recalc-dims="1" />](https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/simple-cubic-2-1.png?ssl=1)

<span style="font-weight: 400;">Useful stuff. If you&#8217;ve read my post on the Madelung Constant finder, you might notice that this snippet can actually do more than the </span>_<span style="font-weight: 400;">entire generator</span>_ <span style="font-weight: 400;">I had in that post, since it actually covers all the coordinates in the lattice, circumventing the need for the “equidistant atom finder.” </span>

<span style="font-weight: 400;">So why didn&#8217;t I use it back then? Two reasons: First, I liked the maths fun of figuring out the equidistant atom sequence, which turned out to be the <a href="https://oeis.org/A005875">number of ways to write an integer as the sum of three squares</a>. Second, even once I did come across the more complete generator, despite its length, the original code still proved much faster in execution (and it had the added benefit of already been written).</span>

<span style="font-weight: 400;">We’ll definitely need the full generator here though, and you can probably already see why: If we want to generate a complex lattice from a simple cubic, it&#8217;s better to have </span>_<span style="font-weight: 400;">all</span>_ <span style="font-weight: 400;">the atoms to manipulate. Multiplying by equidistant atoms to cover the ones you don&#8217;t have requires knowledge of the lattice that we can&#8217;t easily work out for non-simple cubic arrangements. Luckily, all you need are four lines in Python to start this up.</span>

### **Step 1: Layers**

* * *

<span style="font-weight: 400;">The first step is to work out how many layers the unit cell of the crystal has. This is pretty easy: pick any arbitrary axis to be your vertical/z axis, and count how many unique heights there are, so that any atoms on the exact same height are said to be on the same layer.</span>

<span style="font-weight: 400;">We’ll be making extensive use of the modulus function here (represented by a &#8216;%&#8217; in Python), which allows us to perform operations on the lattice that are essentially analogous to “every X layers, do Y”. The idea of it is simple: take the modulus of the z coordinate and the amount of layers (or less if you found a symmetry), then do something to each layer to make it like the desired lattice. After the z coordinate passes the last layer of the unit cell, it’ll reset to the first, hence the modulus.</span>

### **Step 2: Mapping**

* * *

<span style="font-weight: 400;">Next, based on its position in the simple cubic lattice, we&#8217;ll remove some atoms that don&#8217;t fit into the final lattice. This one is tricky to visualize, but think of it like mapping atoms in our generated simple cubic lattice to one in the target lattice. Sometimes you&#8217;ll need to remove every other atom to checker the pattern, or flip them along some coordinate line, before multiplying them all by some number to move them into place according to the atomic coordinates. That&#8217;s okay too.</span>

<span style="font-weight: 400;">You’ll need to do some logic to figure out how to exactly move the atoms into place, but the principle is fairly simple. The best way to learn how to do this is to apply the method to actual crystal lattices, so let&#8217;s take a look at two quick examples.</span>

### Example 1: URu2Si2

* * *<figure id="attachment_1943" aria-describedby="caption-attachment-1943" style="width: 205px" class="wp-caption alignleft">

[<img class="wp-image-1943" src="https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/URu2Si2.jpg?resize=205%2C255&#038;ssl=1" alt="" width="205" height="255" srcset="https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/URu2Si2.jpg?w=377&ssl=1 377w, https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/URu2Si2.jpg?resize=241%2C300&ssl=1 241w" sizes="(max-width: 205px) 85vw, 205px" data-recalc-dims="1" />](https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/URu2Si2.jpg?ssl=1)<figcaption id="caption-attachment-1943" class="wp-caption-text">Figure taken from &#8216;[Rotational Symmetry Breaking in the Hidden-Order Phase of URu2Si2](https://arxiv.org/abs/1107.5480)&#8216; by R. Okazaki et al.</figcaption></figure> 

We&#8217;ll use uranium ruthenium silicide as an initial pedagogic model for the method. It&#8217;s a fairly straightforward lattice (the &#8220;122&#8221;) but complex enough where the layer-fitting method is probably one of the best ways to model its coordinates. In fact, the grid-like nature of it really lends itself to this method, which we&#8217;ll see shortly.

Here&#8217;s a few quick facts about the material if you&#8217;re interested: URu2Si2 is a low-temperature superconductor with an interesting &#8220;hidden phase&#8221; at around 17.5K, below which it suddenly becomes magnetic. Apparently, there&#8217;s still debate as to the exact mechanism that causes that phenomena. Below ~1.5K it superconducts.

URu2Si2 has a unit cell with 8 unique layers before it repeats. That means our logic tree could look something like this:

<pre class="brush: python; title: ; notranslate" title="">for i in range(len(triplets)):
    coordset = triplets[i]
    if coordset[2]%8 == 0:
        #do stuff for layer 1
    elif coordset[2]%8 == 1:
        #do stuff for layer 2
    elif coordset[2]%8 == 2:
        #do stuff for layer 3
    elif coordset[2]%8 == 3:
        #do stuff for layer 4
    elif coordset[2]%8 == 4:
        #do stuff for layer 5
    elif coordset[2]%8 == 5:
        #do stuff for layer 6
    elif coordset[2]%8 == 6:
        #do stuff for layer 7
    elif coordset[2]%8 == 7:
        #do stuff for layer 8
</pre>

<span class="" style="display:block;clear:both;height: 0px;padding-top: 20px;border-top-width:0px;border-bottom-width:0px;"></span> 

Let&#8217;s do these layers one by one starting from the bottom.

The first thing you should notice is that every layer of the unit cell should be able to be described as a 2D grid of 3&#215;3, where each of the 9 places for atoms can either be filled or not. The uranium and silicon atoms occupy the corners or the center spots and ruthenium atoms occupy the sides. You can imagine this pattern repeating through the unit cells adjacent to this one.

Assuming [0,0,0] is the point at the center-bottom of the unit cell, the first layer [x,y,0] should follow a trend like this:[<img class="wp-image-1945 aligncenter" src="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/U-layer-1-1.png?resize=395%2C373&#038;ssl=1" alt="" width="395" height="373" srcset="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/U-layer-1-1.png?w=1240&ssl=1 1240w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/U-layer-1-1.png?resize=300%2C283&ssl=1 300w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/U-layer-1-1.png?resize=768%2C725&ssl=1 768w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/U-layer-1-1.png?resize=1024%2C966&ssl=1 1024w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/U-layer-1-1.png?resize=1200%2C1132&ssl=1 1200w" sizes="(max-width: 395px) 85vw, 395px" data-recalc-dims="1" />](https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/U-layer-1-1.png?ssl=1)The [0,0] is the center, and [-1,-1], [-1,1], [1,-1], and [1,1] are the corners of the 3&#215;3 unit cell grid. I&#8217;ve also included the extra atoms that would be introduced by the unit cells directly adjacent to the unit cell in the center. Do you notice a pattern for when the uranium atoms show up or not?

Here&#8217;s one way to think about it: it appears U atoms are showing up when the x and y coordinates are both _not_ multiples of 2. In other words, when x mod 2 _and_ y mod 2 evaluate to 1, rather than 0.

In Python speak, this would look like:

<pre class="brush: python; title: ; notranslate" title="">if coordset[2]%8 == 0:
    if coordset[0]%2 == 1:
        if coordset[1]%2 == 1:
            coordset[2] = coordset[2]/8 * cheight
            U.append(coordset)
</pre>

<span class="" style="display:block;clear:both;height: 0px;padding-top: 20px;border-top-width:0px;border-bottom-width:0px;"></span> 

Alternatively:

<pre class="brush: python; title: ; notranslate" title="">if coordset[2]%8 == 0:
    if (coordset[0]%2 == 1) and (coordset[1]%2 == 1):
        coordset[2] = coordset[2]/8 * cheight
        U.append(coordset)
</pre>

<span class="" style="display:block;clear:both;height: 0px;padding-top: 20px;border-top-width:0px;border-bottom-width:0px;"></span> 

The first IF statement checks if it&#8217;s in layer 1, the next IF statement checks if x is not a multiple of 2, and the final IF does the same for y. Then, if all conditions are met, it appends the coordinate set to a list called &#8216;U&#8217; after multiplying by the correct unit cell height (we&#8217;ll do the widths manually later). It&#8217;s useful to separate the atom types into different lists even if they serve the same purpose in whatever calculation you plan to do, so that you can plot them differently later to easily check if they&#8217;re correct.

Notice that the first layer is not the only one that follows this pattern. Take a look at the picture—layers 4 and 6, both layers of silicon atoms, also do the same thing. Which means:

<pre class="brush: python; title: ; notranslate" title="">if coordset[2]%8 == 3:
    if (coordset[0]%2 == 1) and (coordset[1]%2 == 1):
        coordset[2] = coordset[2]//8 * cheight + Si2height
        Si.append(coordset)
</pre>

<span class="" style="display:block;clear:both;height: 0px;padding-top: 20px;border-top-width:0px;border-bottom-width:0px;"></span> 

and

<pre class="brush: python; title: ; notranslate" title="">if coordset[2]%8 == 5:
    if (coordset[0]%2 == 1) and (coordset[1]%2 == 1):
        coordset[2] = coordset[2]//8 * cheight + Si3height
        Si.append(coordset)
</pre>

<span class="" style="display:block;clear:both;height: 0px;padding-top: 20px;border-top-width:0px;border-bottom-width:0px;"></span> 

seem to be in order.

The &#8220;coordset[2]//8 * cheight + Siheight&#8221; statements do floor division to find out what unit cell the set is in vertically, and then multiply that identifying number by the height of a cell (cheight). The Si2height and Si3height correspond to the heights of the 2nd and 3rd appearances of silicon, going from layers bottom to top.

With the same logic, you can easily figure out that the 2nd, 5th, and 8th layers (where just the center of the 3&#215;3 appears to be filled) should follow a similar pattern, except x mod 2 and y mod 2 evaluate to 0, not 1. Here&#8217;s a graph of layer 2 for better intuition:[<img class="wp-image-1948 aligncenter" src="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/Si-layer-2-1.png?resize=388%2C369&#038;ssl=1" alt="" width="388" height="369" srcset="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/Si-layer-2-1.png?w=1232&ssl=1 1232w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/Si-layer-2-1.png?resize=300%2C285&ssl=1 300w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/Si-layer-2-1.png?resize=768%2C729&ssl=1 768w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/Si-layer-2-1.png?resize=1024%2C972&ssl=1 1024w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/Si-layer-2-1.png?resize=1200%2C1140&ssl=1 1200w" sizes="(max-width: 388px) 85vw, 388px" data-recalc-dims="1" />](https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/Si-layer-2-1.png?ssl=1)Now only layer 3 and layer 7 remain, both composed of ruthenium atoms. Their pattern is slightly different from what we&#8217;ve dealt with before; it&#8217;s like a checkerboard, and the boolean logic behind it will involve an &#8220;either&#8221; rather than an &#8220;and&#8221;.

Take a look at the graph of layer 3 here:[  
<img class="wp-image-1953 aligncenter" src="https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/Ru-layer-3.png?resize=394%2C376&#038;ssl=1" alt="" width="394" height="376" srcset="https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/Ru-layer-3.png?w=1225&ssl=1 1225w, https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/Ru-layer-3.png?resize=300%2C287&ssl=1 300w, https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/Ru-layer-3.png?resize=768%2C734&ssl=1 768w, https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/Ru-layer-3.png?resize=1024%2C978&ssl=1 1024w, https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/Ru-layer-3.png?resize=1200%2C1146&ssl=1 1200w" sizes="(max-width: 394px) 85vw, 394px" data-recalc-dims="1" />](https://www.physicstomato.com/wp-content/uploads/2018/04/Ru-layer-3.png) What&#8217;s the pattern this time?

An easy way to think about it is that ruthenium atoms only show up when the modulus of the x and y coordinate with respect to 2 are not equal to eachother.

In other words, if x mod 2 = 1 and y mod 2 =0, or if x mod 2 = 0 and y mod 2 = 1.

<pre class="brush: python; title: ; notranslate" title="">if coordset[2]%8 == 2:
    if coordset[0]%2 == 1:
        if coordset[1]%2 == 0:
            Ru.append(coordset)
    if coordset[0]%2 == 0:
        if coordset[1]%2 == 1:
            Ru.append(coordset)
</pre>

<span class="" style="display:block;clear:both;height: 0px;padding-top: 20px;border-top-width:0px;border-bottom-width:0px;"></span> 

Since those are the only options, a simpler way to write it would be:

<pre class="brush: python; title: ; notranslate" title="">if coordset[2]%8 == 2:
    if coordset[0]%2 != coordset[1]%2:
        Ru.append(coordset)
</pre>

<span class="" style="display:block;clear:both;height: 0px;padding-top: 20px;border-top-width:0px;border-bottom-width:0px;"></span> 

Now we have all eight layers! Let&#8217;s put them all together in the final tree:

<pre class="brush: python; title: ; notranslate" title="">for i in range(len(triplets)):
    coordset = triplets[i]
    if coordset[2]%8 == 0:
        if (coordset[0]%2 == 1) and (coordset[1]%2 == 1):
            coordset[2] = coordset[2]/8 * cheight
            U.append(coordset)
    elif coordset[2]%8 == 1:
        if (coordset[0]%2 == 0) and (coordset[1]%2 == 0):
                coordset[2] = (coordset[2]//8)*cheight + 0.125
                Si.append(coordset)
    elif coordset[2]%8 == 2:
        if coordset[0]%2 != coordset[1]%2:
            coordset[2] = (coordset[2]//8)*cheight + 0.25
            Ru.append(coordset)
    elif coordset[2]%8 == 3:
        if (coordset[0]%2 == 1) and (coordset[1]%2 == 1):
            coordset[2] = (coordset[2]//8)*cheight + 0.375
            Si.append(coordset)
    elif coordset[2]%8 == 4:
        if (coordset[0]%2 == 0) and (coordset[1]%2 == 0):
            coordset[2] = (coordset[2]//8)*cheight + 0.5
            U.append(coordset)
    elif coordset[2]%8 == 5:
        if (coordset[0]%2 == 1) and (coordset[1]%2 == 1):
            coordset[2] = (coordset[2]//8)*cheight + 0.625
            Si.append(coordset)
    elif coordset[2]%8 == 6:
        if coordset[0]%2 != coordset[1]%2:
            coordset[2] = (coordset[2]//8)*cheight + 0.75
            Ru.append(coordset)
    elif coordset[2]%8 == 7:
        if (coordset[0]%2 == 0) and (coordset[1]%2 == 0):
            coordset[2] = (coordset[2]//8)*cheight + 0.875
            Si.append(coordset)
</pre>

<span class="" style="display:block;clear:both;height: 0px;padding-top: 20px;border-top-width:0px;border-bottom-width:0px;"></span> 

I assumed the layers were spaced evenly, but that&#8217;s only an approximation valid for a teaching example. You could get the spacings correctly by finding literature on the exact atomic coordinates and then fitting the size of a unit cell using axis-wise operations on the Numpy array. We do this in the next example, if you&#8217;re interested.

Still, the graph looks pretty good (after doing some quick adjustments to the input triplets to reduce it to one unit cell):

<pre class="brush: python; title: ; notranslate" title="">S = S*8
S_range = list(range(-S,(S+1)))
trips = list(list(tup) for tup in itertools.product(S_range, repeat=3))
triplets = []
for i in range(len(trips)):
    if (trips[i][0] &lt;= (S/4)-1) and (trips[i][0] &gt;= -((S/4)-1)) and (trips[i][1] &lt;= (S/4)-1) and (trips[i][1] &lt;= -((S/4)-1)) and (trips[i][2]&gt;=0):
        triplets.append(trips[i])
#Logic tree goes here.
fig = plt.figure()
ax = fig.add_subplot(111, projection='3d',)
ax.scatter(U[:,0], U[:,1], U[:,2], c='white', s = 550)
ax.scatter(Ru[:,0], Ru[:,1], Ru[:,2], c='orange', s = 300)
ax.scatter(Si[:,0], Si[:,1], Si[:,2], c='blue', s = 225)
plt.show()
</pre>

<span class="" style="display:block;clear:both;height: 0px;padding-top: 20px;border-top-width:0px;border-bottom-width:0px;"></span> 

Drum roll, please&#8230;

[<img class="aligncenter wp-image-1955 " src="https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/URu2Si2_gen-e1523567183404.png?resize=274%2C439&#038;ssl=1" alt="" width="274" height="439" srcset="https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/URu2Si2_gen-e1523567183404.png?w=442&ssl=1 442w, https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/URu2Si2_gen-e1523567183404.png?resize=188%2C300&ssl=1 188w" sizes="(max-width: 274px) 85vw, 274px" data-recalc-dims="1" />](https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/URu2Si2_gen.png?ssl=1)Hey, not bad! It looks pretty similar to the lattice we wanted originally. Again, it&#8217;d look a little bit better with the exact atomic coordinates. Let&#8217;s look at the next example for some ideas on how to fit that.

### Example 2: LaO1−xFx BiS2

* * *

<span style="font-weight: 400;">We’ll use LaO1−xFx BiS2 as our next example lattice, which has a structure that is a fair bit more complicated than uranium ruthenium disilicide.</span>

<span style="font-weight: 400;">LaO1 (as we’ll now call it to save your mental reading voice some syllables) is a BiS2-based superconductor with a few interesting properties (namely, that its <a href="https://en.wikipedia.org/wiki/Spin%E2%80%93lattice_relaxation">T1 relaxation time</a> is generally </span>_<span style="font-weight: 400;">not</span>_ <span style="font-weight: 400;">inversely proportional to its temperature) and it’s a material I’ve worked a lot with before. </span><figure id="attachment_1961" aria-describedby="caption-attachment-1961" style="width: 215px" class="wp-caption alignright">

[<img class="wp-image-1961 size-full" src="https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/LaO1_Structure.png?resize=215%2C320&#038;ssl=1" alt="" width="215" height="320" srcset="https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/LaO1_Structure.png?w=215&ssl=1 215w, https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/LaO1_Structure.png?resize=202%2C300&ssl=1 202w" sizes="(max-width: 215px) 85vw, 215px" data-recalc-dims="1" />](https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/LaO1_Structure.png?ssl=1)<figcaption id="caption-attachment-1961" class="wp-caption-text">Figure taken from &#8216;[The Crystal Structure of Superconducting LaO1−xFxBiS2](https://link.springer.com/content/pdf/10.1007%2Fs10948-014-2918-0.pdf)&#8216; by A. Athauda et. al.</figcaption></figure> 

<span style="font-weight: 400;">It has 9 “layers” per unit cell (the Bis and S1s are close—not quite on the same layer). We could construct the logic tree like we did for URu2Si2, except for 9 layers instead of 8, but there is a shortcut here: if you take each individual slice along the x axis, there&#8217;s only 5 unique layers. It simply switches between two 5 layer arangements, where one is a flipped version of the other along the z axis.</span>

<span style="font-weight: 400;">In other words, looking at the figure from the front face, you&#8217;ll notice that every other column looks the same, only that they vertically flip, before translating half a unit cell towards/away from as you move across adjacently one-by-one. This gives us our first tip: we want to make sure every other x axis position has reversed z coordinates.</span>

To implement it, we can use a logic tree that looks something like this:

<pre class="brush: python; title: ; notranslate" title="">for i in range(len(triplets)):
    coordset = triplets[i]
    if coordset[0]%2 == 0:
        if coordset[2]%5 == 0:
            if coordset[1]%2 == 0:
                #do stuff for layer 1, even slices
        elif coordset[2]%5 == 1:
            if coordset[1]%2 == 1:
                #do stuff for layer 2, even slices
        elif coordset[2]%5 == 2:
            if coordset[1]%2 == 1:
                #do stuff for layer 3, even slices
        elif coordset[2]%5 == 3:
            if coordset[1]%2 == 1:
                #do stuff for layer 4, even slices
        else:
            if coordset[1]%2 == 1:
                #do stuff for layer 5, even slices
    else:
        if coordset[2]%5 == 0:
            if coordset[1]%2 == 1:
                #do stuff for layer 1, odd slices
        elif coordset[2]%5 == 1:
            if coordset[1]%2 == 0:
                #do stuff for layer 2, odd slices
        elif coordset[2]%5 == 2:
            if coordset[1]%2 == 0:
                #do stuff for layer 3, odd slices
        elif coordset[2]%5 == 3:
            if coordset[1]%2 == 0:
                #do stuff for layer 4, odd slices
        else:
            if coordset[1]%2 == 0:
                #do stuff for layer 5, odd slices
</pre>

<span class="" style="display:block;clear:both;height: 0px;padding-top: 20px;border-top-width:0px;border-bottom-width:0px;"></span> 

A shorter way to write this that takes advantage of the symmetry:

<pre class="brush: python; title: ; notranslate" title="">for i in range(len(triplets)):
    coordset = triplets[i]
    x_type = coordset[0]%2
    if coordset[2]%5 == 0:
        if coordset[1]%2 == 0+x_type:
            #do stuff for layer 1, either slice
    elif coordset[2]%5 == 1:
        if coordset[1]%2 == 1-x_type:
            #do stuff for layer 2, either slice
    elif coordset[2]%5 == 2:
        if coordset[1]%2 == 1-x_type:
            #do stuff for layer 3, either slice
    elif coordset[2]%5 == 3:
        if coordset[1]%2 == 1-x_type:
            #do stuff for layer 4, either slice
    else:
        if coordset[1]%2 == 1-x_type:
            #do stuff for layer 5, either slice
</pre>

<span class="" style="display:block;clear:both;height: 0px;padding-top: 20px;border-top-width:0px;border-bottom-width:0px;"></span> 

Then, within the slices, we&#8217;ll need to multiply the coordinates by either 1 or -1 depending on if it&#8217;s even or odd. The variable &#8220;x\_type&#8221; should come in handy here (e.g. sgn(x\_type-0.5)).

LaO1 has these atomic coordinates (taken from [Y. Mizuguchi, et al.](https://arxiv.org/abs/1207.3558)):

<table width="343">
  <tr>
    <td width="64">
      Site
    </td>
    
    <td width="64">
      x
    </td>
    
    <td width="64">
      y
    </td>
    
    <td width="64">
      z
    </td>
    
    <td width="87">
      Occupancy
    </td>
  </tr>
  
  <tr>
    <td>
      La1
    </td>
    
    <td>
      0.5
    </td>
    
    <td>
    </td>
    
    <td>
      0.1015
    </td>
    
    <td>
      1
    </td>
  </tr>
  
  <tr>
    <td>
      Bi1
    </td>
    
    <td>
      0.5
    </td>
    
    <td>
    </td>
    
    <td>
      0.6231
    </td>
    
    <td>
      1
    </td>
  </tr>
  
  <tr>
    <td>
      S1
    </td>
    
    <td>
      0.5
    </td>
    
    <td>
    </td>
    
    <td>
      0.3657
    </td>
    
    <td>
      1
    </td>
  </tr>
  
  <tr>
    <td>
      S2
    </td>
    
    <td>
      0.5
    </td>
    
    <td>
    </td>
    
    <td>
      0.8198
    </td>
    
    <td>
      1
    </td>
  </tr>
  
  <tr>
    <td>
      O/F
    </td>
    
    <td>
    </td>
    
    <td>
    </td>
    
    <td>
    </td>
    
    <td>
      0.5/0.5(Fixed)
    </td>
  </tr>
</table>

The &#8216;occupancy&#8217; is just the proportion of the atom that&#8217;s in the site. Oxygen and fluorine are evenly distributed throughout the lattice. These coordinates are in atomic units, so are only valid if you assume that 1 is the width/depth of the unit cell for the x and y coordinates, and that 1 is the height of the unit cell for z. Since 1 isn&#8217;t the actual physical distance, we&#8217;ll need to &#8220;reallign&#8221; these later with the correct width, depth, and height.

We already know how to &#8220;checker&#8221; or stagger the pattern from our earlier example, and it&#8217;s always a simple mod 2 for this lattice, so I&#8217;ll skip over that. We&#8217;ll use np.sign(x\_type-0.5) to flip the z coordinate every other column (it evaluates to 1 if x\_type = 1 and -1 if x_type = 0). Then we&#8217;ll alter the z-heights to reflect the coordinates in atomic units, leaving the widths alone (they&#8217;re already exactly twice as far as 0.5 times the unit cell, so we&#8217;ll just reallign them by a factor of two times the actual distance later). Finally, we can reallign by the actual physical width and height of the unit cell and plot the resulting coordinates.

Putting it all together:

<pre class="brush: python; title: ; notranslate" title="">OF,La,S,Bi = [],[],[],[]

for i in range(len(triplets)):
    coordset = triplets[i]
    x_type = coordset[0]%2
    if coordset[2]%5 == 0:
        if coordset[1]%2 == 0+x_type:
            coordset[2] = (coordset[2]/5)*np.sign(x_type-0.5)
            OF.append(coordset)
    elif coordset[2]%5 == 1:
        if coordset[1]%2 == 1-x_type:
            coordset[2] = ((coordset[2]//5) + 0.1015)*np.sign(x_type-0.5)
            La.append(coordset)
    elif coordset[2]%5 == 2:
        if coordset[1]%2 == 1-x_type:
            coordset[2] = ((coordset[2]//5) + 0.3657)*np.sign(x_type-0.5)
            S.append(coordset)
    elif coordset[2]%5 == 3:
        if coordset[1]%2 == 1-x_type:
            coordset[2] = ((coordset[2]//5) + 0.6231)*np.sign(x_type-0.5)
            Bi.append(coordset)
    else:
        if coordset[1]%2 == 1-x_type:
            coordset[2] = ((coordset[2]//5) + 0.8198)*np.sign(x_type-0.5)
            S.append(coordset)

OF,La,S,Bi = np.array(OF),np.array(La),np.array(S),np.array(Bi)

#From atomic units to actual distances
def reallign(array):
    array[:,0] = array[:,0]*4.0596e-8/2
    array[:,1] = array[:,1]*4.0596e-8/2
    array[:,2] = array[:,2]*13.293e-8

reallign(OF), reallign(La), reallign(S), reallign(Bi)
</pre>

<span class="" style="display:block;clear:both;height: 0px;padding-top: 20px;border-top-width:0px;border-bottom-width:0px;"></span> 

The actual width and depth are equivalent at 4.0596 angstroms (4.0596e-8 meters), and the height is 13.293 angstroms. We divided the width/depth reallignment function by 2 because the width of a unit cell is 2 in our original lattice (e.g. -1 to 1).

Finally, let&#8217;s plot (using another quick function I whipped up that allows you to choose if you want negative, positive, or all z-values and also set the width/depth ranges):

<pre class="brush: python; title: ; notranslate" title="">width = 1*0.21e-7 #0.21e-7 is approx. the width of a unit cell.
height = 1*1.4e-7 #1.4e-7 is approx. the height of a unit cell.

def prep_plot(arr,zrange = "all"):
    new_arr = np.copy(arr)
    new_arr[new_arr[:,0] &gt; width] = np.nan
    new_arr[new_arr[:,0] &gt; -width] = np.nan
    new_arr[new_arr[:,1] &gt; width] = np.nan
    new_arr[new_arr[:,1] &lt; -width] = np.nan
    if zrange in ["positive","Positive","+"]:
        new_arr[new_arr[:,2] &gt; height] = np.nan
        new_arr[new_arr[:,2] &lt; 0] = np.nan
    elif zrange in ["negative","Negative","-"]:
        new_arr[new_arr[:,2] &gt; 0] = np.nan
        new_arr[new_arr[:,2] &lt; -height] = np.nan
    else:
        new_arr[new_arr[:,2] &gt; height] = np.nan
        new_arr[new_arr[:,2] &lt; -height] = np.nan
    return new_arr

set_range = "+"

plot_OF = prep_plot(OF,zrange = set_range)
plot_La = prep_plot(La,zrange = set_range)
plot_S = prep_plot(S,zrange = set_range)
plot_Bi = prep_plot(Bi,zrange = set_range)

fig = plt.figure()
ax = fig.add_subplot(111, projection='3d',)
ax.scatter(plot_OF[:,0], plot_OF[:,1], plot_OF[:,2], c='r', s = 150)
ax.scatter(plot_La[:,0], plot_La[:,1], plot_La[:,2], c='g', s = 800)
ax.scatter(plot_S[:,0], plot_S[:,1], plot_S[:,2], c='y', s = 250)
ax.scatter(plot_Bi[:,0], plot_Bi[:,1], plot_Bi[:,2], c='purple', s = 800)
plt.show()
</pre>

<span class="" style="display:block;clear:both;height: 0px;padding-top: 20px;border-top-width:0px;border-bottom-width:0px;"></span> 

Let&#8217;s see what we get&#8230;

[<img class="wp-image-1964 aligncenter" src="https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/URu2Si2_gen2-e1523574941135.png?resize=225%2C458&#038;ssl=1" alt="" width="225" height="458" srcset="https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/URu2Si2_gen2-e1523574941135.png?w=348&ssl=1 348w, https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/URu2Si2_gen2-e1523574941135.png?resize=147%2C300&ssl=1 147w" sizes="(max-width: 225px) 85vw, 225px" data-recalc-dims="1" />](https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2018/04/URu2Si2_gen2.png?ssl=1)Sweet, it works! Notice the O/F (reference) atom at 0,0,0 is missing, because we want to avoid divide by zero error in any calculation that involves distance. Now, we can do whatever we want with this lattice. As an example, my research requires that I calculate the Van Vleck second moment of LaO1, which is a simple sum that requires the distance and angle to the reference. As you might imagine, having coordinates for the crystal lattice is a big help for this. But you can apply it to practically any sum. Happy modeling!

### Some Final Remarks

* * *

A few caveats: this method is only really useful for experimental crystal lattices. For well-known crystals, there tends to be online coordinates available (e.g. the CCDC or COD). Also, for many parts of my code, there are probably a number of ways to make it more succint or run faster (especially in the logic trees), but I wanted to make it as readable as possible for the scope of this post.

Let me know if there&#8217;s something to add, something to get rid of, or something I missed. Have at it, and tell me how it goes.