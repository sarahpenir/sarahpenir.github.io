---
layout: single
title: "Solution: Unable to execute a script on a mounted external drive on Linux"
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Linux
tags:
  - mount
  - Ubuntu
  - Linux
  - noexec
  - exec
  - can't execute on disk
  - umount
  - mount
  - fstab

---

If you're unable to execute a script on a mounted external drive on Linux, it's likely that a ```noexec``` flag has been invoked during the mounting of the disk. To check whether the desired volume has a ```noexec``` flag:

<!-- readmore -->

```
findmnt -l | grep noexec
```

```
TARGET       SOURCE	FSTYPE  OPTIONS
/media/disk/  /dev/sda6 fuseblk rw,nosuid,nodev,relatime,noexec
```

To fix this, unmount and mount the disk again, but this time with an ```exec``` flag:

```
sudo umount /media/disk/		
sudo mount -o rw,exec /dev/sda6
```

A more permanent solution would be to edit ```/etc/fstab``` with your editor of choice:

```
pluma /etc/fstab
```

Change the line:

```
UUID=135C3E180E89ABB3	/media/disk/	ntfs-3g	auto,users,permissions,nls=utf8  0 0
```
to

```UUID=135C3E180E89ABB3	/media/disk/	ntfs-3g	auto,users,permissions,exec,nls=utf8  0 0```

The position of the ```exec``` flag is important as it overwrites the default ```noexec``` applied by ```user```. This behavior is explained in the ```user``` section of ```man mount```:

```
user   Allow an ordinary user to mount the filesystem.  The name of the
              mounting  user  is  written  to the mtab file (or to the private
              libmount file in /run/mount on systems without a  regular  mtab)
              so  that  this same user can unmount the filesystem again.  This
              option implies the options noexec,  nosuid,  and  nodev  (unless
              overridden   by  subsequent  options,  as  in  the  option  line
              user,exec,dev,suid).
```
