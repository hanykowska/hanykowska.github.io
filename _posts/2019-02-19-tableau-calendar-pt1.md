---
layout: post
cover: /assets/images/posts-images/calendar1.png
navigation: True
title: "Tableau Tip: Calendar View (Part 1)"
date: 2019-02-19 00:00:00
tags: [tableau]
class: post-template
subclass: "post"
author: hanykowska
excerpt_separator: <!--more-->
external_url: https://www.thedataschool.co.uk/hanna-nykowska/tableau-tip-calendar-view-part-1/
external_site: ds
---

A tutorial on creating a calendar view to visualise your date-related data.

[First published on The Data School Blog.]({{page.external_url}}){:target="\_blank"}

<!--more-->

<p>There were three things that prompted me to write this: <br><a href="https://www.thedataschool.co.uk/blog/debora-contente/">Déb&#8217;s</a> <a href="https://www.thedataschool.co.uk/debora-contente/calendar-picker-takes-over-boring-dropdown/">post</a> on calendar parameter (if you haven&#8217;t, go and read it),<br><a href="https://www.thedataschool.co.uk/blog/andy-kriebel/">Andy</a>&#8216;s #MakeoverMonday on President Trump&#8217;s Executive Time (see <a href="https://www.vizwiz.com/2019/02/executive-time.html">here</a>) and<br>2019 week 2 Workout Wednesday (see <a href="http://www.workout-wednesday.com/2019-week-2-order-sales-spread-by-region/">here</a>).</p>

<p>When I was working on my Interview Viz for the DS (checkout the vizzes of my fellow cohortians and mine <a href="https://www.thedataschool.co.uk/andy-kriebel/ds13/">here</a>), I came up with an idea of using a calendar view as part of visualisation. Unfortunately, this concept came to me in the late evening on the day before the interview so I didn&#8217;t incorporate it in my viz. I played a bit with the idea for a few days after the interview but it didn&#8217;t seem to work for me at that time, so I dropped it. Until now.</p>

<p>The purpose of this post is to give you a tutorial on how to create a calendar visual (something like that below). I thought I&#8217;d start with a vertical layout as that is easier to do. If you prefer a horizontal option, wait for my next blog.</p>

<p>If you&#8217;re stuck, check out my public <a href="https://public.tableau.com/profile/hanna.nykowska#!/vizhome/CalendarTutorial/calendarfullwithmiddlelabels">workbook</a> with all the views described and don&#8217;t hesitate to contact <a href="https://www.thedataschool.co.uk/blog/hanna-nykowska/">me</a>. </p>

<figure class="wp-block-image"><img loading="lazy" width="381" height="581" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-41.png" alt="" class="wp-image-24085" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-41.png 381w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-41-197x300.png 197w" sizes="(max-width: 381px) 100vw, 381px" /></figure>

<h2>How to</h2>

<p>To create the calendar above I used the Order Date from Tableau&#8217;s Sample &#8211; Superstore data set.</p>

<p>1.Right-click and drag Order Date onto Rows shelves. This will trigger a pop-up window just like this below, go ahead and select discrete  month: </p>

<figure class="wp-block-image"><img loading="lazy" width="346" height="513" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/popup-window-month.png" alt="" class="wp-image-23993" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/popup-window-month.png 346w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/popup-window-month-202x300.png 202w" sizes="(max-width: 346px) 100vw, 346px" /></figure>

<p>2. Again, right-click on Order Date, drag it onto rows shelf to the right-hand side of month pill, but now select the discrete &#8216;WEEK&#8217; (two positions below the previously selected month).</p>

<p>This is what you should have now: </p>

<figure class="wp-block-image"><img loading="lazy" width="468" height="837" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/2.-month-and-week.png" alt="" class="wp-image-23994" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/2.-month-and-week.png 468w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/2.-month-and-week-168x300.png 168w" sizes="(max-width: 468px) 100vw, 468px" /></figure>

<p>3. Right-click and drag (you guessed it!) the Order Date on the columns shelf and select &#8216;WEEKDAY&#8217; (there&#8217;s only one such option).</p>

<p>4. Change the mark type to square. Now this starts to look like a calendar&#8230; (Your week may start with Sunday, that&#8217;s fine. If you want to change it, right-click on data source -&gt; date properties -&gt; select your preferred week start)</p>

<figure class="wp-block-image"><img loading="lazy" width="787" height="740" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/4.-early-calendar.png" alt="" class="wp-image-23996" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/4.-early-calendar.png 787w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/4.-early-calendar-300x282.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/4.-early-calendar-768x722.png 768w" sizes="(max-width: 787px) 100vw, 787px" /></figure>

