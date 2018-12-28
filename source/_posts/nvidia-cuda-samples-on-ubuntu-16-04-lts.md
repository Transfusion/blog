---
title: nVidia CUDA samples on Ubuntu 16.04 LTS
url: 686.html
id: 686
categories:
  - Unix
date: 2016-06-25 00:28:25
tags:
---

Here they are in case anyone else needs to download them separately (and the rest of cuda-repo-ubuntu1504-7-5-local\_7.5-18\_amd64.deb): [https://drive.google.com/open?id=0B_SnrcTvZzIXX2dkM0pwT2E3U2s](https://drive.google.com/open?id=0B_SnrcTvZzIXX2dkM0pwT2E3U2s) [https://mega.nz/#F!dVBghK7J!6nvh-XvvoiqqeGp144jouw](https://mega.nz/#F!dVBghK7J!6nvh-XvvoiqqeGp144jouw) The file you're looking for is var/cuda-repo-7-5-local/cuda-samples-7-5\_7.5-18\_amd64.deb To extract and compile the samples (make sure you have your nVidia GPU active if you're using Optimus, e.g. by using

sudo prime-switch nvidia

or otherwise;

nvidia-smi

should show your GPU's details.

ar x cuda-samples-7-5\_7.5-18\_amd64.deb
tar -xf data.tar.gz
cd usr/local/cuda-7.5/samples/5_Simulations/smokeParticles/
CUDA\_PATH=/usr CUDA\_SEARCH\_PATH=/usr/libx86\_64-linux-gnu/ make -j5