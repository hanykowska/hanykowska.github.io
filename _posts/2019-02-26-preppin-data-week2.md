---
layout: post
cover: /assets/images/posts-images/preppin-data-week2.png
navigation: True
title: "Preppin’ Data: Week 2 Recap"
date: 2019-02-26 00:00:00
tags: []
class: post-template
subclass: "post"
author: hanykowska
external_url: https://www.thedataschool.co.uk/hanna-nykowska/preppin-data-week-2-recap/
external_site: ds
excerpt_separator: <!--more-->
---

Summary of the week 2 Preppin’ Data challenge.

[First published on The Data School Blog.]({{page.external_url}}){:target="\_blank"}

<!--more-->

<p>For those of you who don&#8217;t know what Preppin&#8217; Data is about, it&#8217;s an initiative of Coach <a href="https://www.thedataschool.co.uk/blog/carl-allchin/">Carl</a> and my fellow cohortian <a href="https://www.thedataschool.co.uk/blog/jonathan-allenby/">Jon</a> to popularise Tableau Prep in a weekly series of challenges. It works in a similar way to Alteryx Community Weekly Challenges, where you&#8217;re presented with input data and the expected outcome, and the task is to figure out the flow that gets you from point A to point B. For more info, check their <a href="https://preppindata.blogspot.com/">blog</a>.</p>

<p>It&#8217;s been almost a whole week since Week 2 problem was published and I thought (or rather Carl thought&#8230;) I give you a short summary of the problem and solution 🙂</p>

<h3>Problem</h3>

<p>This is the preview of the dataset (in Excel, sorry):</p>

<figure class="wp-block-image"><img loading="lazy" width="564" height="266" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-80.png" alt="" class="wp-image-24536" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-80.png 564w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-80-300x141.png 300w" sizes="(max-width: 564px) 100vw, 564px" /></figure>

<figure class="wp-block-image"><img loading="lazy" width="549" height="171" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-81.png" alt="" class="wp-image-24537" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-81.png 549w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-81-300x93.png 300w" sizes="(max-width: 549px) 100vw, 549px" /></figure>

<p>As you can see, we have some fancy headers at the top of the spreadsheet and there&#8217;s some extra space between data for London and Edinburgh. Another thing to notice (not so obvious from the snippets above) is that the values for City field have some interesting typos in them. The expected output also had separate fields for all Metric and Measure combinations.</p>

<div style="height:43px" aria-hidden="true" class="wp-block-spacer"></div>

<h3>Solution</h3>

<h4>Wildcard Input</h4>

<p>First of all, you need to upload your data. I know there are a few things to do it but I used the data interpreter (my new friend), which quite accurately splits the whole sheet into two tables, and then used the <strong>wildcard</strong> option:</p>

<figure class="wp-block-image"><img loading="lazy" width="812" height="823" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-82.png" alt="" class="wp-image-24552" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-82.png 812w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-82-296x300.png 296w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-82-768x778.png 768w" sizes="(max-width: 812px) 100vw, 812px" /></figure>

<p>For a matching pattern in sheet names, I put &#8216;* A*&#8217; which takes anything that has &#8216; A&#8217; in its name. &#8216;*&#8217; is the wildcard which takes anything. This way we have both tables loaded as one. Noice.</p>

<h4>Group and Replace</h4>

<p>Moving on, we need to sort out our cities. Once you add the clean step, right-click on the City field -&gt; Group and Replace -&gt; Spelling. This will magically pick the values with similar spelling and group them together assigning the most common value. You can overwrite the automatic grouping by clicking on the group:</p>

<figure class="wp-block-image"><img loading="lazy" width="547" height="379" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-83.png" alt="" class="wp-image-24557" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-83.png 547w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-83-300x208.png 300w" sizes="(max-width: 547px) 100vw, 547px" /></figure>

<p>In the screenshot above, you can see one value that should be in London group, just check its box on the right-hand side. To rename the whole group, either click on three dots in the window on the left or double-click on the group on the left. Sweet.</p>

<h4>Combine Metric and Measure</h4>

<p>This is easy, just requires one calculated field (I called it &#8216;Metric &#8211; measure&#8217;, the name doesn&#8217;t make much of a difference here):</p>

<pre class="wp-block-code"><code>[Metric] + ' - ' + [Measure]</code></pre>

<p>It just concatenates the texts in the Metric and Measure fields together.</p>

<p>Now we can get rid of unnecessary fields. For me these would be: Metric, Measure, Table Names, File Paths. The last two are automatically generated when using a wildcard input.</p>

<h4>Pivot Rows to Columns</h4>

<p>In Alteryx, this is a separate tool. In Prep, this is an option within Pivot tool. Columns to Rows is the default option. To change it, click on the caret next &#8216;Columns to Rows&#8217; in the Pivoted Fields pane. Whoa&#8230; Then I dragged my calculated field (Metric &#8211; measure) on &#8216;Fields that will pivot rows to columns&#8217; or the upper part of the Pivot Fields pane and Value field on &#8216;Field to aggregate for new columns&#8217;. It will automatically set the aggregation method to sum which is fine as there should only be one value per specific date.</p>

<figure class="wp-block-image"><img loading="lazy" width="407" height="643" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-84.png" alt="" class="wp-image-24562" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-84.png 407w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-84-190x300.png 190w" sizes="(max-width: 407px) 100vw, 407px" /></figure>

<h4>Output</h4>

<p>Make sure to output your data in a format of your choice. It can be .csv .hyper or .tde. That&#8217;s it!</p>

<figure class="wp-block-image"><img loading="lazy" width="987" height="420" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-85.png" alt="" class="wp-image-24563" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-85.png 987w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-85-300x128.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/image-85-768x327.png 768w" sizes="(max-width: 987px) 100vw, 987px" /></figure>

<p>That&#8217;s much easier to process than the original data set&#8230;</p>

<p>If you haven&#8217;t already, have a look at the Preppin&#8217; Data <a href="https://preppindata.blogspot.com/">blog</a> and start Preppin&#8217;!</p>
