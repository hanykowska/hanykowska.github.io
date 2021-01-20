---
layout: post
cover: /assets/images/posts-images/tableau-dynamic-date-level.gif
navigation: True
title: "Tableau Tip: dynamic date level aggregation"
date: 2019-02-28 00:00:00
tags: [tableau]
class: post-template
subclass: "post"
author: hanykowska
external_url: https://www.thedataschool.co.uk/hanna-nykowska/tableau-tip-dynamic-date-level-aggregation/
external_site: ds
excerpt_separator: <!--more-->
---

Quick way of creating a dynamic date level aggregation using a parameter.

[First published on The Data School Blog.]({{page.external_url}}){:target="\_blank"}

<!--more-->

<p>For one of the exercises yesterday, we had to create a view that dynamically changed the date level depending on the user&#8217;s choice (year, quarter, month). Today, I&#8217;m going to show you how to do it.</p>

<h4>Goal</h4>

<figure class="wp-block-image"><img loading="lazy" width="1541" height="941" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/dateLevelFin-1.gif" alt="" class="wp-image-24851" /></figure>

<p>As you can see, depending on the choice in &#8216;Select Date Level&#8217; section, the view adjusts accordingly and shows the sum(Sales) at the year, quarter or month level of Order Date.</p>

<h3>How To</h3>

<h4>1. Parameter</h4>

<p>I&#8217;m going to use Sample &#8211; EU Superstore data set from Tableau for the purpose of this tutorial. To get the result we want, we need a parameter. This is exactly what the user will change. Let&#8217;s create the &#8216;Select Date Level&#8217; parameter, set the data type to string and allowable values to List. It&#8217;s important what we put in the list: start with value field and type in &#8216;year&#8217;, &#8216;quarter&#8217;, &#8216;month&#8217; all in separate rows, make sure they are all <strong>lowercase</strong>. Thankfully, we can change what the user sees, let&#8217;s change Display As to title case. This is what your settings should look like:</p>

<figure class="wp-block-image"><img loading="lazy" width="573" height="520" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-114.png" alt="" class="wp-image-24821" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-114.png 573w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-114-300x272.png 300w" sizes="(max-width: 573px) 100vw, 573px" /></figure>

<p>It&#8217;s important that you type in lowercase in Value field because anytime you change the Value, Display As will also update. However, if you change Display As, the value stays unchanged.</p>

<h4>2. Calculated Field</h4>

<p>If you ever worked with parameters, you know you need a calculated field to actually use the parameter functionality. If you&#8217;re new to parameters, now you know 😉</p>

<p>Usually, you create a field that checks the value of the parameter and then performs a certain function. Due to characteristics of dates and associated functions we can do it slightly differently, in a shorter way. Let&#8217;s create a calculated field called &#8216;Date Level Aggregation&#8217;:</p>

<pre class="wp-block-code"><code>DATENAME([Select Date Level], [Order Date])</code></pre>

<p>What&#8217;s happening here: I used DateName function because it returns a string for the date part of the given date. For year and quarter, it will return the number as a string, for month, it will return the name of the month (eg. January). [Select Date Level] should be purple on your screen, as it is a parameter; it is also what we use as the date part. Because we&#8217;re using the parameter in the function, the values need to be lowercase so that Tableau recognise them as valid arguments. </p>

<p>Let&#8217;s create the view. Drag Date Level Aggregation on Columns shelf and Sales on Rows shelf. Right-click on the Select Date Level parameter and check &#8216;Show Parameter Control&#8217;. We want to allow only one option to choose. To get that, click on the caret in the parameter control (should be on your right-hand side) and select &#8216;Single Value List&#8217;. I also change the fit to Entire View. This is what your view should look like:</p>

<figure class="wp-block-image"><img loading="lazy" width="1541" height="941" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/dateLevel1.gif" alt="" class="wp-image-24835" /></figure>

<p>Hold on, we want the quarters to show up as &#8216;Q1&#8217; not just &#8216;1&#8217;. Alright, calm down, we&#8217;ll fix it. Originally, I created the following If-Statement:</p>

<pre class="wp-block-code"><code>IF [Select Date Level] = 'quarter'
THEN 'Q' + DATENAME([Select Date Level], [Order Date])
ELSE DATENAME([Select Date Level], [Order Date])
END</code></pre>

<p>But with <a href="https://www.thedataschool.co.uk/blog/jonathan-allenby/">Jon</a>&#8216;s help we managed to make it even neater:</p>

<pre class="wp-block-code"><code>IF [Select Date Level] = 'quarter'
THEN 'Q'
ELSE ''
END
+
DATENAME([Select Date Level], [Order Date])</code></pre>

<p>With the updated calculated field, you should get what was advertised. To improve the view, let&#8217;s hide the field labels for columns. There you go:</p>

<figure class="wp-block-image"><img loading="lazy" width="1541" height="941" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/dateLevelFin.gif" alt="" class="wp-image-24849" /></figure>

<p>Byeeee!</p>
