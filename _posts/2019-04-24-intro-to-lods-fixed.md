---
layout: post
cover: /assets/images/posts-images/lods-fixed.png
navigation: True
title: "Intro to Tableau LODs (fixed)"
date: 2019-04-24 00:00:00
tags: [tableau]
class: post-template
subclass: "post"
author: hanykowska
external_url: https://www.thedataschool.co.uk/hanna-nykowska/intro-to-tableau-lods-fixed/
external_site: ds
excerpt_separator: <!--more-->
---

Trying to understand Level Of Detail (LOD) expressions in Tableau? You're in the right place.

[First published on The Data School Blog.]({{page.external_url}}){:target="\_blank"}

<!--more-->

<p>LODs (Level Of Detail expressions) are a very special type
of calculations in Tableau. They are the ones with the curly brackets. But
that’s not the end of the specialness. LODs can change the level of aggregation
that the calculations are performed for and also confuse many people…</p>

<p>Within the past two weeks, I had the opportunity to <a href="https://www.thedataschool.co.uk/hanna-nykowska/teaching-tableau/">teach LODs</a> to the public and a younger cohort and so I had to wrap my head around LODs themselves.</p>

<h2>How I started with LODs?</h2>

<p>To be honest, I expected more people to have played with LODs. This assumption is strongly biased by my own experience. I had an idea and wanted to get something done but couldn’t figure out how to do it. My first thought was to google it and so I came across these calculations with curly brackets around them. I wasn’t sure how it was working and what exactly was happening but after enough playing around, I managed to figure out how to use FIXED LOD, while being absolutely oblivious to INCLUDE and EXCLUDE…</p>

<p>Fast forward to a few weeks in the Data School and I had to teach this bloody thing to the public. It’s fine though, after a few tries I think I got it sorted(-ish).</p>

<p><em>For the purpose of
this blog post, I’m using Sample – Superstore data available in Tableau.</em></p>

<h2>Back to basics: blue and green, dimensions and measures</h2>

<p>In order to understand LODs we need to understand how
Tableau calculates the data you have in the view. </p>

<h3>Blue vs Green &#8211; Measures</h3>

<p>If you’ve played with Tableau, you probably have noticed that the pills you drag to use various fields are often blue or green. The colour corresponds to whether the field is considered discrete or continuous. (Check out Déb’s <a href="https://www.thedataschool.co.uk/debora-contente/why-are-they-blue-or-green/">blog</a> on this as well!)</p>

<p>If you create a calculated field:</p>

<pre class="wp-block-code"><code>MONTH([Order Date])</code></pre>

<p>It will automatically land in Measures and will be green. (MONTH function returns the number associated with the month of the given date, e.g. 4 for April)</p>

<figure class="wp-block-image"><img loading="lazy" width="191" height="112" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-98.png" alt="" class="wp-image-26269" /></figure>

<p>Dragging it onto Drop field here gives you a ruler on the side of your canvas. If you drop it there, you will actually get an axis:</p>

<ul class="wp-block-gallery columns-2"><li class="blocks-gallery-item"><figure><img loading="lazy" width="65" height="123" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/ruler-drop-here.png" alt="" data-id="26274" data-link="/?attachment_id=26274" class="wp-image-26274" /></figure></li><li class="blocks-gallery-item"><figure><img loading="lazy" width="292" height="284" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/cont-sum-of-month-1.png" alt="" data-id="26275" data-link="/?attachment_id=26275" class="wp-image-26275" /></figure></li></ul>

<p>You can also notice that the month field is aggregated, there’s
SUM(month) on the pill. </p>

<p>We know that month number is not really continuous. To
indicate mid-April, you’d likely use something else than 4.5.</p>

<p>Let’s change the pill to discrete: right-click on the pill in the Measures section in the Data pane -&gt; Convert to Discrete. </p>

<figure class="wp-block-image"><img loading="lazy" width="292" height="242" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-101.png" alt="" class="wp-image-26272" /></figure>

<p>The pill now should be blue but still in Measures:</p>

<figure class="wp-block-image"><img loading="lazy" width="193" height="111" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-102.png" alt="" class="wp-image-26278" /></figure>

<p>Dragging it onto Drop field here will give you separated
rows on the side of the canvas. If you drop it there, you will get table-like
looking rows:</p>

<ul class="wp-block-gallery columns-2"><li class="blocks-gallery-item"><figure><img loading="lazy" width="109" height="179" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/rows-drop-here.png" alt="" data-id="26279" data-link="/?attachment_id=26279" class="wp-image-26279" /></figure></li><li class="blocks-gallery-item"><figure><img loading="lazy" width="292" height="130" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/discr-sum-of-month.png" alt="" data-id="26280" data-link="/?attachment_id=26280" class="wp-image-26280" /></figure></li></ul>

<p>What we’re getting here is a single row that sums all month
numbers: there’s still SUM(month) on the pill even though the pill is blue.</p>

<p>You can see now, that <strong>measures
will be aggregated</strong> no matter if the field is discrete or continuous.</p>

