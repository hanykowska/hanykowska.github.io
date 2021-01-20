---
layout: post
cover: /assets/images/posts-images/cogs.webp
navigation: True
title: "Alteryx Challenge: Macros"
date: 2019-03-03 00:00:00
tags: [alteryx]
class: post-template
subclass: "post"
author: hanykowska
external_url: https://www.thedataschool.co.uk/hanna-nykowska/alteryx-challenge-macros/
external_site: ds
excerpt_separator: <!--more-->
---

Alteryx Challenge update: I’m describing the macros-related weekly challenges.

[First published on The Data School Blog.]({{page.external_url}}){:target="\_blank"}

<!--more-->

<p>Another week is over and another section of Alteryx weekly challenges is (almost) finished for me. Almost, because I&#8217;ve left out a few difficult ones for a time when I&#8217;m more competent. The section I&#8217;m talking about is Macros. </p>

<p>As I mentioned in my <a href="https://www.thedataschool.co.uk/hanna-nykowska/alteryx-challenge-data-cleansing/">post</a> on Monday, we had some training on macros in Alteryx with <a href="https://twitter.com/Phil_L57">Phil</a> this week. It was super beneficial to me as beside learning about another functionality of Alteryx I managed to finish a few challenges during training (yesssss!). With a good start into Macros challenges and to solidify what we&#8217;ve learnt with Phil, I decided to finish off macros-related tasks.</p>

<p>If you don&#8217;t know what macros are and how to deal with them, <a href="https://www.thedataschool.co.uk/blog/jonathan-allenby/">Jon</a>&#8216;s giving a very short overview in his <a href="https://www.thedataschool.co.uk/jonathan-allenby/jons-ds13-week-4-recap/">weekly recap</a>, <a href="https://www.thedataschool.co.uk/author/samuel-shurmer/">Sam</a>&#8216;s describing them in more detail in his <a href="https://www.thedataschool.co.uk/samuel-shurmer/macros-they-arent-as-scary-as-they-sound/">post</a> and this could be a good place to start. For our Friday project, we had to write macros with Tableau&#8217;s table calculations functionality (not gonna lie, taking up macros-related challenges came in quite handy&#8230;). As it turned out, the project was actually quite difficult and <a href="https://www.thedataschool.co.uk/author/alessandro-costanzo/">Alessandro</a> described <a href="https://www.thedataschool.co.uk/alessandro-costanzo/project-week-4-table-calculations-in-alteryx/">his experience</a> with it while <a href="https://www.thedataschool.co.uk/author/robert-headington/">Robert</a> found a <a href="https://www.thedataschool.co.uk/robert-headington/alteryx-macro-tip-making-dynamic-drop-downs-using-the-inputs-fields/">solution</a> to a problem we&#8217;ve encountered. </p>

<p>Alright, let&#8217;s get started. With some knowledge of macros, what do you need to finish the weekly challenges?</p>

<div style="height:33px" aria-hidden="true" class="wp-block-spacer"></div>

<h4>Know your challenge</h4>

<p>I&#8217;ve said it already, and I&#8217;ll say it again. It is so important to know what you need to do in the challenge. I write down the key information and maybe the structure of the input and the desired output. From there, I try to figure out what has to be done to get the job done. I noticed I work faster once I&#8217;m aware what is needed from me (duh!).</p>

<p>Knowing what kind of transformations are necessary, I look into what kind of macro I should implement&#8230; (There are four types and they work in really different ways.) To find the right type of macro, it&#8217;s helpful to actually read the description of the challenge in the post on Alteryx Community, as they might hint what kind you should use.</p>

<div style="height:37px" aria-hidden="true" class="wp-block-spacer"></div>

<h4>Key differences between macros</h4>

<p><strong>Standard macro</strong> &#8211; nothing fancy, just a workflow wrapped as a macro. Can be dynamic and take arguments from the user.</p>

<p><strong>Iterative macro</strong> &#8211; can be very useful especially when you want to update the same data set multiple times. A few things to keep in mind:</p>

<ul><li>input and output should have ideally the same structure</li><li>you can use the iteration number as a variable in expressions (formula tool and other tools as well) &#8211; [Engine.IterationNumber]</li><li>the iteration number starts at 0 and increments with every iteration (0-24 for 25 iterations)</li><li>within the iterative macro the data set is still processed for all rows (I sometimes get confused and think it works only for one row at a time but that&#8217;s not true)</li><li>iteration input and output need to be configured in Interface Designer, it&#8217;s also where you can change max number of iterations</li></ul>

<p><strong>Batch macro</strong> &#8211; quite a handy option if you want to repeat the same operation for a list of values. If a macro has a Control Parameter it&#8217;s a batch macro. What Phil suggested during the training, was to create a flow for a single value in the mentioned list, then figure out what needs to be changed to get the right outcome for the second value. Once that&#8217;s sorted, you should know how to adjust the flow to become actually dynamic and work properly.</p>

<p>I like to think of iterative macros as while-loops and batch macros as for-loops (if you have some programming experience, this should ring a bell, if you don&#8217;t, just ignore this).</p>

<div style="height:40px" aria-hidden="true" class="wp-block-spacer"></div>

<h4>The challenges</h4>

<p>The challenges themselves were sometimes super easy and sometimes very complicated. At least until I properly wrapped my head around them. Some were actually quite interesting math problems (nerd alert&#8230;) that I enjoyed figuring out how to represent in a math notation. This also helped a lot in creating then the right workflow.</p>

<p>There are some that build on previous challenges and it helps to do them chronologically, but I wouldn&#8217;t stress out too much about it.</p>

<p>That&#8217;s it for now&#8230; Go and have fun with macros and let me know how it goes. Also, hit me up if you have any problems. Who knows, maybe I&#8217;ll be able to help 😉</p>

<p>Byeee!</p>
