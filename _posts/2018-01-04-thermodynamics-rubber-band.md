---
id: 1806
title: Thermodynamics of a Rubber Band
date: 2018-01-04T12:51:39+00:00
author: Alex Z.
layout: post
guid: https://www.physicstomato.com/?p=1806
permalink: /thermodynamics-rubber-band/
wp_featherlight_disable:
  - 
views:
  - 243
categories:
  - Thermodynamics
---
### Preface

* * *

<span style="font-weight: 400;">What makes rubber bands stretchy?</span>

<span style="font-weight: 400;">It seems like a question with an obvious answer, but perhaps obvious in the vein of answers to questions like “What makes water wet?” or “Why is the sky blue?” There&#8217;s no quick and easy explanations, and in many cases parents who find their children asking them will discover it&#8217;s easier to say that there is no reason; they just</span>_ <span style="font-weight: 400;">are</span>_<span style="font-weight: 400;">.</span>

<span style="font-weight: 400;">However, rubber bands actually have a very good reason for being stretchy, and the full explanation relies on thermodynamics. So worry not, future physicist parents: studying thermodynamics will let you </span>_<span style="font-weight: 400;">properly</span>_ <span style="font-weight: 400;">answer at least this tricky question, and you will never in your life have to let another child down by explaining to them, “That&#8217;s just how rubber bands work, sweetie.” Unless you’re a lazy parent—that’s on you.</span>

<span style="font-weight: 400;">The modern rubber band is made out of natural rubber, a polymer derived from the latex of a rubber tree (synthetic rubber is generally not as stretchy). Polymers are essentially long, chainlike molecules composed of many identical or nearly identical subunits. Many polymers can sort of combine through a process called “cross-linking,” and they end up behaving in many ways more like a single molecule than a large group of them.</span>

<span style="font-weight: 400;">The cross-linked polymers of a rubber band begin in a chaotic, low energy, tangled state. When the bands are stretched, the energy is increased and the polymers untangle until they reach a local maximum of their length, and a local minimum of entropy. When released, the entropy rapidly increases until they tangle again, compressing the rubber band back to its original state.</span>

<span style="font-weight: 400;">The “cross-linking” property of polymers is vital to the band’s elasticity. Without this property, the rubber band would have no reason to tend towards a tangled state, since the entropy would be about the same in both states. If you released a rubber band with properties like that, it would just stay in the outstretched position until you force into another state.</span>

<span style="font-weight: 400;">So that’s it, right? Case closed? Rubber bands compress because of entropy; it’s beautiful, it’s elegant, and it’s eye-opening, yes, but aren’t we done?</span>

<span style="font-weight: 400;">No, silly. We have maths to do.</span>

### Rubber Band Math

* * *

<span style="font-weight: 400;">An ideal “band-like” model can be constructed using a finite series of <img src="//s0.wp.com/latex.php?latex=%5Cwidetilde%7BN%7D&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="&#92;widetilde{N}" title="&#92;widetilde{N}" class="latex" /> linked segments of length a, each having two possible states of “up” or “down.” For fun, let’s say one end is attached to the ceiling, and the other end is attached to an object of mass m. The segments themselves are weightless.</span>

<span style="font-weight: 400;">The entropy can be found by computing the microstates using combinatorics:</span>

<img src="//s0.wp.com/latex.php?latex=%5COmega%28N_%7Bup%7D%2CN_%7Bdn%7D%29+%3D+%5Cfrac%7BN%21%7D%7BN_%7Bup%7D%21%28N-N_%7Bup%7D%29%21%7D+%3D+%5Cfrac%7BN%21%7D%7BN_%7Bup%7D%21N_%7Bdn%7D%21%7D&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="&#92;Omega(N_{up},N_{dn}) = &#92;frac{N!}{N_{up}!(N-N_{up})!} = &#92;frac{N!}{N_{up}!N_{dn}!}" title="&#92;Omega(N_{up},N_{dn}) = &#92;frac{N!}{N_{up}!(N-N_{up})!} = &#92;frac{N!}{N_{up}!N_{dn}!}" class="latex" /> 

Given that any segment can be found either parallel or antiparallel to the vertical direction, the amount of segments<img src="//s0.wp.com/latex.php?latex=N_%7Bup%7D&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="N_{up}" title="N_{up}" class="latex" /> pointing up and<img src="//s0.wp.com/latex.php?latex=N_%7Bdn%7D&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="N_{dn}" title="N_{dn}" class="latex" /> pointing down can be determined from N using:

