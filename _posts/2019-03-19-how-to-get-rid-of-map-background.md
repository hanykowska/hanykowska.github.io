---
layout: post
cover: /assets/images/posts-images/get-rid-of-background-map.png
navigation: True
title: "Tiny Tableau Tip: How to get rid of the map background"
date: 2019-03-19 00:00:00
tags: [tableau]
class: post-template
subclass: "post"
author: hanykowska
external_url: https://www.thedataschool.co.uk/hanna-nykowska/tiny-tableau-tip-how-to-get-rid-of-the-map-background/
external_site: ds
excerpt_separator: <!--more-->
---

A tiny tableau tip on getting rid of the map background, very useful when you’re building a dashboard with a coloured background.

[First published on The Data School Blog.]({{page.external_url}}){:target="\_blank"}

<!--more-->

<p>During the #vizforsocialgood hackathon last weekend (I wrote a blog post on what it is, check it out <a href="https://www.thedataschool.co.uk/hanna-nykowska/attending-vizforsocialgood-hackathon-what-is-it-and-why-is-it-worth-going-to/">here</a>), <a href="https://twitter.com/RomeoAI_">Rai</a>, one of the participants, was trying to get rid of the white background of a map because he had a different background colour on the dashboard. This turned out to be something else than I expected and so I decided to share the solution with you.</p>

<p>My first thought was to change washout to 100%. This fades out the map marks but the white background remained:</p>

<figure class="wp-block-image"><img loading="lazy" width="745" height="567" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-47.png" alt="" class="wp-image-25254" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-47.png 745w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-47-300x228.png 300w" sizes="(max-width: 745px) 100vw, 745px" /></figure>

<p>Here’s what you need to do instead. First, go to Format -&gt; Shading and set Worksheet and Pane values to None. Then, go to Map-&gt; Map Layers and untick all of the Map Layers. Unfortunately, I couldn’t find a way to unselect all of them so you need to uncheck them individually. This should do the trick! </p>

<figure class="wp-block-image"><img loading="lazy" width="720" height="547" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-48.png" alt="" class="wp-image-25255" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-48.png 720w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-48-300x228.png 300w" sizes="(max-width: 720px) 100vw, 720px" /></figure>

<p>If you don&#8217;t see the @OpenStreetMap note, that&#8217;s because I also change the washout to 0%. To be honest, you can pick which layers you want to keep but Base is the one you want to remove. </p>

<p>If you have some gaps that you want to have a background for, you&#8217;ll need to do the trick Jon wrote about in his <a href="https://www.thedataschool.co.uk/jonathan-allenby/a-quick-map-hack-to-display-a-single-region/">post</a> (just remember to get rid of the Base).</p>

<p></p>

<p>Thanks for reading, byeeee!</p>
