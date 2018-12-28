title: Compiling UnrealIRCD on an iPod Touch 2G
url: 408.html
id: 408
categories:
  - Unix
date: 2014-06-18 20:57:46
tags:
---
Note: This is an old post, from an old blog far, far away 

![](/images/f0zupg.jpg)

![](/images/qp5pj5.jpg)

Prerequisites
=============

*   openssl (I have version 0.9.8k-9 from Cydia)
*   iphone-gcc (follow this guide: [http://code.google.com/p/iphone-gcc-full/](http://code.google.com/p/iphone-gcc-full/ "http://code.google.com/p/iphone-gcc-full/"))
*   libgcc (follow this guide: [http://code.google.com/p/iphone-gcc-full/](http://code.google.com/p/iphone-gcc-full/ "http://code.google.com/p/iphone-gcc-full/"))
*   libz.dylib / zlib (If you can’t be bothered to get this from the iPhone SDK [http://cydia.radare.org/debs/](http://cydia.radare.org/debs/ "http://cydia.radare.org/debs/") works too) wget (who doesn’t need wget)

`wget "http://www.unrealircd.com/downloads/Unreal3.2.10.1.tar.gz" | tar -xvzf -`

Configuring
===========

For some reason I had to run the ./configure as root after cd’ing into the directory where I extracted the files as the mobile user; perhaps due to an inability to run unsigned applications?

checking whether we are cross compiling... configure: error: in `/var/mobile/Unreal3.2.10.1':
configure: error: cannot run C compiled programs.
If you meant to cross compile, use `--host'.

After running as root, everything went rather smoothly. Edit dpath and spath as you wish.

```
./configure --with-showlistmodes --enable-ssl --enable-ziplinks --enable-inet6 --with-listen=5 --with-dpath=/var/mobile/UnrealIRCD-build --with-spath=/var/mobile/UnrealIRCD-build/src/ircd --with-nick-history=2000 --with-sendq=3000000 --with-bufferpool=18 --with-permissions=0600 --with-fd-setsize=1024 --enable-dynamic-linking
```


I forgot to use ‘time’ but estimate it perhaps took around 20 minutes. After make && make install:


```bash
openssl genrsa -out server.key 2048
openssl req -new -x509 -key server.key -out server.cert.pem -days 1826
cp server.key server.key.pem
```

to generate the certificate and key needed for the SSL connection. After running ./unreal start ; it required some source modules in the build folder and the config file for the IRCD.

```bash
cp -r /var/mobile/Unreal3.2.10.1/src/ ../UnrealIRCD-build/
cp /var/mobile/UnrealIRCD-build/src/example.conf /var/mobile/UnrealIRCD-build/unrealircd.conf
```

Edit the config file as you wish!…