<img src="//s0.wp.com/latex.php?latex=N_%7Bup%7D+%2B+N_%7Bdn%7D+%3D+%5Cwidetilde%7BN%7D&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="N_{up} + N_{dn} = &#92;widetilde{N}" title="N_{up} + N_{dn} = &#92;widetilde{N}" class="latex" /> 

and

<img src="//s0.wp.com/latex.php?latex=L+%3D+a%28N_%7Bdn%7D+-+N_%7Bup%7D%29&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="L = a(N_{dn} - N_{up})" title="L = a(N_{dn} - N_{up})" class="latex" /> 

which gives

<img src="//s0.wp.com/latex.php?latex=N_%7Bdn%7D+%3D+%5Cfrac%7B1%7D%7B2%7D%28%5Cwidetilde%7BN%7D-%5Cfrac%7BL%7D%7Ba%7D%29&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="N_{dn} = &#92;frac{1}{2}(&#92;widetilde{N}-&#92;frac{L}{a})" title="N_{dn} = &#92;frac{1}{2}(&#92;widetilde{N}-&#92;frac{L}{a})" class="latex" /> 

<img src="//s0.wp.com/latex.php?latex=N_%7Bup%7D+%3D+%5Cfrac%7B1%7D%7B2%7D%28%5Cwidetilde%7BN%7D-%5Cfrac%7BL%7D%7Ba%7D%29&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="N_{up} = &#92;frac{1}{2}(&#92;widetilde{N}-&#92;frac{L}{a})" title="N_{up} = &#92;frac{1}{2}(&#92;widetilde{N}-&#92;frac{L}{a})" class="latex" /> 

The Boltzmann entropy is thus given by:

<img src="//s0.wp.com/latex.php?latex=S+%3D+k_bln%28%5COmega%29+%3D+k_b%5Bln%28%5Cwidetilde%7BN%7D%21%29-ln%28N_%7Bup%7D%21%29-ln%28N_%7Bdn%7D%29%21%5D&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="S = k_bln(&#92;Omega) = k_b[ln(&#92;widetilde{N}!)-ln(N_{up}!)-ln(N_{dn})!]" title="S = k_bln(&#92;Omega) = k_b[ln(&#92;widetilde{N}!)-ln(N_{up}!)-ln(N_{dn})!]" class="latex" /> 

Applying the earlier equations:

<img src="//s0.wp.com/latex.php?latex=S+%3D+k_bln%28%5COmega%29+%3D+k_b%5Bln%28%5Cwidetilde%7BN%7D%21%29-ln%28%5Cfrac%7B1%7D%7B2%7D%28%5Cwidetilde%7BN%7D-%5Cfrac%7BL%7D%7Ba%7D%29%21%29-ln%28%5Cfrac%7B1%7D%7B2%7D%28%5Cwidetilde%7BN%7D%2B%5Cfrac%7BL%7D%7Ba%7D%29%29%21%5D&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="S = k_bln(&#92;Omega) = k_b[ln(&#92;widetilde{N}!)-ln(&#92;frac{1}{2}(&#92;widetilde{N}-&#92;frac{L}{a})!)-ln(&#92;frac{1}{2}(&#92;widetilde{N}+&#92;frac{L}{a}))!]" title="S = k_bln(&#92;Omega) = k_b[ln(&#92;widetilde{N}!)-ln(&#92;frac{1}{2}(&#92;widetilde{N}-&#92;frac{L}{a})!)-ln(&#92;frac{1}{2}(&#92;widetilde{N}+&#92;frac{L}{a}))!]" class="latex" /> 

And we get something useful!

Some follow up questions:

  1. Given the internal energy equation U = TS + W (where W is work), find U.
  2. Find the chain length L as a function of T, U, and<img src="//s0.wp.com/latex.php?latex=%5Cwidetilde%7BN%7D&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="&#92;widetilde{N}" title="&#92;widetilde{N}" class="latex" /> given<img src="//s0.wp.com/latex.php?latex=dU+%3D+TdS+%2B+%5Ctau+dL&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="dU = TdS + &#92;tau dL" title="dU = TdS + &#92;tau dL" class="latex" /> where<img src="//s0.wp.com/latex.php?latex=%5Ctau&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="&#92;tau" title="&#92;tau" class="latex" /> is the tension (in this case equivalent to the gravitaitonal force mg)
  3. Does the chain obey Hooke&#8217;s law? If so, what is the value of the stiffness constant?