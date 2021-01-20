---
layout: post
cover: /assets/images/posts-images/filter.webp
navigation: True
title: "Tableau (Server) Tip: Intro to User Filters"
date: 2019-05-24 00:00:00
tags: [tableau]
class: post-template
subclass: "post"
author: hanykowska
external_url: https://www.thedataschool.co.uk/hanna-nykowska/tableau-server-tip-intro-to-user-filters/
external_site: ds
excerpt_separator: <!--more-->
---

What are user filters and how can you start using them.

[First published on The Data School Blog.]({{page.external_url}}){:target="\_blank"}

<!--more-->

<p>Even though we might be finishing the training, it doesn&#8217;t mean the learning is finished. Earlier this week we had a Tableau Server Refresher with Ravi. We went over some topics we wanted clarified but also discussed user filters which we hadn&#8217;t had much experience with so far. As a way of solidifying and sharing the knowledge, here&#8217;s the intro to the topic.</p>

<h3>What are user filters?</h3>

<p>User filters are, lo and behold, filters that are using information about the Tableau user (eg, the username and the groups the user belongs to) to show only relevant data. You might want to use it for data security reasons or to improve the user experience.</p>

<h3>What do you need?</h3>

<p>User filters are only available with <strong>Tableau Server</strong> and <strong>Tableau Online</strong>. User groups on the server might also come in handy (especially if you want to follow this blog post).</p>

<h4>User groups</h4>

<p>On the server, got to Groups (we had an update recently so you can see what the new Tableau Server looks like):</p>

<figure class="wp-block-image"><img loading="lazy" width="228" height="456" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-102.png" alt="" class="wp-image-27163" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-102.png 228w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-102-150x300.png 150w" sizes="(max-width: 228px) 100vw, 228px" /></figure>

<p>In the new view, navigate to + New Group and type in the name of the group. I created three groups for this post: Hanna &#8211; Technology, Hanna &#8211; Furniture, Hanna &#8211; Office Supplies. If you&#8217;re familiar with Tableau&#8217;s data sources, you might know what&#8217;s coming: Sample &#8211; Superstore.</p>

<p>I prefixed the groups with my name so that it&#8217;s easier for me to find the groups and delete them afterwards.</p>

<p>Once the groups are created, you should see them in the list:</p>

<figure class="wp-block-image"><img loading="lazy" width="630" height="133" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-103.png" alt="" class="wp-image-27164" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-103.png 630w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-103-300x63.png 300w" sizes="(max-width: 630px) 100vw, 630px" /></figure>

<p>I have three groups with 0 users each. Let&#8217;s change that. Click on the group name and this is what you should see (if the group has no users):</p>

<figure class="wp-block-image"><img loading="lazy" width="893" height="347" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-104.png" alt="" class="wp-image-27165" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-104.png 893w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-104-300x117.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-104-768x298.png 768w" sizes="(max-width: 893px) 100vw, 893px" /></figure>

<p>Add a user or two so that we can test the filters later on. Click on + Add Users and in the pop-up window select those you want to add (you should see names next to the tick boxes):</p>

<figure class="wp-block-image"><img loading="lazy" width="454" height="578" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/add-users.png" alt="" class="wp-image-27167" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/add-users.png 454w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/add-users-236x300.png 236w" sizes="(max-width: 454px) 100vw, 454px" /></figure>

<p>After adding users, the group page should look slightly differently:</p>

<figure class="wp-block-image"><img loading="lazy" width="984" height="305" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/added-users.png" alt="" class="wp-image-27169" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/added-users.png 984w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/added-users-300x93.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/added-users-768x238.png 768w" sizes="(max-width: 984px) 100vw, 984px" /></figure>

<p>I&#8217;ll do the same for my other two groups and will assign myself to both of them. Ok, now I have two users in each of my groups:</p>

<figure class="wp-block-image"><img loading="lazy" width="617" height="138" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-107.png" alt="" class="wp-image-27170" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-107.png 617w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-107-300x67.png 300w" sizes="(max-width: 617px) 100vw, 617px" /></figure>

<h4>User Filters</h4>

<h4>1. Sign into the server</h4>

<p>In Tableau Desktop, open Sample Superstore and log into the server: Server -&gt; Sign In</p>

