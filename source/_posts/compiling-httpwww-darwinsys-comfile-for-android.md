---
title: 'Compiling http://www.darwinsys.com/file/ for Android'
tags:
  - android
  - file
  - gnu
url: 293.html
id: 293
categories:
  - Unix
date: 2014-04-14 19:58:26
---

Cross compiling is always a PITA, so here goes:

AR=arm-linux-androideabi-ar
OLDPWD=/home/transfusion/android-bash/fileutil
LD\_LIBRARY\_PATH=/home/transfusion/android-ndk-r9c/platforms/android-18/arch-arm/usr/lib/
PATH=/home/transfusion/android-ndk-r9c/toolchains/arm-linux-androideabi-4.8/prebuilt/linux-x86_64/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games
LD=arm-linux-androideabi-ld
PWD=/home/transfusion/android-bash/fileutil/bin
STRIP=arm-linux-androideabi-strip --strip-unneeded
CXX=arm-linux-androideabi-g++
CFLAGS=-L/home/transfusion/android-ndk-r9c/platforms/android-18/arch-arm/usr/lib/ --sysroot=/home/transfusion/android-ndk-r9c/platforms/android-18/arch-arm/ -I/home/transfusion/android-ndk-r9c/platforms/android-18/arch-arm/usr/include/
RANLIB=arm-linux-androideabi-ranlib
ANDROID_NDK=/home/transfusion/android-ndk-r9c
CC=arm-linux-androideabi-gcc
READELF=arm-linux-androideabi-readelf

I have android-ndk-r9c extracted to my home directory.

cd file-5.11
cd src
ln -s $ANDROID\_NDK/platforms/android-19/arch-arm/usr/lib/crtend\_so.o
ln -s $ANDROID\_NDK/platforms/android-19/arch-arm/usr/lib/crtbegin\_so.o
./configure --prefix=/home/transfusion/file-android-build --host=arm-linux ---datarootdir=/system/share
make && make install

See [https://stackoverflow.com/questions/6881164/crtbegin-so-o-missing-for-android-toolchain-custom-build](https://stackoverflow.com/questions/6881164/crtbegin-so-o-missing-for-android-toolchain-custom-build) as to why those two files need to be linked. The magic.mgc file is going to be placed in /system/share/misc/magic on the device. Copy all the files into /system on the device, and create the symlink to libmagic.so in /system/lib if it hasn't been created

cd /system/lib
ln -s libmagic.so.1.0.0 libmagic.so.1

If all works well,

$ file /system/bin/file
/system/bin/file: ELF 32-bit LSB executable, ARM, version 1 (SYSV), dynamically linked (uses shared libs), not stripped