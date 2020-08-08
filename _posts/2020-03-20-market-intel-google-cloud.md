---
id: 2360
title: How to Use SEC Filings in Market Intelligence – A Case Study for Google Cloud
date: 2020-03-20T15:49:00+00:00
author: Alex Z.
layout: post
guid: https://www.physicstomato.com/?p=2360
permalink: /market-intel-google-cloud/
views:
  - 117
wp_featherlight_disable:
  - 
image: /wp-content/uploads/2020/04/media_bf4_bf482d09-2453-40e2-be9b-f8395717f5b4_phpI8Z7Lc.png
categories:
  - Idea Space
tags:
  - code
  - hackathon
  - market intelligence
---
The Technical Infrastructure at Google Cloud team recently came to our school with a question about the scale of its biggest competitor, Amazon Web Services (AWS). 

To summarize, Amazon recently swapped out the depreciation schedule of its servers from 3 years to 4 years, [straight line](https://www.investopedia.com/terms/s/straightlinebasis.asp). This is a big deal since extending a depreciation schedule means significantly less reported expenses each quarter while that change takes effect. Specifically, they reported [$800 million](https://www.fool.com/investing/2020/02/04/how-an-accounting-tweak-will-make-amazons-most-pro.aspx) for the next quarter alone.

It turns out you could actually work out a lot about Amazon&#8217;s server spending by just crunching some numbers over the past 3 years. In short, you could estimate the portion of capital expenditures allocated to servers by calculating what spending schedule would sum to the $800 million figure (assuming that the depreciation change was implemented). Sound complicated? Read ahead, it&#8217;s easier than you think.

So here&#8217;s the $800 million accounting question: From that figure and other publicly available data (SEC filings, earnings statements, industry reports, etc.), would it be possible to reverse engineer how much Amazon spends on their servers, and thus, get an idea of how many they currently have in their fleet?

This problem was the impetus for our school hosting a 6-hour hackathon with Google to see who could come up with the best answer. We eventually took home the prize (go team Lime Green)! Here&#8217;s what we did.

## Theory & Background

Why does Google want this info? A good estimate of AWS&#8217;s scale could help a competitor understand where they stand in terms of theoretical capacity (not just market share), how they compare in spending, and make predictions of an approximate rate of expansion through a time series.

In turn, AWS is [fairly secretive](https://www.theatlantic.com/technology/archive/2016/01/amazon-web-services-data-center/423147/) about exactly how many servers they have and where their data centers are even located. I mean, why wouldn&#8217;t they be?

Despite this, we can derive a pretty good estimate using figures from their SEC reports and, crucially, that figure they released in their most recent [earnings call](https://www.fool.com/earnings/call-transcripts/2020/01/31/amazoncom-inc-amzn-q4-2019-earnings-call-transcrip.aspx) (the $800 million effect). If we set that as a constant, we can do some fancy Excel math to work backward and approximate each quarter&#8217;s spending on servers. From there, we can estimate the server fleet size by dividing that spending by cost-per-server. 

It&#8217;s far from perfect, but it&#8217;s not a bad method for uncovering market intelligence intended to be kept hidden using widely available data. Here&#8217;s the idea:

  1. Using past [10-Q reports](https://ir.aboutamazon.com/quarterly-results/default.aspx), scrape Amazon&#8217;s capital expenditures (CapEx) for the past 3 years/12 quarters. The idea here is that server spending will fall under CapEx, but the breadth of that category usually &#8220;hides&#8221; it with other expenses.
  2. Calculate how much each quarter&#8217;s depreciation expense would be affected by the change in schedule. e.g. if it was purchased just last quarter, it would change from the total 3 to 4 years remaining or 12 to 16 quarters. If two quarters ago, then it would change from 11 to 15 quarters, and so on.
  3. Make an assumption about relative spending. There&#8217;s too many unknowns since we don&#8217;t know what portion was spent on servers _within each quarter_. The simplest is to assume that the percent CapEx allocated to servers is constant. There are other possibilities, though adjusting this parameter doesn&#8217;t turn out to be that important compared to the other assumptions.
  4. Finally, determine a moving estimate of the average server cost for a firm like Amazon based on various assumptions (how long servers last, OEM server manufacturer averages, how long it takes to expense them, potential fixed costs, where/how AWS servers are manufactured, etc) and market trends adjustede for each year. Divide and get an estimate for server fleet size. Done!

## Writeup

Okay, let&#8217;s see it in action. What follows is a slightly edited version of the deliverable that won us the hackathon. If you want to follow the modeling aspect, you&#8217;ll also need this 
	<a class="download-link" title="" href="https://www.physicstomato.com/download/2405/" rel="nofollow"> excel sheet (28 downloads) </a>.

We only had six hours to write in the actual competition, but we had the chance to refine some things afterward in preparation for a presentation with the Google Cloud team. There&#8217;s also extra considerations like subtracting the cost of server racks and adjusting for DRAM prices (the main cost-driver of servers):

#### **Estimating the Scale of Amazon’s Server Operation**

_A Market Intelligence Report based on SEC Filings, Earnings Statements, Industry Reports, and Other Public Information_

<hr class="wp-block-separator" />

Submitted for Consideration in the 2020 MQM Forensics Hackathon

**Team Lime Green – _Shay Xueyao Fu, Shangyun Song, Yingli Sun, and Alex Zhou_**

### **What We Know**

<hr class="wp-block-separator is-style-wide" />

Amazon recently extended the depreciation schedule of its servers from a straight-line 3 years schedule to 4 years, which will result in an [$800 million](https://www.fool.com/investing/2020/02/04/how-an-accounting-tweak-will-make-amazons-most-pro.aspx) decreased depreciation expense. Amazon’s total quarterly capital expenditures are made publicly available from [SEC filings](https://ir.aboutamazon.com/quarterly-results). AWS currently accounts for [about 71%](https://www.geekwire.com/2019/amazon-web-services-growth-slows-missing-analyst-expectations/) of Amazon’s operating profit.&nbsp;

IDC-published results put ODM servers at an average cost of $6,486.55 each for Q3 of 2019, which are about in line with recent averages for x86 server [selling prices](https://www.nextplatform.com/2018/05/31/the-server-boom-town-is-built-on-high-component-prices/). AWS uses [custom-made](https://www.forbes.com/sites/johnsonpierr/2017/06/15/with-the-public-clouds-of-amazon-microsoft-and-google-big-data-is-the-proverbial-big-deal/#43e2b0f92ac3) white box systems (likely designed in-house and produced by [an ODM](https://www.computerweekly.com/opinion/The-rise-of-the-ODMs-Should-the-branded-hardware-suppliers-be-worried)) and is even building a repertoire of [custom silicon](https://www.bloomberg.com/news/articles/2019-12-03/amazon-unveils-new-server-chip-to-compete-with-intel-s-product) for servers, likely driving unit cost down. From the same published results, we can obtain the total revenue and market share of key players and ODM direct sources in the server market for each quarter.

### **What We’ll Assume**

<hr class="wp-block-separator is-style-wide" />

Since we cannot isolate the relative CapEx set aside for servers in each quarter by Amazon based on SEC filings, we assumed two possible spending schedules: a constant-rate schedule and a market-adjusted schedule. The constant schedule makes the simplest assumption that Amazon’s server spending does not change much year-over-year. 

The market-adjusted schedule uses trends in ODM server revenue by quarter and adjusts Amazon’s predicted spending based on this growth, as well as considering the growth rate of AWS availability zones and the change in DRAM pricing. Additionally, we subtract the cost of racks and network switches from the CapEx in both schedules when we calculate the number of servers.

While this assumption is not perfect and Amazon’s spending could differ from market trends, this helps to account for explosive growth in the ODM server market (which is driven [not in small part](https://marketrealist.com/2018/01/whats-amazons-role-odm-growth-global-server-market/) by AWS). The ODM market’s expansion, combined with [nonlinear revenue growth](https://www.statista.com/statistics/250520/forecast-of-amazon-web-services-revenue/) for AWS in recent years, gives us reason to challenge a constant percent assumption for Amazon’s server spending. We provide estimates based on both assumptions in our appendix.

### **What We Found**

<hr class="wp-block-separator is-style-wide" />

Using the $800 million decrease, we estimate Amazon’s percent CapEx spent on servers to be **53.03%** based on the constant-rate schedule and **47.34%** from the market-adjusted schedule. Over the past 6 years, we estimate Amazon’s server spending to total **$28.23** billion according to the constant-rate and **$25.20** billion with the market-adjusted rate. Adjusting for average ODM server prices starting from 2014 and assuming an average useful life of 7 years and using both a floating/constant server price, Amazon currently has approximately **4.9 to 5.5 million servers** in operation. This is in line with another estimate we produced based on the approximate amount of servers per data center per availability zone.

## **Appendix**

### **Percent of Amazon’s (and/or AWS) CapEx spent on servers**

We created two excel models and used Solver to find the base percent of Amazon’s CapEx going towards servers. CapEx was set as the “purchases of property and equipment, including internal-use software and website development, net” from each quarterly and annual filings’ consolidated statements of cash flows. 

The first model was based on the Amazon quarterly CapEx spending which can be found from Amazon websites under investor relation. The second model considered the market adjusted schedule taken from the [total revenue](https://www.statista.com/statistics/269399/global-server-systems-factory-revenue-by-corporate-family/) of the ODM server market from IDC, as well as considering the growth rate of AWS availability zones and the change in DRAM pricing.

Reference used:

  * [Amazon quarterly results](https://ir.aboutamazon.com/quarterly-results)
  * [Market adjusted schedule](https://ir.aboutamazon.com/quarterly-results)
  * [DRAM prices](https://thememoryguy.com/dram-prices-hit-historic-low/)
  * [DRAM prices cont&#8217;d](http://insye.com/dram/)

Fixed percent of CapEx on servers:<figure class="wp-block-image">

![](https://lh6.googleusercontent.com/iedVfjQ3Pkh-hcHe8TghwKqJYggJphNZKblCYlIUzrd6zQ4IsLl4J0CkplTdSxw9Rc5r9KwgEBWA0LV7XpHlIA_2buXh2LAOIKyXsdusPbVo6bRZif_vLekberq5BF-vvhxSYgxI) </figure> 

Market-adjusted floating percent of CapEx on Servers:<figure class="wp-block-image">

![](https://lh3.googleusercontent.com/I43su0FURFtapQj94D68MiWg2rOvGKkwDPwwtrUOP7Dt3OTcG9-yxor6fRL__Dtk2i-3kgcZNwoXZ2-hxlr9cIedGofgsP4oPNuiNzO5igEkn3li9RIqDwNWF0Tdt7FytQnpG1Wl) </figure> 

### **How Much Amazon has Spent on Servers over the Last 6 years**

We used the base rate calculated from question 1 multiplied by the yearly CapEx spending found from Amazon 10k.

Reference used:

  * Amazon SEC filings: <https://ir.aboutamazon.com/sec-filings><figure class="wp-block-image">

![](https://lh5.googleusercontent.com/Z1wuGbFwP_Ux6EFMoeJEAPfLpZ6jK5QRdmzAAgzx3M65SHqIAczbsI68I3dbxVgGNAu3tPOYNuh_V9Vcjf6m36z0iN2kBKaLYP46fr_PTme7fOvMRtBzIUNX-_3PaLzhzd5tH4bL) </figure> <figure class="wp-block-image">![](https://lh6.googleusercontent.com/CjlcRmHTdOiG7IzNBYLvAPF3b72-5-KQUNdODI4goYj0LiTS4EIpgMOSfzIgh9CBDNU-2dHOGlOxhdgOBjgiVqvQKPfh12FdpyLcEj7nQSA_UyOfQSsCqOlmOOUWEVOtxM5oTvtP)</figure> <figure class="wp-block-image">![](https://lh6.googleusercontent.com/auXmRKltjRPKos46CSKISnxkxiACzHSw6dOlT9_UNSMI3JxVSfcT_hZvoChaiJ_2QZjtPpS11UFjRGEs0wNTWOCgmhkMigjpIU6ugTh1fvHWjePBzhdjpAMxSg8ceqs_2wKAnPFh)</figure> 

### **Number of Servers AWS Currently Has in Their Fleet**

We must assume servers last between 5-8 years (competition guidelines). We’ll pick the higher end of this scale due to Amazon’s lengthy tenure in the server market and simplify calculations by choosing a constant server lifetime of 7 years. This means all servers purchased from 2014 (and no earlier) should still be in operation today.

We used average ODM server prices from each year starting from 2014 to estimate the cost Amazon paid to their manufacturers. We also considered adjusting the CapEx [spending for network switches and racks](http://www.data3.com/wp-content/uploads/2018/04/HPEONPREM.pdf) to calculate the number of servers.

Another way to estimate server count is to use the number of server [availability zones](https://www.infrastructure.aws/) (69) and then approximate the number of datacenters per availability zone and the number of servers per datacenter. Estimates given at a conference by AWS engineer James Hamilton place the range of servers per data center at 50,000-80,000, and the number of centers per availability zone somewhere between 1-6. We still need to consider the cost of racks and network switches that are recorded as servers. From these ranges and educated guesses from the article, we can determine a current server count using the number of availability zones.

69\[1 to 6 DCs/AZ\]\[50000 to 65000 Servers/DC\] = 3.4&nbsp; million to 26.9 million servers

This upper bound of the base estimate is likely high since newly established AZs should have fewer average data centers than the ones referenced when the article was published. Each data center should also have fewer than the maximum number of servers as they ramp up. Likewise, our final estimate based on the financials resulted in 4.9 to 5.5 million servers, depending on whether or not we adjusted for ODM server prices in the market and other uncertain factors.

The calculation can be found at the screenshot attached to question 2 and our Excel workbook.&nbsp;

References Used:

  * [ODM server price in 2014- 2015](https://www.nextplatform.com/2018/05/31/the-server-boom-town-is-built-on-high-component-prices/)
  * For server price in the years 2016, we took the middle number from the range $2805-$6500, which is ~ $4500 in our calculation.&nbsp;
  * [ODM server price in 2017 and 2018](https://www.idc.com/getdoc.jsp?containerId=prUS44905719)
  * [ODM server price in 2019](https://www.idc.com/getdoc.jsp?containerId=prUS45692819)
  * [CapEx spending on server adjusted by spending on network and racks](http://www.data3.com/wp-content/uploads/2018/04/HPEONPREM.pdf)
  * [Cost of racks and networks](http://www.data3.com/wp-content/uploads/2018/04/HPEONPREM.pdf)
  * [DRAM pricing&nbsp;](https://thememoryguy.com/dram-prices-hit-historic-low/)
  * [Amazon availability zones](https://aws.amazon.com/about-aws/global-infrastructure/)
  * [Availability zone launching announcement](https://aws.amazon.com/about-aws/whats-new/2019/04/announcing-the-aws-asia-pacific-hong-kong-region/)