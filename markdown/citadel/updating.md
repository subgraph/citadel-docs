# Updating Citadel

Eventually this will be handled automatically and there will be a graphical
application, but for now use the following instructions to do it manually.

## Update Citadel Kernel

Open `Citadel Terminal` and create a new realm called `build`

```shell
$ su
# realms new build
# realms current build
```

Open regular `Terminal` in the `build` realm you just created, and install and
follow one of these two building instructions:

- [Build Citadel on Debian](develop/build-citadel-on-debian.html)
- [Build Citadel using Docker](develop/build-citadel-using-docker.html)

Once you have completed the following step:

```shell
$ make citadel-kernel
```

Then return to `Citadel Terminal` and do the following:

```shell
# mount -o remount,rw /
# mount /dev/sda1 /boot
# cd /boot
```

Make a backup of your `bzImage` and copy the new one you built

```shell
# cp bzImage bzImage.old
# cp /realms/realm-build/home/citadel/build/images/bzImage /boot
```

Reboot your machine and you will be using an updated Citadel kernel.