<h3>Blue vs Green &#8211; Dimension</h3>

<p>OK, let’s try converting month field into a dimension. To do
that, right-click on the pill in the data pane -&gt; Convert to Dimension. The
pill should now move to Dimensions section and should be blue.</p>

<p>If you drag it onto Drop field here, you will get separated rows but now instead of a summarised single value, you should get 12 unique ones:</p>

<figure class="wp-block-image"><img loading="lazy" width="295" height="351" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-103.png" alt="" class="wp-image-26282" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-103.png 295w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-103-252x300.png 252w" sizes="(max-width: 295px) 100vw, 295px" /></figure>

<p>The view is now split by the unique values in the dimension
and the data is not aggregated. The pill on Rows shelf has month on it, not
SUM(month).</p>

<p>But what happens if we use a continuous dimension? Let’s right-click on month pill in the Dimensions section and Convert to Continuous. The pill now is still in Dimensions but it is green:</p>

<figure class="wp-block-image"><img loading="lazy" width="217" height="237" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-104.png" alt="" class="wp-image-26283" /></figure>

<p>Dragging it onto Drop field here will show a ruler on the side of the canvas, just like it did for a continuous measure. If you drop it, you will again get an axis but instead of a single mark, you will get 12. One for each of the unique values of the dimension:</p>

<figure class="wp-block-image"><img loading="lazy" width="282" height="377" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-105.png" alt="" class="wp-image-26284" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-105.png 282w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-105-224x300.png 224w" sizes="(max-width: 282px) 100vw, 282px" /></figure>

<p>You can see that the pill is green and not aggregated: month
instead of SUM(month).</p>

<blockquote class="wp-block-quote is-style-default"><p>Blue means discrete</p><p>Green means continuous</p><p>Dimension and Measures can be discrete or continuous</p><p>Dimensions have separate marks for unique values</p><p>Measures are aggregated</p></blockquote>

<h2>How are the values calculated?</h2>

<p>Whenever you add a dimension to the view, it will specify
the level of detail you’re looking at. The more dimensions you have on your
Columns, Rows shelves or Marks card, the more granular (or detailed) view you
have. (This will also result in more and more marks.)</p>

<p>The measures will be aggregated to whatever granularity you
have in the view. In other words, to the level of detail specified by the
dimensions.</p>

<p>Below you can see just that. Starting with just SUM(Sales), I have only one value in the view. Whenever I add dimensions, I get more values for a more detailed look at the data:</p>

<figure class="wp-block-image"><img loading="lazy" width="1745" height="871" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/dimensions-and-measures-in-the-view.gif" alt="" class="wp-image-26286" /></figure>

<p>Sometimes, you want to calculate things at a different level
than what you have in the view. This is where LODs work magic. </p>

<h2>FIXED Level Of Detail</h2>

<h3>Syntax</h3>

<p>The FIXED LOD can specify the granularity of the calculation
independently of what is in the view. This is what the syntax looks like:</p>

<figure class="wp-block-image"><img loading="lazy" width="541" height="35" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-106.png" alt="" class="wp-image-26287" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-106.png 541w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-106-300x19.png 300w" sizes="(max-width: 541px) 100vw, 541px" /></figure>

<p>The keyword is the LOD type: FIXED,
INCLUDE or EXCLUDE.
In this post, I will only cover FIXED, I’ll write about INCLUDE and EXCLUDE in
one of my next blog posts. The list of dimensions can have zero, one or multiple fields. Whenever
there is more than one, they should be separated with a comma. After a colon,
there is the aggregate expression, where you
can also use if-statements (as long as they result in an aggregate expression).
You cannot use table calculations or attribute function in LODs.</p>

<h3>Translate to English</h3>

<p>The syntax may be a bit off-putting for some and not that intuitive, so it’s good to know how to actually understand it. In order to ease this process, I’ll use a method that Coach Andy describes in his <a href="http://www.vizwiz.com/2017/04/fixed-lod-pt1.html">blog</a> FIXED LOD to plain English.</p>

<p>You can translate your FIXED LOD as ‘For every dimension calculate the aggregate expression’:</p>

<figure class="wp-block-image"><img loading="lazy" width="345" height="41" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-107.png" alt="" class="wp-image-26288" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-107.png 345w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-107-300x36.png 300w" sizes="(max-width: 345px) 100vw, 345px" /></figure>

<p>Translates to: For every Category, calculate the sum of
sales.</p>

<p>With FIXED, you can also not specify any dimensions. This will result in calculating the grand total for the given aggregate expression:</p>

<figure class="wp-block-image"><img loading="lazy" width="231" height="37" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-108.png" alt="" class="wp-image-26289" /></figure>

<p>Translates to: Compute total sum of sales.</p>

<p>Pro tip: here, you can skip FIXED and the colon:</p>

<figure class="wp-block-image"><img loading="lazy" width="131" height="36" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-109.png" alt="" class="wp-image-26290" /></figure>

