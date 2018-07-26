# Installing Application Images

From within the running container

```shell
$ sudo apt-get install debootstrap
$ git clone https://github.com/subgraph/citadel
$ make build-appimg
```

Then from within Citadel as root run

```shell
$ mkdir -p /storage/appimg/cool-new/rootfs
$ tar -C /storage/appimg/cool-new/rootfs -xf /path/to/appimg-rootfs.tar.xz
```

When seen from `citadel` the path will look like

```shell
/storage/user-data/primary-home/citadel/build/appimg/appimg-rootfs.tar.xz
/storage/appimg/primary/rootfs/appimg-rootfs.tar.xz (BUG)
```

Now switch to your new appimg with `default.appimg` symlink trick below

```shell
$ cp -a /storage/user-data/primary-home/work/appimg/rootfs /storage/appimg/somename
```
