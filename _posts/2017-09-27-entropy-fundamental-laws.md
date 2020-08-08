---
id: 1278
title: Entropy and the Fundamental Laws
date: 2017-09-27T05:48:40+00:00
author: Alex Z.
layout: post
guid: https://www.physicstomato.com/?p=1278
permalink: /entropy-fundamental-laws/
wp_featherlight_disable:
  - 
views:
  - 140
categories:
  - Thermodynamics
---
<span style="font-weight: 400;">Like <a href="https://en.wikipedia.org/wiki/Laws_of_science" target="_blank" rel="noopener">every field of physics worth its salt</a>, thermodynamics has, at its heart, some fundamental, unchanging principles dubbed “laws.” </span><span style="font-weight: 400;">Thermodynamics has four laws, arguably five. Inexplicably, you’ll find in the literature that they are usually not numbered 1-4 but instead </span>_<span style="font-weight: 400;">0-3</span>_<span style="font-weight: 400;">. </span><span style="font-weight: 400;">There&#8217;s probably a legitimate reason for this that I&#8217;m not bothering to find, but in my defense, how legitimate can a reason really be if it completely defies proper numbering conventions and basic logic?</span><span style="font-weight: 400;"> </span>

<span style="font-weight: 400;">No matter. The four laws, in order from, erm&#8230; zero to three, are simply stated as follows:</span>

