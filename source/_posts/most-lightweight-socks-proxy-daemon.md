title: most lightweight socks proxy daemon
url: 128.html
id: 128
categories:
  - Uncategorized
date: 2014-01-16 23:24:39
tags:
---
[http://lowendtalk.com/discussion/4466/lightweight-socks5-proxy](http://lowendtalk.com/discussion/4466/lightweight-socks5-proxy)

```bash
$ file /usr/local/bin/ssocksd
/usr/local/bin/ssocksd: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.24, stripped
$ du -h /usr/local/bin/ssocksd
36K     /usr/local/bin/ssocksd
# pgrep ssocksd
24904
# pmap 24904
.......
 total            15104K
 ```

ssocksd takes the cake for being the lightest. 15MB RAM (shared with some other libraries) on x86_64 system, single process, no forks. The only caveat is that very little browsers support its antiquated RFC1929 simple socks auth.