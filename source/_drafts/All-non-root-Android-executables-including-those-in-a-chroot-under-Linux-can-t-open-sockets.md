---
title: >-
  All non-root Android executables, including those in a chroot under Linux,
  can't open sockets
url: 198.html
id: 198
categories:
  - Uncategorized
tags:
---

[https://github.com/guardianproject/lildebi/issues/6](https://github.com/guardianproject/lildebi/issues/6) I stumbled upon this error while trying to use stunnel4 in client mode in an Ubuntu chroot inside Android 4.3 (yeah, so specific :P)

\# stunnel4
2014.02.27 19:34:28 LOG5\[6976:1074732944\]: stunnel 4.53 on arm-unknown-linux-gnueabihf platform
2014.02.27 19:34:28 LOG5\[6976:1074732944\]: Compiled with OpenSSL 1.0.1c 10 May 2012
2014.02.27 19:34:28 LOG5\[6976:1074732944\]: Running  with OpenSSL 1.0.1e 11 Feb 2013
2014.02.27 19:34:28 LOG5\[6976:1074732944\]: Update OpenSSL shared libraries or rebuild stunnel
2014.02.27 19:34:28 LOG5\[6976:1074732944\]: Threading:PTHREAD SSL:+ENGINE+OCSP Auth:LIBWRAP Sockets:POLL+IPv6
2014.02.27 19:34:28 LOG5\[6976:1074732944\]: Reading configuration from file /etc/stunnel/stunnel.conf
2014.02.27 19:34:28 LOG5\[6976:1074732944\]: Configuration successful
2014.02.27 19:34:38 LOG5\[6976:1077785712\]: Service \[proxy\] accepted connection from 127.0.0.1:55017
2014.02.27 19:34:38 LOG3\[6976:1077785712\]: remote socket: Permission denied (13)
2014.02.27 19:34:38 LOG5\[6976:1077785712\]: Connection reset: 0 byte(s) sent to SSL, 0 byte(s) sent to socket

This was with

chroot = /var/lib/stunnel4/
; Chroot jail can be escaped if setuid option is not used
setuid = stunnel4
setgid = stunnel4
foreground = yes
; PID is created inside the chroot jail
pid = /stunnel4.pid

in the stunnel.conf. So, taking a look at /etc/group, http://pastebin.com/g80W9qb7 So, time to add user stunnel4 to group android_inet then.