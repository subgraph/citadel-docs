# Application Images

An `Application Image` can be thought of as a foundation or base which is
virtually copied every time you create a realm. By default Citadel comes with 
a [Debian](https://debian.org) `buster` image but it would not be difficult to 
create an image for another Linux distribution.

The root filesystem for realms are called an `Application Image` but we often 
use the shorter name *appimg*, which is not to be confused with [App
Images](https://appimages.com) package manager.

## Tree Application Images

Currently, these are the only type of application image which are currently
implemented for realms. The `rootfs` is a tree of files on the filesystem, and 
it is also a `btrfs subvolume` which is cloned at zero cost (internally with 
`btrfs subvolume snapshot`) to use as the root filesystem of newly created realms.

## Block Application Images & Sealed Application Images

In the future we will add another type of application image called a **Block
Application Image**. This type of image will be stored as a disk volume image file
and will be mounted with a loop device rather than existing as a tree of files on the
filesystem.

This will make it possible to enforce [dm-verity](https://www.kernel.org/doc/Documentation/device-mapper/verity.txt)
verification over the image and ensure that no malicous or unintended modifications
can be made to any of the the files on the root filesystem. Signature verification
over the dm-verity root hash is done from the citadel rootfs image which is also
secured with dm-verity.  When enforcement of boot integrity is also implemented this
will create a chain of cryptographic assurances that no component of the system has
been tampered with.

Block images with signatures and dm-verify verification enabled are called **Sealed Application Images**

## Updating an Application Image

To modify or update an application image run the `realms update-appimg` command.
A container will be created for updating the image and a root shell session will
open. From this session regular package management commands can be run.  Any changes
made will only affect future realms created from this appimg.

```shell
$ su
# realms update-appimg
[+]: Entering root shell on base appimg
root@base-appimg-update:/# apt update
```

## Creating Application Images

We created a framework called [appimg-builder](develop/appimg-builder,html)
for building a Debian based images and we use this to build the default appimg that we ship.
We encourage users to experiment with building their own custom images using the
following guides:

- [Application Image Builder](develop/appimg-builder.html)
- [Creating an Application Image](develop/appimg-creating.html)  