<p>This will have the same result as FIXED on nothing.</p>

<p>Since we’re using fixed here, we don’t really care what is in the view. The data calculated for this calculation will be based on 1. Category and Sales and 2. Sales only.</p>

<figure class="wp-block-image"><img loading="lazy" width="602" height="232" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-110.png" alt="" class="wp-image-26292" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-110.png 602w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-110-300x116.png 300w" sizes="(max-width: 602px) 100vw, 602px" /></figure>

<p>Each LOD is calculated separately, so the data the LOD is using will depend only on the LOD in question.</p>

<h3>LOD vs basic calculations in the view</h3>

<p>Let’s try and recreate the situation above. We want to have
Category and Sub-Category in the view and look at sum(Sales). Normally, this
means you will have different values for all Category and Sub-Category
combinations. But we also want to compare these values with the Sales at the
Category level and with the overall Sales.</p>

<p>Let’s prepare the view: Category, Sub-Category and Sales in the view:</p>

<figure class="wp-block-image"><img loading="lazy" width="587" height="522" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-111.png" alt="" class="wp-image-26293" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-111.png 587w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-111-300x267.png 300w" sizes="(max-width: 587px) 100vw, 587px" /></figure>

<p>Let’s create Category Sales (calculation 1 above):</p>

<figure class="wp-block-image"><img loading="lazy" width="411" height="213" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-112.png" alt="" class="wp-image-26294" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-112.png 411w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-112-300x155.png 300w" sizes="(max-width: 411px) 100vw, 411px" /></figure>

<p>If I add it to the view, you can see below that for different Sub-Categories within the same Category, I’m getting the same values and for different Categories, I’m getting different values. I can also compare it with subtotals to make sure the values are correct:</p>

<figure class="wp-block-image"><img loading="lazy" width="602" height="537" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-113.png" alt="" class="wp-image-26295" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-113.png 602w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-113-300x268.png 300w" sizes="(max-width: 602px) 100vw, 602px" /></figure>

<p>Let’s create Overall Sales and add it to the view.</p>

<figure class="wp-block-image"><img loading="lazy" width="372" height="167" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-114.png" alt="" class="wp-image-26296" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-114.png 372w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-114-300x135.png 300w" sizes="(max-width: 372px) 100vw, 372px" /></figure>

<p>Now, I’m getting the same value for all of the rows, no matter the Category or Sub-Category. Comparing it with the Grand Total, I can see that the value is correct:</p>

<figure class="wp-block-image"><img loading="lazy" width="602" height="460" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-115.png" alt="" class="wp-image-26298" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-115.png 602w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-115-300x229.png 300w" sizes="(max-width: 602px) 100vw, 602px" /></figure>

<p>The difference between basic
calculations such as SUM(Sales) and LODs is that the basic calculations will be
computed based on what is in the view, whereas FIXED LOD will be calculated
based on dimensions and measures specified in the LOD.</p>

<h3>LODs in calculations</h3>

<p>You may wonder why to go through all that trouble just to get the same values as in Subtotals and Grand Total. The totals are useful to compare values in the view but you can’t really use them in your calculations. You can, however, use LODs in calculations.</p>

<p>To compute Sub-Category contribution to Overall Sales, we can create another field Sub-Category Sales Contribution:</p>

<figure class="wp-block-image"><img loading="lazy" width="524" height="268" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-116.png" alt="" class="wp-image-26299" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-116.png 524w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-116-300x153.png 300w" sizes="(max-width: 524px) 100vw, 524px" /></figure>

<figure class="wp-block-image"><img loading="lazy" width="602" height="506" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-117.png" alt="" class="wp-image-26300" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-117.png 602w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-117-300x252.png 300w" sizes="(max-width: 602px) 100vw, 602px" /></figure>

<p>The advantage of FIXED LOD is that it also isn’t affected by dimension filters so if we now filter to only see Furniture Category or Appliances Sub-Category, the LOD values should remain the same, while the Totals will change their values:</p>

<figure class="wp-block-image"><img loading="lazy" width="602" height="407" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-118.png" alt="" class="wp-image-26301" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-118.png 602w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-118-300x203.png 300w" sizes="(max-width: 602px) 100vw, 602px" /></figure>

<figure class="wp-block-image"><img loading="lazy" width="602" height="404" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-119.png" alt="" class="wp-image-26302" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-119.png 602w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-119-300x201.png 300w" sizes="(max-width: 602px) 100vw, 602px" /></figure>

<div style="height:76px" aria-hidden="true" class="wp-block-spacer"></div>

<p>I hope this clears out a few things and makes FIXED LODs more digestible. If you liked this and want more, look out for my future post where I’ll describe INCLUDE and EXCLUDE. There is also a webinar recording available on <a href="https://www.youtube.com/watch?v=kfXwYGaZvLc&amp;t=7s">youtube</a> and check out the <a href="https://public.tableau.com/profile/hanna.nykowska#!/vizhome/LOD_webinar/Intro">workbook</a> I used in that webinar on Tableau Public.</p>
