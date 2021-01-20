---
layout: post
cover: /assets/images/posts-images/tooltip-viz.png
navigation: True
title: "Tableau Tip: Tooltip Viz"
date: 2019-03-05 00:00:00
tags: [tableau]
class: post-template
subclass: "post"
author: hanykowska
external_url: https://www.thedataschool.co.uk/hanna-nykowska/tableau-tip-tooltip-viz/
external_site: ds
excerpt_separator: <!--more-->
---

Short tutorial on how to create a tooltip viz that is susceptible to dashboard actions

[First published on The Data School Blog.]({{page.external_url}}){:target="\_blank"}

<!--more-->

<p>I was always impressed whenever someone had an actual chart/view whatever you want to call it in the tooltips. In my opinion, it&#8217;s a great way to go into more detail for those interested without cluttering the dashboard. After one of the Friday projects, one of our coaches, <a href="https://www.thedataschool.co.uk/blog/carl-allchin/">Carl</a>, showed me how easy it is in Tableau. Brace yourselves to have your minds blown.</p>

<h4>What&#8217;s the hype about?</h4>

<p>If you&#8217;re not sure what this whole tooltip viz is, I&#8217;ll use my <a href="https://public.tableau.com/profile/hanna.nykowska#!/vizhome/MM2019w10_15517330792230/Dashboard">submission</a> for this week&#8217;s <a href="https://www.makeovermonday.co.uk/">#makeovermonday</a>:</p>

<figure class="wp-block-image"><img loading="lazy" width="655" height="875" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/tooltipgif.gif" alt="" class="wp-image-25042" /><figcaption>The program I&#8217;m using for creating gifs doesn&#8217;t allow me to have hover actions on the dashboard within the recording area but I&#8217;ve found my way around it 😀</figcaption></figure>

<p>The dashboard itself is fairly simple, which is what I wanted. I wanted something that is not overwhelming (I&#8217;d found the topic itself quite overwhelming so a lot of white space was important for me, to breathe I guess&#8230;). But when you make something simple you may lose some key information. For those interested in how the metrics in the view changed over time I added the time trends in the tooltips.</p>

<p>In the gif above, you can see the tooltip viz changing, it&#8217;s due to dashboard actions that filter the data. I&#8217;ll get to it shortly.</p>

<h4>How to</h4>

<p>If you want to create a tooltip viz, you&#8217;ll need at least two sheets: one with the view you want to show in the tooltip and one where you want to have the tooltip on. </p>

<p>The former needs to be fairly easy to read because if you want to have responsive tooltips (the default setting, they show instantly), you won&#8217;t be able to hover on top of that tooltip, so you can&#8217;t get nested tooltips. Even if you select tooltip on hover, you still won&#8217;t get nested tooltip, so just make that graph easy to read.</p>

<p>To actually set the tooltip viz, click on Tooltip on marks card and edit the tooltip how you want it to look like apart from the extra view. Once that is done, place your cursor where you want to have your view, go to Insert -&gt; Sheets. You should be able to see all of your sheets now:</p>

<figure class="wp-block-image"><img loading="lazy" width="927" height="141" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-8.png" alt="" class="wp-image-25044" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-8.png 927w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-8-300x46.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-8-768x117.png 768w" sizes="(max-width: 927px) 100vw, 927px" /></figure>

<p>What is quite helpful here, are appropriate names for the sheets so you can easily find what you&#8217;re after.</p>

<p>Ok, here&#8217;s something similar to what you&#8217;d get after selecting the sheet of choice:</p>

<figure class="wp-block-image"><img loading="lazy" width="469" height="48" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-9.png" alt="" class="wp-image-25045" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-9.png 469w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-9-300x31.png 300w" sizes="(max-width: 469px) 100vw, 469px" /></figure>

<p>I think it&#8217;s fairly self-explanatory: Sheet name indicates which sheet we&#8217;re inserting, maxwidth and maxheight limit the size of the view, in filter you&#8217;re likely to have &lt;All Fields&gt; rather than anything specific.</p>

<p>If you click OK and check the tooltip in the sheet, it should already have that viz inside. So easy!</p>

<h4>Tooltip Viz and Dashboard Actions</h4>

<p>Because my dashboard used the map as the filter for other fields, I wanted the tooltips to also include this functionality. It wasn&#8217;t as straightforward as I expected, but not really too difficult either.</p>

<p>Once you have you dashboard actions all prepared, go to the sheet that has you customised tooltip. On the filters shelf, you should have at least one that&#8217;s automatically generated (<em>in italics</em>) called <em>Action (</em>something<em>).</em> Right-click on that pill (or click on the caret) -&gt;Apply to Worksheets -&gt; Selected Worksheets&#8230;</p>

<figure class="wp-block-image"><img loading="lazy" width="407" height="312" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-10.png" alt="" class="wp-image-25046" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-10.png 407w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-10-300x230.png 300w" sizes="(max-width: 407px) 100vw, 407px" /></figure>

<p>A pop-up window will open where you can select which sheet the action should apply to:</p>

<figure class="wp-block-image"><img loading="lazy" width="554" height="454" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-11.png" alt="" class="wp-image-25047" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-11.png 554w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-11-300x246.png 300w" sizes="(max-width: 554px) 100vw, 554px" /></figure>

<p>If you want the action to affect your tooltip (I hope you do, that&#8217;s the reason you would keep reading this far), select the sheet with your tooltip view &#8211; &#8216;nurses trend&#8217; in my case.</p>

<p>That&#8217;s it! Now you should have a functional view in tooltip that also works with your dashboard actions:</p>

<figure class="wp-block-image"><img loading="lazy" width="1183" height="719" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-12.png" alt="" class="wp-image-25048" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-12.png 1183w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-12-300x182.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-12-768x467.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-12-1024x622.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-12-1080x656.png 1080w" sizes="(max-width: 1183px) 100vw, 1183px" /></figure>

<p></p>

<p>Byeee!</p>
