---
layout: post
cover: /assets/images/posts-images/calendar3.png
navigation: True
title: "Tableau Tip: Calendar View (Part 3)"
date: 2019-02-21 00:00:00
tags: [tableau]
class: post-template
subclass: "post"
author: hanykowska
excerpt_separator: <!--more-->
external_url: https://www.thedataschool.co.uk/hanna-nykowska/tableau-tip-calendar-view-part-3/
external_site: ds
---

3rd in the series, this blog post describes how to deal with missing data in dates. For a 12-month calendar tutorial, go to Part 4 (link in this post as well)

[First published on The Data School Blog.]({{page.external_url}}){:target="\_blank"}

<!--more-->

<p>In my previous posts, Tableau Tip: Calendar View <a href="https://www.thedataschool.co.uk/hanna-nykowska/tableau-tip-calendar-view-part-1/">Part 1</a> and <a href="https://www.thedataschool.co.uk/hanna-nykowska/tableau-tip-calendar-view-part-2/">Part 2</a>, I explained how to build vertical and horizontal calendar views. This time I&#8217;ll show you what to do if you&#8217;re missing some dates and also how to build a year view with all 12 months.</p>

<p><strong>EDIT</strong>: Because this ended up being quite a length post, I decided to split it. For 12-month calendar, go <a href="https://www.thedataschool.co.uk/hanna-nykowska/tableau-tip-calendar-view-part-4/">here.</a></p>

<p>If you&#8217;re stuck, check out my public <a href="https://public.tableau.com/profile/hanna.nykowska#!/vizhome/CalendarTutorial/calendarfullwithmiddlelabels">workbook</a> with all the views described and don&#8217;t hesitate to contact <a href="https://www.thedataschool.co.uk/blog/hanna-nykowska/">me</a>. </p>

<h2>Missing dates</h2>

<p>In Part 2, when we added the day number as Label we realised we used all years which messed up the view. To solve that we filtered the data to only use one year. That in turn showed how much data was missing:</p>

<figure class="wp-block-image"><img loading="lazy" width="803" height="285" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-49.png" alt="" class="wp-image-24148" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-49.png 803w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-49-300x106.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-49-768x273.png 768w" sizes="(max-width: 803px) 100vw, 803px" /><figcaption>Where my Thursdays at?<br></figcaption></figure>

<p>Let&#8217;s deal with it.</p>

<h3>How to</h3>

<p>First, you need to specify the range of dates you&#8217;re interested in. Let&#8217;s say we want to show all dates in 2018. As Tableau can&#8217;t generate them for us, let&#8217;s go to Google Sheets or Excel. In the top cell, I put &#8217;01/01/2018&#8242;. Select that cell and drag by that little square in the bottom right corner down to 365th row or until you reach &#8217;31/12/2018&#8242;. </p>

<p>Go to Data Source view in Tableau and add a connection to you existing data source:</p>

<figure class="wp-block-image"><img loading="lazy" width="1001" height="798" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-51.png" alt="" class="wp-image-24190" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-51.png 1001w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-51-300x239.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-51-768x612.png 768w" sizes="(max-width: 1001px) 100vw, 1001px" /></figure>

<p>If it&#8217;s your first time connecting to Google Sheets (it is for me!), you&#8217;ll need to sign in to Google in your browser and should see something similar in Tableau Desktop: </p>

<figure class="wp-block-image"><img loading="lazy" width="903" height="639" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-52.png" alt="" class="wp-image-24195" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-52.png 903w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-52-300x212.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-52-768x543.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-52-400x284.png 400w" sizes="(max-width: 903px) 100vw, 903px" /></figure>

<p>Connect to your created sheet with all of the dates. Tableau will automatically try to combine your two data sets. </p>

<figure class="wp-block-image"><img loading="lazy" width="869" height="299" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-53.png" alt="" class="wp-image-24196" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-53.png 869w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-53-300x103.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-53-768x264.png 768w" sizes="(max-width: 869px) 100vw, 869px" /></figure>

<p> Add a join clause with Order Date and F1 (which should the only field in your date sheet, Sheet1 in my case, unless you changed that). We also want to do a right join: </p>

