+++
title = "My approach to problem solving"
date = "2021-11-18T16:36:52-07:00"
author = "Jay Faulkner"
authorTwitter = "jayofdoom" 
tags = []
parent = "posts"
keywords = []
description = "A few basic principles I use to solve problems"
showFullContent = false
+++
The last few days, I've had the opportunity to help a few different people solve problems. Regardless of the problem I
am up against, I use a few basic principles to solve it. I thought I'd share them here, in case they are useful to you.

Reduce your reproduction
------------------------
Reproduce your problem, then reduce your reproduction. What do I mean by reduce? I mean, try to remove as much of the
extra stuff around your problem as possible -- this may be as simple as taking the time to run only the broken test
case instead of all of them (or writing a new test case to exercise your bug).

Congratulations; you've reduced the surface area you have to troubleshoot significantly. Get it out of a container? 
Perfect, now you don't have to consider that layer at all anymore. Write a new test case that reproduces it simply and
quickly? Even better, you can now know that you've fixed the problem when that test passes (and it won't be as easy to
break next time).

This isn't always possible, but it's worth trying.

Do what Big Bird taught you
---------------------------
When I was a kid, I'd watch Sesame Street, and they would sing a [song](https://www.youtube.com/watch?v=rsRjQDrDnY8):
"One of these things does not belong". This approach, looking at one or more examples of how others have solved this
problem can be a useful approach when troubleshooting.

Earlier today, during my [Office Hours](https://www.youtube.com/watch?v=tWAkQIuoX7M), I was helping someone troubleshoot
an issue in their DB migration -- a unit test was failing, indicating that the output of our migrations might not be the
same as what would be in a fresh DB. We were able to dig and find another instance of a field that was the same type,
and we compared the old, working code to the new code, and found the [trick to get the right type](https://review.opendev.org/c/openstack/ironic/+/862569/9#message-d60e442f3dd78866b027be06602d80321c02a3f5)
into the migration.

The most common implementation of this you see is people using Stack Overflow or similar websites to find examples of
how to solve common problems. Another good place to look is the documentation, if it exists, for examples related to
what you're solving.

Know why it broke in the first place
------------------------------------
Using a shortcut to solve the problem is great; but it's incredibly important not to stop there! You can't be certain
that your issue is actually fixed unless you can understand what happens. You have to turn into a detective and figure
out what happened and why it's better now.

In the case above; we were using a SQLAlchemy type which on all databases except MySQL, resolved to the same type. This
is why our test was complaining -- SQLAlchemy would create with a slightly different type than MySQL. So the fix was to
put the SQLAlchemy type in the migration; which fixed it!

Conclusion
----------
When you combine these together; you get a useful trio that feeds into itself: you make it easy to brute-force attempt
fixes that don't require full understanding and then, once you have a fix, you can work backwards to understand why that
fixed your issue.

Just really, don't ever skip that last step. It's the most important one. It's dangerous to ship code you don't
understand, and it's silly to pass up such a golden opportunity to learn something new.