> **The Zeroth** <span style="font-weight: 400;"><strong><em>(&#8230;why?)</em> Law of Thermodynamics</strong> – If two thermodynamic systems are each in thermal equilibrium with a third, then they are in thermal equilibrium with each other.</span>

> <span style="font-weight: 400;"><strong>The First Law of Thermodynamics</strong> – Energy can neither be created nor destroyed. It can only change forms.</span>

> <span style="font-weight: 400;"><strong>The Second Law of Thermodynamics</strong> – It is impossible for a process to have as its sole result the transfer of heat from a cooler body to a hotter one.</span>

> <span style="font-weight: 400;"><strong>The Third Law of Thermodynamics</strong> – As temperature approaches absolute zero, the entropy of a system approaches a constant minimum. </span>

<span style="font-weight: 400;">The reason why I noted that there are arguably </span>_<span style="font-weight: 400;">five </span>_<span style="font-weight: 400;">laws (except, in this blasted numbering system, it would henceforth be labeled as the <em>&#8220;f</em></span>_<span style="font-weight: 400;">ourth&#8221;</span>_<span style="font-weight: 400;">) is that the all-important <a href="https://en.wikipedia.org/wiki/Ideal_gas_law" target="_blank" rel="noopener">ideal gas law</a> isn’t included here. Sure, it isn’t as directly related to energy transfer as the other four, but you’ll soon find that PV=nRT is involved in much more than the trivial algebra of your CHEM 101 course.</span>

<span style="font-weight: 400;">Before we go into more detail about the laws and their implications, we need to discuss what is possibly the most important yet nebulous and oft-misunderstood concept in thermodynamics: </span>**entropy.**

### Entropy – A Better Description

* * *

<span style="font-weight: 400;">You will often hear entropy described as </span>_<span style="font-weight: 400;">“disorder,” </span>_<span style="font-weight: 400;">but this description is actually rather misleading; between, say, a cup that’s filled with a bunch of crushed ice cubes and a tall glass of water, the cup of water actually has the higher entropy in the context of its environment, even though you’d be hard pressed to find anyone who would argue it more “disordered.” </span>

<span style="font-weight: 400;">Basically, the issue lies in the fact that “disorder” is subjective and does not have a rigorous scientific definition, while entropy, the thing you’re trying to describe it with, does.</span>

<span style="font-weight: 400;">So there are numerous more accurate descriptions of entropy available than simply calling it “disorder” and being done with it. In my opinion, the best and most useful description for understanding thermodynamics goes like this: entropy is, at its core, a </span>_<span style="font-weight: 400;">statistic</span>_<span style="font-weight: 400;">. It measures the distribution of </span>_<span style="font-weight: 400;">energy</span>_ <span style="font-weight: 400;">in a system. In particular, it measures the locations that the energy is stored in, quantifying how </span>_<span style="font-weight: 400;">spread out</span>_ <span style="font-weight: 400;">these locations are.</span><figure id="attachment_1282" aria-describedby="caption-attachment-1282" style="width: 225px" class="wp-caption alignright">

[<img class="wp-image-1282" title="&quot;Imagine a staircase...&quot;" src="https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/09/elevels.gif?resize=225%2C158&#038;ssl=1" alt="" width="225" height="158" data-recalc-dims="1" />](https://i1.wp.com/www.physicstomato.com/wp-content/uploads/2017/09/elevels.gif?ssl=1)<figcaption id="caption-attachment-1282" class="wp-caption-text">At the microscopic level, energy is quantized, meaning it is measured in discrete numbers. This means that microscopic energy isn’t continuous like the real number scale, but more analogous to the list of all integers (this also means that dividing energy into &#8220;units&#8221; as we&#8217;re doing is a lot more accurate than you probably just gave me credit for).</figcaption></figure> 

<span style="font-weight: 400;">We can effectively demonstrate this description of entropy with a simple case study. First, imagine a closed system containing two identical molecules, A and B, that each can store energy. Now suppose that each molecule has 6 distinct locations that all can store an arbitrary number of discrete units of energy, and that there are 8 energy units in total available in the system. </span>

<span style="font-weight: 400;">We can now easily see that there are many different possible states the system can take on (e.g. 1 unit somewhere in molecule A and 7 in molecule B). These are called </span>_<span style="font-weight: 400;">microstates</span>_<span style="font-weight: 400;">.</span>

<span style="font-weight: 400;">Let’s also assume that each distinct microstate is equally likely to occur (e.g. the state which corresponds to 2 units placed in some arrangement in molecule A and 6 in molecule B is just as likely as 4 somewhere in each), and that a microstate counts as distinct if at least one energy unit is placed in a different location. </span>

<span style="font-weight: 400;">For example, 2 energy units might be placed in the same spot in molecule A, and so both are taking up one of any of the six possible locations, or each could be in a different spot; every possible configuration of these, multiplied by all the different ways to arrange the remaining 6 energy units in molecule B, would be considered a distinct microstate.</span>

<span style="font-weight: 400;">It turns out <a href="http://sixideasapps.pomona.edu//StatMech/" target="_blank" rel="noopener">there are 75582 ways</a> to organize those 8 units of energy in the system we have just described. The distribution works out like this:</span><span style="font-weight: 400;"><br /> </span>

<table>
  <tr>
    <td>
      <span style="font-weight: 400;">Energy Units in A</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">Energy Units in B</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">Possible Microstates</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">Probability</span>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="font-weight: 400;"></span>
    </td>
    
    <td>
      <span style="font-weight: 400;">8</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">1287</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">2%</span>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="font-weight: 400;">1</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">7</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">4752</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">6%</span>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="font-weight: 400;">2</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">6</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">9702</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">13%</span>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="font-weight: 400;">3</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">5</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">14112</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">19%</span>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="font-weight: 400;">4</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">4</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">15876</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">21%</span>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="font-weight: 400;">5</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">3</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">14112</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">19%</span>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="font-weight: 400;">6</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">2</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">9702</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">13%</span>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="font-weight: 400;">7</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">1</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">4752</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">6%</span>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="font-weight: 400;">8</span>
    </td>
    
    <td>
      <span style="font-weight: 400;"></span>
    </td>
    
    <td>
      <span style="font-weight: 400;">1287</span>
    </td>
    
    <td>
      <span style="font-weight: 400;">2%</span>
    </td>
  </tr>
</table>

<span style="font-weight: 400;">(Caution: the probabilities will questionably add up to 101%, an artifact of rounding).</span>

<span style="font-weight: 400;">If every microstate is indeed equally likely, then we can clearly see now which microstates the system will tend towards over time. The states where the energy is more evenly distributed (3 and 5, 4 and 4, etc.) are much more likely to occur than the states at the edges, where the energy is mostly concentrated in one molecule or the other. Entropy quantifies this </span>_<span style="font-weight: 400;">spread</span>_ <span style="font-weight: 400;">of energy, and since 4 and 4 is more evenly spread than 1 and 7, it would thus have a higher entropy. </span>

<span style="font-weight: 400;">It’s important to note that entropy is proportional to the number of possible microstates in any given state. Since there are less ways to arrange the energy units when all 8 are in one molecule than when there are 4 in each, it has a correspondingly lower entropy.</span>

This correlation between possible microstates and entropy implies that higher entropy states are _more likely_. If we let this system run, after a sufficient interval of time, there would be a 21% chance you will find it with 4 units of energy in each molecule, and a lower chance as you go out.

<span style="font-weight: 400;">Interestingly, you may notice that there are cases, though less likely, where the entropy actually goes down. In other words, a case where the energy becomes </span>_<span style="font-weight: 400;">less spread out</span>_<span style="font-weight: 400;">. If we start with 5 energy units in one molecule and another with 3, there’s actually a 13% chance that the next time we check on the system, the distribution will become 6 and 2, respectively. In fact, there’s even a 2% chance that </span>_<span style="font-weight: 400;">all the energy units</span>_ <span style="font-weight: 400;">move to the molecule with initially more energy. </span><span style="font-weight: 400;">If this energy were stored in part kinetically (i.e. temperature, at the microscopic scale) the “hotter” molecule will have just become hotter and the “colder” molecule colder, even though they are completely free to transfer energy between each other!</span>

<span style="font-weight: 400;">This is completely counterintuitive to anyone in real life who has ever burned themselves on a hot stove. Hot objects (the pot) will always transfer energy to colder objects (your now burnt hand). Yet, in the system we just described, there&#8217;s a 21% total chance it ends up in any of the less entropic states. Certainly you’ve never touched a hot pot only to find that your hand </span>_<span style="font-weight: 400;">cooled down</span>_<span style="font-weight: 400;">, right? </span><span style="font-weight: 400;">Ice cubes melt in water until they reach an equilibrium temperature, rooms get messy without deliberate intervention, and hands touching hot pots will be burned. It’s just how things work; energy </span>_<span style="font-weight: 400;">wants</span>_ <span style="font-weight: 400;">to equalize. What gives?</span>

<span style="font-weight: 400;">To put it simply, at a macroscopic scale (the general size range of objects like burnt hands and ice cubes), the amount of atoms—and thus, places where energy can be stored—is so unimaginably high that, when you do the math, the disparity between the higher probabilities of “spread out” states and lower probabilities of states where most or all the energy is concentrated in one location is <em>way too large</em> for it to ever realistically be the case where, for example, your hand cools down upon touching a hot pot.</span>

<span style="font-weight: 400;">Let’s go back to our original system of two molecules. Imagine multiplying all the parameters one-thousand fold (still far from the realm of macroscopic systems), so that we now have 6000 distinct locations to store energy in each molecule (now probably more appropriately called an “object”) and 8000 discrete energy units. Now, let’s pose the obvious follow-up question.</span>

<span style="font-weight: 400;">Question: If we start from a reasonably uneven microstate—one where 6000 of the energy units are stored somewhere in object A and 2000 in object B—what’s the probability of this microstate evolving such that net energy moves from object B to A instead of the reverse, as we’d expect?</span>

<span style="font-weight: 400;">Answer: </span>**Just about 0.000000000000000000000000000003%**

<span style="font-weight: 400;">That’s the beauty of combinatorics: when you mess with big numbers, you&#8217;ll quickly find some ridiculous scaling.</span>

<span style="font-weight: 400;">Remember that the system which gave us that astronomically low probability is still much, </span>_<span style="font-weight: 400;">much</span>_ <span style="font-weight: 400;">smaller than a macroscopic system. For reference, your hand is about 0.5% of your body weight, which itself has about 7 billion billion </span>_<span style="font-weight: 400;">billion </span>_<span style="font-weight: 400;">atoms. So, we find that a human hand is about 35,000,000,000,000,000,000,000,000 atoms. </span>

<span style="font-weight: 400;">Triple that number to estimate the amount of discrete locations where energy can be stored in it, and we can soon see that, compared to the measly 6000 locations which already gave an astronomically low chance of entropy decreasing, the probability that a system of macroscopic objects acts against the second law of thermodynamics, even briefly, is essentially too unlikely to </span>_<span style="font-weight: 400;">ever </span>_<span style="font-weight: 400;">occur.</span>

<span style="font-weight: 400;">Well, isn’t that remarkable? Heat doesn’t </span>_<span style="font-weight: 400;">want</span>_ <span style="font-weight: 400;">to transfer to colder objects, as per our original intuition. The simple fact is that energy occupies whatever state it wants to. Its just that, at macroscopic scales, the higher entropy states happen to be overwhelmingly more likely than the lower entropy states by virtue of having more possible microstates. This is where the &#8220;disorder&#8221; description of entropy comes from; there are simply more ways to be disorderly than orderly. </span><span style="font-weight: 400;">Your hand got burnt because the heat energy of the pan was allowed to evolve in its state by your touching it, and it ended up randomly (as it basically always will) with a higher entropy state of a hotter hand and a slightly colder pan.</span>

_<span style="font-weight: 400;">Some additional notes: entropy can be quantified, and its quantity is oft-used in thermodynamics calculations. To give you a taste, the formula most commonly given for entropy is Boltzmann’s equation:</span>_

**_S = k ln(W)_**

_<span style="font-weight: 400;">where k is the Boltzmann constant equal to 1.38065 x 10^(-23) J/K and W is the number of real microstates.</span>_

### Back to the Laws

* * *

Do you remember the second law? If not, here’s a refresher:

> <span style="font-weight: 400;"><strong>The Second Law of Thermodynamics</strong> – It is impossible for a process to have as its sole result the transfer of heat from a cooler body to a hotter one.</span>

<span style="font-weight: 400;">Did you catch the error? We know now that this statement is not entirely true. Energy transfers </span>_<span style="font-weight: 400;">can</span>_ <span style="font-weight: 400;">sometimes occur from cooler bodies to hotter ones in a closed system, provided the system is small enough for it to be reasonably likely. </span>

<span style="font-weight: 400;">In macroscopic systems, like a car engine, your hand, or the entire universe, it may as well be true, but let’s now rephrase it to be more precise, using our newfound knowledge of entropy.</span>

> <span style="font-weight: 400;"><strong>The Second Law of Thermodynamics</strong> – The entropy of an isolated system not in equilibrium will tend to increase over time, approaching a maximum value at equilibrium.</span>

<span style="font-weight: 400;">With that sorted, let’s revisit the implications of the other laws, starting with the first, er&#8230; zeroth.</span>

> <span style="font-weight: 400;"><strong>The Zeroth Law of Thermodynamics</strong> – If two thermodynamic systems are each in thermal equilibrium with a third, then they are in thermal equilibrium with each other.</span>

<span style="font-weight: 400;">Not much to add here. It’s the thermodynamics equivalent of the transitive property—a=c and b=c implies a=b. Though keep in mind what it says about what you can deduce about systems in thermal equilibrium (states that are spatially and temporally uniform in temperature). </span>

<span style="font-weight: 400;">Two systems are said to be in thermal equilibrium if they are connected by a path permeable to heat and no heat transfer occurs over time.</span>

> <span style="font-weight: 400;"><strong>The First Law of Thermodynamics</strong> – Energy can neither be created nor destroyed. It can only change forms.</span>

<span style="font-weight: 400;">So in thermodynamics, you’ll find that the concept of thermal energy and its relation to work is used a lot. Let’s just add a little extra onto this law to acknowledge that fact.</span>

> <span style="font-weight: 400;"><strong>The First Law of Thermodynamics</strong> – Energy can neither be created nor destroyed. It can only change forms. The change in the energy of a system is the amount of net energy added to the system minus the net energy spent doing work.</span>

<span style="font-weight: 400;">Perfect.</span>

<span style="font-weight: 400;">(This can be mathematically represented as </span><span style="font-weight: 400;">U=Q-W</span><span style="font-weight: 400;">, where U is the total change in energy, Q is the heat energy, and W is the energy spent doing work.)</span>

> <span style="font-weight: 400;"><strong>The Third Law of Thermodynamics</strong> – As temperature approaches absolute zero, the entropy of a system approaches a constant minimum. </span>

<span style="font-weight: 400;">Okay, so there are some interesting implications to this.</span>

<span style="font-weight: 400;">First, that it is impossible to reduce any system to absolute zero in a finite series of operations, which basically means that absolute zero cannot be achieved.</span>

<span style="font-weight: 400;">This also means that a perfectly efficient engine, which delivers energy in work precisely equivalent to the heat energy put in, cannot be constructed. That&#8217;s because the efficiency of a heat engine is reliant on the ratio of the difference in absolute temperature of the working hot and cold sections to the hot section (i.e. unless the cold section has an absolute temperature measuring zero, the ratio, and thus the efficiency, will be less than one).</span>

<span style="font-weight: 400;">&#8230;</span>

<span style="font-weight: 400;">That’s all for the fundamental laws, and for this section. </span>

<span style="font-weight: 400;">Interesting stuff, no? Maybe I was wrong earlier when I said thermodynamics was boring.</span>