---
layout: post
cover: /assets/images/posts-images/copy-and-paste-datasource.png
navigation: True
title: "Tableau Tip: copy and paste data from a data source already in Tableau"
date: 2019-02-17 00:00:00
tags: [tableau]
class: post-template
subclass: "post"
author: hanykowska
external_url: https://www.thedataschool.co.uk/hanna-nykowska/tableau-tip-copy-and-paste-data-from-open-data-source/
external_site: ds
excerpt_separator: <!--more-->
---

Why and how would you copy and paste part of a dataset that is already loaded to Tableau? Keep reading.

[First published on The Data School Blog.]({{page.external_url}}){:target="\_blank"}

<!--more-->

<p>Following up on Jon&#8217;s post on <a href="https://www.thedataschool.co.uk/jonathan-allenby/tableau-tip-you-can-paste-data-directly-into-tableau/">copying and pasting data directly into Tableau</a>, I just wanted to add, that you can do that with the data you already have in Tableau. Wait a minute, but why would I paste the data I <strong>already&nbsp;have</strong> in Tableau? In some cases, which I&#8217;ll discuss, it may save you some time. Perhaps it&#8217;s not the best approach but if it&#8217;s a one-off and you don&#8217;t want to faff around with data, it may be useful.</p>

<div style="height:23px" aria-hidden="true" class="wp-block-spacer"></div>

<h3>Use case</h3>

<p>Let&#8217;s have a look at a situation, this could be (and actually was) applied to.</p>

<p>For my application <a href="https://public.tableau.com/profile/hanna.nykowska#!/vizhome/FemaleKagglers/Story">viz</a>, I used data from <a href="https://www.kaggle.com/kaggle/kaggle-survey-2018">Kaggle Survey</a>. It meant that I had to deal with survey data, which I&#8217;d never done before. Probably not the best decision but it still got me to the interview. </p>

<p>I chose this dataset because I had taken part in that survey so I knew more or less what was in it and I was just curious about the results. There were 50 questions total and some of them had multiple parts, number of which easily reached double figures. As some of the questions were multiple choice,  all of the parts of a question were saved as separate fields. In the end there were over 400 fields (columns) and many were referring to the same questions.</p>

<p>This wasn&#8217;t that much of a problem in simple questions, but I wanted to show the popularity of specific media platform with highlighting of top 5 positions. It turned out I didn&#8217;t quite know how to build a calculation that would deal with 20 or so fields. Or maybe I was just lazy. Either way, I decided I needed to do something about it. </p>

<p>I think I might have researched the problem and I&#8217;m very sorry but I simply don&#8217;t remember how I got across the concept of copying part of your own dataset to solve it. Thus, I can&#8217;t give appropriate acknowledgement to the author of the idea.</p>

<div style="height:27px" aria-hidden="true" class="wp-block-spacer"></div>

<h3>How to</h3>

<p>To understand the situation, here&#8217;s what my view looked like originally:</p>

<figure class="wp-block-image"><img loading="lazy" width="760" height="927" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/start-point.png" alt="" class="wp-image-23706" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/start-point.png 760w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/start-point-246x300.png 246w" sizes="(max-width: 760px) 100vw, 760px" /></figure>

<p>You can see at the top that I already have two datasets, one of which is from a clipboard. This is because I used that trick already to get the visualisation I wanted. Notice how many measures are there on the measures shelf. TWENTY. Who wants to take care of that many measures when they all relate to the same question?</p>

<p>Here&#8217;s what you want to do.  </p>

<ol><li>Right-click on on any value in the view and hit &#8216;Select All&#8217;.</li><li>ctrl+c (or mac equivalent) to copy.</li><li>Go to a new sheet and ctrl+p to paste your data.</li></ol>

<figure class="wp-block-image"><img loading="lazy" width="1137" height="961" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/copy_and_paste-5.gif" alt="" class="wp-image-23734" /></figure>

<p>Simple, isn&#8217;t it? </p>

<figure class="wp-block-image"><img loading="lazy" width="778" height="811" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/after-pasting-1.png" alt="" class="wp-image-23733" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/after-pasting-1.png 778w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/after-pasting-1-288x300.png 288w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/after-pasting-1-768x801.png 768w" sizes="(max-width: 778px) 100vw, 778px" /><figcaption> <br>View after pasting the data. Notice extra Clipboard position and no measures on the measures shelf. </figcaption></figure>

<p>The measures shelf disappears. A new data source is showing up that seems to be named as &#8216;Clipboard_yyyymmdd_T_hhmmss&#8217;. The names of the fields are also automatically saved as &#8216;Measure Names&#8217; and &#8216;Measure Values&#8217;. Not ideal, could make things a bit confusing. And there&#8217;s also this blank space.</p>

<p>To deal with these, you can also continue with the following steps:</p>

<p>4. Change the name of the data source (right-click on its name and hit &#8216;Rename&#8217;). Use something informative so that later you know what that is.<br>5. Rename the fields to make sense (right-click on its name and hit &#8216;Rename&#8217; or select the field and hit F2 on Windows). I used &#8216;Media&#8217; instead of &#8216;Measure Names&#8217; and &#8216;Media popularity&#8217; instead of &#8216;Measure Values&#8217;.<br>6. Exclude the empty value. (right-click on the empty row and hit &#8216;Exclude&#8217;. I&#8217;m not sure why does it come up, but I assume it has something to do with selection and whitespace characters. Anyway, it doesn&#8217;t really bother me that much.)</p>

<div style="height:33px" aria-hidden="true" class="wp-block-spacer"></div>

<p>There you go! You have a simplified version of your data that you can play with further:</p>

<figure class="wp-block-image"><img loading="lazy" width="769" height="674" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/end.png" alt="" class="wp-image-23710" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/02/end.png 769w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/end-300x263.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/02/end-768x673.png 768w" sizes="(max-width: 769px) 100vw, 769px" /><figcaption>The end product.</figcaption></figure>

<div style="height:35px" aria-hidden="true" class="wp-block-spacer"></div>

<h3>The Dangers</h3>

<p>There are a few problems with this approach. Firstly, I highly doubt it&#8217;s the best practice. Second, it doesn&#8217;t update, so if you want to use some filters on the data, it won&#8217;t work for you. This holds also, if it should update based on new data (Live connection). I assume there are more problems with it, but there are some positives too.</p>

<div style="height:22px" aria-hidden="true" class="wp-block-spacer"></div>

<h3>The Benefits</h3>

<p>If the viz is a one-off kind of story, than this trick solves your problem in a rather quick way. For a static visualisation and a summary view, it will work.</p>

<div style="height:51px" aria-hidden="true" class="wp-block-spacer"></div>

<p>Having said that, I thought I was creating a one-time viz and then I had to improve it during our first project at DS. I could have expected that, but it slipped my mind. I&#8217;m looking forward (kind of) to a session on survey data so that I can learn how to properly deal with the data set that I had. Look out for a blog post, because there will definitely be one.</p>

<p>In summary, this trick may be useful in some situations but it may be the case of dangers outweighing benefits.  In other words,<strong> do it at your own risk</strong>.</p>
