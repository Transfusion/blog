title: 'Gentoo on OpenVZ VPS, my experience'
url: 238.html
id: 238
categories:
  - Unix
date: 2014-03-12 02:20:38
tags:
---
The target VPS is running Debian 6 i686 from an OpenVZ template. First, I used this straightforward script; you can find the stage3 tarball in /releases/x86/current-stage3/ : [http://linux.arantius.com/how-to-install-gentoo-onto-any-openvz-vps](http://linux.arantius.com/how-to-install-gentoo-onto-any-openvz-vps) Next I set portage up: [https://matt.bionicmessage.net/blog/2011/02/05/Recipe%3A%20'Gentooize'%20an%20existing%20virtual%20server%20(VPS)](https://matt.bionicmessage.net/blog/2011/02/05/Recipe%3A%20'Gentooize'%20an%20existing%20virtual%20server%20(VPS))

```bash
localhost usr # wget http://distfiles.gentoo.org/snapshots/portage-latest.tar.bz2
localhost usr # eselect profile set 1
localhost usr # emerge --sync
```

Here is how I managed to get networking working with /etc/conf.d/net ; apparently venet0:0 isn't necessary anymore (we can simply add our IPv4 address to venet0 but very strangely, our external IPv4 address doesn't show up in ifconfig but works.) Without further do...

```bash
 # cat /etc/conf.d/net
config_venet0="127.0.0.2/32 198.***.***.***/32 2a01:****:***:**::****:****/128 2a01:****:***:**::****:****/128 2a01:****:***:**::****:****/128 2a01:****:***:**::****:****/128"
routes_venet0=("default")
route -A inet6 add ::/0 dev venet0
postup() {
        route -A inet6 add ::/0 dev venet0
}
predown() {
        route -A inet6 del ::/0 dev venet0
}
```

`routes_venet0=("default")` only sets the IPv4 default route, and I haven't found a way to set the IPv6 default route without knowledge of the gateway IP address, hence the postup() and predown() scripts. Nevertheless, they are "good enough."

```bash
# rc-update add net.venet0 default
```

to bring venet0 up at default runlevel. At this point you should be able to run

```bash
localhost usr # /etc/init.d/net.venet0 restart
SIOCADDRT: File exists
 * Bringing down interface venet0
 *   Running predown ...
SIOCADDRT: No such device
 * Bringing up interface venet0
 *   127.0.0.2/32 ...                                                                                                    [ ok ]
 *   198.***.***.***/32 ...                                                                                              [ ok ]
 *   2a01:****:****:**::****:****/128 ...                                                                                 [ ok ]
 *   2a01:****:****:**::****:****/128 ...                                                                                 [ ok ]
 *   2a01:****:****:**::****:****/128 ...                                                                                 [ ok ]
 *   2a01:****:****:**::****:****/128 ...                                                                                 [ ok ]
 *   You are using a bash array for routes_venet0.
 *   This feature will be removed in the future.
 *   Please see net.example for the correct format for routes_venet0.
 *   Adding routes
 *     default ...                                                                                                       [ ok ]
 *   Running postup ...
```

while logged in without your SSH connection dropping on either IPv4 or IPv6. I am still in the process of setting up ntp, a mailer daemon, syslog-ng, etc. so I may post an update if I find anything extraordinary.