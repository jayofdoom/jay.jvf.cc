+++
title = "Why I'm blogging and using hugo to do it"
date = "2021-09-26T02:33:52-07:00"
author = "Jay Faulkner"
authorTwitter = "jayofdoom" 
#cover = "What I plan to talk about here, and how it works"
tags = ["blog", "hugo", "golang"]
keywords = ["blog", "hugo", "golang", "cloud", "google"]
description = "Why I'm blogging and using hugo to do it"
showFullContent = false
+++
It's been a long time since I've posted regularly to the internet -- short or long form. As I get older, I find I don't
enjoy publishing in Facebook or Twitter-sized snippets. So I decided to try and start blogging on a longer form again.

My primary topic will be the various personal projects I've started working on in the last few years. None of this is
to be seen as a review or endorsement of the products or software I've used. Some of it was picked nearly at random.
Such as the static site generator I'm using for this, [hugo](https://gohugo.io "gohugo.io"). I found it by simply
Googling for a static site generator in go, and picking the first response on Google. It's been so easy I've never
thought of trying anything else.

First, why a static site generator? One of my goals was to make sure my blog would be near-zero upkeep outside
of writing new posts. My previous experience with the main [oldos.org](http://oldos.org "OldOs.org") website taught me
that dynamic blogging/wiki software means either ignoring blatant software vulnerabilities or signing up for a nightmare
of maintenance. Part of why I stopped updating that site is because the software running it, PMWiki, was too heavily
modified by my custom theme to easily apply security updates. It runs today as a static archive on Google Sites -- part
of why it's no longer maintained. I'm using these lessons to guide how I set up this blog -- perhaps in the future I
could even adapt oldos.org's theme to use hugo and migrate the content.

Hugo was pleasantly simple to get going -- there was an ebuild available for it with Gentoo which I installed, then I 
followed the [hugo quick start](https://gohugo.io/getting-started/quick-start/ "Hugo Quick Start"), found a
[theme](https://themes.gohugo.io/ "Hugo Themes"), and I was up and running in a few minutes. I found and installed the
IDEA plugin for hugo, which manages the hugo server for me, and now I'm watching it open in my browser updating live
each time it saves.

I can also at a later point add more static pages -- I would expect this to become the permanent home of my resume, for
instance. For now, I'm happy it allows me to publish this site without having to have a menu or alternate pages at all.
That means I was able to go from zero to having this post drafted in less than ninety minutes. This kind of low-friction
blogging is the only way I'll be able to keep this updated regularly.

I'm going to save this draft, revise it, then get hosting setup. My next post will detail how I'm hosting it! Other
topics you can expect to come up  as I get through them may include "Why I run Gentoo", "My home router setup", and a
whole series of posts on my  experiences with Home Assistant, and the journey I'm undergoing to smartify my home.

Thanks for reading,

Jay