---
id: 2493
title: Calculating the Nutritional Content of Popular Online Recipes
date: 2019-09-28T22:21:00+00:00
author: Alex Z.
layout: post
guid: https://www.physicstomato.com/?p=2493
permalink: /recipe-nutrition/
wp_featherlight_disable:
  - 
views:
  - 25
image: /wp-content/uploads/2020/05/Recipes-Meta-1200x675.jpg
categories:
  - Executables
  - Idea Space
tags:
  - code
  - nutrition
---
I just started business school at Duke University two months ago, and it’s been fantastic. I’ve made some great friends, and there are lots of events for my program as well as fun things to do in Durham.

Our program, the Master of Quantitative Management (MQM), recently hosted its Summer Data Competition. The basic idea was to produce an interesting _data set_ (ostensibly not including any insights taken from it) using any means available. We&#8217;d be judged on criteria like originality, cleverness, and usability/potential for insights – of course, demonstrating that potential means performing at least some analysis yourself&#8230;

An entry I made with my friend [Mayank](https://www.linkedin.com/in/mayank-tulsiani/) ended up making it into the finals. I thought the idea was awesome. Here&#8217;s what we did:

## Premise

<div class="wp-block-image">
  <figure class="aligncenter size-large is-resized"><img src="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2020/05/Recipes-Meta-graph.jpg?fit=840%2C473&ssl=1" alt="" class="wp-image-2497" width="632" height="355" srcset="https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2020/05/Recipes-Meta-graph.jpg?w=1920&ssl=1 1920w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2020/05/Recipes-Meta-graph.jpg?resize=300%2C169&ssl=1 300w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2020/05/Recipes-Meta-graph.jpg?resize=1024%2C576&ssl=1 1024w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2020/05/Recipes-Meta-graph.jpg?resize=768%2C432&ssl=1 768w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2020/05/Recipes-Meta-graph.jpg?resize=1536%2C864&ssl=1 1536w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2020/05/Recipes-Meta-graph.jpg?resize=1200%2C675&ssl=1 1200w, https://i2.wp.com/www.physicstomato.com/wp-content/uploads/2020/05/Recipes-Meta-graph.jpg?w=1680&ssl=1 1680w" sizes="(max-width: 709px) 85vw, (max-width: 909px) 67vw, (max-width: 984px) 61vw, (max-width: 1362px) 45vw, 600px" /><figcaption>&#8220;Pick <em>two.</em>&#8220;</figcaption></figure>
</div>

Like many, I’ve been trying to maintain a good diet for the past year or so, and I’ve come to notice an inescapable dilemma for all healthy eaters. Basically, you can eat cheaply, eat healthily, or eat out. Pick _two_.&nbsp;

Students/early career folks like me generally end up sacrificing the convenience and time savings of having someone else make our meals in favor of cost savings. 

If we’re lucky, we also get to maintain our overall health. It’s obviously not guaranteed you even get two of them. The broke college student chowing down on instant ramen every night is a cliche for a reason.

There are a plethora of reasons as to why it can be difficult to cook for yourself all the time, especially when you’re low on ingredients, money, or you have to follow some specific diet or nutritional guidelines.&nbsp;But that&#8217;s no good.

A lack of easily accessible basic nutritional information for common recipes should never be a reason to sacrifice your health. I thought with some simple transformations it would be possible to get nutritional information for recipes online.

## Introduction

Our dataset focuses on the nutritional profiles of publicly available food and drink recipes on various popular culinary websites; we chose to focus on US-based recipe catalogues to avoid language confusion and to ensure a stronger cultural grasp of the recipes we studied.

The record is arranged into 976 rows and 19 columns, with each row corresponding to a given recipe entry. Five columns are reserved for recipe metadata (e.g. title, average rating, url, etc), and the remaining are nutrition based. We used the USDA Food Composition Databases API to access nutritional information for each ingredient, then applied natural language processing techniques to parse the units of measurement according to each recipe – think pounds, cups, teaspoons, or grams – and converted each to a standard that the API could retrieve.

## Data Acquisition

While the data acquisition process was relatively straightforward in principle, our team had to overcome significant logistical hurdles to obtain the recipe data and convert it to useful nutritional information.

First, we needed to design a web crawler that found directories in target websites that matched a particular signature pointing only to recipe pages. For most of the sites we tested, the recipe websites had a “recipe” in their url path that made this distinction obvious. We used [dirhunt](https://github.com/Nekmo/dirhunt), a command-line open source site analyzer that attempts to compile all directories while minimizing requests to the server (Nekmo).

<div class="wp-block-image">
  <figure class="aligncenter size-large is-resized"><img src="https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2020/07/Screen-Shot-2019-09-25-at-3.22.05-PM.png?resize=604%2C390&#038;ssl=1" alt="" class="wp-image-2524" width="604" height="390" srcset="https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2020/07/Screen-Shot-2019-09-25-at-3.22.05-PM.png?resize=1024%2C663&ssl=1 1024w, https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2020/07/Screen-Shot-2019-09-25-at-3.22.05-PM.png?resize=300%2C194&ssl=1 300w, https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2020/07/Screen-Shot-2019-09-25-at-3.22.05-PM.png?resize=1200%2C777&ssl=1 1200w, https://i0.wp.com/www.physicstomato.com/wp-content/uploads/2020/07/Screen-Shot-2019-09-25-at-3.22.05-PM.png?w=1278&ssl=1 1278w" sizes="(max-width: 709px) 85vw, (max-width: 909px) 67vw, (max-width: 984px) 61vw, (max-width: 1362px) 45vw, 600px" data-recalc-dims="1" /><figcaption>Here&#8217;s what &#8220;dirhunt&#8221; looks like in action. There&#8217;s a lot of blog posts/stories we don&#8217;t want, but we can filter out the second to last URL sections that include &#8220;recipe&#8221; to get actual recipes we can use!</figcaption></figure>
</div>

Next, we needed to scrape the data from each recipe URL. We settled on using [recipe-scrapers](https://github.com/hhursev/recipe-scrapers), an open-source Python package for gathering basic data from popular recipe site formats (hhursev). This package gave us access to the recipe titles, average ratings, and ingredient lists, among other important data.

Critically, the ingredients were formatted as a Python list of strings in their raw delineation. For instance, one item could look like “1 1/2 cups unbleached white flour”. We needed to first convert the “1 1/2” into a proper floating point, as well as change all measurements into the standard grams that the USDA nutritional database requires. Python offers a “fraction” package for converting strings of fractions into floating point numbers, as well as a “word2number” package for converting strings of numbers (e.g. “three” to 3).

We wrote a lookup table for converting all masses into grams, as well as all volumes into grams based on the ingredient type. For volume-based ingredients not found in our lookup table, the script defaulted to using the conversion factor for water (approx. 240 grams per cup), which proved to be a close estimate for a wide range of food types.

Finally, we used the Food Composition Databases API to search for these ingredients and obtain nutritional data. The API allows for searching with natural language, though some foods were still impossible to find through the API; we discarded any recipes that had untraceable ingredients. The request limit on this API meant that we were realistically limited to a few hundred recipes per site for our final dataset; we decided to spread relatively evenly over the sites to include a wide range of recipe influences.

## Dataset Description

Recipes-Meta is a database of recipes scraped from popular websites with computed detailed nutrition data taken from USDA for each ingredient to potentially help consumers make more informed eating choices and offer insights in the relationships between ingredients, nutrients, and site visitor opinions. Each row is a recipe entry that can be uniquely referenced by its URL.

**Columns:**

**<span class="has-inline-color has-bright-blue-color">Title: </span>**Name of recipe&nbsp;  
**<span class="has-inline-color has-bright-blue-color">Rating:</span>** Average rating of recipe as given by users (some sites do not have this feature)  
**<span class="has-inline-color has-bright-blue-color">URL:</span>** Web address of the recipe (unique/primary key)  
**<span class="has-inline-color has-bright-blue-color">Servings:</span>** Number of people the recipe serves, i.e. serving size (nutrition data is divided by this)  
**<span class="has-inline-color has-bright-blue-color">Ingredients:</span>** List of ingredients in the recipe  
**<span class="has-inline-color has-bright-red-color">Energy (kcal):</span>** Total calories of the recipe per serving in kcal  
**<span class="has-inline-color has-bright-red-color">Carbohydrate, by difference (g):</span>** Total carbohydrates of the recipe per serving in g**  
<span class="has-inline-color has-bright-red-color">Protein (g):</span>** Total protein of the recipe per serving in g**  
<span class="has-inline-color has-bright-red-color">Calcium, Ca (mg):</span>** Total calcium of the recipe per serving in mg**  
<span class="has-inline-color has-bright-red-color">Cholesterol (mg):</span>** Total cholesterol in the recipe per serving in mg**  
<span class="has-inline-color has-bright-red-color">Fatty acids, total saturated (g):</span>** Total saturated fat of the recipe per serving in g**  
<span class="has-inline-color has-bright-red-color">Fatty acids, total trans (g):</span>** Total trans fats of the recipe per serving in g**  
<span class="has-inline-color has-bright-red-color">Fiber, total dietary (g):</span>** Total dietary fibre of the recipe per serving in g**  
<span class="has-inline-color has-bright-red-color">Iron, Fe (mg):</span>** Total iron content of ingredients used in the recipe per serving in mg**  
<span class="has-inline-color has-bright-red-color">Sodium, Na (mg):</span>** Total sodium of ingredients used in the recipe per serving in mg**  
<span class="has-inline-color has-bright-red-color">Sugars, total (g): </span>**Total sugar content of recipe per serving in g**  
<span class="has-inline-color has-bright-red-color">Total lipid (fat) (g): </span>**Total lipids/fats of the recipe per serving in g  
**<span class="has-inline-color has-bright-red-color">Vitamin A, IU (IU): </span>**Total Vitamins A of the recipe per serving in IU**  
<span class="has-inline-color has-bright-red-color">Vitamin C, total ascorbic acid (mg): </span>**Total Vitamin C of the recipe per serving in mg

  * <span class="has-inline-color has-bright-red-color"><strong>Red</strong></span> indicates nutrition related data
  * <span class="has-inline-color has-bright-blue-color"><strong>Blue</strong></span> indicates recipe related recipe related data

## Potential Insights

There exists a critical gap between growing consumer demand for health-conscious eating options and readily available nutrition data for recipes online. Most consumers looking to eat balanced, tasty, and affordable meals while meeting their health goals must eventually learn to cook their own meals. However, convenient data to make informed choices for recipe-based meal planning does not exist for most popular recipe sources online.

We also noticed that the few websites that do show nutrition data for their recipes are geared towards consumers that already follow a diet plan or practice healthy eating as a part of their lifestyle. Further, these websites are often limited in scope, including only a small set of specific recipe choices or community-generated recipes from a small user base.

Considering that access to healthy eating options and food education in America is growing increasingly unequal, our approach to spreading awareness about nutrition aims to target the ‘common man’ or general public (Hiza et al.). This requires us to access nutrition data for a wide range of popular websites, rather than the few that readily offer this information. While our algorithm is not perfect, it can serve as a starting point and proof-of-concept for similar endeavours in the future.

We suggest the following potential insights, though there are many more viable routes for analysis:

  1. Determine if “healthiness”/nutrition stats relate to the **average rating** of recipes.&nbsp;
  2. Generate a **custom list** of recipes that fit a specific range of macronutrients (protein/carbs/fats).
  3. Define overall **nutrition metrics** in all recipes, for example, to find meals that have an especially high protein to calorie ratio.
  4. Check if recipes that include certain ingredients tend to be more or less healthy.
  5. Analyze which websites tend to post **healthier** and/or **more well balanced** recipes.
  6. Produce a **nutritional ranking** of all recipes according to their adherence to USDA guidelines (or some other metric).
  7. **Flag recipes** with especially high sugar, fat content, trans fat or cholesterol content and make this flag obvious if and when it is retrieved.
  8. Write an algorithm that generates customized eating plans that meet daily nutritional requirements.

For a more business oriented goal, this data could be integrated with personalised consumer-level data to design customized eating plans that follow individual nutritional requirements based on height, age, weight, BMI, or other factors. There are surely many interesting possibilities we did not discuss in this report. Happy hacking.

## Sources

Hiza, Hazel A.B. et al. “Diet Quality of Americans Differs by Age, Sex, Race/Ethnicity, Income, and Education Level”. _Journal of the Academy of Nutrition and Dietetics_, Volume 113, Issue 2, 297 &#8211; 306.

hhursev. “recipe-scrapers – Python package for scraping recipes data”. _Github Repository_, 2019, <https://github.com/hhursev/recipe-scrapers>.

Nekmo. “Dirhunt – Find web directories without bruteforce”. _Github Repository_, 2019, <https://github.com/Nekmo/dirhunt.>

**Recipe websites referenced:**

<https://allrecipes.com/>

<https://epicurious.com/>

<https://seriouseats.com/>