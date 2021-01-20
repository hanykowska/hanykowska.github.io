---
layout: post
cover: /assets/images/posts-images/alteryx-tableau.png
navigation: True
title: "Scheduling Alteryx workflow that updates data used in Tableau"
date: 2019-04-14 01:00:00
tags: [tableau, alteryx]
class: post-template
subclass: "post"
author: hanykowska
external_url: https://www.thedataschool.co.uk/hanna-nykowska/scheduling-alteryx-workflow-that-updates-data-used-in-tableau/
external_site: ds
excerpt_separator: <!--more-->
---

How to schedule Alteryx workflow and keep your Tableau dashboard up-to-date?

[First published on The Data School Blog.]({{page.external_url}}){:target="\_blank"}

<!--more-->

<p>This is something with a lot of potential. Let&#8217;s say you are gathering your own data (eg. via web scraping or APIs) and you want your visualisations to be up-to-date without the need of you running the data workflow manually. It is actually something I&#8217;ve learnt during our Friday project of web scraping and API week with <a href="https://twitter.com/andre347_">Andre</a>.</p>

<p>The first part of the project was to web scrape a meteorological institute website to get weather data for the Netherlands. Easy enough. (Although there was a bit that I&#8217;ll blog about. If you wonder how to download zip files and un-zip them automatically in Alteryx, look out for my next blog posts.) </p>

<p>The second part was to schedule the workflow to run daily and set up a dashboard that would use the updated data, so that whenever you access the dashboard you know it&#8217;s the latest information. Not so easy. </p>

<p>This project was quite nice because we were working in pairs and we had Thursday afternoon and Friday morning for it. By the end of Thursday, Joe and I had our workflow ready, we just needed to upload the data to Tableau Server so that we could have a live connection there. <em>Just</em>&#8230;</p>

<p>This turned out to be quite a hefty task actually and so I decided to share it with you. Especially that I think it&#8217;s an important thing to know. OK, so how do you go about it? (It might be a lengthy post so if you&#8217;re not interested in the journey but the solution, you can head to the end of the post.)</p>

<h3>Step 1. Logistics</h3>

<p>First of all, think about the final outcome. To schedule an Alteryx workflow you&#8217;ll either need Alteryx Server or Scheduler (read more <a href="https://help.alteryx.com/current/ScheduleNewJob.htm?tocpath=Alteryx%20Scheduler%7C_____1">here</a>). The advantage of Alteryx Server is that you set it once and don&#8217;t really have to worry about it. With the Scheduler, you&#8217;d have to make sure your local computer is running. Thankfully, we have an Alteryx Server so we could go with that.</p>

<p>How do you want the users to access your viz? Is it just you, do you have a Tableau Server that you could publish your viz to? The connection to data will have to be a live connection since we want the viz to use the latest data. This means that Tableau Public is rather a no-go since not all live connections are available there.</p>

<h3>Step 2. Publish to Tableau Server</h3>

<p>In our case, we wanted to publish our viz on Tableau Server and so it made sense to publish the data there as well. It turned out that there even is a &#8216;Publish to Tableau Server&#8217; tool in Alteryx. Great! And so the struggle began&#8230; (Spoiler alert: this didn&#8217;t work but I&#8217;ll still explain the tool and why it didn&#8217;t work)</p>

<figure class="wp-block-image"><img src="https://dabblingwithdata.files.wordpress.com/2015/12/capture.png?w=665" alt="Image result for publish to tableau server tool alteryx" /></figure>

<p>As part of the connectors section, this <a href="https://help.alteryx.com/2018.3/TableauServerPublish.htm">tool</a>, allows you to publish your output as .hyper or .tde on a Tableau Server. First things first. The newest version is not the best so I&#8217;d advise you to delete the current version (if you have it) and install 1.09 (I ended up using 1.09.2). The path to where you might find Publish to Tableau Server tool is C:\Users\[your_user]\AppData\Roaming\Alteryx\Tools. I have found a folder there which was named &#8216;Publish to Tableau Server&#8217; or something along those lines. Delete it and instal the mentioned 1.09 from <a href="https://gallery.alteryx.com/#!app/Publish-to-Tableau-Server-Tool/599c93c8f499c7141c13a619">Alteryx Gallery</a>. Whenever you&#8217;re using Publish to Tableau Server, now you should have the option to choose the tool version when you right-click on it:</p>

<figure class="wp-block-image"><img loading="lazy" width="814" height="425" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-6.png" alt="" class="wp-image-25607" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-6.png 814w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-6-300x157.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-6-768x401.png 768w" sizes="(max-width: 814px) 100vw, 814px" /></figure>

<p>Ok, so now that you&#8217;re using 1.09 version, you can actually connect to the Tableau Server. All the information about the server itself and your credentials are set up in the configuration pane:</p>

<figure class="wp-block-image"><img loading="lazy" width="427" height="599" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-7.png" alt="" class="wp-image-25608" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-7.png 427w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-7-214x300.png 214w" sizes="(max-width: 427px) 100vw, 427px" /></figure>

<p>An important thing to remember: <strong>include https://</strong> when typing in the server URL. I would suggest to use a specific site instead of the default one. You can also save the connection so that you don&#8217;t have to type all of it in every single time. You will also need to provide your credentials just as you would when accessing Tableau Server via a web browser.</p>

<p>The next tab allows you to specify where you want to publish your data to:</p>

<figure class="wp-block-image"><img loading="lazy" width="419" height="440" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-8.png" alt="" class="wp-image-25609" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-8.png 419w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-8-286x300.png 286w" sizes="(max-width: 419px) 100vw, 419px" /></figure>

<p>What you can do here is to populate the project names list from Tableau Server. To do that, you need to select &#8216;Select project name&#8217; -&gt; Updated from and check the &#8216;Refresh project name list&#8230;&#8217;:</p>

<figure class="wp-block-image"><img loading="lazy" width="402" height="152" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-9.png" alt="" class="wp-image-25610" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-9.png 402w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-9-300x113.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-9-400x152.png 400w" sizes="(max-width: 402px) 100vw, 402px" /></figure>

<p>You&#8217;ll have to run the workflow and then you&#8217;ll be able to access the list of the projects. Another important note: if the &#8216;Refresh project name list&#8217; is ticked, the data will not be published.</p>

<p>When you have the project list updated, simply select the project you want to publish to (you might need to create it via browser) and give your data source a name. You have three options on how to save the data:</p>

<figure class="wp-block-image"><img loading="lazy" width="405" height="95" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-10.png" alt="" class="wp-image-25611" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-10.png 405w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-10-300x70.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-10-400x95.png 400w" sizes="(max-width: 405px) 100vw, 405px" /></figure>

<p>whatever you choose, will depend on your task at hand. In my case we went with overwriting the data source just because it was easier. Sometimes appending the data might be a better option. I&#8217;m not sure if overwriting will automatically create a new data source if it doesn&#8217;t exist. Just to be sure, we ran the flow once creating the data source and then changed it to overwriting.</p>

<p>A few things to mention&#8230; Apparently if you select .hyper as the output file it may incorrectly show up as .tde. It is, however, a .hyper file (according to documentation/forums). The file may look empty on Tableau Server when you just open it to explore it (eg. using Ask Data). To make sure it is not empty, just download the data and open it in Tableau. In my case it turned out it wasn&#8217;t empty after all.</p>

<h3>Step 3. Publish to Alteryx Gallery (Why this didn&#8217;t work?)</h3>

<p>Publishing to Alteryx Gallery/Server is very easy. File -&gt; Save As -&gt; your gallery, if you don&#8217;t have any set up yet (you should still have Alteryx Gallery), just click on Add a Gallery. This will open a window where you should type in the Gallery URL and then log in:</p>

<figure class="wp-block-image"><img loading="lazy" width="552" height="346" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-11.png" alt="" class="wp-image-25612" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-11.png 552w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-11-300x188.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-11-400x250.png 400w" sizes="(max-width: 552px) 100vw, 552px" /></figure>

<p>When you publish your workflow to Alteryx Gallery (Alteryx Server), you&#8217;ll get a message about the workflow&#8217;s assets, similarly when you export your workflow as a packaged workflow. There, you can select all extra files (macros, configurations, etc.). There were actually a few connected to Publish to Tableau Server tool, including one with authentication details. Despite including these files, it seemed that running the workflow from the gallery resulted in an authentication error from Tableau Server. This seemed to be quite tricky because I checked all possible boxes that would include those files but for some reason, the authentication did not work. And so I decided to try something else (after a suggestion both from Andre and <a href="https://twitter.com/benjnmoss">Ben</a>).</p>

<h3>Back to step 2. Output data to SQL database</h3>

<p>We&#8217;ve done probably a session on using SQL databases with Alteryx so I wasn&#8217;t quite sure how to approach this without all of the settings given to me. Thankfully, Andre helped a lot and pretty much set up the connection for me. The connection is chosen in the Output tool itself. (Maybe I&#8217;ll write a blog on it one day, who knows? But for the time being, you&#8217;ll need some extra resources to find out how to do this.) This turned out to work successfully from my local machine &#8211; yay! But then so did Publish to Tableau Server tool.</p>

<h3>Step 3. Publish to Alteryx Gallery (Why this didn&#8217;t work?)</h3>

<p>I did the same as I did when I was publishing my flow with Publish to Tableau Server tool, except this time there were no boxes to check that could hold the authentication details&#8230; Not a good sign.</p>

<p>Unsurprisingly (at least to Andre&#8230;), I got an error when I tried to run the flow from within the gallery. It turned out to be most likely linked to the lack of credentials information.</p>

<p>Great, it was pretty late by that point and we still didn&#8217;t manage to fulfill the project requirements. At that time, Ben reminded me that I can set up the connection in the gallery that I could use straight away from Designer. He also reminded me that we&#8217;d apparently done it already!</p>

<h3>Back to step 2. Output data to SQL database (connection from the gallery) [this worked]</h3>

<p>To set up SQL connection in Alteryx Gallery/Server you&#8217;ll have to be an admin. Alternatively, ask the administrator of your Alteryx Gallery to do it for you.</p>

<p>To access the admin site, click on the cog in the upper right corner and select (surprise, surprise) &#8216;admin&#8217;. From there, go to Data Connections, in the panel on the left, -&gt; Add New. You should see something like this:</p>

<figure class="wp-block-image"><img loading="lazy" width="826" height="670" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-12.png" alt="" class="wp-image-25616" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-12.png 826w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-12-300x243.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-12-768x623.png 768w" sizes="(max-width: 826px) 100vw, 826px" /></figure>

<p>In this case, I wanted to use Microsoft SQL. The name of the connection is just something you can easily identify in your Alteryx Gallery Data Connections. I called mine [FirstnameLastname]_[name of the server]. For authentication type, I selected SQL Server Authentication where you can type in your credentials (this is the part I had problems with both with Publish to Tableau Server tool and SQL connection from Alteryx). Hit &#8216;test connection&#8217; to make sure everything works. Finally, select the correct database you want to access. Make sure to click save!</p>

<p>In the Data Connections, find your new connection. It should have 0 users and 0 studios assigned. To change this, click on the pencil icon. You should now see the following:</p>

<figure class="wp-block-image"><img loading="lazy" width="362" height="89" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-22.png" alt="" class="wp-image-25649" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-22.png 362w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-22-300x74.png 300w" sizes="(max-width: 362px) 100vw, 362px" /></figure>

<p>You&#8217;ll also see Name and Connection boxes. Connection  text box will have the odbc connection string which summarises the connection details (what you set up in the previous step). You can actually change it if you&#8217;re more familiar with the topic, but let&#8217;s leave it as it is for now. </p>

<p>In users and studios tab, you&#8217;ll be able to add users or private studios to the connection. Simply use the search bar to find the users (eg. yourself). They will show up below and you should see an updated number for users in the Data Connections view.</p>

<figure class="wp-block-image"><img loading="lazy" width="515" height="157" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-23.png" alt="" class="wp-image-25651" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-23.png 515w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-23-300x91.png 300w" sizes="(max-width: 515px) 100vw, 515px" /></figure>

<p>The cool thing about this is that if you go to your Alteryx Designer, you can find that database connection right there. Drag and drop input tool on the canvas. In the configuration, click on the arrow next to Connect a File or Database -&gt; Saved Data Connections -&gt; [your Alteryx Gallery] -&gt; [your saved connection]. And that&#8217;s it! you can as easily as that connect to that database and you don&#8217;t lose your credentials. You can set it up in the same way for output tool.</p>

<p>Once I&#8217;ve done this and changed the configuration of the output tool, I tried to run the flow on my local machine. It didn&#8217;t work because the odbc connection string had a driver that I don&#8217;t have on my computer. You could change the string in the connection settings (General Information tab in Edit Data Connections). I actually didn&#8217;t mind in this case because I was running low on time and decided to publish the flow and run it from the gallery. (I would advise to actually double check things first on your local machine.) </p>

<h3>Step 3. Publish to Alteryx Gallery and Schedule the Flow [this worked]</h3>

<p>After publishing my workflow to the gallery, I ran it from there.  The good news is&#8230; It worked! </p>

<p>OK, to actually run the flow in the gallery, you have to locate your workflow. You can go to Private Studio and find the name you gave it. this will take to a page with a big icon that you can change. You&#8217;ll see the name of your workflow, the private studio it belongs to, the version control, the description from metadata of the workflow and information about the runs; something like this:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="410" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-24-1024x410.png" alt="" class="wp-image-25804" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-24-1024x410.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-24-300x120.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-24-768x308.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-24-1080x433.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-24.png 1760w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>You can see there are three blue buttons: RUN, DOWNLOAD, SCHEDULE. To check the workflow works fine in the gallery, just hit RUN. Make sure you do this before scheduling. There&#8217;s no point in scheduling a workflow that doesn&#8217;t work.</p>

<p>To schedule a workflow, hit SCHEDULE. This will open a pop-up window where you can configure your private schedule:</p>

<figure class="wp-block-image"><img loading="lazy" width="795" height="722" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-25.png" alt="" class="wp-image-25805" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-25.png 795w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-25-300x272.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-25-768x697.png 768w" sizes="(max-width: 795px) 100vw, 795px" /><figcaption><br></figcaption></figure>

<p>As you can see, you have option to schedule a single run, recurring runs or custom (specific days or times that are not easily put into a pattern). I went for a daily recurring schedule at 4 AM so it is unlikely to clash with other potential schedules. You can add a name and comment for an easier identification of its purpose (both for yourself and other users).</p>

<p>To double-check your schedule is set up correctly, go to SCHEDULES (the panel on the left). You should see your schedule in the list with the workflow you scheduled. You can also check there if the schedule is active or complete and when is the next run happening.</p>

<h3>Step 4. Publish to Tableau Server [this worked]</h3>

<p>Now that your Alteryx workflow is all good and happy with all scheduling set up, you can work on your viz. Make sure you connect to the same SQL database from Tableau and this should do the trick.</p>

<p>If you use live connection, you can just publish your workbook to Tableau Server as it is. Go to Server -&gt; Publish Workbook. You have to be logged in to be able to do this. Just find the project you want to publish to, type in a name (or select it from the list if you&#8217;re re-uploading) and hit Publish.</p>

<p>I would, however, recommend using extract. It will work faster and so the user experience will be better. When you&#8217;re publishing, you&#8217;ll have the option to select a &#8216;Refresh Extract&#8217; schedule. You can opt for None but why would you read this blog then? You can also select one from pre-configured schedules on Tableau Server. If you want to have a different schedule than available, go to Tableau Server via web browser -&gt; Schedules -&gt; + New Schedule this will open a pop-up window where you can configure the schedule:</p>

<figure class="wp-block-image"><img loading="lazy" width="691" height="505" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-26.png" alt="" class="wp-image-25806" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-26.png 691w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-26-300x219.png 300w" sizes="(max-width: 691px) 100vw, 691px" /></figure>

<p>Make sure to choose Extract Refresh as task type and configure the rest according to your requirements. Then go back to Tableau Desktop and pick that schedule when publishing your workbook.</p>

<p>That&#8217;s it!</p>

<div style="height:62px" aria-hidden="true" class="wp-block-spacer"></div>

<p>All in all, this turned out to be quite a difficult task but also something that everyone who works with Tableau and Alteryx should do at least once. It helped that it was a project and that I had to figure it out myself. Sometimes if you just follow along, you don&#8217;t really remember that well what you had to do and why you had to do it.</p>

<p>Hopefully, this post is useful to others. It will certainly be useful to me whenever I have to do this task again.</p>

<p>Thanks for the reading, byeee!</p>
