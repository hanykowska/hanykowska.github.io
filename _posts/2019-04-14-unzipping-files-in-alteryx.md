---
layout: post
cover: /assets/images/posts-images/zipper.webp
navigation: True
title: "Unzipping files in Alteryx"
date: 2019-04-14 00:00:00
tags: [alteryx]
class: post-template
subclass: "post"
author: hanykowska
external_url: https://www.thedataschool.co.uk/hanna-nykowska/unzipping-files-in-alteryx/
external_site: ds
excerpt_separator: <!--more-->
---

How to automatically unzip files in Alteryx using download tool and dynamic input

[First published on The Data School Blog.]({{page.external_url}}){:target="\_blank"}

<!--more-->

<p><em>(This blog post assumes you are familiar with download tool and web scraping basics. If there is interest in explaining web scraping, please let me know and I&#8217;ll try to write a sensible blog on that as well.)</em></p>

<div style="height:48px" aria-hidden="true" class="wp-block-spacer"></div>

<p>Hi everyone! In my latest <a href="https://www.thedataschool.co.uk/hanna-nykowska/scheduling-alteryx-workflow-that-updates-data-used-in-tableau/">post</a>, I described how to schedule Alteryx workflow so that the data used in Tableau is automatically updated. I figured it out during a project <a href="https://twitter.com/andre347_">Andre</a> set up for DS13. Another part of that project was to actually get the data from <a href="https://www.knmi.nl/nederland-nu/klimatologie/daggegevens">KNMI</a> (a meteorological institute in the Netherlands). Let&#8217;s take a look at how the website looks like:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="789" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-40-1024x789.png" alt="" class="wp-image-25848" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-40-1024x789.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-40-300x231.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-40-768x591.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-40-1080x832.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-40.png 1083w" sizes="(max-width: 1024px) 100vw, 1024px" /><figcaption><a href="https://www.knmi.nl/nederland-nu/klimatologie/daggegevens">https://www.knmi.nl/nederland-nu/klimatologie/daggegevens</a><br></figcaption></figure>

<p>After some scrolling, you can notice there is a table with some links. If you right-click on the web page you can <em>inspect</em> it (at least in Chrome):</p>

<figure class="wp-block-image"><img loading="lazy" width="295" height="73" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-41.png" alt="" class="wp-image-25849" /></figure>

<p>This will open developer tools panel on the right-hand side where you can inspect the underlying HTML of the website:</p>

<figure class="wp-block-image"><img loading="lazy" width="1024" height="444" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-42-1024x444.png" alt="" class="wp-image-25850" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-42-1024x444.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-42-300x130.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-42-768x333.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-42-1080x468.png 1080w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-42.png 1835w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>

<p>At the very top of developer tools there&#8217;s a button that triggers finding html code based on the mouse location: if you hover on element, they will be highlighted in the code on the right.</p>

<figure class="wp-block-image"><img loading="lazy" width="52" height="35" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-43.png" alt="" class="wp-image-25851" /></figure>

<p>Using this we managed to identify the underlying links which turned out to be links to zip files.</p>

<figure class="wp-block-image"><img loading="lazy" width="526" height="147" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-45.png" alt="" class="wp-image-25853" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-45.png 526w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-45-300x84.png 300w" sizes="(max-width: 526px) 100vw, 526px" /></figure>

<p>How do you get all of the files uploaded as a data source without manually downloading them? Well, let&#8217;s see. </p>

<h3>Step 1. Download one of the files</h3>

<p>First of all, you need to find out what the file looks like inside &#8211; what kind of data it holds and how is it stored. What is inside that might be of interest? Simply click on one of the links, it should trigger downloading of the underlying file. Then unzip this file and have a look inside.</p>

<p>In our case, it turned out to be a single csv file per folder. The name of the folder and the file inside was etmgeg_[station number]. From this I knew I needed to have the station number and the links.</p>

<p>You can also download one or two more just to make sure the format is the same.</p>

<h3>Step 2. Get the links and other needed information</h3>

<p>This requires a bit of data parsing in Alteryx. When you use download tool to get the underlying HTML it will be downloaded as a string (or at least configure download tool to do so):</p>

<figure class="wp-block-image"><img loading="lazy" width="103" height="78" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-46.png" alt="" class="wp-image-25854" /></figure>

<p>The parsing of that string depends on the website that you are accessing. In my case, I used RegEx tool and <strong>tokenized</strong> (split to rows) parts of the HTML code that were between &lt;tr&gt; and &lt;/tr&gt; using:</p>

<pre class="wp-block-code"><code>&lt;tr&gt;(.*?)&lt;/tr&gt;</code></pre>

<p>Then, I <strong>parsed</strong> the station number:</p>

<pre class="wp-block-code"><code>&lt;td class=""&gt;(\d{3})&lt;/td&gt;</code></pre>

<p>This resulted only in a three-digit numbers. If my new field with station number had Null value, it meant I didn&#8217;t need it because it didn&#8217;t contain the data I needed.</p>

<p>Finally, I <strong>parsed</strong> the zip URL:</p>

<pre class="wp-block-code"><code>a href='(.*?)'</code></pre>

<p>OK, so now I have pretty much all I need from the web HTML.</p>

<h3>Step 3. Download the zip files as temporary files</h3>

<p>To get that, I used the links I parsed in Step 2. and a download tool with output configuration to a temporary file:</p>

<figure class="wp-block-image"><img loading="lazy" width="395" height="425" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-47.png" alt="" class="wp-image-25855" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-47.png 395w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-47-279x300.png 279w" sizes="(max-width: 395px) 100vw, 395px" /></figure>

<p>The output of the download tool now returns the filepath to the temporary file it save the zip file to. Instead of normal DownloadData field there is a DownloadTempFile field. This allows to create an exact filepath of the csv file within the downloaded zip file.</p>

<h3>Step 4. Create file paths for the files within downloaded zip files</h3>

<p>For this, just use a formula tool. In my case the formula looked as following:</p>

<pre class="wp-block-code"><code>[DownloadTempFile] + '|||etmgeg_' + toString([Station]) + '.txt'</code></pre>

<p>DownloadTempFile is the location of the temporary file, &#8216;|||&#8217; specifies location within that zip files (you can use the same syntax for accessing specific excel sheets in Alteryx) and is followed by the name of the file inside that you want to access. In my case, it was <em>etmgeg_[station number].txt.</em></p>

<h3>Step 5. Dynamic Input</h3>

<figure class="wp-block-image is-resized"><img loading="lazy" src="https://help.alteryx.com/11.7/DynamicInput.png" alt="Image result for dynamic input alteryx" width="59" height="59" /></figure>

<p>This tool is so helpful, you can also use it to upload multiple excel sheets. </p>

<p>In the configuration you need to set up the file Template. The file you downloaded earlier will come in handy now. Make sure the folder is unzipped and that you can easily access the file(s) inside. </p>

<p>On your left, in the configuration pane, you should see something similar:</p>

<figure class="wp-block-image"><img loading="lazy" width="437" height="369" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-48.png" alt="" class="wp-image-25856" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-48.png 437w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-48-300x253.png 300w" sizes="(max-width: 437px) 100vw, 437px" /></figure>

<p>Hit Edit&#8230; in the &#8216;Input Data Source Template&#8217; section. This will open a pop-up window like this:</p>

<figure class="wp-block-image"><img loading="lazy" width="522" height="550" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-49.png" alt="" class="wp-image-25857" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-49.png 522w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-49-285x300.png 285w" sizes="(max-width: 522px) 100vw, 522px" /></figure>

<p>At the top, you need to specify a file with the <strong>exact&nbsp;same</strong> format as the files you will be uploading. If the files are different in terms of the number of columns, they will be skipped entirely. <del>The template file needs to be in an unzipped folder and easily accessible. </del></p>

<p><strong>EDIT: The template file needs to be in fact zipped. Then you can choose which file from the archive you want to use as a template.</strong></p>

<p>Then you can go on with configuring the options as normal. In our case, we had to start data import at 48th line to skip the headings preceding the data itself:</p>

<figure class="wp-block-image"><img loading="lazy" width="241" height="27" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-50.png" alt="" class="wp-image-25858" /></figure>

<p>Hit OK and continue with the configuration. Make sure you have Read a List of Data Sources checked. In the Field drop down you should choose the field with the previously created file path and the action should be set to Change Entire File Path.</p>

<figure class="wp-block-image"><img loading="lazy" width="434" height="84" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-51.png" alt="" class="wp-image-25859" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-51.png 434w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-51-300x58.png 300w" sizes="(max-width: 434px) 100vw, 434px" /></figure>

<div style="height:35px" aria-hidden="true" class="wp-block-spacer"></div>

<p>That&#8217;s it! Now run your workflow to make sure everything works. It may be that you need some corrections. It all depends on how the data is structured.</p>

<p>Just so that you know how such workflow may look like, here&#8217;s a part of mine:</p>

<figure class="wp-block-image"><img loading="lazy" width="1173" height="123" src="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-52.png" alt="" class="wp-image-25860" srcset="https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-52.png 1173w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-52-300x31.png 300w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-52-768x81.png 768w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-52-1024x107.png 1024w, https://www.thedataschool.co.uk/content/images/wordpress/2019/04/image-52-1080x113.png 1080w" sizes="(max-width: 1173px) 100vw, 1173px" /></figure>

<p>You could use this technique even when you&#8217;re not downloading the zip files. Use Directory tool to get all the file names and continue from Step 4. Create file paths. (I haven&#8217;t tried it myself that way but it seems it should work.)</p>

<p>Here&#8217;s the <a href="https://gallery.alteryx.com/#!app/DownloadAndUnzip/5cc564978a93370e40239b69">link</a> to the workflow on Alteryx Gallery. As it uses download tools, you can&#8217;t run it from there but you should be able to download it.</p>

<div style="height:100px" aria-hidden="true" class="wp-block-spacer"></div>

<p>Thanks for reading and let me know if you have any questions. Byeee!</p>