<figure class="wp-block-image"><img loading="lazy" width="637" height="54" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-108.png" alt="" class="wp-image-27171" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-108.png 637w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-108-300x25.png 300w" sizes="(max-width: 637px) 100vw, 637px" /></figure>

<p>Now, at the bottom of the view, you&#8217;ll be able to &#8216;switch&#8217; users. You can&#8217;t really switch user but it works as &#8216;view as&#8217; function:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="556" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-109-1024x556.png" alt="" class="wp-image-27173" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-109-1024x556.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-109-300x163.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-109-768x417.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-109-1080x587.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-109.png 1915w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<h4>2. Create a calculation</h4>

<p>Now that you can see the users, create a calculated field. I called mine User Filter. Make sure to open the functions popup and select User from the drop-down. </p>

<figure class="wp-block-image"><img loading="lazy" width="974" height="355" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-110.png" alt="" class="wp-image-27174" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-110.png 974w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-110-300x109.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-110-768x280.png 768w" sizes="(max-width: 974px) 100vw, 974px" /></figure>

<p>There are a few functions you can use, but let&#8217;s focus on ismemberof. This function will check whether the current user if a member of the specified group. One thing to mention is the group needs to be a literal string &#8211; something you literally type in as opposed to a string field.</p>

<p>In the calculated field write an expression that will return true only if the user is a member of a group associated with a specific Category:</p>

<pre class="wp-block-code"><code>(ISMEMBEROF('Hanna - Furniture') AND [Category] = 'Furniture')

OR 

(ISMEMBEROF('Hanna - Technology') AND [Category] = 'Technology')

OR 

(ISMEMBEROF('Hanna - Office Supplies') AND [Category] = 'Office Supplies')</code></pre>

<p>Now let&#8217;s build the view and test the filter. Put Categories on the columns and Sales on rows. This will result in a bar chart:</p>

<figure class="wp-block-image"><img loading="lazy" width="316" height="527" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-111.png" alt="" class="wp-image-27179" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-111.png 316w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-111-180x300.png 180w" sizes="(max-width: 316px) 100vw, 316px" /></figure>

<p>Now, if you put the User Filter field on the filters and select True, you should only see the category assigned to the group the user is a member of:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="668" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-112-1024x668.png" alt="" class="wp-image-27180" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-112-1024x668.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-112-300x196.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-112-768x501.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-112-1080x705.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-112.png 1477w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>Because I&#8217;m a member of two groups, I can see two categories. But If I change the user to Jonathan Allenby, I can only see Furniture:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="667" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-113-1024x667.png" alt="" class="wp-image-27181" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-113-1024x667.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-113-300x195.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-113-768x500.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-113-1080x704.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-113.png 1472w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>Or Office Supplies in case of Débora Contente:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="671" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-114-1024x671.png" alt="" class="wp-image-27182" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-114-1024x671.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-114-300x197.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-114-768x503.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-114-1080x708.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-114.png 1470w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>The advantage of the proposed calculated field is that it&#8217;s independent of the measures you&#8217;re using. This means you can include the field in the Extract Filters or Data Source Filters.</p>

<p>Go to Data Source tab, and in the top right corner you can add these filters:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="514" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-115-1024x514.png" alt="" class="wp-image-27183" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-115-1024x514.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-115-300x151.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-115-768x386.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-115-1080x543.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-115.png 1907w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>Find your User Filter field and set it to true:</p>

<figure class="wp-block-image"><img loading="lazy" width="512" height="216" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-116.png" alt="" class="wp-image-27184" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-116.png 512w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-116-300x127.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/05/image-116-510x216.png 510w" sizes="(max-width: 512px) 100vw, 512px" /></figure>

<p>This will apply the filter to all of the sheets.</p>

<h3>A note on security</h3>

<p>If you use user filters for data security reasons, keep in mind the permissions the users have. If someone is not supposed to have access to some data but they can web edit the workbook or download the workbook, they will be able get rid of the filter and therefore access the data. You might try to find a walkaround by applying an extract filter, but be cautious.</p>

<p>More on User Filters:  <br><a href="https://onlinehelp.tableau.com/current/pro/desktop/en-us/publish_userfilters_create.htm">https://onlinehelp.tableau.com/current/pro/desktop/en-us/publish_userfilters_create.htm</a></p>
