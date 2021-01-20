---
layout: post
cover: /assets/images/posts-images/MM2019w16.png
navigation: True
title: "Makeover Monday 2019w16 – bars bars (bars)"
date: 2019-04-15 00:00:00
tags: [tableau]
class: post-template
subclass: "post"
author: hanykowska
external_url: https://www.thedataschool.co.uk/hanna-nykowska/hannas-makeover-monday-2019w16-bars-bars-bars/
external_site: ds
excerpt_separator: <!--more-->
---

Looking at #makeovermonday 2019w16: word use in the ‘Info we Trust’ book by RJ Andrews

[First published on The Data School Blog.]({{page.external_url}}){:target="\_blank"}

<!--more-->

<p>After a bit of a break (I still haven&#8217;t finished my 2019w15 Makeover Monday, but don&#8217;t worry, I&#8217;m getting there), I&#8217;m back with my blogs.</p>

<p>This week focuses on the words used in the <em><a href="https://infowetrust.com/inspire/">Info we Trust</a></em><a href="https://infowetrust.com/inspire/"> by RJ Andrews</a>. The original visualisation is shown below:</p>

<figure class="wp-block-image"><img src="https://media.data.world/HqPI2jUxRF69iYygJP7W_voyant-tools-wordcloud.png" alt="" /></figure>

<h3>What doesn&#8217;t work?</h3>

<p>First of all, I don&#8217;t even know what I&#8217;m looking at. It is a word cloud, fine, but I don&#8217;t know where do the words come from. What are they representing? I simply don&#8217;t know. </p>

<p>Another thing is the colours. Just too many. Way too many.</p>

<h3>What does work?</h3>

<p>Even though a word cloud may not be the best chart type, it is quite intuitive. The fact that <em>data</em> is by far the biggest and in the horizontal orientation is helping focus the attention.</p>

<h3>How can I improve it?</h3>

<p>I thought I&#8217;d definitely want to add some information, at least where is the data coming from and what is the viz showing. I&#8217;m not convinced using all of the words is the best idea since some are barely noticeable and just add clutter without adding extra information.</p>

<p>Below you can see my makeover:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="683" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/dash-1-1024x683.png" alt="" class="wp-image-25888" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/dash-1-1024x683.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/dash-1-300x200.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/dash-1-768x512.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/dash-1-1080x720.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/dash-1.png 1200w" sizes="(max-width: 1024px) 100vw, 1024px" /><figcaption><a href="https://public.tableau.com/profile/hanna.nykowska#!/vizhome/MM2019w16/InfoWeTrustTop10Words">Interactive viz</a></figcaption></figure>

<p>In here, I focused on the top 10 words by count and their use throughout the book. During our Makeover Monday session in the Data School, <a href="https://www.thedataschool.co.uk/blog/robert-headington/">Robert</a> had pointed out that some of the sections are longer than others. To accommodate for this I just wrote an LOD that calculated word count per page. This allowed comparing the word concentration in different sections of the book. (If you don&#8217;t know what LODs are or just want some extra clarification, stay tuned because I&#8217;ll be writing a blog post on it very soon!)</p>

<p>In my viz I also incorporated the colours of the book itself which is always a nice touch:</p>

<figure class="wp-block-image"><img src="https://i0.wp.com/infowetrust.com/wp-content/uploads/2019/01/IMG_6927.jpg?resize=700%2C525&amp;ssl=1" alt="" /></figure>

<p>That&#8217;s it from me for now. It seems that I&#8217;m catching up with my blog posts so expect more content soon 🙂</p>
