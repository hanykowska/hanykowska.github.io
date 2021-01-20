---
layout: post
cover: /assets/images/posts-images/calendar4.png
navigation: True
title: "Tableau Tip: Calendar View (Part 4)"
date: 2019-02-22 00:00:00
tags: [tableau]
class: post-template
subclass: "post"
author: hanykowska
external_url: https://www.thedataschool.co.uk/hanna-nykowska/tableau-tip-calendar-view-part-4/
external_site: ds
excerpt_separator: <!--more-->
---

If you want to build a 12-month calendar in one view in Tableau, you’ve found the right place. (I even explain how to add month labels!)

[First published on The Data School Blog.]({{page.external_url}}){:target="\_blank"}

<!--more-->

<p>As the original Part 3 of my Calendar View series turned out pretty long, I decided to split it. This is then the Part 4, showing you how to build a 12-month calendar. With labels!</p>

<p>I continued with my work from <a href="https://www.thedataschool.co.uk/hanna-nykowska/tableau-tip-calendar-view-part-3/">Part 3</a>, so check it out if you haven&#8217;t read it yet.</p>

<p>If you&#8217;re stuck, check out my public <a href="https://public.tableau.com/profile/hanna.nykowska#!/vizhome/CalendarTutorial/calendarfullwithmiddlelabels">workbook</a> with all the views described and don&#8217;t hesitate to contact <a href="https://www.thedataschool.co.uk/blog/hanna-nykowska/">me</a>.</p>

<h2>12 month calendar</h2>

<p>I know that some people might be interested in showing a whole year in one view. So let&#8217;s get down to business!</p>

<p>To continue, grab a full calendar we created in the previous section.</p>

<h3>How to</h3>

<p>We&#8217;ll need some calculations to specify which row and column each month should be. Let&#8217;s start with rows, create a calculated field called &#8216;Year Calendar Rows&#8217;. We&#8217;ll be creating a vertical option (4 rows by 3 columns) so we want each quarter to be in one row. There are a couple ways to do it:</p>

<pre class="wp-block-code"><code>//Option 1
DATENAME('quarter',[Full 2018])</code></pre>

<p>This works well and it&#8217;s an easy calculation, we don&#8217;t necessarily need a separate field for it. The thing to consider is what are your Fiscal Year settings. If the start of FY is set to a month different than January but you want your calendar to start in January, you might want to use the second option:</p>

<pre class="wp-block-code"><code>//Option 2
STR(CEILING(DATEPART('month',[Full 2018])/3))</code></pre>

<p>What&#8217;s happening here? Whenever the month number division by 3 returns a decimal number it will be changed to the first larger whole number. And so Jan, Feb and March (1, 2, 3) would return 0.3, 0.6 and 1 in division but with ceiling function they will be all changed to 1. I added a string function to force the field to be categorised as a dimension.</p>

<p>Pick whichever method you prefer and let&#8217;s create another calculated field called &#8216;Year Calendar Columns&#8217;. This one is quite easy, we just need the remainder of month number division by 3. Tableau doesn&#8217;t seem to have a modulo function which is finding that remainder, but thankfully, it has a modulo operator (%). Modulo will return 0 for March, June, September and December so we need another if-statement to change that 0 to 3 (IIF function is a one-line if-statement):</p>

<pre class="wp-block-code"><code>STR(IIF(DATEPART('month', [Full 2018]) % 3 = 0,3, DATEPART('month', [Full 2018]) % 3))</code></pre>

<p>Again, I used the string function shortcut to force the field to be treated as dimension.</p>

<div style="height:41px" aria-hidden="true" class="wp-block-spacer"></div>

<p>OK! Let&#8217;s drag the created fields on rows and columns shelves, but make sure they are first in the queue. This is what you should have:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="603" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-61-1024x603.png" alt="" class="wp-image-24248" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-61-1024x603.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-61-300x177.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-61-768x453.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-61-1080x636.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-61.png 1539w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>It may seem broken, but we&#8217;re actually very close.</p>

