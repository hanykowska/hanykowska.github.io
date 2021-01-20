---
layout: post
cover: /assets/images/posts-images/highlight-table-with-info-icon-cover.png
navigation: True
title: "Tableau Tip: Highlight Table with Info Icons"
date: 2019-07-23 00:00:00
tags: [tableau]
class: post-template
subclass: "post"
author: hanykowska
excerpt_separator: <!--more-->
external_url: https://www.theinformationlab.co.uk/2019/07/23/tableau-tip-highlight-table-with-info-icons/
external_site: til
---

Oh, so you want detailed data in form of highlight table that includes info button for each row? I got you covered!

[First published on The Information Lab Blog.]({{page.external_url}}){:target="\_blank"}
<!--more-->

<p>Let's say you want to give your audience detailed data in form of a table. At the same time, you want to add colour but also and information button, which makes it obvious that you can hover over it for more details. In short, you want something like this:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-49.png" alt="" class="wp-image-14606"/></figure>
<p>To have the names of the fields present in the table, you'll need to do a bit of trick, but I'll walk you through it step-by-step. In this example, I'm using Sample Superstore available with Tableau Desktop.</p>
<h3>1. Build the table</h3>
<p>First, we just want to have the table ready. Go ahead an put the following fields onto Rows shelf:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-50.png" alt="" class="wp-image-14608"/></figure>
<p>Product ID is by default hidden. To show all hidden fields, click on the small arrow next to <strong>Dimensions</strong> -&gt; Show Hidden Fields:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-51.png" alt="" class="wp-image-14609"/></figure>
<p>You should end up with something similar:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-52-1024x595.png" alt="" class="wp-image-14610"/></figure>
<p>Now, double-click on Profit, Quantity and Sales. This should do a few things. Instead of just the measures on the columns, there is Measure Names, Measure Values are on text and three measures that were clicked on are on the Measure Values tab:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-53.png" alt="" class="wp-image-14611"/></figure>
<p>We have our table.</p>
<h3>2. Change it to a highlight table</h3>
<p>Now that we have the values in the table, we want to help the audience get the message easier. To do that, hit ctrl and drag Measure Values onto colour. This will change the colour of the text which is not exactly what we want. </p>
<p>To change it into a highlight table, change the mark type to square. Now, we do have a background for each cell, but there's only a single colour legend. The problem with this is that Profit will range between negative and positive values, Sales will have only positive but might have very high positive values while quantity will have values of tens, maybe. To separate the colours, right-click on Measure Values assigned to colour -&gt; Use Separate Legends:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-54.png" alt="" class="wp-image-14612"/></figure>
<p>This will separate the legends by Measure Names and you can adjust them by right-clicking on the legends -&gt; Edit colours.</p>
<p>You should have something like this:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-55.png" alt="" class="wp-image-14613"/></figure>
<h3>3. The trick</h3>
<p>Ok, here we go. Double-click on the white space next to Measure Names on Columns shelf and type in avg(0). Double-click on the white space next to the new green pill and type in avg(0.5). Then right-click on either of the new green pills -&gt; Dual Axis. You might be thinking we're breaking our beautiful highlight table, but bear with me. This is the view for now:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-56.png" alt="" class="wp-image-14614"/></figure>
<p>On avg(0.5) tab on Marks card, get rid of any Measure Values, as nothing else was there, it should be empty now:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-57.png" alt="" class="wp-image-14615"/></figure>
<p>Compared to the previous photo, you can see that now there are four measure-related columns, despite having only three measures on the Measure Values card. The name of the new column is not exactly elegant, so right-click on it and hit Edit Alias and change avg(0.5) to Information:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-58.png" alt="" class="wp-image-14616"/></figure>
<p>Right-click on any of the axes -&gt; Synchronise Axis. Right-click again -&gt; Edit Axis then change range to fixed from 0 to 1:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-59.png" alt="" class="wp-image-14617"/></figure>
<p>Now right-click on the axes and unselect Show Header. </p>
<p>Ok, we're almost there. </p>
<p>On avg(0.5) tab on Marks card, change the marks type to shape. Create a new calculated field called Dummy (or whatever you'd like) and type in</p>
<pre class="wp-block-code"><code>''</code></pre>
<p>This is only an empty string as we need an actual field to have more control over the shape and its colour. Drag new Dummy field onto colour and shape and adjust it to your preferences. Depending on your available shapes and selected colour, your view will be probably slightly different to mine:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-60.png" alt="" class="wp-image-14618"/></figure>
<p>Now let's rebuild our highlight table.</p>
<p>On the avg(0) tab on the Marks card, change the mark type to Gantt Bar. Double-click on the white space on the tab and type in avg(1), then move it to size. This will create a colour coded background, almost like in the highlight table we've had previously. Click on the size on this tab and move the slider to the right, it will fill the cell vertically:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-61.png" alt="" class="wp-image-14619"/></figure>
<p>The last thing is to get rid of the grid lines. Go to Format -&gt; Lines. Grid Lines says None but don't believe it and re-set it to None, and the grid lines should disappear! </p>
<p>Now you can add whatever information you'd like to have in the tooltip on the information icon. You can either have the same tooltips for the other measures or disable the tooltips for highlight table by deleting text from tooltip for Gantt Bar mark.</p>
<p>There you go! Thanks for reading :)</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-62.png" alt="" class="wp-image-14620"/></figure>
