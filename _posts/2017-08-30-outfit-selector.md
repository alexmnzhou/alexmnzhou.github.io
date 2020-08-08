---
id: 1032
title: A Python Script to Pick Me Outfits Based on the Weather
date: 2017-08-30T20:11:01+00:00
author: Alex Z.
layout: post
guid: https://www.physicstomato.com/?p=1032
permalink: /outfit-selector/
views:
  - 1614
wp_featherlight_disable:
  - 
post_views_count:
  - 32
wpb_post_views_count:
  - 4
image: /wp-content/uploads/2017/08/outfit-selector-screenshot-1.png
categories:
  - Executables
  - Idea Space
---
<span class="wpsdc-drop-cap">T</span> here’s a well-supported theory in psychology called “decision fatigue,” which predicts that your decision-making ability goes down as you’re forced to make more decisions throughout a day. As a real life example, in supermarkets, candy and processed snacks are regularly placed near the cash register* to take advantage of your decision fatigue after a long stint <span style="font-weight: 400;">of making decisions on which groceries to buy.</span><figure id="attachment_1112" aria-describedby="caption-attachment-1112" style="width: 187px" class="wp-caption alignright">

<img class="wp-image-1112" style="background-color: transparent; text-align: inherit; color: #1a1a1a; font-size: 16px;" src="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/08/grocery-checkout-line_mainthumb.jpeg?resize=187%2C124&#038;ssl=1" alt="" width="187" height="124" srcset="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/08/grocery-checkout-line_mainthumb.jpeg?w=640&ssl=1 640w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/08/grocery-checkout-line_mainthumb.jpeg?resize=300%2C199&ssl=1 300w" sizes="(max-width: 187px) 85vw, 187px" data-recalc-dims="1" /> <figcaption id="caption-attachment-1112" class="wp-caption-text">*Pictured here: the culprit (Also: an <a href="http://www.nytimes.com/2011/08/21/magazine/do-you-suffer-from-decision-fatigue.html" target="_blank" rel="noopener noreferrer">interesting read</a> on decision fatigue&#8217;s role in day-to-day life).</figcaption></figure> 

On a similar note, there are actually many examples of powerful politicians and businessmen reducing their wardrobes down to a few or even just one outfit in order to minimize the amount of trivial decisions that have to be made throughout a day—think Steve Jobs or Mark Zuckerberg in their simple, iconic garbs.

<span style="font-weight: 400;">As former president Barack Obama said of his famously slim wardrobe, “You’ll see I wear only gray or blue suits. I’m trying to pare down decisions. I don’t want to make decisions about what I’m eating or wearing, because I have too many other decisions to make.”</span>

<span style="font-weight: 400;">A few years ago, I (still in my early teens) was probably most concerned with two things in my life:</span>

<li style="list-style-type: none;">
  <ol>
    <li style="font-weight: 400;">
      <span style="font-weight: 400;">How I looked (and by extension, what I was wearing).</span>
    </li>
    <li style="font-weight: 400;">
      <span style="font-weight: 400;">Feeling like I made good decisions (emphasis on &#8220;feeling&#8221;).</span>
    </li>
  </ol>
</li>

<span style="font-weight: 400;">But decision fatigue seems to indicate that these two goals are incompatible; if I really wanted to stop wasting mental energy on picking out an outfit every morning, I should’ve just adopted a uniform to wear daily, like Barack or Steve. When</span> I thought about it though, I _really_ didn’t like the idea of wearing the same thing every day, or even outfits from the same, small set of clothes (i.e. a “capsule” wardrobe). Still, I also wasn’t about to just give up on trying to rid myself of my clothing-based decision fatigue.

<span style="font-weight: 400;">The clear compromise was to get my computer to do so for me; every morning, instead of laboring over what to wear, I would load up a program that spits out an outfit or a few on the daily, down to the smallest accessory. I’d follow it without question, and so (presumably) would never again have to painstakingly consider what to put on my body in the morning. This is what passed for a good idea in the mind of 15-year-old me.</span>

<span style="font-weight: 400;">The thing is, I actually ended up (mostly) finishing the project. And while I don’t ever really use it anymore, I figured it would be a fun thing to share and pick apart today (The file is <a class="download-link" title="" href="https://www.physicstomato.com/download/1500/" rel="nofollow"> here (228 downloads) </a>if you want it, and the spreadsheet required to run it <a class="download-link" title="" href="https://www.physicstomato.com/download/1503/" rel="nofollow"> here (185 downloads) </a>– You&#8217;ll also need <a href="https://github.com/csparpa/pyowm" target="_blank" rel="noopener noreferrer">PyOWM</a>).<br /> </span>

<span style="font-weight: 400;">Let’s take a look.</span>

### Moods and Weather

* * *

<span style="font-weight: 400;">Before picking outfits at random, it seems reasonable that we would need to “prune” the potential list based on a few categories. Weather was the first and most obvious; if it was 90 degrees outside in LA, I better not be recommended to wear a parka and ski pants.</span>

<span style="font-weight: 400;">Luckily, for the weather, we can use the free Open Weather Map API (OWM) along with a wrapper for Python called PyOWM for easy interfacing with the local weather data. OWM is a commercial API designed mostly for business or agricultural use, so it was fun letting them know exactly what I planned on using <em>my</em> API key for:</span><figure id="attachment_1047" aria-describedby="caption-attachment-1047" style="width: 604px" class="wp-caption alignnone">

[<img class="wp-image-1047" title="Ah, the good old days of 50 tabs and Spotify open." src="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/08/received_1366189136765850-1.png?resize=604%2C339&#038;ssl=1" alt="" width="604" height="339" srcset="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/08/received_1366189136765850-1.png?w=1920&ssl=1 1920w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/08/received_1366189136765850-1.png?resize=300%2C169&ssl=1 300w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/08/received_1366189136765850-1.png?resize=768%2C432&ssl=1 768w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/08/received_1366189136765850-1.png?resize=1024%2C576&ssl=1 1024w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/08/received_1366189136765850-1.png?resize=1200%2C675&ssl=1 1200w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/08/received_1366189136765850-1.png?w=1680&ssl=1 1680w" sizes="(max-width: 709px) 85vw, (max-width: 909px) 67vw, (max-width: 984px) 61vw, (max-width: 1362px) 45vw, 600px" data-recalc-dims="1" />](https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2017/08/received_1366189136765850-1.png?ssl=1)<figcaption id="caption-attachment-1047" class="wp-caption-text">I think this image sums up my early teenage years pretty handily.</figcaption></figure> 

<span style="font-weight: 400;">The other important category was something I called “mood,” which was supposed to be the </span>_<span style="font-weight: 400;">feeling</span>_ <span style="font-weight: 400;">you wanted out of your clothes that day (outfits could encompass multiple moods).</span>

<span style="font-weight: 400;">My four preselected “moods” were: </span>

<li style="list-style-type: none;">
  <ol>
    <li style="font-weight: 400;">
      <span style="font-weight: 400;">Cool (Default, daily-driver outfits)</span>
    </li>
    <li style="font-weight: 400;">
      <span style="font-weight: 400;">Sexy (For when I’m feeling extra</span><span style="font-weight: 400;"> confident)</span>
    </li>
    <li style="font-weight: 400;">
      <span style="font-weight: 400;">Cozy (Comfortable and lazy)</span>
    </li>
    <li style="font-weight: 400;">
      <span style="font-weight: 400;">Fancy (Anything from business casual to a full on suit-and-tie ensemble)</span>
    </li>
  </ol>
</li>

<span style="font-weight: 400;">So the user-input loop would have you select a mood and then automatically find the weather in your city for that day. It would then take the list of outfits at the intersection of those two categories and pick a few at random.</span>

<span style="font-weight: 400;">If you’re curious, the input loop looked like this:</span>

<pre class="prettyprint">while 1:
    category_choice = input("Today I'm feeling... 1)Cool 2)Sexy 3)Cozy 4)Fancy 5|Other Options ")
    if category_choice in accepted_in:
        choice = category_list[int(category_choice) - 1]
        break
    elif category_choice == '5':
        while 1:
            option_choice = input("Other Options: 1)Themes 2)Add an Outfit 3)Force Weather 4)Back to Selection ")
            if option_choice == '4':
                break
            elif option_choice in accepted_in:
                while 1:
                    if option_choice == '3':
                        force_temp = True
                        try:
                            temp = float(input("What is the temperature (high) for today (in fahrenheit)? "))
                        except:
                            ("Oops. Enter a valid number.")
                        break
                #outfitter()
                #themer
            else:
                print("Oops! Enter '1', '2', '3', or '4'")
                continue
    else:
        print("Oops! Enter '1', '2', '3', or '4'")
        continue</pre>

<span style="font-weight: 400;">(&#8220;Outfitter&#8221; was supposed to be the function for adding new outfits, but I never got around to implementing that. The &#8220;themer&#8221; function is in the code, but not put into the loop here. &#8220;Force weather&#8221; lets you manually set the weather, if you want to wear cold weather clothes in hot weather for some inexplicable reason)</span>

<span style="font-weight: 400;">And the PyOWM “weather finder” looked like this:</span>

<pre class="prettyprint">#Takes input in degrees and outputs the array truncated by temperature. Prints the weather category.

def select_by_degrees(degrees,categ_array):
    if degrees &gt;= 90:
        weather_array = categ_array[categ_array['Weather_value'] &gt;= 3]
        print("Today is hot! (~%.1f F\xb0)" %degrees)
    elif degrees &gt;= 70:
        weather_array = categ_array[(categ_array['Weather_value'] &gt;= 1) & (categ_array['Weather_value'] &lt;= 4)]
        print("Today has fair weather. (~%.1f F\xb0)" %degrees)
    else:
        weather_array = categ_array[(categ_array['Weather_value'] &lt;= 1) | (categ_array['Weather_value'] == 3)]
        print("Today is cold... (~%.1f degrees F\xb0)" %degrees)
    return(weather_array)</pre>

(This is what prunes the full outfit array into only those that can &#8220;work&#8221; in the right temperature. Degrees are in fahrenheit.)

<pre class="prettyprint">#OWM implementation uses Open Weather Map API to find today's forecast for East LA. Manual input if cannot be accessed (e.g. no WiFi connection).

def select_by_inputs(categ_array):
    try:
        owm = OWM('0d68d0be097dc01d8a14a1ff41785d03', version= '2.5')
        fc = owm.daily_forecast(city, limit = 1) 
        f = fc.get_forecast()
        #print(f.get_weathers)
        w = f.get_weathers()[0]
        #print(w.get_temperature)
        if force_temp == False:
            temp = (float(w.get_temperature('fahrenheit')['max'])+5)
        rain = fc.will_have_rain()
        if rain == True:
            print("Rainy day! Bring an umbrella.")
    except:
        while 1:
            try:
                temp = float(input("What is the temperature (high) for today? (in fahrenheit) "))
                break
            except:
                print("Oops! Enter a number.")
                continue
    weather_array = select_by_degrees(temp, categ_array)
    return list(weather_array['Outfits'])</pre>

(This is the OWM implementation, courtesy of PyOWM. The &#8216;0d68d0be097dc01d8a14a1ff41785d03&#8217; is my API key. I&#8217;d recommend that you generate your own key if you download this code to try it, but you don&#8217;t _have_ to. An extensive PyOWM documentation can be found at its GitHub at the link above.)

### **Design Philosophy**

* * *

<span style="font-weight: 400;">I initially toyed with the idea of having each piece of an outfit be put together at random, and even a neural network that learned over time which pieces go with each other. Neither idea seemed very good or tenable, so I went with user-defined, static outfits instead. Each outfit would be stored in a spreadsheet, along with a few variables to define its “categories.”</span>

<span style="font-weight: 400;">I had a column for each mood, with ones and zeros telling whether it fit those moods or not, and another column for a “weather value,” which encoded the temperature ranges it could be worn in.</span>

<span style="font-weight: 400;">The spreadsheet looked something like this:</span><figure id="attachment_1087" aria-describedby="caption-attachment-1087" style="width: 583px" class="wp-caption alignnone">

[<img class="wp-image-1087 " title="Also ignore &quot;Kdrama.&quot; We all have phases." src="https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/08/Capture.png?resize=583%2C199&#038;ssl=1" alt="" width="583" height="199" srcset="https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/08/Capture.png?w=1024&ssl=1 1024w, https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/08/Capture.png?resize=300%2C102&ssl=1 300w, https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/08/Capture.png?resize=768%2C262&ssl=1 768w" sizes="(max-width: 583px) 85vw, 583px" data-recalc-dims="1" />](https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2017/08/Capture.png?ssl=1)<figcaption id="caption-attachment-1087" class="wp-caption-text">Honestly, I&#8217;d still wear a lot of these</figcaption></figure> 

<span style="font-weight: 400;">And the temperature column values break down like this:</span>

0) Cold weather only  
1) Cold and fair weather  
2) Fair weather only  
3) All weather  
4) Fair and hot weather  
5) Hot weather only

