debian-ssd-optim
================
Here is my SSD optimisation for Debian.

## Why ?
Because some of the 'tricks' are not easy to find.

## Hardware
I use a SSD Samsung 850 pro 512.

## Features
* Activate the trim (if available).
* Use tmpfs for some cache directory.
* Change the RAM usage of the kernel.
* Change the mounting option of the partitions.

## TRIM
You have to check that your hardware support the trim, with:
sudo hdparm -I /dev/sda | grep TRIM

If you can add the discard option in your fstab, like below.

## FSTAB
You can configure the mounting options, in the fstab file, like:

/dev/mapper/home    /home   ext4 noatime,nodiratime,discard,defaults            0   2

## RAM
You can configure you kernel ability to put more or less things in RAM.

On Debian this value, is at 60, which say to the kernel to start swap after 60% of the RAM is filled.

Create a file in /etc/sysctl.d/60-swappiness.conf:
vm.swappiness=1
vm.vfs_cache_pressure=50

## TMPFS
This is done in the fstab file, by:

tmpfs                                       /tmp    tmpfs defaults,size=1g
