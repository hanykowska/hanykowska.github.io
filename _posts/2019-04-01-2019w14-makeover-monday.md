---
layout: post
cover: /assets/images/posts-images/cotton-buds.png
navigation: True
title: "Makeover Monday 2019w14: 2 metres of cotton buds"
date: 2019-04-01 00:00:00
tags: [tableau]
class: post-template
subclass: "post"
author: hanykowska
external_url: https://www.thedataschool.co.uk/hanna-nykowska/hannas-makeover-monday-2019w14-2-metres-of-cotton-buds/
external_site: ds
excerpt_separator: <!--more-->
---

Looking at makeovermonday 2019w14: the good the bad and how to improve

[First published on The Data School Blog.]({{page.external_url}}){:target="\_blank"}

<!--more-->

<p>This week of <a href="http://www.makeovermonday.co.uk/">#MakeoverMonday</a> is dedicated to the state of the British beaches. More precisely the amount of waste that litters them. The data itself comes 2017 Great British Beach Clean Report which mentions that nearly 7,000 volunteers gathered 255,209 individual pieces of litter from 339 beaches with devastating average of 718 pieces per 100m.</p>

<p>The original visualisation by BBC can be seen below:  </p>

<figure class="wp-block-image"><img loading="lazy" width="615" height="936" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-2.png" alt="" class="wp-image-25563" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-2.png 615w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-2-197x300.png 197w" sizes="(max-width: 615px) 100vw, 615px" /><figcaption> <br><a href="https://www.bbc.co.uk/news/science-environment-42264788">https://www.bbc.co.uk/news/science-environment-42264788﻿</a> </figcaption></figure>

<h4>What works?</h4>

<p>First of all, it just looks nice. It grabs your attention but not in an aggressive way. The blue bubbles make me think of water which is a nice touch. The data itself is somehow sorted so that the items with the highest numbers are first and scrolling down you see the remaining objects.</p>

<h4>What doesn&#8217;t work?</h4>

<p>The bubbles look nice but are not very easy to compare the values. Another thing is that the decimal parts of the number of items don&#8217;t really help the visualisation. What is 0.4 of a wet wipe and did anyone bite off a half of that cigarette stub? It just doesn&#8217;t really make sense to me. It&#8217;s also hard to imagine the actual effect of these numbers.</p>

<p>Another thing is that the article mentions 718 pieces of litter found for every 100m of a beach. The chart doesn&#8217;t address it in any way, it doesn&#8217;t state that it only shows the top 10 items (which you can find out from the article). Actually, many have fallen for that misinformation doing the #makeovermonday this week.</p>

<h4>How can I improve it?</h4>

<p>I think the key here is to make the data relatable so that it really resonates with the audience. I tried to have a look at the data set which is very simple (10 rows of two fields). In the end I decided to take a look at cotton buds which are easily measured. They pretty much have one dimension (length) and they all seem to be fairly similar length of 7.5cm or so. I thought about that scene in Friends where they build a giant poking stick from chopsticks they gathered over the years*. I wondered how long would a combined length of those cotton buds be for every 100m of a British beach. </p>

<p>As you can see below, the viz is super simple. But it tells you something. Also, when preparing the description, I wondered how the situation has changed in 2018 and it turns out the average number was lower! Not much, but lower. There is still a lot of work but, hopefully, the recent movements for limiting the waste will have their positive effect on the pollution levels.</p>

<figure class="wp-block-image"><img loading="lazy" width="950" height="600" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/dash.png" alt="" class="wp-image-25564" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/dash.png 950w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/dash-300x189.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/dash-768x485.png 768w" sizes="(max-width: 950px) 100vw, 950px" /><figcaption><a href="https://public.tableau.com/profile/hanna.nykowska#!/vizhome/MM2019w14/2metresofcottonbuds">tableau public</a></figcaption></figure>

<p></p>

<p>*They probably shouldn&#8217;t have gathered as many chopsticks as they did. But, hey, it was the 90&#8217;s and also a comedy show so I guess we can forgive that. Hopefully, things are getting better now. (It seems so&#8230;)</p>
