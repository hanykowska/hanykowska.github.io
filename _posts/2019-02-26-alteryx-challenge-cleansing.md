---
layout: post
cover: /assets/images/posts-images/cleaning.jpg
navigation: True
title: "Alteryx Challenge: Data Cleansing"
date: 2019-02-26 00:00:00
tags: [alteryx]
class: post-template
subclass: "post"
author: hanykowska
external_url: https://www.thedataschool.co.uk/hanna-nykowska/alteryx-challenge-data-cleansing/
external_site: ds
excerpt_separator: <!--more-->
---

Tips for Data Cleansing challenges and an update on Alteryx Challenge (finishing all Weekly Challenges by the end of DS training)

[First published on The Data School Blog.]({{page.external_url}}){:target="\_blank"}

<!--more-->

<p>Hey, Data People! After being behind with my Alteryx Challenge (to finish all Weekly Challenges by the end of my DS training), I&#8217;m finally back on track! I managed to catch up over the weekend and I finished another set of challenges. Well, almost, I&#8217;m leaving one or two for when I&#8217;m more competent&#8230;</p>

<p>As promised, here&#8217;s the summary of tools I&#8217;d used and some tips for solving Data Cleansing challenges.</p>

<div style="height:45px" aria-hidden="true" class="wp-block-spacer"></div>

<h4>Know your challenge</h4>

<p>I think I&#8217;ll repeat that one quite often&#8230; Even though some of the tasks are fairly straightforward and don&#8217;t need too much brainpower to figure them out, it&#8217;s a good practice to write down what you need to do. </p>

<p>I tend to start by describing what my data set is. This is super helpful if there&#8217;s more than one starting set so I don&#8217;t need to click on different icons to know where things are. Once that&#8217;s done, I organise what to do with the fields. The organisation might take a form of verbal steps, drawings, crossing-out, whatever works and requires the minimum effort. For more complex problems, I&#8217;d also write down the functions I expect to use.</p>

<p>It might sound like an extra step before building the flow but it actually gives you something specific to build. So know your challenge to know your flow.</p>

<div style="height:51px" aria-hidden="true" class="wp-block-spacer"></div>

<h4>Tools</h4>

<p><strong>Text&nbsp;To&nbsp;Columns</strong> &#8211; While doing my Data Cleansing challenges, I&#8217;ve found that Text To Columns can split the text also to rows! This was a revelation to me that helped me out quite a bit. If you want separate fields and know how many separate expressions are in the text, select &#8216;Split to columns&#8217; in the configuration and make sure you selected the <strong>right number of columns</strong>. In case the number of expressions varies between the rows and/or you prefer to treat them as the same field but different options, select &#8216;Split to rows&#8217; in configuration. </p>

<p>Extra tip: Whatever you put as delimiters (\s &#8211; whitespace, \t &#8211; tab, other separators &#8211; you can find the list on Functions help web page, and any specific characters) will be used to split the text. &#8216;2018/03/05 13:00&#8217; with delimiters set to &#8216;/\s:&#8217; (the order is irrelevant) will be split to &#8216;2018&#8217;, &#8217;03&#8217;, &#8217;05&#8217;, &#8217;13&#8217;, &#8217;00&#8217;.</p>

<p><strong>Substring</strong> and <strong>FindString</strong> combination &#8211; A few times, I&#8217;ve found myself in need of getting a part of a string (text) that started after a certain character combination. To do that I used a combination of Substring and FindString functions. </p>

<p>Substring(text, start, [length]) returns part of the text argument starting at <em>start</em> until the end of the text unless <em>length</em> is specified. The important thing to remember is that the position within the string starts from 0. </p>

<p>FindString(text, target) will return the position of first character of <em>target</em> within <em>text.</em> If the target is not found, the function will return -1.</p>

<p>Let&#8217;s say you have a text field &#8216;Capacity: 5,000&#8217; and you want to get the number part of it. There are quite a few rows in your data and each has a different numerical value. You could count which position is that of the first digit but I&#8217;m too lazy for that&#8230; Instead, I can use FindString([text field], &#8216;: &#8216;) to find where the separator starts. It&#8217;s easier to count the length of the separator (2), add it to the returned value from FindString and use it with Substring function:</p>

<pre class="wp-block-code"><code>Substring([text field],FindString([text field],': ')+2)</code></pre>

<div style="height:61px" aria-hidden="true" class="wp-block-spacer"></div>

<p>Apart from the mentioned tricks, I used quite a lot of tools mentioned in my first <a href="https://www.thedataschool.co.uk/hanna-nykowska/alteryx-challenge-intro-to-alteryx/">post</a>. Whenever in doubt, try to search for a specific functionality or have a read through the functions to know more or less what they&#8217;re doing. The functions are organised by topic which helps a lot.</p>

<p>My solutions may not be the most optimal options but they work. Feel free to contact <a href="https://www.thedataschool.co.uk/blog/hanna-nykowska/">me</a> if you need anything.</p>

<p>I was doing some data preparation challenges lately but we have just finished a session on macros as part of our DS training, so I might squeeze in macros before the data prep blog. Stay tuned for more!</p>