<p>Let&#8217;s drag MONTH(Full 2018) from columns shelf and put it on details.</p>

<figure class="wp-block-image"><img loading="lazy" width="937" height="897" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-62.png" alt="" class="wp-image-24250" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-62.png 937w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-62-300x287.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-62-768x735.png 768w" sizes="(max-width: 937px) 100vw, 937px" /></figure>

<p>Looks better, doesn&#8217;t it? Although, it does seem quite busy and it&#8217;s difficult to find a specific month quickly. To solve this, let&#8217;s add the row and column dividers, set them to the widest option and to white colour. Also while you&#8217;re at it, get rid of the shading.</p>

<figure class="wp-block-image"><img loading="lazy" width="743" height="725" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-63.png" alt="" class="wp-image-24266" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-63.png 743w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-63-300x293.png 300w" sizes="(max-width: 743px) 100vw, 743px" /></figure>

<p>Slightly better, but the month is not as obvious as it could be with month labelled. The next techniques are a combination of <a href="https://twitter.com/lorna_eden">Lorna</a>&#8216;s <a href="https://missdataviz.wordpress.com/2019/02/19/tableautiptuesday-week-7-small-multiple-labels/">post</a>, Andy&#8217;s <a href="http://www.vizwiz.com/2017/03/how-to-heatmap-calendar.html">post</a> and my own ideas.</p>

<h4>Option 1</h4>

<p>In my opinion, that&#8217;s the easiest way to get month labels. The downside is that you&#8217;re limited with where you can have your month labels (either to the left or right).</p>

<p>Change Month Week on rows shelf to continuous:</p>

<figure class="wp-block-image"><img loading="lazy" width="890" height="798" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-64.png" alt="" class="wp-image-24268" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-64.png 890w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-64-300x269.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-64-768x689.png 768w" sizes="(max-width: 890px) 100vw, 890px" /></figure>

<p>Change the mark type to Gantt Bar, right-click on Number of Records and drag it onto Size on marks card, pick AVG as the aggregation method. This trick will change the height of the Gantt bars, if you click on the Size on marks card, you can only change the width. Click on Label and change Vertical Alignment to middle:</p>

<figure class="wp-block-image"><img loading="lazy" width="945" height="889" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-66.png" alt="" class="wp-image-24270" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-66.png 945w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-66-300x282.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-66-768x722.png 768w" sizes="(max-width: 945px) 100vw, 945px" /></figure>

<ul><li>double-click on the rows shelf</li><li>type AVG(0)</li><li>create a dual axis, synchronise axes</li><li>edit either of the axis and check &#8216;Reversed&#8217;</li><li>change mark type on AGG(AVG(0)) card to line</li><li>drag measure names off Color on All card</li><li>drag measure names off Color on AGG(AVG(0)) card:</li></ul>

<figure class="wp-block-image"><img loading="lazy" width="1137" height="961" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/avg0-dual-axis.gif" alt="" class="wp-image-24271" /></figure>

<p>In case you have some problems with the gif above, this is what you should have now:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="883" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-67-1024x883.png" alt="" class="wp-image-24273" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-67-1024x883.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-67-300x259.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-67-768x663.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-67.png 1042w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>You can see that Number of Records trick for Gantt bars is still on our &#8216;line&#8217; chart. Let&#8217;s drag it off, together with DAY(Full 2018) associated with text.</p>

<p>Change MONTH to Label:</p>

<figure class="wp-block-image is-resized"><img loading="lazy" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-68.png" alt="" class="wp-image-24276" width="132" height="241" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-68.png 233w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-68-164x300.png 164w" sizes="(max-width: 132px) 100vw, 132px" /></figure>

<p>Open the Label menu, check &#8216;Show mark labels&#8217;, select line ends and depending whether you prefer your label to be on the left or the right, keep the &#8216;start of the line&#8217; or &#8216;end of the line&#8217; respectively and uncheck the other option. I prefer it on the left, so I&#8217;ll keep &#8216;start of the line&#8217; checked and &#8216;end of the line&#8217; unchecked. </p>

