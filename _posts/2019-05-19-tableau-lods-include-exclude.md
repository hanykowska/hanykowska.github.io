---
layout: post
cover: /assets/images/posts-images/lods-include-exclude.png
navigation: True
title: "Tableau LODs: include and exclude"
date: 2019-05-19 00:00:00
tags: [tableau]
class: post-template
subclass: "post"
author: hanykowska
external_url: https://www.thedataschool.co.uk/hanna-nykowska/tableau-lods-include-and-exclude/
external_site: ds
excerpt_separator: <!--more-->
---

Continuing on my post on FIXED LODs, I wanted to shed some light on INCLUDE and EXCLUDE Level of Detail expressions.

[First published on The Data School Blog.]({{page.external_url}}){:target="\_blank"}

<!--more-->

<p>Continuing on my post on FIXED LODs, I wanted to shed some light on INCLUDE and EXCLUDE Level of Detail expressions. It&#8217;s an advanced topic and if you haven&#8217;t read my <a href="https://www.thedataschool.co.uk/hanna-nykowska/intro-to-tableau-lods-fixed/">blog introducing LODs,</a> make sure to do so before continuing with this post.</p>

<p><em>I&#8217;ll be using Sample-Superstore dataset available in Tableau for the purpose of this blog.</em></p>

<div style="height:36px" aria-hidden="true" class="wp-block-spacer"></div>

<h3>INCLUDE Level of Detail</h3>

<p>The syntax for INCLUDE LOD is very similar compared to FIXED. The only difference is changing the keyword to &#8216;include&#8217;. The meaning, however, is quite different. You may recall that I used Coach Andy&#8217;s <a href="http://www.vizwiz.com/2017/04/fixed-lod-pt1.html">approach</a> to translate FIXED LODs into plain English. I decided to apply the idea to INCLUDE LODs as well.</p>

<p>You can translate INCLUDE LOD as &#8216;For every dimension in the view AND every listed dimension, calculate the aggregate expression&#8217;:</p>

<figure class="wp-block-image is-resized"><img loading="lazy" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-44.png" alt="" class="wp-image-26864" width="369" height="88" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-44.png 748w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-44-300x71.png 300w" sizes="(max-width: 369px) 100vw, 369px" /></figure>

<p>For example, if we already have Sub-Category and Category in the view, the calculation will get the sum of Sales for each Sub-Category, Category and Product:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="366" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-46-1024x366.png" alt="" class="wp-image-26866" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-46-1024x366.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-46-300x107.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-46-768x275.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-46-1080x386.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-46.png 1202w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>Hold on, but what happens now? We don&#8217;t have Product in the view, so what are we actually seeing? </p>

<p>Whenever you use INCLUDE LOD, you&#8217;re using <strong>more granular</strong> data than what you have in the view, so then this calculation needs to be <strong>aggregated </strong>to get back to the original (view) level of detail:</p>

<figure class="wp-block-image"><img loading="lazy" width="717" height="442" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-47.png" alt="" class="wp-image-26867" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-47.png 717w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-47-300x185.png 300w" sizes="(max-width: 717px) 100vw, 717px" /><figcaption><br></figcaption></figure>

<p>To make sure you use the correct aggregation for INCLUDE calculation, you can wrap the whole expression in the function of choice or right-click on the field pill -&gt; Default Properties -&gt; Aggregation -&gt; [choose the aggregation here].</p>

<h4>Use Case</h4>

<p>Let&#8217;s say you want to know what are the average Sales by product within each Sub-Category. One way is to have Sub-Category, Product ID and Sales in the view creating a bar chart and then finding the average with a reference line:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="608" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-48-1024x608.png" alt="" class="wp-image-26868" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-48-1024x608.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-48-300x178.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-48-768x456.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-48-1080x641.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-48.png 1498w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>It doesn&#8217;t look very nice, slightly too busy especially that we only want to see the averages, we don&#8217;t really care about particular product sales. </p>

<p>Another way is to use an INCLUDE calculation:</p>

<figure class="wp-block-image is-resized"><img loading="lazy" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-49.png" alt="" class="wp-image-26869" width="457" height="245" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-49.png 562w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-49-300x161.png 300w" sizes="(max-width: 457px) 100vw, 457px" /></figure>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="626" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-50-1024x626.png" alt="" class="wp-image-26870" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-50-1024x626.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-50-300x183.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-50-768x469.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-50-1080x660.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-50.png 1479w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>Apart from cleaning up the view, you can easily sort the data based on the average Sales.</p>

<p>You could argue that this can be also achieved with a FIXED LOD, which is true:</p>

<figure class="wp-block-image"><img loading="lazy" width="599" height="132" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-53.png" alt="" class="wp-image-26873" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-53.png 599w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-53-300x66.png 300w" sizes="(max-width: 599px) 100vw, 599px" /></figure>

<p>INCLUDE, however, adds more flexibility: you can add more dimensions in the view and values will change accordingly:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="603" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-51-1024x603.png" alt="" class="wp-image-26871" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-51-1024x603.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-51-300x177.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-51-768x452.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-51-1080x636.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-51.png 1536w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="600" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-52-1024x600.png" alt="" class="wp-image-26872" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-52-1024x600.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-52-300x176.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-52-768x450.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-52-1080x633.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-52.png 1525w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>FIXED LOD would result in wrong values, unless you build a separate calculation for each of the options.</p>

