---
layout: post
cover: /assets/images/posts-images/calendar2.png
navigation: True
title: "Tableau Tip: Calendar View (Part 2)"
date: 2019-02-19 01:00:00
tags: [tableau]
class: post-template
subclass: "post"
author: hanykowska
excerpt_separator: <!--more-->
external_url: https://www.thedataschool.co.uk/hanna-nykowska/tableau-tip-calendar-view-part-2/
external_site: ds
---

Part 2 of calendar magic AKA tutorial on creating a horizontal calendar view.

[First published on The Data School Blog.]({{page.external_url}}){:target="\_blank"}

<!--more-->

<p>Continuing with the tutorial on how to build a calendar view (for Part 1 go <a href="https://www.thedataschool.co.uk/hanna-nykowska/tableau-tip-calendar-view-part-1/">here</a>), let&#8217;s try to create a horizontal calendar (<a href="https://www.thedataschool.co.uk/blog/andy-kriebel/">Andy</a> used it in his #MakeoverMonday <a href="https://www.vizwiz.com/2019/02/executive-time.html">viz</a> and it&#8217;s also a part of <a href="http://www.workout-wednesday.com/2019-week-2-order-sales-spread-by-region/">2019 week 2 Workout Wednesday</a>):</p>

<figure class="wp-block-image"><img loading="lazy" width="766" height="286" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-39.png" alt="" class="wp-image-24071" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-39.png 766w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-39-300x112.png 300w" sizes="(max-width: 766px) 100vw, 766px" /></figure>

<p>As in the previous part, I&#8217;ll be using Sample &#8211; Superstore data set that Tableau provides. Let&#8217;s dive in, shall we?</p>

<p>If you&#8217;re stuck, check out my public <a href="https://public.tableau.com/profile/hanna.nykowska#!/vizhome/CalendarTutorial/calendarfullwithmiddlelabels">workbook</a> with all the views described and don&#8217;t hesitate to contact <a href="https://www.thedataschool.co.uk/blog/hanna-nykowska/">me</a>. </p>

<h2>How to</h2>

<p>1.Right-click on Order Date and drag it onto columns shelf. From the pop-up window select discrete &#8216;MONTH&#8217; (just like in Part 1):</p>

<figure class="wp-block-image"><img loading="lazy" width="346" height="513" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/popup-window-month.png" alt="" class="wp-image-23993" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/popup-window-month.png 346w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/popup-window-month-202x300.png 202w" sizes="(max-width: 346px) 100vw, 346px" /></figure>

<p>2. Right-click on Order Date and drag it onto columns shelf to the right of the month and select &#8216;WEEKDAY&#8217; from the pop-up window.</p>

<p>Now the party begins. In the previous part, when we were building a vertical calendar, we could just drag the week on the rows shelf and then we were left with some formatting to do. We can&#8217;t really do the same here as we will have all weeks on rows (see below) while we want to have 5-6 rows total.</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="499" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/wrong-setup-1024x499.png" alt="" class="wp-image-24018" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/wrong-setup-1024x499.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/wrong-setup-300x146.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/wrong-setup-768x374.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/wrong-setup-1080x526.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/wrong-setup.png 1514w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>To solve this, we need to create two calculated fields. Click on the caret at the top of dimensions pane and select &#8216;Create Calculated Field&#8230;&#8217;:</p>

<figure class="wp-block-image"><img loading="lazy" width="242" height="294" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-28.png" alt="" class="wp-image-24020" /></figure>

<p>3. Create a calculated field called &#8216;Month Start Week&#8217;. It&#8217;s an LOD (Level Of Detail) calculation which I won&#8217;t get into (that&#8217;s a material for another blog post itself):</p>

<pre class="wp-block-code"><code>{FIXED MONTH([Order Date]): MIN(DATEPART('week', [Order Date]))}</code></pre>

<p>What is happening here: the minimum week [number] is stored for every month. In other words, we know now what is the starting week of each month.</p>

<p>4. Let&#8217;s create another calculated field called &#8216;Month Week&#8217;:</p>

<pre class="wp-block-code"><code>DATEPART('week',[Order Date]) - [Month Start Week] + 1</code></pre>

<p>This gives us the week number at the month level. DATEPART function gives us the week number of the original date and subtracting the starting week results in a week number of the month. For longer months (29-31 days), we can get five or six different values depending on which day of the week the month in question had actually started. If 01 March was on a Monday, it will have five weeks; if it started on a Saturday, it will have six weeks. The &#8216;+1&#8217; is optional, it means that the week numbers start at 1 rather than at 0.</p>

