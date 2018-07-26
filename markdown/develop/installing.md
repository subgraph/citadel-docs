# Installing Citadel

This guide assumes you have already built Citadel. If you have not, start by 
cloning the `citadel` source code:

```shell
$ git clone https://github.com/subgraph/citadel
```

Then follow one of these build instructions:

- [Build Citadel on Debian](citadel-build-on-debian.md)
- [Build Citadel using Docker](citadel-build-using-docker.md)

## Prepare USB Stick Boot

1. You will need to download Gentoo boot disk 
2. Use the utility `dd` to copy that to `USB Stick Boot`

## Prepare USB Stick Citadel

1. Format with an easy to mount filesystem like `FAT` or `ext4`
2. Copy the `installpack.tar` onto `USB Stick Citadel`
3. Boot into Gentoo with `USB Stick Boot`
4. Once booted into Gentoo Live, insert `USB Stick Citadel` into a port
5. Mount `USB Stick Citadel`
6. Untar `installpack.tar` directory and install on your hard drive `/dev/sda`

```shell
$ tar -xvf installpack.tar
$ cd installpack/
$ ./install.sh /dev/sda
```

If the last message from `install.sh` is not completely successfull, then it 
didn't work and you should check the `install.log` file.

## Corebooted Machines

The `biosboot.tar` is instructions to convert an already working sgos-ng install
which is installed on a usb pendrive to one that will boot on legacy bios

To do this, requires a handful of extra steps that are not in Gentoo distro and
I manually copied over from a Debian machine to `USB Stick Citadel`