<div style="height:33px" aria-hidden="true" class="wp-block-spacer"></div>

<h3>EXCLUDE Level of Detail</h3>

<p>EXCLUDE LOD is pretty much the opposite of INCLUDE. Instead of adding more dimensions, you&#8217;re getting rid of them. </p>

<p> You can translate EXCLUDE LOD as &#8216;For every dimension in the view EXCEPT the listed dimension(s), calculate the aggregate expression&#8217;: </p>

<figure class="wp-block-image is-resized"><img loading="lazy" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-54.png" alt="" class="wp-image-26875" width="391" height="83" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-54.png 801w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-54-300x64.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-54-768x164.png 768w" sizes="(max-width: 391px) 100vw, 391px" /></figure>

<p>If we have Sub-Category and Category in the view, the sum of Sales will be calculated for each Category, disregarding the Sub-Category field:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="399" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-55-1024x399.png" alt="" class="wp-image-26877" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-55-1024x399.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-55-300x117.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-55-768x299.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-55-1080x421.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-55.png 1157w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>This time the calculation is performed at a <strong>less granular</strong> level than what you have in the view and so the resulting values will be <strong>duplicated </strong>in the view:</p>

<figure class="wp-block-image"><img loading="lazy" width="699" height="431" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-56.png" alt="" class="wp-image-26878" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-56.png 699w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-56-300x185.png 300w" sizes="(max-width: 699px) 100vw, 699px" /></figure>

<h4>Use Case</h4>

<p>One thing you can use exclude for is to present detailed data together with less granular values for reference. For example, you can calculate the difference between average sales for Sub-Categories and average sales for the corresponding Category.</p>

<p>You&#8217;ll need one EXCLUDE LOD for this:</p>

<figure class="wp-block-image"><img loading="lazy" width="408" height="214" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-57.png" alt="" class="wp-image-26879" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-57.png 408w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-57-300x157.png 300w" sizes="(max-width: 408px) 100vw, 408px" /></figure>

<p>And a basic calculation using the above:</p>

<figure class="wp-block-image"><img loading="lazy" width="415" height="258" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-58.png" alt="" class="wp-image-26880" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-58.png 415w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-58-300x187.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-58-400x250.png 400w" sizes="(max-width: 415px) 100vw, 415px" /></figure>

<p>If you add Category, Sub-Category, Avg(Sales) and the two calculations above, this is what you get in your view:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="480" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-59-1024x480.png" alt="" class="wp-image-26882" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-59-1024x480.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-59-300x140.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-59-768x360.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-59-1080x506.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-59.png 1247w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>Again, you could argue that instead of EXCLUDE you could use FIXED. This is true (again). With EXCLUDE (just like with INCLUDE), you can add more dimensions into the view and the values will be recalculated:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="539" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-60-1024x539.png" alt="" class="wp-image-26883" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-60-1024x539.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-60-300x158.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-60-768x404.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-60-1080x569.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-60.png 1700w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>FIXED calculation</p>

<figure class="wp-block-image"><img loading="lazy" width="285" height="68" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-61.png" alt="" class="wp-image-26884" /></figure>

<p>would have duplicated values across the segments:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="542" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-62-1024x542.png" alt="" class="wp-image-26885" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-62-1024x542.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-62-300x159.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-62-768x406.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-62-1080x571.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-62.png 1698w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>To get exactly the same values, you&#8217;d need to create separate caluclations for each option.</p>

<div style="height:100px" aria-hidden="true" class="wp-block-spacer"></div>

<h3>Recap</h3>

<p>To recap, the type of LOD (and whether you need an LOD calculation in the first place) will depend on what you have in the view. Another factor is whether you want your calculation to be flexible or not. </p>

<p>Apart from exams and exercises I haven&#8217;t used many INCLUDE or EXCLUDE LODs but it is definitely beneficial to understand what is going on.</p>

<p>I imagine the calculations are based on temporary tables that are changed whenever you use an LOD expression:</p>

<figure class="wp-block-image"><img loading="lazy" width="812" height="614" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-63.png" alt="" class="wp-image-26887" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-63.png 812w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-63-300x227.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-63-768x581.png 768w" sizes="(max-width: 812px) 100vw, 812px" /></figure>

<p>Whenever the calculation is performed for more granular data than the view, the values will be aggregated. When the calculation is performed for less granular data, the values will be duplicated:</p>

<figure class="wp-block-image"><img loading="lazy" width="705" height="433" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-64.png" alt="" class="wp-image-26888" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-64.png 705w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-64-300x184.png 300w" sizes="(max-width: 705px) 100vw, 705px" /></figure>

<p>This is quite a lot to handle, but I hope this post was helpful. There is still more to LODs. For example, FIXED is calculated before INCLUDE or EXCLUDE and so it will work differently with filters. To learn more on LODs and filters, check out <a href="https://onlinehelp.tableau.com/current/pro/desktop/en-us/calculations_calculatedfields_lod_filters.htm">Tableau help page</a>.  The <a href="https://www.youtube.com/watch?v=kfXwYGaZvLc&amp;t=7s">recording</a> of my webinar on LODs is up on YouTube if you want to check it out and the <a href="https://public.tableau.com/profile/hanna.nykowska#!/vizhome/LOD_webinar/Intro">workbook</a> I used for that webinar is on Tableau Public.</p>
