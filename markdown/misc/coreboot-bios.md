# Coreboot BIOS

To complete installing Citadel on a machine that runs the open source 
[Coreboot BIOS](https://www.coreboot.org). These instructions are for a Debian 
machine, but other distributions package `syslinux` a bit differently. 
Install the following dependencies:

```shell
$ apt install extlinux syslinux-common
```

Then move onto to modifying the file system of the disk you are installing
Citadel onto. This assumes you installed Citadel to hardrive `/dev/sda` 


```shell
$ mount /dev/sda1 /boot
$ mkdir /boot/syslinux
$ cp syslinux.cfg /boot/syslinux
$ cp /usr/lib/syslinux/modules/bios/*.c32 /boot/syslinux
$ extlinux --install /boot/syslinux
$ umount /boot
```

Last, set the the following values

```shell
$ dd bs=440 count=1 conv=notrunc if=/usr/lib/syslinux/mbr/gptmbr.bin of=/dev/sda
$ parted /dev/sda set 1 legacy_boot on 
```
