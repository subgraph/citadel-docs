# Realms

Every *Realm* on your system is based on an *Application Image*, but realms are
where your applications actually run and where you interact with your data.
Technically speaking, a realm is a container similar to a Docker or LXC
container in which any Linux distribution could be installed.

The realm containers are launched with systemd-nspawn but this is a detail of
how they are implemented and not something it is necessary to learn about in order to use them.

### Realms base directory layout

The realms base directory is stored on the storage partition at `/storage/realms` and is bind mounted to `/realms` on the root filesystem for convenience.

```shell
/realms
    config
    /Shared
    /skel
    /default.realm -> realm-main
    /realm-main
    /realm-project
    /realm-testing
```

#### Config File 

`/realms/config`

This file is a template of the configuration file for individual realms. When a new
realm is created this file in copied into the new realm instance directory. By
modifying this file, the default configuration for new realm instances can be changed.

#### Shared Directory 

`/realms/Shared`

This directory is bind mounted to `/home/user/Shared` of each running realm that has
the option `use-shared-dir` enabled.  It's a convenient way to move files between
different realms and between citadel and realms.

#### Skel Directory 

`/realms/skel`

Files which are added to this directory will be copied into the home directory of
any newly created realm.  The directory is copied as a tree of files and may contain
subdirectories. After moving files into the `/realms/skel` you should set the permissions as such

```shell
chown 1000:1000 ,dotfile
```

#### Default Symlink 

`/realms/default.realm`

A symlink which points to a realm instance directory of the default realm.  The
default realm is the realm which starts when the system is booted.

#### Realm Directory

`/realms/realm-main`

This is a realm instance directory, for a realm with `main` as the realm name.

```shell
/realms/realm-main
    config
    /home
    /rootfs
```

```shell
config
```

Configuration file for the realm instance copied from `/realms/config` or
created by the user.

```shell
home
```

Home directory for this realm. It will be mounted to `/home/user` in
the realm instance.

```shell
rootfs
```

The root filesystem of this realm. It is cloned from (a btrfs subvolume snapshot
of) some application image.
