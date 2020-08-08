---
id: 1339
title: Introduction to Thermostatistics and Macroscopic Coordinates
date: 2017-09-28T20:57:37+00:00
author: Alex Z.
layout: post
guid: https://www.physicstomato.com/?p=1339
permalink: /thermostatistics-intro/
wp_featherlight_disable:
  - 
views:
  - 123
categories:
  - Thermodynamics
---
### A Coarse Description of Physics

* * *

<span style="font-weight: 400;">Thermostatistics lies at the intersection of thermodynamics and statistical mechanics. Thermodynamics is the study of the movement of heat and energy and the heat and energy of movement. On the other hand, statistical mechanics is a branch of theoretical physics that applies principles of probability theory to study the average behavior of a system when it would be difficult to apply more direct methods (as is often the case in thermodynamics).</span>

<span style="font-weight: 400;">Statistical mechanics is kind of remarkable when you consider how people use its conceptual framework—averaging the useful properties of complex systems—on the daily. Here’s an example paraphrased from my <a href="https://www.goodreads.com/book/show/183469.Thermodynamics_and_an_Introduction_to_Thermostatistics" target="_blank" rel="noopener">study book</a>: imagine going to the drug store to purchase a liter of isopropyl alcohol. For the situation at hand, this simple, volumetric specification is pragmatically sufficient. Yet, at the atomic level, we have actually specified very little. </span>

<span style="font-weight: 400;">The container which you actually want is one filled with some 8 septillion molecules of CH₃CHOHCH₃. To completely characterize the system in the mathematical formalism, you would need the exact coordinates and velocities of every atom in the system, as well as a menagerie of variables describing the bonds, internal states, and energies of each—altogether </span>_<span style="font-weight: 400;">at least</span>_ <span style="font-weight: 400;">in the order of </span><span style="font-weight: 400;">10<sup>25</sup> numbers to completely describe that thing you were able to specify earlier by just asking for &#8220;a liter&#8221; of alcohol!</span>

<span style="font-weight: 400;">Yet somehow, among all those 10<sup>25</sup> coordinates and velocities and energies and state variables, every single one, save for a few,</span>_ <span style="font-weight: 400;">is totally irrelevant</span>_ <span style="font-weight: 400;">to describe the macroscopic system. The few that emerge as relevant are what we refer to as </span>_<span style="font-weight: 400;">macroscopic coordinates</span>_ <span style="font-weight: 400;">or thermodynamic coordinates.</span>

<span style="font-weight: 400;">The key to this macroscopic simplicity is threefold:</span>

<li style="font-weight: 400;">
  <span style="font-weight: 400;">Macroscopic measurements are extremely slow at the atomic scale of time.</span>
</li>
<li style="font-weight: 400;">
  <span style="font-weight: 400;">Macroscopic measurements are extremely coarse at the atomic scale of distance.</span>
</li>
<li style="font-weight: 400;">
  <span style="font-weight: 400;">The scope of macroscopic measurement is just about the scope of what is useful to human beings doing normal human things.</span>
</li>

<span style="font-weight: 400;">For example, to determine the size of an object too far from you to measure directly, you might take a photograph of the object with a reference scale. The speed at which this measurement takes place is determined by your camera’s shutter speed, an action in the order of hundredths of a second. On the other hand, the kinetic motion and vibration of particles at the surfaces of the object, which are constantly at work altering its observable size, act in the order of 10<sup>-15</sup> seconds</span><span style="font-weight: 400;">.</span>

<span style="font-weight: 400;">Macroscopic observation can never respond to such minute action. At best, under ideal circumstances, we can consistently detect macroscopic quantities of microprocesses in the range of 10<sup>-7</sup> seconds. As such, only those combinations of coordinates that are relatively <em>time-independent</em> are macroscopically useful. </span>

<span style="font-weight: 400;">The word “relatively” is an important qualifier here. While we can measure processes in time quite “finely” relative to discernable human experience, it is still far from the atomic scale of 10<sup>-15</sup> seconds.</span>

<span style="font-weight: 400;">It seems rational, then, to construct a theory to describe all the relationships of the time-independent phenomena of macroscopic systems. </span>_<span style="font-weight: 400;">Such a theory is called thermodynamics.</span>_

<span style="font-weight: 400;">In considering the few coordinates that are time-independent, some obvious candidates arise: quantities constrained by the conservation laws, like total energy or angular momentum, are clearly properties that are unaffected by time. </span>

<span style="font-weight: 400;">We’ll soon find that there are many more relatively time-independent coordinates dealt with in the broad scope of thermodynamics and thermostatistics.</span>

### The Thermodynamic Definition of Heat

* * *

<span style="font-weight: 400;">Of the ludicrous amount of atomic coordinates, we&#8217;ve found that only a few combinations with some unique symmetry properties can survive the merciless averaging associated with transitioning to a macroscopic description. Some “surviving” coordinates prescribe mechanical properties, like volume or elasticity. Others are electrical, like the electric and magnetic dipole moments, various multipole moments, etc. Under this description, we can rewrite broad areas of physics according to which macroscopic coordinates they focus on.</span>

<span style="font-weight: 400;">Classical mechanics is then the study of one closely related set of surviving atomic coordinates. Electromagnetism is the study of another set of surviving coordinates. Thermodynamics and thermostatistics, on the other hand, are concerned with those numerous atomic coordinates that, by virtue of the coarseness of macroscopic measurement,</span>_ <span style="font-weight: 400;">are not defined explicitly</span>_ <span style="font-weight: 400;">in the macroscopic description of a system.</span>

<span style="font-weight: 400;">To illustrate, one of the most evident consequences of these “hidden” coordinates is found in energy. Energy transferred mechanically (i.e. associated with a mechanical macroscopic coordinate) is called “mechanical work,” and its macroscopic consequences are extensively treated in other areas of physics. Energy that is transferred electrically is called “electrical work,” and so on and so forth.</span>

<span style="font-weight: 400;">Notice however, that it’s just as possible for energy to transfer through the motions </span>_<span style="font-weight: 400;">hidden from macroscopic measuremen</span>_<span style="font-weight: 400;"><em>t</em> compared to the ones that are easily observable. </span>_Energy transfer that occurs through these hidden modes is called heat._

<span style="font-weight: 400;">(Of course, this definition serves only to aid with situating heat within the macroscopic coordinate framework. We’ll soon get a more adequate working definition—basically, a mathematically sound one—to use in our studies)</span>

<span style="font-weight: 400;">So what do you say? Are we ready now for some calculations?</span>