---
layout: post
cover: /assets/images/posts-images/mapdrilldown.gif
navigation: True
title: "Tableau Tip: Map Drill-Down"
date: 2019-03-09 00:00:00
tags: [tableau]
class: post-template
subclass: "post"
author: hanykowska
external_url: https://www.thedataschool.co.uk/hanna-nykowska/tableau-tip-map-drill-down/
external_site: ds
excerpt_separator: <!--more-->
---

Tableau tip on creating a drill down map using a simple filter action.

[First published on The Data School Blog.]({{page.external_url}}){:target="\_blank"}

<!--more-->

<p>Hi everyone! This week we had our first client project, which was a lot. A lot of work but also many learning opportunities. That was one thing in particular that I wanted to share with you. Hence this tutorial. </p>

<p>What we were asked for, was to create a dashboard allowing to explore variables at two levels of a geographical hierarchy. In this scenario, geographical meant map (it isn&#8217;t always the case). </p>

<p>First, I approached the problem with set actions. I must stress that I have rather little experience with set actions although if you&#8217;re interested in the topic I can recommend <a href="https://twitter.com/datavizlinds">Lindsey Poulter</a>&#8216;s <a href="http://www.lindseypoulter.com/2018/12/18/getsetgo/">blog</a>. Apart from great content and intro to the topic, you can find a link to Lindsey&#8217;s workbook which proved super helpful for me. </p>

<p>Now back to the challenge. As stated above, I tried with set actions. It worked but to have the map at the higher and lower level with appropriate tooltips I needed to nearly identical dashboards. The only difference would be the map that I was using. Having decided this walkaround is not optimal (both in terms of performance and amount of work), I seeked help. DS12 was in training with Andy (here are my first two options gone), Carl was nowhere to be found (option three gone)&#8230; Thankfully, a few people from the core team were working in the open space of the office. After hearing my weak &#8216;Help!&#8217; cry, <a href="https://twitter.com/bethanyfox17">Bethany</a> decided to try and help me. And she introduced me into a super quick solution that now I&#8217;m going to share with you!</p>

<div style="height:46px" aria-hidden="true" class="wp-block-spacer"></div>

<h3>How To</h3>

<p>For the purpose of the tutorial, I decided to rebuild my map trick with Sample &#8211; Superstore data so that you can easily follow along.</p>

<p><strong>Create&nbsp;hierarchy.</strong> First, we need to have a hierarchy of geographical fields. Let&#8217;s use fields State and Region to do that. If you&#8217;re familiar with the Superstore data, you&#8217;ll know that Regions contain States. It&#8217;s a one-to-many relation (one Region contains many States) which is an important point in creating hierarchy.</p>

<p>To create the hierarchy, click and drag the Region between State and Country:</p>

<figure class="wp-block-image"><img loading="lazy" width="289" height="132" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-13.png" alt="" class="wp-image-25069" /></figure>

<figure class="wp-block-image"><img loading="lazy" width="223" height="112" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-14.png" alt="" class="wp-image-25070" /></figure>

<p>Now you should have the Region field in the Location hierarchy. The problem is, it&#8217;s still a string. We need it to be a geographical field. In order to get this sorted, right-click on Region -&gt; Geographical Role -&gt; Create from -&gt; State:</p>

<figure class="wp-block-image"><img loading="lazy" width="630" height="638" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-15.png" alt="" class="wp-image-25072" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-15.png 630w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-15-296x300.png 296w" sizes="(max-width: 630px) 100vw, 630px" /></figure>

<p>Now the icon next to &#8216;Region&#8217; should change from &#8216;Abc&#8217; to a little globe!</p>

<p><strong>Check the hierarchy.</strong> Alright, let&#8217;s check that we actually have a geographical hierarchy. Double-click on Region, this should result in a map with points on it. (If you have 4 Nulls, go to the indicator in the bottom right corner -&gt; Edit Locations -&gt; change the country to US) Let&#8217;s change the mark type to map, the US should be nicely filled with blue colour. To see the difference between regions, we can drag and drop Sales on the Color button:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="546" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-16-1024x546.png" alt="" class="wp-image-25074" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-16-1024x546.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-16-300x160.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-16-768x410.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-16-1080x576.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-16.png 1710w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>I&#8217;m just a tiny little bit pedantic so let&#8217;s fix the formatting of the map. Go to Map -&gt; Map Layers</p>

<figure class="wp-block-image"><img loading="lazy" width="671" height="227" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-17.png" alt="" class="wp-image-25077" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-17.png 671w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-17-300x101.png 300w" sizes="(max-width: 671px) 100vw, 671px" /></figure>

<p>This will open a panel on your left. Change washout to 100% and that will do for now. The map should show now only the coloured areas:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="467" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-19-1024x467.png" alt="" class="wp-image-25079" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-19-1024x467.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-19-300x137.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-19-768x350.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-19-1080x492.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-19.png 1918w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p></p>

<p>Ok, let&#8217;s do the same for States. Before we continue, change the name of the sheet to &#8216;Region Map&#8217; by double-clicking on the label or right-click -&gt; Rename. Add a sheet and rename it to &#8216;State Map&#8217;. Double-click on State and drag Sales on Color. Then change the washout to 100%:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="486" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-20-1024x486.png" alt="" class="wp-image-25080" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-20-1024x486.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-20-300x142.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-20-768x364.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-20-1080x512.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-20.png 1920w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>Sweet. Now for both of the sheets, go to Format -&gt; Borders and change Row Divider -&gt; Pane to None and Column Divider -&gt; Pane None this will change it for Headers as well. You&#8217;ll have to do it separately for both sheets.</p>

<figure class="wp-block-image"><img loading="lazy" width="209" height="705" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-21.png" alt="" class="wp-image-25081" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-21.png 209w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-21-89x300.png 89w" sizes="(max-width: 209px) 100vw, 209px" /></figure>

<p><strong>Create a dashboard with a floating container.</strong> Ok, now that we have both sheets set up, let&#8217;s create a dashboard that will do the drill down. I renamed mine to &#8216;Map Drill-Down&#8217; and checked the &#8216;Show dashboard title&#8217; box. We need a container now. I&#8217;ll go with a tiled one but you can go with a floating one as well. As for the horizontal/vertical option, it depends whether you want your maps one next to the other or one above/below the other. This is what I dragged onto the dashboard:</p>

<figure class="wp-block-image"><img loading="lazy" width="215" height="230" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-22.png" alt="" class="wp-image-25083" /></figure>

<p>To get the sheet into the container you need Tiled to be highlighted and just drag it onto the container. If something&#8217;s off, try hitting the Shift key and that should do the trick. Put Region Map sheet into your container and you should see the legend showing up as well, next to the map. If you don&#8217;t want it in your view, just click on it and delete (to bring it back, you can click on the sheet -&gt; caret -&gt; Legends -&gt; Color Legend). If you want to prevent the legend from popping up in the first place, just hide the legend in the sheet view.</p>

<p>Ok, now you should have something similar to this:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="735" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-23-1024x735.png" alt="" class="wp-image-25084" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-23-1024x735.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-23-300x215.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-23-768x552.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-23-1080x776.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-23.png 1242w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>Drag the State Map to the bottom/right side of the container (depends whether you choose vertical or horizontal container):</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="715" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-24-1024x715.png" alt="" class="wp-image-25085" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-24-1024x715.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-24-300x210.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-24-768x536.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-24-1080x754.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-24.png 1237w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>This is what your dashboard should look like:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="689" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-25-1024x689.png" alt="" class="wp-image-25086" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-25-1024x689.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-25-300x202.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-25-768x517.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-25-1080x727.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-25.png 1200w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>Now, hide the title for the State Map sheet. Make sure the Title is unticked:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="346" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-26-1024x346.png" alt="" class="wp-image-25087" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-26-1024x346.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-26-300x101.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-26-768x260.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-26-1080x365.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-26.png 1221w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>Ok, now the party begins! Go to Dashboard -&gt; Actions -&gt; Add Action -&gt; Filter. Change the name of the filter to Map Drill Down (this will make the action easier to identify). Set &#8216;Run action on&#8217; to Select. In source sheets, make sure that only Region Map is checked and in the target sheets only State Map is checked. You can change that if you want your action to work on more things. The final change is to set &#8216;Clearing the selection will&#8217; to &#8216;Exclude all values&#8217;:</p>

<figure class="wp-block-image"><img loading="lazy" width="592" height="715" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-27.png" alt="" class="wp-image-25088" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-27.png 592w, https://www.thedataschool.co.uk/content/images/wordpress/2019/03/image-27-248x300.png 248w" sizes="(max-width: 592px) 100vw, 592px" /></figure>

<p>Hit OK, and once more. And there you go! You have a drill down map. How cool is that?</p>

<figure class="wp-block-image"><img loading="lazy" width="982" height="792" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/03/mappdrilldown.gif" alt="" class="wp-image-25089" /></figure>

<p>Because they&#8217;re on different sheets you can have different tooltips for different levels. Also, you can add more levels! This, however, can make things slightly more confusing for the users, so be careful with that. (If there&#8217;s interest in a post on adding more levels, e.g. cities, let me know on <a href="https://twitter.com/hanykowska">twitter</a> or via any other route. In case there&#8217;s anyone interested in seeing that, I&#8217;ll write a follow-up!)</p>

<p>Check out my workbook with the map <a href="https://public.tableau.com/profile/hanna.nykowska#!/vizhome/MapDrillDown_15521531242950/MapDrill-Down">here</a>.</p>

<p>Well done for getting to the end of this tutorial! Byeeeee!</p>
