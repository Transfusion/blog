---
title: Fixing mIRC's broken ping implementation
url: 88.html
id: 88
categories:
  - Uncategorized
date: 2013-11-19 17:08:01
tags:
---

[https://github.com/tannn/TriviaTime/pull/147](https://github.com/tannn/TriviaTime/pull/147 "Shortening ctcp ping payload for mirc, using first 5 of sha1 hash by rootcoma · Pull Request #147 · tannn/TriviaTime · GitHub") Apparently mIRC doesn't respond to ping messages over a certain length. This is the first part of the problem. According to [http://www.irchelp.org/irchelp/rfc/ctcpspec.html](http://www.irchelp.org/irchelp/rfc/ctcpspec.html)

> The querying client can then subtract the recieved timestamp from the current time to obtain the delay between clients over the IRC network.

The client sending the ping will do Current Time - Timestamp that it sent out (which is echoed by the target of the ping) , so it can send the ping payload in any format it finds convenient. All we have to do is:

> The replying client sends back an identical message inside a notice: 01PING timestamp01

So add this to the top of your Remote script....

ctcp 1:ping:/raw NOTICE $nick : $+ $chr(1) $+ $1- $+ $chr(1)

Perfect. A better ping script that will display ping replies in miliseconds: [http://www.mircscripts.org/showdoc.php?type=code&id=1102](http://www.mircscripts.org/showdoc.php?type=code&id=1102 "Code Snippet - Millisecond ping snippet")