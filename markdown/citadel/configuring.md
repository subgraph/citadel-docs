# Configuring Citadel

Considering that Citadel is the main controller of your operating system, be
careful what you change in it. Currently, you can only configure Citadel by
using the `Citadel Terminal` application, but there will soon be a GUI.

## Default Passwords

The default the passwords on a newly installed Citade system are:

- Realms: **user**
- Lockscreen: **citadel**

You can change a realm password with `passwd` like on any linux system. 
However, it is not currently easy to change the lockscreen password without 
using `Citadel Terminal`

## Making rootfs writable

Open `Citadel Terminal` and use `su` to become root

```shell
$ su
```

Remount the root filesytem as read-write with `rw`

```shell
# mount -o remount,rw /
```

Making the rootfs writable is needed in all of the steps below.

## Changing Gnome lock screen passwd

Open `Citadel Terminal` and generate new password with `openssl`

```shell
$ openssl passwd
Password: 
Verifying - Password: 
sGYyWXqDuh64g
```

Then become root and make it writable

```shell
$ su
# mount -o remount,rw /
```

Open up the file `/etc/shadow`

```shell
# vim /etc/shadow
```

In that file find the line that looks like the following:

```shell
citadel:$1$/zh4a3$D52BPg242/vL21D937/:17693:0:99999:7:::
```

Replace `$1$/zh4a3$D52BPg242/vL21D937/` with the password hash `sGYyWXqDuh64g`

## Using QEMU

Open `Citadel Terminal` then become root and make it writable

```shell
$ su
# mount -o remount,rw /
```

Enable `/dev/kvm bind mount` in `primary.nspawn` file

```shell
# vim /etc/systemd/nspawn/primary.nspawn
```

## Changing Gnome timezone

Open `Citadel Terminal` then become root and make it writable

```shell
$ su
# mount -o remount,rw /
```

Launch the `Settings` application and navigate to the correct screen:

**Details -> Date & Time**

Change values as you desire, then quit `Settings` application.

## Configuring Bash

Ignore the `checkwinsize` option, it's probably not actually needed and irrelevant
but the color sequences need to have `\[` and `\]` delimiters around some things.
These are currently needed to prevent a strange wraping issue in Citadel.

## Dotfile Configs

Gets copied everytime Citadel boots

[dot.bashrc](https://github.com/subgraph/citadel/meta-citadel/recipes-core/base-files/files/share/dot.bashrc)

That file ends up in `/usr/share/factory/home/citadel/.bashrc` and when citadel
boots it mounts a `tmpfs` for the `/home` directory and then copies the files 
from `/usr/share/factory/home` over.
