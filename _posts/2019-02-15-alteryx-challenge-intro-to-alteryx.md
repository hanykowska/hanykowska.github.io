---
layout: post
cover: /assets/images/posts-images/alteryx_logo.png
navigation: True
title: "Alteryx Challenge: Intro to Alteryx"
date: 2019-02-15 00:00:00
tags: [alteryx]
class: post-template
subclass: "post"
author: hanykowska
excerpt_separator: <!--more-->
external_url: https://www.thedataschool.co.uk/hanna-nykowska/alteryx-challenge-intro-to-alteryx/
external_site: ds
---

First post in the Alteryx Challenge series, where I describe the tools I’ve used for Weekly Challenges and some tricks I’ve learnt.

[First published on The Data School Blog.]({{page.external_url}}){:target="\_blank"}

<!--more-->

<p>Last week, I wrote a short <a href="https://www.thedataschool.co.uk/hanna-nykowska/week-1-done-15-more-to-go/">summary</a> on the Alteryx Challenge idea. The objective is to finish all Alteryx <a href="https://community.alteryx.com/t5/Weekly-Challenge/Weekly-Challenge-Index-amp-Welcome/td-p/48275">Weekly Challenges</a> by the end of the DS training. This is my first blog in the series describing the lessons learnt and the tools used to complete the challenges. This one is mostly about certain tools that I’ve found myself using a lot, no matter the topic. For specific subjects, scroll down to see the list of my posts.</p>

<div style="height:30px" aria-hidden="true" class="wp-block-spacer"></div>

<h3>Weekly Challenge Structure</h3>

<p>As far as I know, every alteryx flow starts with an input (Input Data), this is provided by Weekly Challenge. After running the flow (ctrl+r) you can see how the data looks like. The start files (see below) also give you the expected output (Output Data) and the task is to create a flow that transforms the data into a required format. </p>

<figure class="wp-block-image"><img loading="lazy" width="691" height="351" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/weekly-challenge-file.png" alt="" class="wp-image-23659" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/weekly-challenge-file.png 691w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/weekly-challenge-file-300x152.png 300w" sizes="(max-width: 691px) 100vw, 691px" /><figcaption>Weekly Challenge start file</figcaption></figure>

<p>This week I’ve been introduced to Crew Macros (download <a href="http://www.chaosreignswithin.com/p/macros.html">here</a>, thanks <a href="https://twitter.com/VizMyData">Jonathan</a>!). One of them allows comparing datasets in a form of a test. Once installed, find CReW Test and use Expect Equal (BETA) to check whether your output matches the expected one.</p>

<h4> A word of caution </h4>

<p>It’s possible that there’s a mistake in the solution (expected output). If you get errors, double check your solution to make sure the flow you created is doing what you wanted it to do and that your logic is correct. In case everything on your side is fine, you can check replies under the Weekly Challenge to see if others had the same reservations. Once you’re sure you’re right, I’d just comment when submitting the solution (you submit it by responding to the original post and including your solution file).</p>

<p>Now that we have that sorted, let’s get to some tools.</p>

<div style="height:45px" aria-hidden="true" class="wp-block-spacer"></div>

<h3>Tools</h3>

<p><strong>Formula Tool</strong> &#8211; fairly intuitive if you had some experience with programming, just need to get used to the syntax (fairly easy). If you click on blue icons on your left-hand side, you can see the list of functions, variables, etc. you can use, also you’ll get suggestions once you start typing. If you start with ‘[‘ the suggestions will start with the available fields. </p>

<p>Important things to remember when setting a formula tool: </p>

<ul><li>Do you want to overwrite a field or create a new one?</li><li>If the latter, what data type do you want it to be? (I tend to keep forgetting about this one and realise something’s wrong when I get errors from other tools…)</li><li>You can create multiple separate expressions within one formula tool. They seem to be run sequentially in the order they are in the tool configuration.</li></ul>

<p>The Alteryx documentation seems sensible and I find myself using it a lot. I even added <a href="https://help.alteryx.com/2018.2/Reference/Functions.htm">the functions section</a> to bookmarks in my browser! If you plan to do a lot of challenges, I suggest you do the same. It&#8217;s just easier for me to figure out what kind of function I need and how to use it.</p>

<div style="height:25px" aria-hidden="true" class="wp-block-spacer"></div>

<p><strong>Multi-Field Formula and Multi-Row Formula</strong>. There are some things that you need to do for a few fields or it may be easier/necessary to use values from nearby rows to get what you want. For these cases, you’d likely use multi-field and multi-row formula tools respectively. Multi-Row Formula allows grouping by certain fields so it’s quite helpful if you need to create a sequence of numbers for each group (eg. month number for all months for multiple years, see below).</p>

<div class="wp-block-image"><figure class="aligncenter is-resized"><img loading="lazy" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/generate-rows-1.png" alt="" class="wp-image-23665" width="434" height="469" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/generate-rows-1.png 458w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/generate-rows-1-278x300.png 278w" sizes="(max-width: 434px) 100vw, 434px" /><figcaption> <br>Generate month numbers with Multi-Row Formula Tool. <br>Whenever the Year value changes, the Month field starts from Null() as there was no Month field before. Once that first value is changed to one, the next values just increment on the previous ones.  <br></figcaption></figure></div>

<p>If you want to do a combination of multi-row and multi-field you can either use a few of multi-row formula tools or transpose the fields of interest, add a multi-row formula and cross-tab it back to normal (thanks <a href="https://twitter.com/benjnmoss">Ben</a> for that tip!).<br></p>

<p><strong>Generate Rows</strong> &#8211; as the name suggests, it generates rows. However, if you use a custom expression (‘&#8230;’ on the right-hand side in the configuration next to ‘Condition Expression’ text box), this tool can be useful for creating various types of data. It can generate a set of dates that change according to your ‘Loop Expression’ (DateTimeAdd([date],1,&#8221;days&#8221;) would increment by one day). I haven’t tried other types apart from numeric and dates but I assume the biggest limitation would be the logic needed (something you just have to figure out).</p>

<p><strong>RegEx</strong> can be a helpful tool for extracting specific expressions from a string. In the beginning, it may feel a bit overwhelming but there&#8217;s a nice website that highlights the matched expressions within a string. If you want to practice or just see whether your expressions have the expected result, head to <a href="https://regex101.com/">regex101.com</a> and give it a go (again, thanks Jonathan). There are a few output methods for RegEx, I have only used Tokenize so far. Maybe once I&#8217;m more familiar with it, RegEx will get its own post.</p>

<div style="height:29px" aria-hidden="true" class="wp-block-spacer"></div>

<p>The subjects that I&#8217;ve explored so far:</p>

<ul><li><a href="https://www.thedataschool.co.uk/hanna-nykowska/alteryx-challenge-dates/">dates</a></li><li><a href="https://www.thedataschool.co.uk/hanna-nykowska/alteryx-challenge-data-cleansing/">data cleansing</a></li><li><a href="https://www.thedataschool.co.uk/hanna-nykowska/alteryx-challenge-macros/">macros</a></li></ul>

<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>

<p>That&#8217;s it!</p>
