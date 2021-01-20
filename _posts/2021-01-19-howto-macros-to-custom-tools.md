---
layout: post
cover: https://www.theinformationlab.co.uk/wp-content/uploads/2021/01/Take-macros-to-next-lvl.png
navigation: True
title: "How to turn macros into custom Alteryx tools"
date: 2021-01-19 00:00:00
tags: [alteryx]
class: post-template
subclass: "post"
author: hanykowska
excerpt_separator: <!--more-->
external_url: https://www.theinformationlab.co.uk/2021/01/19/how-to-turn-macros-into-custom-alteryx-tools/
external_site: til
---

If you like to build macros to make your life easier and want to take it to the next level, you're in the right place!
Learn how to turn macros into custom tools. in Alteryx exemplified by the Test 1:1 Join

[First published on The Information Lab Blog.]({{page.external_url}}){:target="\_blank"}

<!--more-->
<p><em>Disclaimer: This post focuses on Alteryx macros. You can actually make custom tools that are not a macro, but that is way beyond the scope of this post. You can find more on custom tools built with SDKs <a href="https://help.alteryx.com/developer/current/SDK/ToolQuickStart.htm?TocPath=SDKs%7CBuild%20Custom%20Tools%7C_____1" target="_blank" rel="noreferrer noopener">here</a>.</em></p>
<div style="height:24px" aria-hidden="true" class="wp-block-spacer"></div>
<h2>Why?</h2>
<p>One of the main reasons (the only reason?) for custom tools is creating ready solutions for problems you find yourself having to solve <strong>a lot</strong>. If you know others run into the same issues, you can share it with them (or better yet, upload it to Alteryx Gallery so that everyone can benefit)!</p>
<p>Of course the custom solution here is a macro. But you can take it to the next level so that Alteryx recognises it and places in the right category!</p>
<p>A great use case for such custom tools is Quality Control - making sure that the data processing is going exactly as planned. Let's look at a macro I have recently built <em>Test 1-1 Join</em>.</p>
<div style="height:45px" aria-hidden="true" class="wp-block-spacer"></div>
<h3>Background on Test 1-1 Join</h3>
<p>Test 1-1 Join was created originally when I was working for a client and had to do many joins. It was expected that not all records will join, but those that did join had to be a 1:1 join, meaning no duplicates. With a big, complex workflow, I wanted a simple tool that would check if the join was 1:1 and let me know if anything was wrong.</p>
<p>Below is what I built:</p>
<figure class="wp-block-image size-large"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2021/01/image-52.png" alt="" class="wp-image-18833"/></figure>
<p>The macro needs to be connected to the data going into and out of the join tool to be tested and based on the count of records throws an error if the join was not one-to-one for both inputs.</p>
<p>After the client engagement, I thought this actually might be useful and so I recreated the macro and <a href="https://gallery.alteryx.com/#!app/Test-1-1-Join/5fff1bed8a93371688307a8e" target="_blank" rel="noreferrer noopener">uploaded it to Alteryx Gallery</a>. Let's talk now about how to get a macro to show up as one of the tools in the tool palette.</p>
<div style="height:83px" aria-hidden="true" class="wp-block-spacer"></div>
<h2>How?</h2>
<p>It's a fairly simple process (once you have your macro ready of course).</p>
<ol><li><a href="#step1">Save it in the right place</a></li><li><a href="#step2">Assign it a Category</a></li><li><a href="#step3">Add Tags</a></li><li><a href="#step4">Add description details</a></li><li><a href="#step5">Add author details</a></li><li><a href="#step6">Share it!</a></li></ol>
<div style="height:48px" aria-hidden="true" class="wp-block-spacer"></div>
<h3 id="step1">1. Save it in the right place</h3>
<p>Alteryx can automatically pick up on new macros. To make it happen, you need to <strong>map</strong> the location where you are storing all macros. Then save the new macro in the mapped folder.</p>
<p>But how does one <em>map a folder</em>?</p>
<p>Go to Options -&gt; User Settings -&gt; Edit User Settings:</p>
<figure class="wp-block-image size-large"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2021/01/image-53.png" alt="" class="wp-image-18838"/></figure>
<p>Navigate to Macros tab and click on the plus button:</p>
<figure class="wp-block-image size-large"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2021/01/image-54.png" alt="" class="wp-image-18841"/></figure>
<p>Give an appropriate Category Name. Macros works perfectly fine. Then click on the button with three dots to navigate to the folder with macros.</p>
<figure class="wp-block-image size-large"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2021/01/image-55.png" alt="" class="wp-image-18844"/></figure>
<p>Click OK to confirm and you should see something similar:</p>
<figure class="wp-block-image size-large"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2021/01/image-56.png" alt="" class="wp-image-18845"/></figure>
<p>Now whenever you build a macro, the first place Alteryx will want to save it to is that folder. (My guess is that if you have more locations saved here, you can pick one as the default for saving with the button on the right.)</p>
<p> If there are any macros added to that location, Alteryx will pick up on that and will show them in the ribbon with tools:</p>
<figure class="wp-block-image size-large"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2021/01/image-57.png" alt="" class="wp-image-18847"/></figure>
<p>If you have any nested folders inside that folder, they will be shown separately:</p>
<figure class="wp-block-image size-large"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2021/01/image-58.png" alt="" class="wp-image-18848"/></figure>
<p>In the above image, you can see that the names of the categories are based on the location relative to Macros folder. Apart from CReW Macros category... Which looks nicely formatted and not referencing the nested path. Which brings me to step 2:</p>
<h3 id="step2">2. Assign it a Category</h3>
<p>Assigning a category in the Meta Info of the workflow configuration, will add the macro into the specified category, or create a new category!</p>
<p>To do so, click on the canvas, so that the configuration pane says Workflow - Configuration, and navigate to Meta Info:</p>
<figure class="wp-block-image size-large"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2021/01/image-59.png" alt="" class="wp-image-18853"/></figure>
<p>Scroll down to the very bottom of the configuration pane. The penultimate section should be called Tool Palette. For Category Name put down any of the existing categories (I chose Developer as it seemed relevant for my Test 1-1 Join) or add a new one, just like CReW Macros in their Moving Summarize macro.</p>
<figure class="wp-block-image size-large"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2021/01/image-60.png" alt="" class="wp-image-18854"/></figure>
<p>After saving any changes made, and maybe restarting Alteryx (particularly if you create a new category), the macro should be presented as one of the tools in the right category!</p>
<figure class="wp-block-image size-large"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2021/01/developer-category-1.png" alt="" class="wp-image-18870"/><figcaption>sidebar nation, did you know you can <strong>pin</strong> categories so they show up next to favorites tab? Really useful if you often use categories that are further down!</figcaption></figure>
<p>This will get your new macro to be presented as one of the tools. But why stop here? We can make our lives even easier!</p>
<h3 id="step3">3. Add tags</h3>
<p>In the same section as assigning the Category Name, you can list tags related to the macro. Why, you ask? This will show your macro in the search!</p>
<p>In Search Tags, list key words which should be associated with your tool. In my quick test, it seemed that the parts of the name of the macro will be picked up on by the search bar/ If you want any additional words to bring up your macro, here's the place to do so. For example, if I add 1:1 phrase (I named my macro Test <strong>1-1</strong> Join, to make sure I don't get any issues with a colon sign in the file path):</p>
<figure class="wp-block-image size-large"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2021/01/image-63.png" alt="" class="wp-image-18891"/></figure>
<p>I can use <strong>1:1</strong> to find my custom macro!</p>
<figure class="wp-block-image size-large"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2021/01/image-62.png" alt="" class="wp-image-18890"/></figure>
<h3 id="step4">4. Add description details</h3>
<p>In Meta Info tab, you can also give the description of the workflow - what is it that the macro is actually doing? This will be displayed on the Alteryx Gallery page of your macro. (Orange highlight in a picture below.)</p>
<p>You can also add a URL and specify the display text (blue highlight below). This is very useful for adding additional resources, eg. documentation. I have created a documentation page on <a href="https://www.notion.so/" target="_blank" rel="noreferrer noopener nofollow">Notion</a> which makes it easy for me to maintain it. But you can use other tools that you like (eg. Google Docs)!</p>
<figure class="wp-block-image size-large"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2021/01/image-64-1024x456.png" alt="" class="wp-image-18897"/></figure>
<p>Both description and URL with display text can be set up in Description section of Meta Info:</p>
<figure class="wp-block-image size-large"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2021/01/image-65.png" alt="" class="wp-image-18899"/></figure>
<h3 id="step5">5. Add author details</h3>
<p>Final touch in terms of providing information is to specify the author and the company, so that people will know who they should contact if they have ideas for improvement or if they look for more goodies!</p>
<figure class="wp-block-image size-large"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2021/01/image-66.png" alt="" class="wp-image-18901"/></figure>
<h3 id="step6">6. Share it!</h3>
<p>OK! Now that the macro is ready to be shared with other people there are pretty much two ways I'd suggest.</p>
<p>ONE: In the mapping section (Step 1), use a folder that's on a shared drive or location that others have access to. That way they can map the same location in their own instance. Whenever the macro is updated they will get it automatically!</p>
<p>TWO: Save the macro on Ateryx Gallery and Publish. This will require an update to the saved file on Alteryx Gallery whenever you want to change anything. The massive advantage of this approach is that it will be available to many other people also outside of your organisation! You can actually find other custom tools (and macros) on Alteryx Gallery, including those developed by Alteryx!</p>
<p>Let's talk through option number TWO (do it <strong>only</strong> if your macro is to be shared publicly). Go to File &gt; Save As &gt; Public Gallery &gt; Alteryx Gallery</p>
<figure class="wp-block-image size-large"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2021/01/image-67.png" alt="" class="wp-image-18903"/></figure>
<p>If you haven't already, log in in the new pop-up window:</p>
<figure class="wp-block-image size-large"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2021/01/image-68.png" alt="" class="wp-image-18907"/></figure>
<p>You will see now a dialog to save the workflow on Alteryx Gallery. You can change workflow name if you want (I left mine as the default). A comment in details (optional) is what shows up as a comment next to the version of the tool (which you can see only after logging in and for your own tools). If you want to have a description of the workflow, go back to Step 4.</p>
<figure class="wp-block-image size-large"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2021/01/image-69.png" alt="" class="wp-image-18909"/></figure>
<p>In workflow options, you can go to manage assets and make sure any necessary external resources are included in the upload. For example, if you build a macro that connects to a data file, you probably want to include that. What you can see in my screenshot below are assets related to Count Records macro. As this is a macro that comes with Alteryx, they don't have to be included for the macro to work. (Same with data cleansing tool!)</p>
<figure class="wp-block-image size-large"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2021/01/image-70.png" alt="" class="wp-image-18911"/></figure>
<p><em>Side note on downloading workflows with Count Records macro from Alteryx Gallery - they will likely throw some errors on those missing dependencies. Clicking through OK is enough - those errors will not affect how the overall workflow works.</em></p>
<p>Once managing assets is sorted click Done, it will take you back to the general save page. When you're happy with your settings, hit Save.</p>
<p>After the upload is complete, you will have the option to see it in the browser. This is what I see (I saved mine as Test 1-1 Join2 so that I know which one to delete once I'm done....)</p>
<figure class="wp-block-image size-large"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2021/01/image-71.png" alt="" class="wp-image-18916"/></figure>
<p>A few things to change: the image, sharing, tags. Click on Change Icon button (below the current icon) and select an appropriate image - I chose the same file I used for the macro icon.</p>
<p>Add Tags (just above the Download tool) will help categorise your upload. It will be a multi-choice selection.</p>
<p>At the moment, the workflow is accessible only to you. Go to Sharing dropdown, select Place in Public Gallery. This will allow anyone with a link to your tool page to access it (including people who are not logged in), and your macro will show up in the search on Alteryx Gallery page.</p>
<figure class="wp-block-image size-large"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2021/01/image-72.png" alt="" class="wp-image-18918"/></figure>
<p>Click on Yes and let people know what you've published so that they can take the advantage of it! If you go to Sharing again, you will see that the options now have changed:</p>
<figure class="wp-block-image size-large"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2021/01/image-73.png" alt="" class="wp-image-18919"/></figure>
<p>For guidance on how to install new tools from the gallery, you can use the <em>How to Install</em> section of my Test 1-1 Join tool documentation <a href="https://www.notion.so/Test-1-1-Join-Macro-Documentation-7a2c1dbbff4743349e46c3eb41fba05f#b35abb94219c4afe9bd5942b06b17120" target="_blank" rel="noreferrer noopener nofollow">here</a>.</p>
<div style="height:56px" aria-hidden="true" class="wp-block-spacer"></div>
<p>That's it! Thanks for reading and enjoy your new custom tools!</p>
