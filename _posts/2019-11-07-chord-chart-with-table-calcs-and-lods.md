---
layout: post
cover: /assets/images/posts-images/chord-chart-cover.png
navigation: True
title: "How to build Chord Chart in Tableau with Table Calculations and LODs"
date: 2019-11-07 00:00:00
tags: [tableau]
class: post-template
subclass: "post"
author: hanykowska
excerpt_separator: <!--more-->
external_url: https://www.theinformationlab.co.uk/2019/11/07/chord-chart-with-table-calcs-and-lods/
external_site: til
---

Want to build a chord chart but don't have access to fancy data preparation tools? I got you covererd!

[First published on The Information Lab Blog.]({{page.external_url}}){:target="\_blank"}

<!--more-->

<p>A chord chart (or schemaball) can be an interesting way to show how strongly two categories are related. Usually, they are pretty tricky to make and can require a lot of data prep that is not always available to everyone. This is the problem I have come across recently: the client wanted a chord chart but they don't have access to Alteryx (which would be what I'd use to build the shapes needed) so I thought I'd try and build this kind of chart with table calculations. I made it work and now I'm here to share it with you!</p>
<p>For the purpose of this blog, I'm using <a href="http://bit.ly/2NMUFes">data</a> on how many people commute between London boroughs (from place of residence to place of work)</p>
<h2>Data</h2>
<p>Let's be honest, the data will still need to be in the right format, but this format should be fairly sensible. Let's say you start with a data set that has a start point (Place of Residence), end point (Place of Work), and weight of the connection (Number of Commuters). To make the chord chart work, you will also need a row ID (actually it just needs something that can be used as an identifier for each connection). If it's something that you can get from your database, that's great. If you can't, create a calculated field:</p>
<p><strong>Row ID</strong> (given [Start Point] and [End Point] are strings)</p>
<pre class="wp-block-code"><code>&#91;Start Point] + &#91;End Point]</code></pre>
<div style="height:23px" aria-hidden="true" class="wp-block-spacer"></div>
<h3>Formatting the data in Tableau</h3>
<p>OK, so we have start point, end point, weight of the connection, and row ID. Lovely.</p>
<p></p>
<figure class="wp-block-image"><img src="https://res.cloudinary.com/dk8jxrhv8/image/upload/v1572964029/Chord%20chart%20blog/original_data.png" alt=""/></figure>
<p>Highlight Start and End points, right-click → pivot. This will reshape the data so that all boroughs (in my case) will be in one column and there will be another column indicating if it's a start or end point. I renamed Pivot Field Values to Borough but you may decide to go with something more appropriate to your data:</p>
<figure class="wp-block-image"><img src="https://res.cloudinary.com/dk8jxrhv8/image/upload/v1572964868/Chord%20chart%20blog/pivot_the_data.gif" alt=""/></figure>
<p>Now, go to a new sheet and create a calculated field called Path - it will specify the direction:</p>
<pre class="wp-block-code"><code>If &#91;Pivot Field Names]='Start Point'
then 1
elseif &#91;Pivot Field Names]='End Point'
then 2
end</code></pre>
<p>This field will by default end in Measures, leave it there for now.</p>
<p>That's it in terms of data prep!</p>
<div style="height:51px" aria-hidden="true" class="wp-block-spacer"></div>
<h2>Chord chart with Table Calcs and LODs!</h2>
<p>This solution isn’t entirely straightforward and you may need to modify it to fit your data set. However, this guide will teach you the concepts required which you can pick up and modify to suit your needs.</p>
<p>With the data prep done, we’re ready to actually begin building the Chord chart in Tableau. If your data format differs significantly then you may need further table calculations. However, the steps below should work with data that is reasonably similar.</p>
<p>OK, let's get to it, shall we?</p>
<h3>Point positions</h3>
<p>First, we need to create a few calculated fields to find the right angle. What do we need an angle for? Tableau uses <a href="https://mathinsight.org/cartesian_coordinates">cartesian coordinates</a> which is great for many types of charts. In order to build the chord chart, however, we need to have points placed on the edge of a circle. For this, <a href="https://mathinsight.org/polar_coordinates">polar coordinates</a> work better - we only need angle and radius to find the position of a point. Thankfully, we can use trigonometry to translate polar coordinates into cartesian ones.</p>
<figure class="wp-block-image"><img src="https://res.cloudinary.com/dk8jxrhv8/image/upload/v1572968411/Chord%20chart%20blog/Cartesian_vs_polar_coordinates.png" alt=""/></figure>
<p>Let's create a calculated field called Total Positions - it will help calculate the smallest angle (1/[Total Positions]).</p>
<p><strong>Total Positions</strong></p>
<pre class="wp-block-code"><code>{COUNTD(&#91;Borough])}</code></pre>
<p>This will return the number of distinct positions you will have in the chord chart. I tried using a table calculation for it instead. That, however, turned to be much more complex to set up than using a fixed (on nothing) LOD instead.</p>
<p>Next calculated field will be Order and it's something to just assign a number to each position.</p>
<p><strong>Order</strong></p>
<pre class="wp-block-code"><code>INDEX()</code></pre>
<p>As you can see, it's just an INDEX function. (The trick will be to set it up correctly with all of the other calculations in the view! But worry not, I've got you covered.)</p>
<p>Now that we have [Total Positions] and [Order] we can finally add another calculated field, Angle.</p>
<p><strong>Angle</strong></p>
<pre class="wp-block-code"><code>( (2 * PI()) / max(&#91;Total Positions]) ) * &#91;Order]</code></pre>
<p>There is quite a lot going on. Let's break it down. 2 π  is a full circle (360°, tableau trigonometric functions use radians and so we need 2 π  instead of 360°). Total Positions should have the same value for all rows in the data so it requires some aggregation, max() should be fairly computationally-light and will give us the right value. Full circle divided by all positions will return the smallest angle. Multiplying that by Order will give us the angle values for all positions.</p>
<p>OK! We have our angles calculated. To check that the calculated fields work, drag Borough (or whatever you use to identify different positions) and Order to the Rows shelf, then drag Angle to the Columns shelf. The image below is what you should get. You may replace 2 π  with 360° if sense checking is easier in degrees (it was for me!) but make sure to go back to radians before we continue. Another alternative would be to use ([Order] - 1) in the Angle calculation instead of [Order]. Then the first position would start with an angle of 0 and be in the middle as opposed to a few degrees to the right.</p>
<figure class="wp-block-image"><img src="https://res.cloudinary.com/dk8jxrhv8/image/upload/v1572973510/Chord%20chart%20blog/angle%20check.png" alt=""/></figure>
<p>Now that we have the angles calculated, we can write translation calculations.</p>
<p>Looking back at the combination of polar and cartesian coordinates we need two fields:</p>
<p><strong>X</strong></p>
<pre class="wp-block-code"><code>cos(&#91;Angle])</code></pre>
<p><strong>Y</strong></p>
<pre class="wp-block-code"><code>sin(&#91;Angle])</code></pre>
<p>We can skip the radius because we want it to be the same for all points. Skipping the radius is equivalent to assigning it a value of 1.</p>
<p>Drag X to columns and Y to rows and Borough to detail. This doesn't seem encouraging. We can see there are 32 marks but they all seem to be in the same place! Fear not, it's the table calculations that require setting up.</p>
<figure class="wp-block-image"><img src="https://res.cloudinary.com/dk8jxrhv8/image/upload/v1573040047/Chord%20chart%20blog/coordinates%20check.png" alt=""/></figure>
<p>Right-click on X → Edit Table Calculation → Compute Using → Specific Dimensions → tick Borough (or your equivalent). This already should end up in a circle but repeat the same for Y. In the gif below, you can also notice that the positions are starting not from the top, like a clock face, but rather from 3 o'clock (horizontal axis) in the anti-clockwise direction.</p>
<figure class="wp-block-image"><img src="https://res.cloudinary.com/dk8jxrhv8/image/upload/v1573042078/Chord%20chart%20blog/positions_in_circle_rqgvfp.gif" alt=""/></figure>
<figure class="wp-block-image"><img src="https://res.cloudinary.com/dk8jxrhv8/image/upload/v1573041948/Chord%20chart%20blog/Cartesian_vs_polar_angle_direction.png" alt=""/></figure>
<p>To accommodate for the above, we simply need to swap columns with rows. For those who like a diagram, here's a comparison of the two:</p>
<figure class="wp-block-image"><img src="https://res.cloudinary.com/dk8jxrhv8/image/upload/v1573043311/Chord%20chart%20blog/Cartesian_vs_polar_change_of_direction.png" alt=""/></figure>
<p>For the practical minds, just click Swap Rows and Columns or hit CTRL+W:</p>
<figure class="wp-block-image"><img src="https://res.cloudinary.com/dk8jxrhv8/image/upload/v1573043429/Chord%20chart%20blog/swap%20rows%20and%20columns.png" alt=""/></figure>
<p>You can change the assignment of Borough pill from detail to text to show the labels.</p>
<p>Here's what I have so far:</p>
<figure class="wp-block-image"><img src="https://res.cloudinary.com/dk8jxrhv8/image/upload/v1573046931/Chord%20chart%20blog/circle.png" alt=""/></figure>
<div style="height:33px" aria-hidden="true" class="wp-block-spacer"></div>
<h2>Connect the dots</h2>
<p>Great, the boroughs are in the right place. Let's now draw the lines between them.</p>
<p>Hit CTRL and drag pill X to the right of itself. Now you should have two X pills on rows. Change the mark type on X(2) from automatic to line. It may look like a mess but let's keep going.</p>
<figure class="wp-block-image"><img src="https://res.cloudinary.com/dk8jxrhv8/image/upload/v1573047207/Chord%20chart%20blog/two%20axes%20circles%20and%20line.png" alt=""/><figcaption> Partaaay </figcaption></figure>
<p></p>
<p>On X(2) (line), drag Path onto Path (see what I did there) on marks card:</p>
<figure class="wp-block-image"><img src="https://res.cloudinary.com/dk8jxrhv8/image/upload/v1573052355/Chord%20chart%20blog/Path%20on%20path.png" alt=""/></figure>
<p>Now drag Row ID onto detail on X(2) marks card. Oh no! what happened to our circular points? Table calcs, that's what happened.</p>
<figure class="wp-block-image"><img src="https://res.cloudinary.com/dk8jxrhv8/image/upload/v1573052485/Chord%20chart%20blog/row%20ID%20on%20detail.png" alt=""/></figure>
<p>To fix that, right-click on the X pill on the right → Edit Table Calculation → Compute Using → Specific Dimensions → make sure both Borough and Row ID are ticked → At the level → Borough. Ta-da!</p>
<figure class="wp-block-image"><img src="https://res.cloudinary.com/dk8jxrhv8/image/upload/v1573052985/Chord%20chart%20blog/chord_chart.gif" alt=""/></figure>
<p>Alright, we're almost there. You already have dots for one axis, now let's do a dual-axis to combine the two views. Right-click on any of the X pills → Dual Axis. Then make sure you synchronise the axes and hide them. You may have noticed that the chord chart disappeared after selecting Dual Axis! Just remove Measure Names from colour (either on the marks card for line chart or on the marks card for All). Finally, change Borough assignment from Label to Detail on marks card for line chart.</p>
<figure class="wp-block-image"><img src="https://res.cloudinary.com/dk8jxrhv8/image/upload/v1573056008/Chord%20chart%20blog/chord_chart_dual_axis.gif" alt=""/></figure>
<div class="wp-block-image"><figure class="aligncenter"><img src="https://media.giphy.com/media/UmBdALbYTmCJ2/giphy.gif" alt=""/><figcaption>via GIPHY</figcaption></figure></div>
<p></p>
<h1>Fun part - AKA formatting</h1>
<p>Fantastic, we have our chord chart ready to be formatted!  I’ll leave this part to you. However, in my example, you can see how I use weight to thicken chords with a strong connection and colour to highlight the direction of connections. </p>
<p>I have also joined my original (not pivoted) data to the pivoted data. Then I created a parameter from Borough and a calculated field to distinguish between from and to and connections that are not related. With parameter actions, you can now click on any of the circles to adjust the colouring for that borough. Pretty cool.</p>
<figure class="wp-block-image"><img src="https://res.cloudinary.com/dk8jxrhv8/image/upload/v1573125270/Chord%20chart%20blog/viz_in_action.gif" alt=""/></figure>
<p>You can find my workbook on <a href="https://public.tableau.com/profile/hanna.nykowska#!/vizhome/ChordchartwithtablecalcsandLODs/Dashboard">Tableau Public</a>.</p>