<span style="font-weight: 400;">Six values to represent all distinct, reasonable combos of 3 broad types of weather (because clothes that only work in hot and cold but not fair weather isn&#8217;t reasonable).</span>

I started adding the option for “themes”—special outfit types that only really work during a specific time: Christmas/Holiday parties, going to a rock concert, blacklight parties, etc. I didn’t really get to adding a lot of themes, but the code is in there and working.

<span style="font-size: 23px; font-weight: 900;">Planned Features</span>

* * *

<span style="font-weight: 400;">I planned a lot of features that I never actually finished. For example, the ability to add or delete new outfit entries through the program, instead of editing the spreadsheet directly. This was tricky to do using Pandas, the data array editing module I used.</span>

Another feature I wanted to add was a way to count how many times I wore a certain outfit. Then, each time I wore an outfit, it would add to each of the garments&#8217; &#8220;wear count.&#8221; At the end of every year, I&#8217;d find out which clothes I wore the least (or not at all) and get rid of those. Again, editing spreadsheets though Pandas proved difficult, and I never got around to it before I decided that using the outfit selector daily was too tedious.

Even with my planned features, I&#8217;m not all too sure about how useful the program would be (To be fair, I also just like the fun of picking out clothes in the morning). The counter for cleaning out your closet annually sounds useful, but you could do so just as easily with a notepad and paper, or even an online note taker. Combined with an automatic outfit selector, though, it may prove to be useful (provided you remember to run it every morning).

But there are just too many situations where I&#8217;d want total control of what I wear: an interview, seeing old friends, a house party, a night out, etc., for me to rely on the program to count _everything_—though things might be different if you could increase the count manually.

On second thought, it&#8217;s quite possible I&#8217;m wrong about this program and those like it. Download it, edit it, and try it out for yourself. Maybe you can find a practical use for automatic outfit selection where I couldn&#8217;t.

As always: Have at it, and tell me how it goes.