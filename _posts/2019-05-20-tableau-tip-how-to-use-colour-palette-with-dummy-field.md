---
layout: post
cover: /assets/images/posts-images/colour-palette-dummy-field.png
navigation: True
title: "Tiny Tableau Tip: how to use a colour palette with a dummy field"
date: 2019-05-20 00:00:00
tags: [tableau]
class: post-template
subclass: "post"
author: hanykowska
external_url: https://www.thedataschool.co.uk/hanna-nykowska/tiny-tableau-tip-how-to-use-a-colour-palette-with-a-dummy-field/
external_site: ds
excerpt_separator: <!--more-->
---

Can you use the saved colour palettes without picking the screen colour or copying the hex codes? Keep on reading.

[First published on The Data School Blog.]({{page.external_url}}){:target="\_blank"}

<!--more-->

<p>There were a few blog posts on dealing with colours in Tableau, but how can you use the saved colour palettes without picking the screen colour or copying the hex codes? Keep on reading.</p>

<p>Whenever you want to change a colour of the marks but you don&#8217;t have any field on the colour, this is what you end up with:</p>

<figure class="wp-block-image"><img loading="lazy" width="213" height="422" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-84.png" alt="" class="wp-image-26947" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-84.png 213w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-84-151x300.png 151w" sizes="(max-width: 213px) 100vw, 213px" /></figure>

<p>If you click on More colors&#8230; you will see a colour picker (1):</p>

<p></p>

<figure class="wp-block-image is-resized"><img loading="lazy" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-85.png" alt="" class="wp-image-26948" width="333" height="270" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-85.png 521w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-85-300x243.png 300w" sizes="(max-width: 333px) 100vw, 333px" /></figure>

<p>not a list of custom colour palettes (2):</p>

<figure class="wp-block-image is-resized"><img loading="lazy" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-86.png" alt="" class="wp-image-26949" width="334" height="272" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-86.png 498w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-86-300x245.png 300w" sizes="(max-width: 334px) 100vw, 334px" /></figure>

<p>So how do you go from (1) to (2)?</p>

<h4>1. Create a dummy field</h4>

<p>You can either create an ad-hoc calculation on the marks card. Double-click on the empty space on the Marks card and just type in:</p>

<pre class="wp-block-code"><code>''</code></pre>

<p>This will automatically assign it to detail.</p>

<p>The alternative is to create a calculated field, call it whatever you like (eg. Dummy) and type in as above.</p>

<h4>2. Put the dummy field on Color</h4>

<p>Whichever method you&#8217;re using (ad-hoc or saved calculation), drag it onto Color.</p>

<figure class="wp-block-image"><img loading="lazy" width="154" height="207" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-87.png" alt="" class="wp-image-26951" /></figure>

<h4>3. Choose a colour from a colour palette</h4>

<p>Now, you can go to Color -&gt; Edit Colors and you end up with (2)!</p>

<figure class="wp-block-image"><img loading="lazy" width="703" height="415" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-88.png" alt="" class="wp-image-26952" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-88.png 703w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-88-300x177.png 300w" sizes="(max-width: 703px) 100vw, 703px" /></figure>

<h4>Caveats</h4>

<p>There&#8217;s something to have in mind, whenever you&#8217;re using an ad-hoc calculations with colours, the colour palette will default to automatic palette when uploaded on Server. The walkaround is to save the calculation and problem solved 🙂</p>

<p>For continuous options (don&#8217;t know why would you want that), use <strong>0</strong> instead of <strong>&#8221;</strong>.</p>
