---
layout: post
title: Adding foundation
tags: TagA TagB
---

Everyman and his dog is likely to have written about adding Foundation (link)
styling to their jekyll blog, but I'll trace my steps anyway, especially as a
record of what I've done.

I'll need to find out what the code settings for jekyll are, or I could pass
through knitr/rmarkdown?

Make sure all the required apps/dependencies are there: bower, grunt(-cli),
foundation, of course you've already installed jekyll!

Need to start a new foundation project:

~~~
foundation new FoundationProject --libsass
~~~

Note that foundation requires a new directory for this, so we'll have to copy files over later.
