+++
title = "HTTPS and other hosting details"
date = "2021-10-02T11:16:52-07:00"
author = "Jay Faulkner"
authorTwitter = "jayofdoom" 
#cover = "What I plan to talk about here, and how it works"
tags = ["blog", "google cloud", "cloudflare" ]
keywords = ["blog", "cloud", "google"]
parent = "posts"
description = "How I'm hosting this blog"
showFullContent = false
+++
Last week, I got my blog up quickly with a simple upload to Google Cloud storage, with public access. However, this has
a huge limitation -- no HTTPS. Google's proscribed message to enable it? Pay them for TLS terminating load balancers.
I have no desire to setup a money-sucking machine in case one of these blogposts go viral one day (unlikely), so that was
out.

Then I read a recent post about a new product released by [Cloudflare](https://cloudflare.com). I looked on their site and
discovered they have a free plan. It's possible they've always had a free plan, and I just wasn't aware of it, but it
looks like I get free DNS hosting and CDN proxying for up to 3 domains, including SSL termination and certificate
management. This seemed pretty great, so I went ahead and signed up and migrated over. I'm still using Google Cloud storage
as the place where the site is actually hosted, but it's all Cloudflare fronted.

I'm glad to have HTTPS working for this, so I can now finally feel like it's completed. This may not be the final form of
hosting for it, but I've done what I needed to.

One big downside of this approach -- Cloudflare requires that they host DNS as well. So my letsencrypt setup for other
(mostly on LAN) TLS services for jvf.cc will have to be updated to use Cloudflare's API instead of Google's. I'll save
that for another day.

Thanks for reading,

Jay
