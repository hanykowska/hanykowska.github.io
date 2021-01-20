---
layout: post
cover: /assets/images/posts-images/spotify-cover.jpg
navigation: True
title: "Connect to Spotify API with Alteryx"
date: 2019-08-07 00:00:00
tags: [alteryx]
class: post-template
subclass: "post"
author: hanykowska
excerpt_separator: <!--more-->
external_url: https://www.theinformationlab.co.uk/2019/08/07/connect-to-spotify-api-with-alteryx/
external_site: til
---

The authentication process for Spotify API is a bit tricky. I thought I’d make your life easier so that you could start using this API yourself!

[First published on The Information Lab Blog.]({{page.external_url}}){:target="\_blank"}
<!--more-->

<p>With the recent <a href="https://public.tableau.com/en-us/s/blog/2019/07/check-out-2019-iron-viz-entries-music-data">Iron Viz feeder focused</a> around the topic of music, many people have started looking into <a href="https://developer.spotify.com/documentation/web-api/">Spotify API</a>, including myself. I actually did use data from Spotify API for <a href="https://public.tableau.com/profile/hanna.nykowska#!/vizhome/whatssospecialaboutmusic/Dashboard">my Iron Viz entry</a>. The authentication process is a bit tricky and so I thought I'd make your life easier so that you could start using this API yourself!</p>
<blockquote class="wp-block-quote is-style-default"><p><em>Disclaimer</em></p><p>This solution uses Client Credentials Flow and allows you to connect to Spotify API data but <strong>not</strong> the user information. This means, you <strong>can't </strong>use this authorization method to connect to Users Profile, Personalization, Player and other end points that are based on user data. You <strong>can</strong> still search/access artist, album, track, etc. information.</p></blockquote>
<h3>Get Client ID and Client Secret</h3>
<ol><li>Create a Spotify user account (it can be Free or Premium), I used my personal one.</li><li>Go to Spotify Developer <a href="https://developer.spotify.com/dashboard">Dashboard</a>, log in and accept <a href="https://developer.spotify.com/terms">Developer Terms of Service</a>.</li><li>Create an app  (in 'What are you building?' section I chose 'I don't know'). </li><li>Once you open your app, you should be able to see Client ID and Secret:</li></ol>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/08/image-37.png" alt="" class="wp-image-14869"/></figure>
<p>More on getting started with Spotify API you can find <a href="https://developer.spotify.com/documentation/web-api/quick-start/">here</a>.</p>
<h3>Get token (ready-to-use macro)</h3>
<p>Now that you have client credentials, you would need to connect to the Spotify API and get a token. To make your life easier, I built a macro, that takes the client credentials and return the token together with the time until it's active. For more on how does the macro actually work, go <a href="https://www.theinformationlab.co.uk/?p=14837#behindthescenes">here</a>.</p>
<ul><li>Download the macro <a href="https://gallery.alteryx.com/#!app/Get%2BToken%2Bfor%2BSpotify%2BAPI/5d4af9948a933712d02145a2">from the Gallery</a></li><li>Import it into the workflow</li></ul>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/08/image-39.png" alt="" class="wp-image-14872"/></figure>
<ul><li>Copy and paste your Client ID and Client Secret. Client Secret should be masked while ID visible</li></ul>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/08/image-38.png" alt="" class="wp-image-14871"/></figure>
<ul><li>Run the macro, it will return an Authorization field that you can use as a header in a download tool and how long the token will be active for</li></ul>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/08/image-40.png" alt="" class="wp-image-14873"/></figure>
<p>I recommend using cache and run so that you don't have ping the API when you're developing your workflow. </p>
<h3>Use Spotify API</h3>
<p>Now that you have your token, you can finally use Spotify API! <a href="https://developer.spotify.com/documentation/web-api/reference/">Web API Reference</a> lists different endpoints you can connect to with examples. Let's demonstrate a simple set up. </p>
<p>I chose Browse endpoint as it doesn't require any additional parameters. The URL to get a list of categories in Browse is</p>
<pre class="wp-block-code"><code>https:&#47;&#47;api.spotify.com/v1/browse/categories</code></pre>
<p>use text input to start your workflow and name the field with the URL just <em>URL</em></p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/08/image-41.png" alt="" class="wp-image-14875"/></figure>
<p>Then append the results of the Get Token macro and drag in the download tool. In its settings, make sure to choose the right field in URL selection and uncheck the Encode URL text box:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/08/image-42.png" alt="" class="wp-image-14876"/></figure>
<p>In Headers, just tick Authorization and it this situation that should do!</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/08/image-43.png" alt="" class="wp-image-14877"/></figure>
<p>If want to pass any parameters (see below), you'll need to use the Payload tab in the download settings:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/08/image-44.png" alt="" class="wp-image-14878"/></figure>
<p>The data will be returned as JSON and will require some extra parsing (JSON Parse will save you a lot of work!). Good luck and have fun playing around with Spotify API!</p>
<div style="height:20px" aria-hidden="true" class="wp-block-spacer"></div>
<h3 id="behindthescenes">Behind the scenes: how does the Get Token macro work?</h3>
<p>This section might be useful if you want to recreate what I did or simply understand what is required.</p>
<p>First I concatenate  clientID + ':' + clientSecret. Then I encode that new string with a base64 encoder. I create a new Authorization field with 'Basic &lt;encoded credentials&gt;' inside. </p>
<p>I can now connect to <a href="https://accounts.spotify.com/api/token">https://accounts.spotify.com/api/token</a>. The Encode URL text tick box needs to be unchecked. I add Authorization header (just as described above). In Payload, I change the HTTP action to POST and add a query parameter <em>grant_type</em> with value <em>client_credentials</em>:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/08/image-46.png" alt="" class="wp-image-14880"/></figure>
<p>Then I check if the response is 200 code, which means it's OK. If it's not, it will send an error to let the user know. I'm also preparing a new Authorization field for the use with API endpoints as well as calculating when will the token expire based on the computer's time.</p>
<p>That's the workflow:</p>
<figure class="wp-block-image"><img src="https://www.theinformationlab.co.uk/wp-content/uploads/2019/08/image-47-1024x483.png" alt="" class="wp-image-14883"/></figure>
