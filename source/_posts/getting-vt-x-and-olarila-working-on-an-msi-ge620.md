---
title: Getting VT-x and Olarila Working on an MSI GE620
url: 397.html
id: 397
categories:
  - Uncategorized
date: 2014-06-18 17:05:30
tags:
---

Note: This is an old post, from an old blog far, far away This is my first BIOS flash in a horribly long time, the last time I did I did on a really low-end GeForce 7025 chipset Foxconn M61PMV, and I flunked that one the second time by using the AMI BIOS flash through Windows. Sure as sandy didn’t want to mess this beauty of a lappy up. The i5-2410M supports VT-x, but VirtualBox coughed up this error: [![](/wp-content/uploads/2014/06/2v7vrza-300x225.png)](/wp-content/uploads/2014/06/2v7vrza.png) [![](/wp-content/uploads/2014/06/adf6v6-300x198.png)](/wp-content/uploads/2014/06/adf6v6.png) [](http://forum-en.msi.com/index.php?topic=147711.0 "http://forum-en.msi.com/index.php?topic=147711.0") [](http://forum-en.msi.com/index.php?topic=150203.0 "http://forum-en.msi.com/index.php?topic=150203.0") These turned up; so time for me to flash the latest BIOS from here! shiver hefty brick shiver because mine is dated at 2011. Downloading the flashing tool: [![](/wp-content/uploads/2014/06/3499mpv-300x276.png)](/wp-content/uploads/2014/06/3499mpv.png) Fair enough, I am confident. [![](/wp-content/uploads/2014/06/13zu5hc-300x115.png)](/wp-content/uploads/2014/06/13zu5hc.png) I had to redo this process because it couldn’t find a boot image; I selected Fix USB drive which rewrites the boot sector. I went into the BIOS, booted from the drive and hesitantly pressed 2, which is the big red button for OVERWRITE BIOS. It finished after an eternity, verifying the flash too. I did as I was told (or rather, as I read), and I took the battery out, unplugged it, and waited for 5 minutes(actually, 2, I couldn’t resist), and plugged it back in and reluctantly pressed the power button, hoping for the worst because the flash ended so abruptly. the Fans whirred, the HDD indicator came on BUT THEN IT ABRUPTLY SHUT DOWN AGAIN. I had a stroke there. I cursed at everything within 15 minutes heartily, then hit the power button, making sure it wasn’t dead. IT CAME BACK FROM THE DEAD. I kissed it smack in the middle of the beautiful FHD LED screen, and I loved Windows again. That beautiful Windows Aero theme, I will not complain, it’s good enough that it boots. [![](/wp-content/uploads/2014/06/90bl8n-300x240.jpg)](/wp-content/uploads/2014/06/90bl8n.jpg) [![](/wp-content/uploads/2014/06/fkchoo-300x142.jpg)](/wp-content/uploads/2014/06/fkchoo.jpg) not-so-cheapo Mackerel Pro I made! Formatting my Macdonald Drive and installing, which took approximately 42 minutes on a WDC-WD5000BEKT-22KA9T0 500GB 7200RPM: [![](/wp-content/uploads/2014/06/33c14b9-300x248.jpg)](/wp-content/uploads/2014/06/33c14b9.jpg) [![](/wp-content/uploads/2014/06/FMOjZhJ-300x248.png)](/wp-content/uploads/2014/06/FMOjZhJ.png) [![](/wp-content/uploads/2014/06/fEt3u1k-300x248.jpg)](/wp-content/uploads/2014/06/fEt3u1k.jpg) After I finished, I restarted with the DVD, this time pressing F8 to toggle advanced boot options and using GraphicsEnabler=yes. Old MacDonald would be pleased. Time to install Chameleon and MultiBeast.