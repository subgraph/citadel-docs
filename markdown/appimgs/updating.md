# Updating Application Images

It is important to recognize the following properties of `Application Images` 
Changes only affect realms you create after these updates have been applied.
This **does not** change anything about `Realms` previously based on that image.

## Updating Exsting Appimg

To update the **base appimg** installed on a machine

In `Citadel Terminal` become root and do the following:

```shell
$ su
# realms update-appimg
[+]: Entering root shell on base appimg
root@base-appimg-update:/# 
```

You shold now be in a root shell in a limited container inside the `appimg`
Next, run the standard commands to update Debian

```shell
root@base-appimg-update:/# apt update
root@base-appimg-update:/# apt upgrade
Setting up ...
Processing triggers for ...
root@base-appimg-update:/#
```

## Updating From Source

Alternatively, you can update an `Application Image` from  the `citadel` 
source code by running the following to create an up-to-date image:

```shell
$ make appimg-rootfs
```

As development of Citadel is rapidly moving and there is not automated way to
update it, you must do the following steps for now.

Open `Citadel Terminal` and become root to determine if current boot is from 
rootfsA or rootfsB. 

```shell
$ su
# findmnt /
TARGET SOURCE                      FSTYPE OPTIONS
/      /dev/mapper/citadel-rootfsA ext2   rw,relatime,errors=continue,user_xattr
```

Make sure you don't overwrite the currently mounted rootfs partition. Locate 
the rootfs update image you want to install:

```shell
# file /storage/user-data/primary-home/citadel-image-intel-corei7-64.ext2 
/storage/user-data/primary-home/citadel-image-intel-corei7-64.ext2: Linux rev 1.0 ext2 filesystem data, UUID=d9dd20e9-9286-4c60-9dc3-37c68e36481c (large files)
```

Write to the correct partition with dd command.

```shell
# dd if=/storage/user-data/primary-home/citadel-image-intel-corei7-64.ext2 of=/dev/mapper/citadel-rootfsB bs=4M
255+1 records in
255+1 records out
1071823872 bytes (1.1 GB, 1022 MiB) copied, 3.01726 s, 355 MB/s
```

Sync just to be sure everything is flushed to disk, then reboot into new image.

```shell
# sync
# reboot
```