<p>5. Armed with calculated fields, let&#8217;s continue and replace the WEEK pill with Month Week by dragging Month Week on top of WEEK (make sure the border around week pill shows up):</p>

<figure class="wp-block-image"><img loading="lazy" width="449" height="85" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-31.png" alt="" class="wp-image-24030" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-31.png 449w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-31-300x57.png 300w" sizes="(max-width: 449px) 100vw, 449px" /></figure>

<p>Still doesn&#8217;t seem to work? Right-click on the Month Week and select &#8216;Dimension&#8217;:</p>

<figure class="wp-block-image"><img loading="lazy" width="495" height="509" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-32.png" alt="" class="wp-image-24031" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-32.png 495w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-32-292x300.png 292w" sizes="(max-width: 495px) 100vw, 495px" /></figure>

<p> (Edit: You can also move both created fields from Measures to Dimensions.)</p>

<p>This is what you end up with:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="351" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-33-1024x351.png" alt="" class="wp-image-24033" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-33-1024x351.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-33-300x103.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-33-768x263.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-33-1080x370.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-33.png 1099w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>Alright!</p>

<p>6. Let&#8217;s do some formatting:<br>&#8211; resize the rows and columns for more square-shaped cells <br>&#8211; change the mark type to square<br>&#8211; add white borders for a cleaner look<br>&#8211; change the size of the mark (Size on mark cards)<br>&#8211; hide the week numbers<br>&#8211; hide the &#8216;Order Date&#8217;<br>(- hide the weekday)</p>

<p>You should have a similar view to that one below:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="441" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-34-1024x441.png" alt="" class="wp-image-24036" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-34-1024x441.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-34-300x129.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-34-768x331.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-34.png 1066w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>Nice, now that we have that, you might want to ask yourself what you&#8217;re trying to show (just like in Part 1).</p>

<p>If you want to show available data/ calendar &#8211; leave it for now, if you want to color-code some values &#8211; drag that measure (eg. Sales) on Color on marks card. Here&#8217;s what adding sales on color changes:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="440" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-35-1024x440.png" alt="" class="wp-image-24044" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-35-1024x440.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-35-300x129.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-35-768x330.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-35.png 1063w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>7. Add the labels: right-click on Order Date and drag it onto Label on marks card and select discrete &#8216;DAY&#8217;.</p>

<p>8. Oh no! Our view is messed up! Just like in Part 1, it&#8217;s due to multiple years. To fix that, just filter the date so that you only have one year in the view.<br>(<strong>ACHTUNG!</strong> We lost some of the weekdays for certain months. To fix that wait for Part 3. Until then, let&#8217;s carry on.)</p>

<p>9. Change the alignment of label by clicking on &#8216;Label&#8217; on marks card and adjust it to your wishes. Here are the results I got:</p>

<figure class="wp-block-image"><img loading="lazy" width="979" height="488" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-36.png" alt="" class="wp-image-24045" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-36.png 979w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-36-300x150.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-36-768x383.png 768w" sizes="(max-width: 979px) 100vw, 979px" /></figure>

<figure class="wp-block-image"><img loading="lazy" width="976" height="416" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-37.png" alt="" class="wp-image-24053" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-37.png 976w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-37-300x128.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-37-768x327.png 768w" sizes="(max-width: 976px) 100vw, 976px" /></figure>

<p>10. Let&#8217;s try to get rid of the borders and add some shading. Right-click anywhere on the white space in the chart area and select &#8216;Format&#8217;. In the format pane, click on the borders and change row and column dividers to None. Here&#8217;s what you should get:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="566" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/border-format-1024x566.png" alt="" class="wp-image-24054" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/border-format-1024x566.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/border-format-300x166.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/border-format-768x424.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/border-format-1080x596.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/border-format.png 1186w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>To add shading, click on the shading at the top of the format pane and change Column Banding for both Pane and Header. Drag the Level slider all the way to the left and this is what you should end up with:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="511" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/column-shading-1024x511.png" alt="" class="wp-image-24058" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/column-shading-1024x511.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/column-shading-300x150.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/column-shading-768x383.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/column-shading-1080x539.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/column-shading.png 1472w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<figure class="wp-block-image"><img loading="lazy" width="971" height="467" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-40.png" alt="" class="wp-image-24076" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-40.png 971w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-40-300x144.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-40-768x369.png 768w" sizes="(max-width: 971px) 100vw, 971px" /></figure>

<p>There you go!</p>

<div style="height:51px" aria-hidden="true" class="wp-block-spacer"></div>

<p>If you try to wrap you head around showing all dates (including those you don&#8217;t have data for) wait for Part 3! I&#8217;ll also describe how to create a calendar that shows all 12 months in the same view. Byeeee!</p>
