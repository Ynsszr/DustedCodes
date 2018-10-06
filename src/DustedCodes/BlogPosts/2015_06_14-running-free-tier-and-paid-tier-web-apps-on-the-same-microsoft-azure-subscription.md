﻿<!--
    Tags: microsoft-azure app-hosting-plan
    Type: HTML
-->

# Running free tier and paid tier web apps on the same Microsoft Azure subscription

<p>Last week I noticed a charge of ~ &pound;20 by MSFT AZURE on my bank statement and initially struggled to work out why I was charged this much.</p>
<p>I knew I'd have to pay something for this website, which is hosted on the shared tier in Microsoft Azure, but according to <a href="http://azure.microsoft.com/en-us/pricing/calculator/">Microsoft Azure's pricing calculator</a> it should have only come to &pound;5.91 per month:</p>
<a href="https://www.flickr.com/photos/130657798@N05/18821999662" title="Windows Azure Shared Pricing Tier by Dustin Moris Gorski, on Flickr"><img src="https://c2.staticflickr.com/6/5328/18821999662_b71b95637e_o.png" alt="Windows Azure Shared Pricing Tier"></a>

<p>After a little investigation I quickly found the issue, it was due to a few on and off test web apps which were running on the shared tier as well.</p>
<p>This was clearly a mistake, because I was confident that I created all my test apps on the free tier, but as it turned out, after I upgraded my production website to the shared tier all my other newly created apps were running on the shared tier as well.</p>

<p>I simply didn't pay close attention during the creation process:</p>
<a href="https://www.flickr.com/photos/130657798@N05/18829751471" title="Windows Azure Create new Web App by Dustin Moris Gorski, on Flickr"><img src="https://c4.staticflickr.com/4/3949/18829751471_b072e0ceaa_o.png" alt="Windows Azure Create new Web App"></a>

<p>Evidentally every new web app gets automatically assigned to my existing app service plan, which I upgraded to the shared tier.</p>
<p>Luckily I learned my lesson after the first bill. However my initial attempt to switch my test apps back to the free tier was not as simple as I thought it would be. I cannot scale one app individually without affecting all other apps on the same plan:</p>
<a href="https://www.flickr.com/photos/130657798@N05/18640926409" title="Windows Azure change pricing tier by Dustin Moris Gorski, on Flickr"><img src="https://c4.staticflickr.com/4/3865/18640926409_dbf2790205_o.png" alt="Windows Azure change pricing tier"></a>

<p>The solution is to create a new app service plan and assign it to the free tier.</p>

<p>You can do this either when creating a new web app, by picking "Create new App Service plan" from the drop down:</p>
<a href="https://www.flickr.com/photos/130657798@N05/18204493134" title="Windows Azure Create new App Service plan by Dustin Moris Gorski, on Flickr"><img src="https://c4.staticflickr.com/4/3868/18204493134_e04eba21dd_o.png" alt="Windows Azure Create new App Service plan"></a>

<p>Or when navigating to the new Portal, where you have the possibility to manage your app service plans:</p>
<a href="https://www.flickr.com/photos/130657798@N05/18821999642" title="Windows Azure switch to Azure Preview Portal by Dustin Moris Gorski, on Flickr"><img src="https://c2.staticflickr.com/6/5541/18821999642_d779125c72_o.png" class="half-width" alt="Windows Azure switch to Azure Preview Portal"></a>
<a href="https://www.flickr.com/photos/130657798@N05/18640926369" title="Windows Azure New Portal App Service Plans Menu by Dustin Moris Gorski, on Flickr"><img src="https://c2.staticflickr.com/6/5496/18640926369_1f679d0f4f_o.png" class="half-width" alt="Windows Azure New Portal App Service Plans Menu"></a>

<p>This wasn't difficult at all, but certainly a mistake which can easily happen to anyone who is new to Microsoft Azure.</p>
<p>Another very useful thing to know is that if you choose the same data centre location for all your app service plans, then you can easily move a web app from one plan to another. This could be very handy when having different test and/or production stages (Dev/Staging/Production).</p>