---
layout: post
cover: /assets/images/posts-images/MM2019w12.png
navigation: True
title: "MakeoverMonday 2019w12"
date: 2019-03-18 00:00:00
tags: [tableau]
class: post-template
subclass: "post"
author: hanykowska
external_url: https://www.thedataschool.co.uk/hanna-nykowska/makeovermonday-2019w12/
external_site: ds
excerpt_separator: <!--more-->
---

My first blog on makeover monday; describing the good and the bad of original viz and how I tried to make it better

[First published on The Data School Blog.]({{page.external_url}}){:target="\_blank"}

<!--more-->

<p>I&#8217;m currently reading the Makeover Monday book by <a href="https://twitter.com/TriMyData">Eva Murray</a> and <a href="https://www.thedataschool.co.uk/blog/andy-kriebel/">Andy</a>. One of the suggestions was to write a blog post about every challenge and so I decided to do that from now on. If you don&#8217;t know what Makeover Monday is check it out <a href="http://www.makeovermonday.co.uk/">here</a>.</p>

<p>The data for week 12 of 2019 was very simple, a Country and Index value pairs for G7 countries, together with average value.</p>

<p>This week&#8217;s original visualisation:</p>

<figure class="wp-block-image"><img src="https://assets.weforum.org/editor/Dz-I3eiR_kuVmyk3AqzU45N0dG1crcJocm6YqpCHttw.png" alt="" /><figcaption><a href="https://www.weforum.org/agenda/2018/12/women-reykjavik-index-leadership">https://www.weforum.org/agenda/2018/12/women-reykjavik-index-leadership</a></figcaption></figure>

<h4>What works</h4>

<p>First of all, it looks nice, the chart is just visually pleasing. The Index values are from 0 to 100 and it seems that 100 would make a full circle although this is not immediately obvious. I also noticed that it&#8217;s quite similar to <a href="https://www.weforum.org/">World</a><a href="https://www.weforum.org/"> Economic Forum</a>&#8216;s logo (a website the viz was published on), which I think is a nice touch:</p>

<figure class="wp-block-image"><img loading="lazy" width="134" height="90" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-36.png" alt="" class="wp-image-25228" /><figcaption><br></figcaption></figure>

<h4>What doesn&#8217;t work</h4>

<p>I think the colours are not the best choice, I have problems distinguishing between purple lines for countries and dark blues for the average. With this type of chart, it is also difficult to compare the values. It may look cool but it&#8217;s not very efficient. </p>

<h4>How can I improve it</h4>

<p>The easiest way would be to straighten it and present it in a bar chart form. To give the intuition that it is out of 100 would be to put a border around a bar that goes from 0 to 100 and fill it to the corresponding score of a country. I additionally coloured the bars depending on whether the score was above or below G7 average (shown as reference line). You can see my submission below:</p>

<figure class="wp-block-image"><img loading="lazy" width="1000" height="700" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/Dashboard-1.png" alt="" class="wp-image-25229" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/Dashboard-1.png 1000w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/Dashboard-1-300x210.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/Dashboard-1-768x538.png 768w" sizes="(max-width: 1000px) 100vw, 1000px" /><figcaption><a href="https://public.tableau.com/profile/hanna.nykowska#!/vizhome/MM2019w12_15529277530680/Dashboard">Interactive Viz</a></figcaption></figure>

<p>I was also thinking that maybe just adding shading for countries with a score above average vs below average while remaining the radial form could make the original viz better. Wait for an update tomorrow 😉</p>
