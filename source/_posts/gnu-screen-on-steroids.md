---
title: GNU Screen on Steroids
url: 415.html
id: 415
categories:
  - Unix
date: 2014-06-18 21:03:52
tags:
---

Note: This is an old post, from an old blog far, far away [![](/wp-content/uploads/2014/06/eplyrn-300x103.jpg)](/wp-content/uploads/2014/06/eplyrn.jpg) Append this to your ~/.bashrc:

case "$TERM" in
    screen*) PROMPT_COMMAND='echo -ne "�33k�33�134"'
esac

and this to your .screenrc:

hardstatus alwayslastline '%{= G}\[ %{G}%H %{g}\]\[%= %{= w}%?%-Lw%?%{= R}%n*%f %t%?%{= R}(%u)%?%{= w}%+Lw%?%= %{= g}\]\[ %{y}Load: %l %{g}\]\[%{B}%Y-%m-%d %{W}%c:%s %{g}\]'
shelltitle '$ |bash'

Courtesy of [http://superuser.com/questions/244299/gnu-screen-how-to-update-dynamically-the-title-of-a-window](http://superuser.com/questions/244299/gnu-screen-how-to-update-dynamically-the-title-of-a-window "http://superuser.com/questions/244299/gnu-screen-how-to-update-dynamically-the-title-of-a-window") and [http://beerpla.net/2009/10/06/supercharge-your-gnu-screen-with-a-power-taskbar-and-never-feel-lost-again/](http://beerpla.net/2009/10/06/supercharge-your-gnu-screen-with-a-power-taskbar-and-never-feel-lost-again/ "http://beerpla.net/2009/10/06/supercharge-your-gnu-screen-with-a-power-taskbar-and-never-feel-lost-again/")

> If you want to keep your splits/panes persistent even when you detach: The short is answer is that you can’t. The longer answer is that you can fake it. (Note: the next screen release, probably numbered 4.1.0, will be able to remember display layouts.) Splits are a property of your display. The process managing your screen session doesn’t really know about them; only the single process that’s displaying the session does. Thus, the screen session can’t remember the splits because it doesn’t know about them, and once you detach, the process that did know about them has exited. The hack is to use nested screen sessions. Start one session and give it some escape sequence that you won’t use much (or just disable its escape character completely). Bind your usual detach key sequence to this screen session. Now, start or attach to your main screen session. All of your work will be done in the inner session, and you can split your display. When you detach, however, it will be the outer session that detaches, so your splits in the inner session will be preserved.

[http://aperiodic.net/screen/faq#when\_i\_split\_the\_display\_and\_then\_detach\_screen\_forgets\_the_split](http://aperiodic.net/screen/faq#when_i_split_the_display_and_then_detach_screen_forgets_the_split "http://aperiodic.net/screen/faq#when_i_split_the_display_and_then_detach_screen_forgets_the_split")