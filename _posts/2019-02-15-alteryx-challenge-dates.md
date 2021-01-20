---
layout: post
cover: /assets/images/posts-images/diary.webp
navigation: True
title: "Alteryx Challenge: Dates"
date: 2019-02-15 01:00:00
tags: [alteryx]
class: post-template
subclass: "post"
author: hanykowska
excerpt_separator: <!--more-->
external_url: https://www.thedataschool.co.uk/hanna-nykowska/alteryx-challenge-dates/
external_site: ds
---

Second in the Alteryx Challenge series. Tackling my experience with dates.

[First published on The Data School Blog.]({{page.external_url}}){:target="\_blank"}

<!--more-->

<p>After finishing my week 1 of Alteryx Challenge (see <a href="https://www.thedataschool.co.uk/hanna-nykowska/week-1-done-15-more-to-go/">post</a>), I thought it would be nice to have some sort of structure to it and so I decided to do the challenges by topic. This allows me to work on similar problems together and I plan to continue with a series of blog posts that explain the tools and approaches I used. The first post in the series on basic tools you can find <a href="https://www.thedataschool.co.uk/hanna-nykowska/alteryx-challenge-intro-to-alteryx/">here</a>.<br></p>

<p>Because dates are a common data type to deal with and to some point intuitive, I chose to start with them. As it turned out, there were only 8 challenges with ‘date’ in the name and I have already completed a few of them. Here’s my summary of dealing with dates in Alteryx.<br></p>

<div style="height:34px" aria-hidden="true" class="wp-block-spacer"></div>

<h3>Know your format</h3>

<p>Even though some programs allow you to change the way a date looks like, Alteryx will always have it in the same format: ‘yyyy-mm-dd’. This means that when you’re importing data from Excel, as long as the cell type was date, it will show up in Alteryx in that ‘yyyy-mm-dd’ format. Don’t panic, it’s all good.<br></p>

<p>If you read a .csv file, all fields will be interpreted as strings and so your date may look like in the original file but it won’t be treated as date. There are a few functions that allow you to turn a string into a date and some even have the to option of specifying the format of the string to make the type conversion just how you like it!<br></p>

<div style="height:29px" aria-hidden="true" class="wp-block-spacer"></div>

<h3>String to Date</h3>

<p>I haven’t used much toDate(x) function, so I’ll focus on <strong>DateTimeParse() </strong>which I’ve found to be very useful. <br></p>

<p>DateTimeParse(string, format) takes two arguments: string (dt in original documentation) which contains the data within it and format (f in original documentation, also in a form of a string) specifies how the data should be extracted from the string argument. To create the format argument, you will need to know your specifiers. Specifiers are short expressions that encode date parts. If this sounds like magic to you, relax, there&#8217;s a list of specifiers in Alteryx documentation:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="755" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/specifiers-1024x755.png" alt="" class="wp-image-23676" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/specifiers-1024x755.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/specifiers-300x221.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/specifiers-768x566.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/specifiers.png 1029w" sizes="(max-width: 1024px) 100vw, 1024px" /><figcaption>Functions section in Alteryx documentation. To see the list of specifiers (bottom of the picture), click DateTime to drill down and then on Specifiers to drill down again. </figcaption></figure>

<p>So. Freaking. Useful.</p>

<p>Below the Specifiers you&#8217;ll find separators but that list is definitely not exhaustive so I wouldn&#8217;t bother paying much attention to it.</p>

<p>Another way to convert one data type into a date is to use <strong>DateTime Tool</strong> in which you can either choose from a pre-specified list of date formats or create your own template.</p>

<div style="height:32px" aria-hidden="true" class="wp-block-spacer"></div>

<h3>Time Difference</h3>

<p>Or in function terms, <strong>DateTimeDiff()</strong>. It may prove to be a very sensible function once you remember which date is subtracted from which. For unknown to me reason, the documentation lists the arguments as <em>dt1</em>, <em>dt2</em>, <em>u</em> which corresponds to <em>date1</em>, <em>date2</em> and <em>unit</em>. What I like to use instead is <em><strong>end date</strong></em><strong>, </strong><em><strong>start date</strong></em><strong> and </strong><em><strong>interval</strong></em> (although <em>unit</em> is not so bad in this case).</p>

<p>You may have guessed that DateTimeDiff() returns the difference between the given dates in the unit (interval) of choice. The important thing to remember is that the returned difference is a whole number (integer). If you want to get a specific level of granularity, you&#8217;ll have to use the unit of the lowest level and then figure out the other values. This is actually one of the weekly challenges.</p>

<p>It seems that to get a boolean comparison of dates you could also use &lt;, &gt;, =, etc. operators. Well, I&#8217;ve seen them in some expressions and they seemed to work.</p>

<div style="height:32px" aria-hidden="true" class="wp-block-spacer"></div>

<p>A side note: challenges #46 and #58 seem identical to me but you can still try to do them in a different way (that&#8217;s what I did).</p>

<div style="height:28px" aria-hidden="true" class="wp-block-spacer"></div>

<p>That&#8217;s it from me on dates in Alteryx. If I find out more interesting bits, I&#8217;ll make sure to write a blog on them as well. Thank you and good night!</p>