<p>5. Some formatting: <br>&#8211; change the sizes of cells so that they&#8217;re more of a square shape<br>&#8211; right-click on week and uncheck &#8216;Show Header&#8217;<br>&#8211; right-click on Month of Order Date and select &#8216;Hide Field Labels for Rows&#8217;<br>&#8211; do the same with Order Date (above days of the week, &#8216;Hide Field Labels for Columns&#8217;)<br>&#8211; right-click on any of the months and select &#8216;Format&#8217; -&gt; Alignment -&gt; Vertical &#8211; Middle and Horizontal &#8211; Right or whatever you like better<br>&#8211; I&#8217;ll go ahead and also get rid of the weekdays (right-click on weekday and uncheck &#8216;Show Header&#8217;)<br></p>

<p>Here&#8217;s what I have:</p>

<figure class="wp-block-image"><img loading="lazy" width="624" height="770" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/5.-formatted-calendar-1.png" alt="" class="wp-image-24000" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/5.-formatted-calendar-1.png 624w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/5.-formatted-calendar-1-243x300.png 243w" sizes="(max-width: 624px) 100vw, 624px" /></figure>

<p>Almost there!</p>

<p>What you want to do now depends on what you want to show.</p>

<p>Do you want to color-code some values (eg. Sales)? If so, drag Sales on Color on marks shelf. Add some white borders to make it look better. Here&#8217;s the result:</p>

<figure class="wp-block-image"><img loading="lazy" width="623" height="770" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/6.-Calendar-coloured-with-sales.png" alt="" class="wp-image-24001" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/6.-Calendar-coloured-with-sales.png 623w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/6.-Calendar-coloured-with-sales-243x300.png 243w" sizes="(max-width: 623px) 100vw, 623px" /></figure>

<p>Do you want to keep one colour and just show where the data is available? Click on Size on marks shelf and change it to the right bar (see below).</p>

<figure class="wp-block-image"><img loading="lazy" width="589" height="768" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-27.png" alt="" class="wp-image-24002" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-27.png 589w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-27-230x300.png 230w" sizes="(max-width: 589px) 100vw, 589px" /></figure>

<p>Let&#8217;s say that&#8217;s not good enough and you want to add the day numbers. That&#8217;s fine. Right-click on Order Date and drag it to Label on marks shelf. </p>

<p>Oh no! What happened?! Your view might look something like that:</p>

<figure class="wp-block-image"><img loading="lazy" width="616" height="770" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/calendar-with-day.png" alt="" class="wp-image-24003" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/calendar-with-day.png 616w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/calendar-with-day-240x300.png 240w" sizes="(max-width: 616px) 100vw, 616px" /></figure>

<p>Don&#8217;t panic! Everything&#8217;s under control. In our Order Date, we have multiple years which mess up our view. Easy to deal with by filtering the Order Date. You can filter however you like, just make sure that you keep only one year, eg. pick year and select whichever you want (I kept 2018).</p>

<p>You may want to change the alignment of the labels. Click on the Label on marks shelf, select Alignment and adjust it to your needs. You can also get rid of the row and column dividers (Format -&gt; borders) and add shading (Format -&gt; shading) for a cleaner look. To have an idea on how to do it, go ahead and check step 10. of <a href="https://www.thedataschool.co.uk/hanna-nykowska/tableau-tip-calendar-view-part-2/?preview=true&amp;_thumbnail_id=24071">Part 2</a>. Here are the final outputs:</p>

<div class="wp-block-columns has-2-columns">
<div class="wp-block-column">
<figure class="wp-block-image"><img loading="lazy" width="619" height="661" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/Calendar-with-day-formatted.png" alt="" class="wp-image-24004" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/Calendar-with-day-formatted.png 619w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/Calendar-with-day-formatted-281x300.png 281w" sizes="(max-width: 619px) 100vw, 619px" /></figure>
</div>

<div class="wp-block-column">
<figure class="wp-block-image"><img loading="lazy" width="601" height="658" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/calendar-with-colour-formatted.png" alt="" class="wp-image-24005" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/calendar-with-colour-formatted.png 601w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/calendar-with-colour-formatted-274x300.png 274w" sizes="(max-width: 601px) 100vw, 601px" /></figure>
</div>
</div>

<p>As you may see, there are some holes in our calendar. They show the lack of specific dates. You can try to create some data to make sure you have all days included in your data set (just like Andy did in his #MakeoverMonday viz. If you don&#8217;t believe me, read it on his <a href="https://www.vizwiz.com/2019/02/executive-time.html">blog</a>.), this should take care of it.</p>

<div style="height:46px" aria-hidden="true" class="wp-block-spacer"></div>

<p>Hope you enjoyed it! Stay tuned for the next part where I&#8217;ll explain the horizontal layout (that one is a bit more tricky).</p>
