title: Another alternative to checkinstall
url: 421.html
id: 421
categories:
  - Unix
date: 2014-07-15 02:28:54
tags:
---
Checkinstall didn't work for me in CentOS 7 even after following this guide: [http://www.patrickmin.com/linux/tip.php?name=checkinstall\_fedora\_13](http://www.patrickmin.com/linux/tip.php?name=checkinstall_fedora_13) and using --fstrans = no. Solution: [https://github.com/jordansissel/fpm](https://github.com/jordansissel/fpm) Using nginx 1.7.3 as an example:
```sh
$ ./configure --sbin-path=/usr/local/sbin/nginx --with-http\_ssl\_module --prefix=/usr/local/nginx
$ make install DESTDIR = /tmp/nginxinstalldir && cd /tmp/nginxinstalldir
$ fpm -s dir -t rpm -n nginx -v 1.7.3 -d 'openssl-devel' -d 'openssl-libs' -d 'openssl' -d 'pcre' -d 'pcre-devel' -d 'zlib' -d 'zlib-devel' usr/
# rpm -qpR nginx-1.7.3-1.x86_64.rpm
openssl-devel
openssl-libs
openssl
pcre
pcre-devel
zlib
zlib-devel
rpmlib(PayloadFilesHavePrefix) <= 4.0-1
rpmlib(CompressedFileNames) <= 3.0.4-1
# rpm -ivh nginx-1.7.3-1.x86_64.rpm
```

Of course, this is by no means a substitute to properly packaging packages for upstream using rpm-build, but it is perfect for compiling from source quickly without having files strewn all over the place, especially when there is no make uninstall.