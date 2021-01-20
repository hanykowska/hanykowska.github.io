---
layout: post
cover: /assets/images/posts-images/the-index-trick-cover.png
navigation: True
title: "Tableau Tip: The INDEX Trick"
date: 2019-12-31 00:00:00
tags: [tableau]
class: post-template
subclass: "post"
author: hanykowska
excerpt_separator: <!--more-->
external_url: https://www.theinformationlab.co.uk/2019/12/31/tableau-tip-the-index-trick/
external_site: til
---

I wanted to share something that I have found very useful in the past year. What I have in mind, is something I call 'the Index trick'.

[First published on The Information Lab Blog.]({{page.external_url}}){:target="\_blank"}
<!--more-->

<p>It is the last day of 2019 and I wanted to share something that I have found very useful in the past year. What I have in mind, is something I call 'the Index trick'. Before I start, I wanted to give a shout to <a href="https://twitter.com/cjdaffern">Charlie Daffern</a> as she suggested it to me when I first needed it but then I have found many other use cases for this technique.</p>
<p>The Index trick is using the INDEX() function as a filter. It is often rather easy to use. However, the configuration of the table calculation can be tricky (something to keep in mind).</p>
<p>I'll first explain the index trick on an example and then will show a few ways of setting it up, and give more use cases. If you're interested in the last bit, jump to the end of this post.</p>
<h2>Example</h2>
<p>Let's say you use a measure filter to see only the products that have sales above a certain threshold and count those products. As measure filters are late in the <a href="https://help.tableau.com/current/pro/desktop/en-us/order_of_operations.htm">order of operations</a> (see below), the COUNTD function will be performed <strong>before</strong> the filter on sales is applied. This means the count of products will take all products into account and will be incorrect. Because it is a measure filter (after all we need a sum of sales), it cannot be added to context.</p>
<figure class="wp-block-image size-large"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/12/image.png" alt="" class="wp-image-15818"/></figure>
<figure class="wp-block-image size-large"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/12/image-1.png" alt="" class="wp-image-15819"/><figcaption>The above also doesn't split the sales for each product</figcaption></figure>
<p>A way around it is to have the Product Name on detail, but this results in many 1s while we just want a single number:</p>
<figure class="wp-block-image size-large"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/12/image-2-1024x598.png" alt="" class="wp-image-15820"/></figure>
<p>This approach, however, shows us how many products meet our filter conditions. In the bottom left corner, you can see there are only 747 Product Names with sales equal or greater to $500, compared to 1850 previously.</p>
<p>To change the 1s into the total number, we need to wrap a TOTAL function around CNTD(Product Name):</p>
<figure class="wp-block-image size-large"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/12/image-3-1024x580.png" alt="" class="wp-image-15821"/></figure>
<p>This is great because now we get the right number. Except that it's repeated 746 unnecessary times. Here we get to the Index trick and I'll show a few ways of setting it up.</p>
<h3>Option 1) INDEX() calculation as filter</h3>
<ul><li>Double-click on the marks shelf and just type INDEX(). This will add it to detail. </li><li>Change that to label, so that you can see how the Index is assigned. </li><li>Right-click on the INDEX() -&gt; Calculate using -&gt; Product Name. Now the 1s change to incrementing numbers. </li><li>With the Index function set up correctly, drag it to the filter shelf -&gt; At Most -&gt; change the number to 1. You should now have only one number visible, as per GIF below:</li></ul>
<figure class="wp-block-image size-large"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/12/adhoc-filter.gif" alt="" class="wp-image-15822"/></figure>
<h3>Option 2) INDEX() = 1</h3>
<ul><li>Another way to get the same affect is to type in INDEX() = 1 instead of INDEX(). This will be a logic statement and so first you should see True everywhere (after changing the pill assignment to label that is!)</li><li>After setting Calculate using -&gt; Product Name, only the first mark should have the value of True, the other ones should be False</li><li>Move the created pill to filters card and tick True. You should get the same result as in Option 1</li></ul>
<figure class="wp-block-image size-large"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/12/logical-filter.gif" alt="" class="wp-image-15823"/></figure>
<p></p>
<h2>Notes</h2>
<p>Of course, both options can be used with a saved calculated field as opposed to an ad-hoc calculation (double-clicking on the marks card).</p>
<p>In Option 2, instead of hard-coding (typing in a specific number) the index value, you could use a parameter to have more flexibility</p>
<h2>Use cases</h2>
<p>The above example shows how useful the Index trick is when the task in question can be quite complex and the order of operations forces you to be more creative. (I was planning to say it gets in the way, but it's not really the order of operations' fault...)<br>Whenever you need to play around with table calculations, such as TOTAL, or Window_&lt;aggregation&gt; functions, the Index trick can be useful to get rid of the repeated values.</p>
<p>Another situation is when you Hide some values. It is likely, you will be able to use the Index trick instead. The advantage of using the Index trick instead of hiding marks is that it's much more visible. This, in turn, helps with documentation and handover of your work. I'm sure those continuing with your work will be grateful for a visible Index filter instead of hiding values away!</p>
<p></p>
<p>Let me know where you use the index trick yourself!</p>
<p>That's it from me in 2019. Have a fantastic next decade!</p>
