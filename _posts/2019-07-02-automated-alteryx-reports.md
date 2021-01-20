---
layout: post
cover: /assets/images/posts-images/automated-alteryx-reports-cover.png
navigation: True
title: "How to: Automated Alteryx Reports"
date: 2019-07-02 00:00:00
tags: [alteryx]
class: post-template
subclass: "post"
author: hanykowska
excerpt_separator: <!--more-->
external_url: https://www.theinformationlab.co.uk/2019/07/02/how-to-automated-alteryx-reports/
external_site: til
---

Say you have data that gets regularly updated and you need to send those updates to multiple people. Build automated reports with Alteryx!

[First published on The Information Lab Blog.]({{page.external_url}}){:target="\_blank"}

<!--more-->
<p><strong>Why bother?</strong> Let's say you have data that gets regularly updated and you need to send those updates to multiple people. What you can do is build an Alteryx workflow that creates reports with the relevant data and sends it via email to selected people. Furthermore, if you have Alteryx Server, you can upload the workflow onto the Server and schedule it so that the reports are updated and sent automatically.</p>
<p>If you want to have a look at a specific tool, here's the list of what is covered in the blog post:</p>
<ul><li><a href="https://www.theinformationlab.co.uk/?p=13874&amp;#table">Table</a></li><li><a href="https://www.theinformationlab.co.uk/?p=13874&amp;#map">Report Map</a></li><li><a href="https://www.theinformationlab.co.uk/?p=13874&amp;#static-text">Report Text&nbsp;Static</a></li><li><a href="https://www.theinformationlab.co.uk/?p=13874&amp;#dynamic-text">Report Text Dynamic</a></li><li><a href="https://www.theinformationlab.co.uk/?p=13874&amp;#layout">Layout</a></li><li><a href="https://www.theinformationlab.co.uk/?p=13874&amp;#render">Render</a></li><li><a href="https://www.theinformationlab.co.uk/?p=13874&amp;#email">Email</a></li></ul>
<h3>Scenario</h3>
<p>Instead of talking in general terms, let's look at a specific scenario. You should be able to apply similar logic to your situation.</p>
<p>Let's imagine we are working for a SuperStore (Sample Superstore data available with Tableau) and we want to send out monthly updates on year-to-date performance to market managers. We have four markets (otherwise known as Regions): East, West, Central, South. In the monthly updates, we were told to include YTD sales and profit for the Region in question and information on underperforming cities by Categories. Underperforming cities are defined as those with YTD profit below -$500.</p>
<p>This is the report I built for one of the Regions using Alteryx:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-5.png" alt="" class="wp-image-13900"/></figure>
<div style="height:43px" aria-hidden="true" class="wp-block-spacer"></div>
<h2>The process</h2>
<p>The general, high-level overview of the process is as follows:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-3.png" alt="" class="wp-image-13897"/></figure>
<blockquote class="wp-block-quote"><p><strong>Intro to reporting in Alteryx.</strong> Any element in the report will most likely need its own reporting tool [step 3 in the process above]. On top of that, the outputs of these reporting tools will need to be combined using layout tools [step 4]. I think of the instances of layout tools as containers, either horizontal or vertical (no other options available). The output of a layout tool can also be an input into another layout tool, creating nested containers. When building an Alteryx report, try to identify the building blocks and break them down to basic elements. This will help you figure out how to combine these elements using layout tools. Once the report is put together, you can save it as a file (render tool) or email it (email tool) [step 5].</p></blockquote>
<p>The first two steps will strongly depend on the task you are dealing with. In the case of the outlined scenario, I'm connecting to two files: one with all of the data (Sample - Superstore, users of Tableau should be quite familiar with this one) and one that has information on the city locations in the USA. (The latter can be accessed from <a href="https://simplemaps.com/data/us-cities">https://simplemaps.com/data/us-cities</a>.) I joined the files so that I can plot the underperforming cities' locations on a map.</p>
<p>In order to prepare the data, I created a YTD flag - a field that checks if the date is from the same year as <em>today</em> and before <em>today</em>. (If the data is only available up until <em>today</em> then you may not need to check the latter. I would, however, recommend it. It's an extra step but will prove helpful in the testing phase, at least the numbers should make more sense.) As for <em>today</em>, the data in Sample -Superstore I'm using goes only up to 30-12-2018 so I created a <em>today</em> field where I hard-code what I want to use as 'today'. This technique might be useful during the development of the workflow. When the workflow goes live, change the hard-coded date into DateTimeToday():</p>
<pre class="wp-block-code"><code>ToDate('2018-11-01')
//Use the below instead when the workflow goes live:
//DateTimeToday()</code></pre>
<p>Make sure that the data type is set to Date.</p>
<div style="height:24px" aria-hidden="true" class="wp-block-spacer"></div>
<p>After filtering out rows that don't meet YTD requirement I just used basic tools to get the values we were asked for. Here are my steps 1 and 2:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-4.png" alt="" class="wp-image-13898"/></figure>
<p>Important thing to remember is that you will need to have your data ready for the reports, so all calculation need to be performed before creating reporting fields.</p>
<h3>Build the Report Fields</h3>
<p>Step 3 is to build a reporting field for every element you want to have in the report. Looking back at the report, we have:</p>
<ul><li>Report header with a photo</li><li>Region header</li><li>YTD Sales</li><li>YTD Profit</li><li>Map header</li><li>Map with a legend for underperforming cities</li><li>Within each category:<ul><li>Category header</li><li>YTD Sales</li><li>YTD Profit</li><li>Table with information on underperforming cities</li></ul></li></ul>
<p>Each of the above will need its own report field. When I was building my workflow, I split this part into four sections: Table by City; Map with its header; Category Level and Region Level Headers.</p>
<div style="height:25px" aria-hidden="true" class="wp-block-spacer"></div>
<h4 id="table">Table by City</h4>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-43.png" alt="" class="wp-image-14222"/></figure>
<p>This is the easiest section and it uses only a single reporting tool.</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-37.png" alt="" class="wp-image-14213"/></figure>
<p>First, I'm using a Select Tool to rename the fields I want to include in the table so that the headings on the report are formatted correctly (title case, correct spelling). This can be also done in the Table Tool itself. </p>
<p>As the data will be presented as it is, I used the sort tool to make sure the profit is in ascending order. (The report is on underperforming cities, so it makes sense to show those with the lowest profit first. In other situations, alphabetical order could be more appropriate and this is something to discuss with the stakeholders: what are they interested in the most.)</p>
<h5>Table</h5>
<p>Once the data is in the right order, we can drag in the Table Tool.</p>
<p>Keep the Table Mode as <em>Basic</em>. In the Group By section, check the Category and Region boxes - we want to have separate reports for each Region and within those reports, separate tables for each Category.</p>
<p>In Table Configuration, I didn't change anything. You can build an in-table Bar Graph, should you want to add more visualisation to the report. The bar graph will be added at the end of the table, so it might make sense to move the field used for building the bars to be at the end s that the values are next to the bars. The graph will have axis range instead of a heading.</p>
<p>In the Per Column Configuration, check only boxes next to fields you want to include in the table. You can also reorder the fields by highlighting them and using green arrows to move them closer to the beginning (↑) or the end (↓) of the table. Highlighting the field will allow you change field-specific parameters, including the name of the field, alignment, decimal places for numeric fields, etc.</p>
<p>Default Table Settings... will open a pop-up window with formatting settings:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-40.png" alt="" class="wp-image-14216"/></figure>
<p>Row Rules and Column Rules can be used, for example, for highlighting cells with profit below -$1K.</p>
<p>You can find the configuration I used below:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-38.png" alt="" class="wp-image-14214"/></figure>
<p>If you add a browse tool afterwards, you should see something similar to the following:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-41.png" alt="" class="wp-image-14217"/></figure>
<p>The results are showing that we have separate Tables for each Region-Category combination: </p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-42.png" alt="" class="wp-image-14218"/></figure>
<p>The first section of the report is thus finished!</p>
<div style="height:53px" aria-hidden="true" class="wp-block-spacer"></div>
<h4>Map and Heading</h4>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-44.png" alt="" class="wp-image-14223"/></figure>
<p>The next section would be the map with the heading and the legend. This part of the workflow consists of three reporting reporting tools: Report Map [2], Text [3], Layout [4]:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-30.png" alt="" class="wp-image-14205"/></figure>
<h5 id="map">Map</h5>
<p>The first step in building a map is creating a spatial object field. In this situation, we only want points so I used the Create Points tool [1] and connected it to Report Map tool [2]. The configuration of the latter is a bit fiddly. The good news is that there is a preview of the map that will be created, so you don't have to run the workflow every time to see minor formatting changes to the map.</p>
<p>The first tab in the configuration is <em>Settings</em>, where you can specify the size of the map, resolution, scale, base map and more. If you haven't changed your user settings for maps, you may not have a background - just pick a Reference Base Map other than [None] (I have it set to Carto (Positron)):</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-9.png" alt="" class="wp-image-13907"/></figure>
<p>The next tab, <em>Data</em>, allows you to select which spatial fields you want to plot on the map, whether you want to group by any of the fields and whether you want to apply conditional formatting based on a field.</p>
<figure class="wp-block-gallery columns-2 is-cropped"><ul class="blocks-gallery-grid"><li class="blocks-gallery-item"><figure><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-10.png" alt="" data-id="13908" class="wp-image-13908"/></figure></li><li class="blocks-gallery-item"><figure><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/Snag_53907368.png" alt="" data-id="13912" data-link="https://www.theinformationlab.co.uk/?attachment_id=13912" class="wp-image-13912"/></figure></li></ul></figure>
<p>There is only one spatial field in the data set I'm using, so the choice is quite easy. (Alternatively, you can keep it on default [All SpatialObjs]). </p>
<p>We know we want to build the reports separately for each of the Regions. This is where Grouping Field comes in. The unique values of the field you select from the drop-down will become the rows in Group field of the Report Map output and each map will use only relevant data points.</p>
<p>Thematic Field allows changing the formatting of map objects based on the selected field's values. The formatting can be changed in the <em>Layers</em> tab. When you first open it, it has only base layers. We need to add a new layer to customise the map. Click on the plus sign -&gt; Points Layer (or whichever option you need) -&gt; #1 (identifies the connection to the tool, compare with what you have in the <em>Data</em> tab):</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-12.png" alt="" class="wp-image-13913"/></figure>
<p>Once added, you can change the name of the layer should you want to. Expand the menu for the newly created layer by clicking on the + sign next to its name. There will be Style and Theme (only if you have a field selected for Thematic Field the <em>Data</em> tab). Style will apply changes to all marks, I used it to change the opacity and mark type to circle instead of diamond. (The list of mark types is quite extensive and you can also pick <em>house</em> as an option! It was a highlight of my day when I've found out. It's the little things, you know?)</p>
<p>In Theme, I set the Tile Method to Unique Values which allows you to manually specify the groups. I think it's weird it won't just take the unique values within the selected field, instead, you need to list them in Specific Values. And I mean manually type those values there:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-13.png" alt="" class="wp-image-14017"/></figure>
<p>To make sure the values are exactly the same as in data, you can copy and paste values from cells in Results pane.</p>
<p>Color Method can vary between discrete and continuous colour palette (Map and Ramp respectively). In our situation, Map makes more sense. I couldn't find a colour palette that I liked, so I decided to manually assign specific colours to each of the Categories. To do so, expand the Theme in the menu. You should see now the same options as what was typed in Specific Values. You will need to expand each of the values separately, then go to Style to update it:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-14.png" alt="" class="wp-image-14019"/></figure>
<p>As you can see, I have only changed the Color. Tick the Color box and click on '...' box. Sadly, there is no place to type in the hex code of the colour, so you'll need to type in the Red, Green and Blue boxes or play around with the Color Picker. Do the same for the remaining values.</p>
<p>Finally, let's move on to the <em>Legend</em> tab. I wanted to have a legend below the map and since there is no such option in the Position, I chose Separate Field:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-15.png" alt="" class="wp-image-14022"/></figure>
<p>This means, that the legend is returned as a separate field in the tool output and I can place it where I want using a layout tool (more on that later on). I have also changed the background colour to white to match the page sheet. This is the output of the Report Map Tool:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-17.png" alt="" class="wp-image-14024"/></figure>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-16.png" alt="" class="wp-image-14023"/></figure>
<div style="height:37px" aria-hidden="true" class="wp-block-spacer"></div>
<h5 id="static-text">Map Heading</h5>
<p>Now that we have the maps ready, let's prepare the headings. For the map heading, we want to have a static text. Connect Report Map tool [2] to the Report Text tool [3]. Set the Text Mode to <em>Create new field for this text</em> and in the Text Data, type in 'Cities with profit below -$500:'.</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-31.png" alt="" class="wp-image-14206"/></figure>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-18.png" alt="" class="wp-image-14025"/></figure>
<p>If you want to change the formatting of the text, particularly the font, highlight the text you want to change and click on <strong><em>A</em></strong>. This will open a pop-up window where you'll be able to adjust the font to your liking. A word of caution: the font style (including the bold, cursive and size) will be applied to the entire highlighted text, in other words, you can't change just the typeface. At least not to my knowledge. If you want fonts of different sizes in the heading, make sure everything else is as you want it to be. Otherwise, you'll have to re-do the whole formatting.</p>
<div style="height:40px" aria-hidden="true" class="wp-block-spacer"></div>
<h5 id="layout">Layout</h5>
<p>Ok, now that we have the map, the legend and the heading, we can put this section together. To do that, we'll need a Layout Tool [4].</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-32.png" alt="" class="wp-image-14207"/></figure>
<p>Keep the Layout Mode as <em>Each&nbsp;Individual&nbsp;Record</em>, this will allow for combining different fields at a row level as opposed to combining one field for all records. I checked the <em>Include Source Fields Output</em> but in this case it doesn't make a difference.</p>
<p>In Layout Configuration, change the Orientation to <em>Vertical</em>. I didn't change anything else, but you can play around with the layout dimensions, separators between elements being put together and cell padding.</p>
<p>In the Per Row Configuration, make sure the Text, Map and Legend are all checked and are in this specific order - this is the order they will laid out. You can move the position of a field by highlighting it and using the green arrows. Highlighting a field will also give you the option of changing certain field-specific parameters:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-33.png" alt="" class="wp-image-14208"/></figure>
<p>Here is the whole configuration for reference:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-19.png" alt="" class="wp-image-14026"/></figure>
<p>And here is the output of the layout tool:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-34-1024x88.png" alt="" class="wp-image-14209"/></figure>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-35.png" alt="" class="wp-image-14210"/></figure>
<p>There are four rows, one per Region (Group) and the next part of the report is ready: the map with the heading and legend.</p>
<div style="height:70px" aria-hidden="true" class="wp-block-spacer"></div>
<h4 id="dynamic-text">Category Level Headers</h4>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-45.png" alt="" class="wp-image-14224"/></figure>
<p>For this section, we need three Text tools and two Layout tools:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-46.png" alt="" class="wp-image-14225"/></figure>
<p>Unlike in the map heading, we want the text objects in this section to by dynamic and change based on the data values.</p>
<p>For YTD Sales, keep Text Mode as <em>Create&nbsp;new&nbsp;field&nbsp;for&nbsp;this&nbsp;text</em>, I named the new field 'YTD Category Sales Text'. In the Text Data, I have:</p>
<pre class="wp-block-code"><code>YTD Sales: $&#91;Category YTD Sales:0]</code></pre>
<p>The square brackets indicate the field I want to get the value of and :0 indicates no decimal format. To include a field from the data, click on Available Fields -&gt; Field of choice -&gt; Format option (if available):</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-49.png" alt="" class="wp-image-14229"/></figure>
<p>See below my configuration for reference:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-48.png" alt="" class="wp-image-14228"/></figure>
<p>Because Sales cannot be negative, I just used dollar sign before the field. In case of profit, however, this is not the case. At the level of category, the value can be positive or negative and I needed to built a formula to make sure the formatting is correct. I created a new string field, called New Profit with following expression:</p>
<pre class="wp-block-code"><code>If &#91;Category YTD Profit] &lt; 0
then '-$'+ToString(ABS(&#91;Category YTD Profit]),0,1)
else '$'+ToString(&#91;Category YTD Profit],0,1)
endif</code></pre>
<p>The above checks whether the profit is negative. If it is, then it returns the profit value with dollar sign between the minus sign and the numbers. Otherwise, it adds the dollar sign before the profit value. ToString function transforms a number into text and it allows you to format the number as you wish: the second argument is the number of decimal places (0 - off above), thousands separator (1 - on above) and decimal separator (not present above, default value is 0 - off).</p>
<p>Text Tool for YTD Profit is very similar to that of YTD Sales. The difference is the field included is a string and not a number:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-50.png" alt="" class="wp-image-14230"/></figure>
<p>Very similar settings for Category Heading (Category Text) as well:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/06/image-51.png" alt="" class="wp-image-14231"/></figure>
<p>Now that we have all the text fields that we need for this section, it's time for the Layout tools. In this case, we'll need two of them: first to join YTD Sales and YTD Profit side by side and second to the Category Heading with the joined Sales and Profit.</p>
<p>Let's drag in a Layout tool. Keep the Layout Mode as <em>Each&nbsp;Individual&nbsp;Record</em>. In the Layout Configuration, I didn't change anything (the orientation should be set to <em>Horizontal</em>). In Per Column Configuration, keep only YTD Sales and YTD Profit checked. To make sure the Sales and Profit sections are distributed evenly, highlight YTD Sales, change Width to <em>Percentage</em> and set it to 50%. (You can repeat it for YTD Profit, but it's not necessary). Here's the full configuration:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-2.png" alt="" class="wp-image-14235"/></figure>
<p> Drag another Layout Tool. I haven't changed anything in the top section. In Layout Configuration, however, make sure to change Orientation to <em>Vertical</em>. In Per Row Configuration, there should be only two fields available: the Category Heading and Layout (the result of the previous layout tool).  Keep both fields checked, with Category Heading first:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-1.png" alt="" class="wp-image-14234"/></figure>
<p>This is the result presented by a Browse Tool:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-3.png" alt="" class="wp-image-14236"/></figure>
<h4 id="mce_33">Region Level Headers</h4>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-7.png" alt="" class="wp-image-14240"/></figure>
<p>The setup here is very similar to that of category level headers. The only differences are: the formatting and the data which is at a regional level.</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-4.png" alt="" class="wp-image-14237"/></figure>
<p>As the tools used and the configuration is so similar to the previous one, I'll cover the differences here. </p>
<p>In the YTD Sales (and YTD Profit), I used central alignment and made the font for the number bigger and bold. To have different formatting within a single Report Text, highlight only a part of the text and then click on <em><strong>A</strong></em> to change the font style:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-5.png" alt="" class="wp-image-14238"/></figure>
<p>The Region Report Text, only has [Region:A] centered in the text input.</p>
<p>After the vertical Layout Tool, you should get something similar to this:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-6.png" alt="" class="wp-image-14239"/></figure>
<div style="height:53px" aria-hidden="true" class="wp-block-spacer"></div>
<h3>Put the Report Together</h3>
<p>Now that we have all sections and almost all elements ready (we are only missing a header at the moment), we need to combine the sections to form a full report. This task will require a few Joins, a few more Layout Tools and a Header Tool:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-8.png" alt="" class="wp-image-14242"/></figure>
<p>First, let's join the Table and the Category Heading by Category and Region. Feel free to get rid of some of the field, but keep Category, Region, Table and Layout. </p>
<p>Then, in the Layout Tool, change Orientation to <em>Vertical</em>, make sure both Layout and Table are checked and that Layout is first. This will create Category sections, each with it's heading and a table with details.</p>
<p>Now we can put all Categories together for a single Region. In the next Layout Tool, change Layout Mode to <em>Each&nbsp;Group&nbsp;of&nbsp;Records</em> and group by Region. Change Orientation to <em>Vertical</em>. I also added cell padding of 15 to separate visually the Categories. Leave Per Row Configuration as is:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-9.png" alt="" class="wp-image-14243"/></figure>
<p>See below an example of the output:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-10.png" alt="" class="wp-image-14244"/></figure>
<p>Let's join now the Categories sections with the Region-level elements. You can use a multi-join tool, but a multiple joins approach is a safer option and it's easier to check everything is joining correctly.  First, join the output of the most recent Layout tool with the Region Level Headers by Region. Then join the inner join (anchor J) with the map also by Region. From the Map section, I only kept the Layout field and renamed it Map.</p>
<p>Now, add another Layout Tool. Change Orientation to <em>Vertical</em>, add white separator of 1 pixel and cell padding of 5 pixels. In Per Row Configuration, keep Region Layout, Map and Category Tables checked and in that order (the field were renamed in the joins, you can also do that before the joins so it's not confusing). </p>
<p>This is the setting:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-11.png" alt="" class="wp-image-14246"/></figure>
<p>And this is the result at this stage:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-12.png" alt="" class="wp-image-14247"/></figure>
<h5 id="header">Header</h5>
<p>The report is nearly ready, we only need a header. Drag in a Header Tool. In its configuration, you can type in the title of the report. I decided to include the date as well (pick whichever date format you prefer). Additionally, you can add more branding to the report by using an image (logo) in the header. By default, it will be an Alteryx logo, but you can also upload your own image.</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-13.png" alt="" class="wp-image-14248"/></figure>
<p>There are two ways to combine the header with the rest of the report. You can either use a Layout Tool or a Render Tool. Render Tool will also render and save the report into a file. However, as I wanted to send the report in the email, I used the Layout method.</p>
<p>Let's take yet another Layout Tool, change the Orientation to <em>Vertical</em> and check Header and Layout (and keep them in this order) in the Per Row Configuration. And here's the report:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-14.png" alt="" class="wp-image-14249"/></figure>
<p>Awesome! The report is pretty much ready, we need to store it somewhere now. We can either save it into a file or send it in an email.</p>
<div style="height:41px" aria-hidden="true" class="wp-block-spacer"></div>
<h3 id="render">Save the report</h3>
<p>To save the report, grab a Render Tool. In Render Configuration,  change Output Mode to <em>Choose&nbsp;a&nbsp;Specific&nbsp;Output&nbsp;File</em>. In the output file, I typed in </p>
<pre class="wp-block-code"><code>report.pdf</code></pre>
<p>The name of the file is not really that important as we will change it. The extension, however, needs to match one of the supported file types. Check Group Data Into Separate Reports, choose <em>Region</em> as Field to Group On and for Modify Filename By select <em>Replacing&nbsp;Filename&nbsp;With&nbsp;Group</em>.</p>
<p>In Report Data, change Separator to <em>Insert&nbsp;Whitespace&nbsp;Between&nbsp;Records</em>. </p>
<p>In Report Style,  change Paper Size to A4 and adjust margins if you want to. </p>
<p>Now every time you run the workflow, the reports will be created and saved to the specified files. Make sure the files are not open when running the workflow as this will result in an error. If you don't want to overwrite files and want to keep history of the reports, you can use a formula tool and combine the Region with today's date - this will also allow for quick identification of the report without opening it.</p>
<div style="height:41px" aria-hidden="true" class="wp-block-spacer"></div>
<h3 id="email">Email the Report</h3>
<p>Alternatively, if you want your colleagues to receive the reports directly, you can do it by sending the report in an email. The workflow here is not a single tool, but that allows you to make the emails dynamic:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-15.png" alt="" class="wp-image-14252"/></figure>
<p>The mailing list input (here as a text input but you can use a file stored somewhere in your database) should contain two columns: Region and Email address. The email addresses might be of specific people or subscription lists:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-16.png" alt="" class="wp-image-14253"/></figure>
<p>Once you have the mailing list with assigned Region, join it with the Layout tool that combined the report with the header. Then drag in an Email Tool and let the magic begin.</p>
<p>Keep the Enabled box checked, this will send out the emails. If the box is unchecked, the Email Tool is disabled but it keeps all the settings (pretty much has the same effect as adding the tool t a container and disabling the container).</p>
<p>SMTP will depend on your company IT infrastructure. If you're using Gmail as your email provider, then type in</p>
<pre class="wp-block-code"><code>smtp-relay.gmail.com</code></pre>
<p>otherwise, I would suggest checking with IT. Consult <a href="https://help.alteryx.com/2018.2/Email.htm">Alteryx help</a> page for more information.</p>
<p>For the next section (To, Cc, Bcc, From, Subject), you can either type in the values or use a field if you want to make them dynamic. The necessary fields are To, From and Subject.</p>
<p>In the Body of the email, I used <em>Use&nbsp;Field</em> and selected <em>Layout</em> from the drop-down. Alternatively, you could send the report as an Attachment but that makes things much more complex and I would advise against it unless it's absolutely necessary (if there's a need for it, I might write a blog post on how to do that as well). In case of sending the report in the body of the email, the workflow can be uploaded to Alteryx Server Gallery and scheduled there so that the reports are built as frequent as need in an automated manner. (If you want to keep the history of the reports, include the Render Tool as described above, but make sure the file is saved on a drive the server has access to.)</p>
<p>Here's the tool configuration:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-17.png" alt="" class="wp-image-14254"/></figure>
<div style="height:38px" aria-hidden="true" class="wp-block-spacer"></div>
<p>The whole workflow, in all its glory:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image-18.png" alt="" class="wp-image-14260"/></figure>
<p>And, finally, the reports. The PDF and email screenshot from my phone:</p>
<figure class="wp-block-gallery columns-2 is-cropped"><ul class="blocks-gallery-grid"><li class="blocks-gallery-item"><figure><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/pdf-report.png" alt="" data-id="14255" data-link="https://www.theinformationlab.co.uk/?attachment_id=14255" class="wp-image-14255"/></figure></li><li class="blocks-gallery-item"><figure><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/07/image1-1-602x1024.png" alt="" data-id="14258" data-link="https://www.theinformationlab.co.uk/?attachment_id=14258" class="wp-image-14258"/></figure></li></ul></figure>
<p>That's it! I know this is a long post and if you managed to get this far, I bow to you!</p>
