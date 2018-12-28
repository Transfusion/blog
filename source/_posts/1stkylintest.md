---
title: 今天我，寒夜里看雪飘过， 一大早装个国产麒麟摸一摸
url: 30.html
id: 30
categories:
  - Uncategorized
date: 2013-10-01 22:14:00
tags:
---

下载地址： ftp://ftp.cs2c.com.cn/download/NeoKylin-Desktop-personal.iso 彪悍的麒麟，直接上图！ \[caption id="attachment_37" align="alignnone" width="300"\][![Install Screen](/wp-content/uploads/2013/10/20130928062042-300x242.png)](/wp-content/uploads/2013/10/20130928062042.png) Install Screen\[/caption\] \[caption id="attachment_38" align="alignnone" width="300"\][![中彪了还这么灵活。。](/wp-content/uploads/2013/10/20130928062132-300x241.png)](/wp-content/uploads/2013/10/20130928062132.png) 中彪了还这么灵活。。\[/caption\] [![20131001043235](/wp-content/uploads/2013/10/20131001043235-300x241.png)](/wp-content/uploads/2013/10/20131001043235.png) 默认桌面系统是 gnome-session 3.4.1。 thunderbird, evince, gimp, ff13.0.1, gedit, filezilla, brasero, rhythmbox, transmission 之类的都自带。 \[caption id="attachment_41" align="alignnone" width="300"\][![呵呵。这个跟office 2003 挺相似的。为用户着想。](/wp-content/uploads/2013/10/20131001042752-300x242.png)](/wp-content/uploads/2013/10/20131001042752.png) 呵呵。这个跟office 2003 挺相似的。为用户着想。\[/caption\] \[caption id="attachment_42" align="alignnone" width="300"\][![基于RHEL 6, yum, 挺新的linux内核。。3.0后。。。看来连CentOS都比他注重稳定。。。?](/wp-content/uploads/2013/10/20130928170554-300x242.png)](/wp-content/uploads/2013/10/20130928170554.png) 基于RHEL 6, yum, 挺新的linux内核。。3.0后。。。看来连CentOS都比他注重稳定。。。?\[/caption\] 默认软件仓库无影无踪。 没办法。 只好用CentOS 库（rhel 完全兼容 CentOS 库中的binary。于是我装了centos-release, 把他变为CentOS 6.4. [![20131001043830](/wp-content/uploads/2013/10/20131001043830-300x242.png)](/wp-content/uploads/2013/10/20131001043830.png) yum update 吐出来这个怪怪的错误。 我就把 http://mirrorlist.centos.org/?release=6.4&arch=i386&repo=os 为地点优化的 repo list 复制到相应的位置。 After that, everything seems hunky dory. Repoforge 和 EPEL

rpm -ivh http://pkgs.repoforge.org/rpmforge-release/rpmforge-release-0.5.3-1.el6.rf.i686.rpm
rpm -ivh http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm

就行了。 (想装 xfce, GNOME 太笨重了！ 呜呜) [![20131001044512](/wp-content/uploads/2013/10/20131001044512-300x241.png)](/wp-content/uploads/2013/10/20131001044512.png) [![20131001122840](/wp-content/uploads/2013/10/20131001122840-300x242.png)](/wp-content/uploads/2013/10/20131001122840.png) 如果要彻底改变去CentOS 6.4 会搞到你头昏脑涨， 毕竟系统核心数据包都是 nk 不存在了的库中装的。所谓的Dependency Hell 会一直追着你。只好一切都从源码编译。 如果你觉得国产真的不错，好马不吃回头草，非得要继续用就长途跋涉吧。难度会跟 linux from scratch 差不多，嘿嘿。 天才的我把libevent 和 rpm -e 卸了，毁了yum 和 gnome. 废了半天才编译回了。弄个大杂烩。徒劳无功。