<p>To have the label slightly further from the edge, change the alignment of the label to right (or left if you kept &#8216;end of line checked&#8217;):</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="692" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-69-1024x692.png" alt="" class="wp-image-24277" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-69-1024x692.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-69-300x203.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-69-768x519.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-69.png 1042w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>Looking good! Let&#8217;s hide the line by decreasing opacity to 0%. There are still some lines on the calendar that we might want to get rid of. Right-click anywhere on the white space within the chart and select &#8216;Format&#8217;. In lines formatting, change the Grid Lines to a solid line and back to None (it originally said &#8216;None&#8217; but it wasn&#8217;t true for all settings&#8230; ridiculous), and Zero Lines to None. Hide headers for all pills and there you go!</p>

<p>Well done, now you have a calendar with labelled months!</p>

<figure class="wp-block-image"><img loading="lazy" width="632" height="804" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-70.png" alt="" class="wp-image-24279" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-70.png 632w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-70-236x300.png 236w" sizes="(max-width: 632px) 100vw, 632px" /></figure>

<p>You can control the spaces between the rows/quarters by editing the range of either Month Week or AVG(0) axes.</p>

<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>

<h4>Option 2</h4>

<p>This one allows you to have labels in the middle but definitely requires more fiddling around. It gives you, however, the opportunity to control the spaces between columns of months which you can&#8217;t control that much in Option 1.</p>

<p>If you&#8217;re one of the crazies who start their week with Sunday, you can skip the calculated field and use WEEKDAY(Full 2018) you already have on columns shelf, just change it to continuous like we did with Month Week.</p>

<p>For those who start with Monday, create a calculated field &#8216;Weekday Starting Monday&#8217;:</p>

<pre class="wp-block-code"><code>{FIXED [Full 2018]:
MIN(IF DATEPART('weekday', [Full 2018]) = 1 THEN 8
ELSE DATEPART('weekday', [Full 2018])
End)}</code></pre>

<p>What&#8217;s happening here: we want to specify the numerical value of a weekday for every day in Full 2018, hence the LOD. Let&#8217;s me explain the second part&#8230; As it turns out, no matter how you set up your data set Date Properties (I mean the week start), the weekday number will always start with 1 for Sunday. This is crazy considering the week calculation seems to be working in line with you custom setting&#8230; (WHY?!) </p>

<p>To solve this, we need to overwrite the weekday number. This is what happening in the second part of the LOD calc (after the colon). In this case, if the weekday number is 1 (aka it&#8217;s a Sunday) we want to change it to 8, for other weekdays we keep the weekday number. You can also change it to 7 and decrement all other values, but that is just more typing&#8230; As long as the weekdays are in the right order, you should be fine.</p>

<div style="height:38px" aria-hidden="true" class="wp-block-spacer"></div>

<p>Replace the WEEKDAY(Full 2018) with Weekday Starting Monday: right-click on the latter and drag it on to columns shelf and select MEDIAN from pop-up menu. Now drag off the WEEKDAY(Full 2018).</p>

<p><strong>Sunday-lovers!</strong> You can join in now.</p>

<p>With a continuous weekday information, you can see something similar to this:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="597" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-72-1024x597.png" alt="" class="wp-image-24282" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-72-1024x597.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-72-300x175.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-72-768x448.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-72-1080x630.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-72.png 1536w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>Change the alignment of labels to middle and narrow down the width of the sheet. As a final correction, hide the header for the continuous weekday.</p>

<p>THERE. YOU. GO. A 12 month calendar with months labelled in the middle:</p>

<figure class="wp-block-image"><img loading="lazy" width="756" height="872" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-73.png" alt="" class="wp-image-24283" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-73.png 756w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-73-260x300.png 260w" sizes="(max-width: 756px) 100vw, 756px" /></figure>

<p>boom! Byeeeeee</p>
