# Creating an Application Image

First create a realm that is used for building software called `build`

```
$ su
# realms new build
# realms current build
```

From within this new `build` realm's terminal, do:

```
wget https://not-here-yet.com/appimg-builder-modified.tar
tar -xvf appimg-builder-modifed.tar -C /usr/share
```

## Build Sandboxed Tor Realm

In this example, we will create an `Application Image` that has
[Tor](https://torproject.org) networking pre-installed as well as the hardened 
`Sandboxed Tor Browser` installed and configured

```shell
$ wget https://www.torproject.org/dist/torbrowser/8.0a8/sandbox-0.0.16-linux64.zip
$ wget https://www.torproject.org/dist/torbrowser/8.0a8/sandbox-0.0.16-linux64.zip.asc
$ gpg --search-keys 0xD1483FA6C3C07136
$ gpg --verify 0xD1483FA6C3C07136
$ unzip sandbox-0.0.16-linux64.zip
```

In `Citadel Terminal` run the following as `root`

```shell
# sysctl kernel.grsecurity.chroot_deny_pivot = 0
# sysctl kernel.grsecurity.chroot_deny_chroot = 0
```

Now, you're ready to build the `Sandboxed Tor Browser` application image in your
`build` realm.

```
$ mkdir work
$ wget https://not-yet-here.com/stb-appimg.tar
$ tar -xvf stb-appimg.tar -C work
$ cp sandbox/sandboxed-tor-browser work/stb-appimg/appimg-files/
$ cd work/stb-appimg
$ sudo appimg-builder -t
```

Inside `Citadel Terminal` run the following as `root`

```
# realms new tb
# btrfs subvolume delete /realms/realm-tb/rootfs/
# tar -C /realms/realm-tb/rootfs -xf /realms/realm-build/home/work/stb-appimg/appimg/appimg-rootfs.tar
# realms current tb
```
