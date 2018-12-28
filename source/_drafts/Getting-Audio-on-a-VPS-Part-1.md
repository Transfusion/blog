---
title: Getting Audio on a VPS - Part 1
url: 206.html
id: 206
categories:
  - Uncategorized
tags:
---

I have been experimenting with audio support using a dummy soundcard and pulseaudio. Initial conclusion - pulseaudio's default stream over TCP is extremely laggy over the internet; and packets sometimes even arrive out of order. In Part 2 we will look at using Ices2/darkice to see if we can achieve streaming in the similar way that Icecast does. This is just proof of concept; if anyone has any suggestions please comment.