<figure class="wp-block-image"><img loading="lazy" width="817" height="273" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-54.png" alt="" class="wp-image-24199" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-54.png 817w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-54-300x100.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-54-768x257.png 768w" sizes="(max-width: 817px) 100vw, 817px" /></figure>

<p>You can also do a Full Outer join if you want to keep all data from the original data source, but since we&#8217;re limiting our data to 2018 for the purpose of this tutorial, I&#8217;ll stick to the right join.</p>

<p>Find you F1 field in the data preview and rename it to &#8216;Full 2018&#8217;.</p>

<p>Alright, now open the horizontal calendar built for Part 2 (or create from scratch; if you&#8217;re here, you might want to use Full 2018 field instead of Order Date and it should save you a few clicks). As a reminder, this is where we left off:</p>

<figure class="wp-block-image"><img loading="lazy" width="971" height="467" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-40.png" alt="" class="wp-image-24076" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-40.png 971w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-40-300x144.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-40-768x369.png 768w" sizes="(max-width: 971px) 100vw, 971px" /></figure>

<p>Right-click on Full 2018 and replace MONTH(Order Date) and select MONTH from the pop-up window. Doesn&#8217;t seem to change much. Do the same for WEEKDAY. It looks weird. Let&#8217;s not worry and continue&#8230;</p>

<figure class="wp-block-image"><img loading="lazy" width="896" height="445" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-55.png" alt="" class="wp-image-24211" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-55.png 896w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-55-300x149.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-55-768x381.png 768w" sizes="(max-width: 896px) 100vw, 896px" /></figure>

<p>Before we did the same thing for Month Week, we&#8217;ll need to update our two calculated fields as they were using Order Date. (For explanations on what the calcs are doing, see Part 2.) There&#8217;s a chance it would work without correcting those calculations, but let&#8217;s keep thing clear.</p>

<p>Month Week calculated field looked like this:</p>

<pre class="wp-block-code"><code>DATEPART('week',[Order Date]) - [Month Start Week] + 1</code></pre>

<p>And we want to change Order Date to Full 2018:</p>

<pre class="wp-block-code"><code>DATEPART('week',[Full 2018]) - [Month Start Week] + 1</code></pre>

<div style="height:34px" aria-hidden="true" class="wp-block-spacer"></div>

<p>We see that Month Week uses Month Start Week, so let&#8217;s edit from</p>

<pre class="wp-block-code"><code>{FIXED MONTH([Order Date]): MIN(DATEPART('week', [Order Date]))}</code></pre>

<p>to</p>

<pre class="wp-block-code"><code>{FIXED MONTH([Full 2018]): MIN(DATEPART('week', [Full 2018]))}</code></pre>

<div style="height:39px" aria-hidden="true" class="wp-block-spacer"></div>

<p>Now that the calculations are correct, let&#8217;s remove the YEAR(Order Date) from filters card and DAY(Order Date) from marks card. If you did the full outer join, you might see some nulls in the view, just filter them out.</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="322" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-56-1024x322.png" alt="" class="wp-image-24232" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-56-1024x322.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-56-300x94.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-56-768x241.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-56-1080x339.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-56.png 1435w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>Yes!</p>

<p>Now we&#8217;re left with some formatting: I&#8217;ll remove the names of the weekdays, add DAY(Full 2018) on the Label on marks card and change the size of the cells to get squares. Here&#8217;s what I got:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="378" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-57-1024x378.png" alt="" class="wp-image-24239" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-57-1024x378.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-57-300x111.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-57-768x283.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-57-1080x398.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-57.png 1475w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>Neat. But I&#8217;m not so satisfied. Let&#8217;s say you want to show which data is available. To do that, we&#8217;ll need another calculated field called &#8216;Is Available&#8217;:</p>

<pre class="wp-block-code"><code>NOT ISNULL([Order Date])</code></pre>

<p>This calculation will return True for rows with available data and False otherwise (we&#8217;re checking this by Order Date but we could use any of the fields from the original data set).</p>

<p>Now drag the Is Available field on Color on marks card and format the colors, so that False is a very light grey and True is blue:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="351" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-58-1024x351.png" alt="" class="wp-image-24242" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-58-1024x351.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-58-300x103.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-58-768x263.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-58-1080x370.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-58.png 1448w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>Well done!</p>
