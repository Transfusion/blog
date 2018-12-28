---
title: Good First Bug
url: 365.html
id: 365
categories:
  - Programming
date: 2014-05-25 23:40:15
tags:
---

[https://wiki.mozilla.org/Good\_first\_bug](https://wiki.mozilla.org/Good_first_bug) So!... I realize the change isn't as trivial in FF 29+ since the switch to the nasty curved tabs. Regardless, here's my solution: [http://forums.mozillazine.org/viewtopic.php?f=38&t=2799203](http://forums.mozillazine.org/viewtopic.php?f=38&t=2799203) and add the code to remove sidebars and this:

.tabbrowser-tab {
  -moz-binding: url("chrome://browser/content/tabbrowser.xml#tabbrowser-tab");
}

.tabbrowser-tab\[selected="true"\] {
  font-weight: bold !important;
  color: rgba(255,255,255,1) !important;
  background-image: linear-gradient(rgba(102,51,102,.85), rgba(102,51,102,.85) 50%),
                    linear-gradient(-moz-dialog, -moz-dialog) !important;
}

tab:not(\[selected="true"\]) {
  background-color: #2F0 !important;
  color: gray !important;
}

into browser.css [![](/wp-content/uploads/2014/05/green_tabs-150x91.jpg)](/wp-content/uploads/2014/05/green_tabs.jpg)