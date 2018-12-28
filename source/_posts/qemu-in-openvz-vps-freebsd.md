---
title: QEMU in OpenVZ VPS - FreeBSD
url: 180.html
id: 180
categories:
  - Unix
date: 2014-02-19 22:40:21
tags:
---

Before you start: it is probably a better idea to run headless operating systems because of the immense overhead compounded by software emulation since OVZ doesn't support hardware virtualization (qemu-kvm). Watch the CPU usage, and make sure you have adequate RAM. Successfully tested with FreeBSD-10.0-RELEASE i386 running inside Ubuntu 13.10 i686.

\# apt-get install qemu-system

$ qemu-img create -f qcow2 freebsd.qcow2 5G

Formatted capacity will be 4.6GB with FreeBSD's default UFS2 filesystem. a minimal install without the ports collection takes approximately 550MB.

$ qemu -localtime -cdrom FreeBSD-10.0-RELEASE-i386-dvd1.iso -m 256 -boot d freebsd.qcow2 -net nic,vlan=0,model=rtl8139 -net user -vnc :3

256MB of memory is more than enough to get by with for the install. -k may be necessary if you are planning to select an alternative keyboard layout during the install. Connect to :5903 via VNC to control it. No authentication is set up, so it might pose a security risk. During the install, install sshd and ntpd too. After you're done installing,

$ qemu -hda freebsd.qcow2 -boot c -m 256 -localtime -net nic,vlan=0,model=rtl8139 -net user -vnc :3

, edit /etc/ssh/sshd_config and set PermitRootLogin to Yes, and do a service sshd restart . VNC is quite clunky to use on a daily basis, not to mention that all data is transferred unencrypted. It would be trivial to use iptables to deny external access and access it via an ssh tunnel only, though. For general use:

$ qemu -hda freebsd.qcow2 -boot c -m 256 -localtime -net nic,vlan=0,model=rtl8139 -net user,mynet0,hostfwd=tcp::9527-:22

This forwards tcp port 22 on the guest to port 9527 on all interfaces of the host. Unfortunately, I haven't found a way to forward ports while the guest is running. Here is an idea of how resource-intensive the guest is: \[caption id="attachment_182" align="alignnone" width="150"\][![](/wp-content/uploads/2014/02/htopidlebsd-150x150.jpg)](/wp-content/uploads/2014/02/htopidlebsd.jpg) Screenshot of htop on a completely idle FreeBSD guest in QEMU\[/caption\] This translates to \[caption id="attachment_183" align="alignnone" width="150"\][![](/wp-content/uploads/2014/02/qemuhosthtop-150x150.jpg)](/wp-content/uploads/2014/02/qemuhosthtop.jpg) htop screenshot of CPU usage on the host with an "idle" freeBSD guest\[/caption\] Something doesn't seem right. htop on FreeBSD that I just installed from pkg has abnormal CPU usage. I suspect this is due to the Linux compatibility layer. Let's take another shot of htop on the host with nothing running on the guest besides system daemons like syslogd and cron: [![](/wp-content/uploads/2014/02/idleguesthtophost-150x150.jpg)](/wp-content/uploads/2014/02/idleguesthtophost.jpg) At this point, strangely,

\# uptime
 5:33PM  up  3:49, 2 users, load averages: 0.48, 0.37, 0.29

The guest CPU seems to be trying to squeeze blood from a turnip. I have no clue why the apparent load is so high, yet top inside the guest bizarrely shows 99.6% idle. Perhaps I will experiment with the qemu -smp option since my VPS has 3 cores assigned to it to see if the guest will be able to use additional cores effectively...