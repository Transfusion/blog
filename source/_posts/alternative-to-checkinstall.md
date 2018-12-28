title: Alternative to checkinstall
url: 257.html
id: 257
categories:
  - Unix
date: 2014-03-25 22:20:50
tags:
---
[https://unix.stackexchange.com/questions/16375/keeping-track-of-programs](https://unix.stackexchange.com/questions/16375/keeping-track-of-programs)
```bash
./configure --prefix /usr/local/stow/PROGRAM_NAME
make
make install
cd /usr/local/stow
stow PROGRAM_NAME
```
When you want to remove the symlinks created in /usr/local/ for your particular program:

```bash
stow -D PROGRAM_NAME
```

Extremely useful in Cygwin where checkinstall and package managers aren't available.