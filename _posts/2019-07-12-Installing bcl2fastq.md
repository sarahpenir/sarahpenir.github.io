---
layout: single
title: "Compiling bcl2fastq v2.20 on Ubuntu 18.04"
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Ubuntu
tags:
  - bcl2fastq
  - Ubuntu
  - boost error bcl2fastq
  - cmake error bcl2fastq
  - sys/stat.h error bcl2fastq

---

Unlike the MiSeq which automatically converts binary base call (BCL) files into FASTQ format using the MiSeq reporter, output from the NextSeq, HiSeq, and NovaSeq systems requires user-developed or third-party data analysis tools, such as ```bcl2fastq```, to be converted into FASTQ. Aside from enabling the conversion of BCL files to FASTQ, ```bcl2fastq``` can also assign sequencing data to specific samples based on their barcode (demultiplexing), trim adapters and Unique Molecular Identifiers (UMIs), and include the UMIs in the read names within the FASTQ files.

<!-- readmore -->

Compiling bcl2fastq is pretty straightforward as long as the following dependencies are met:

* zlib
* librt
* libpthread
* gcc 4.8.2 or later
* boost 1.54
* cmake 2.8.0

The first four is a breeze to install:

```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install zlibc
sudo apt-get install libc6 ## installs librt and libpthread
sudo apt-get install gcc
sudo apt-get install g++
```

But the remaining two (```boost 1.54``` and ```cmake 2.8.0```) are rather pesky with their specific version requirements. In case any of the dependencies are missing, it turns out ```bcl2fastq``` automatically installs the missing dependencies from its archive copy inside the ```/bcl2fastq/redist``` folder . Therefore, it seems prudent to simply purge the currently installed versions of ```boost``` and ```cmake``` to allow the compilation process to refer to ```bcl2fastq```'s own copy of these dependencies:

```
sudo apt-get -y --purge remove libboost1.62-all-dev libboost1.62-dev ## the version I had at that time 
sudo apt-get remove cmake 
```

Configure, build, and install the package using the following commands at the topmost folder of ```bcl2fastq```:

```
./configure && make && sudo make install
```

In case the system complains about the absence of ```sys/stat.h```, do the following:

```
sudo mkdir -p /usr/include/sys
sudo ln -s /usr/include/x86_64-linux-gnu/sys/stat.h /usr/include/sys/stat.h

```

After everything, ```bcl2fastq``` is now ready to use!