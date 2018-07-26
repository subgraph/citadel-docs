# Configuring Application Images

This is a collection of various modification that you need to do within an
Application Image to have them properly function.

## Add Hardware Graphics Acceleration

In `Citadel Terminal` become root and make the rootfs writable

```shell
$ su
# mount -o remount,rw /
```

Enable `/dev/dri/renderD128 bind mount` in the `primary.nspawn` file

```shell
# vim /etc/systemd/nspawn/primary.nspawn
```

## Switching Application Images

To switch between dirrecnt `Application Images` open up `Citadel Terminal` and 
go to the following directory

```shell
$ su
# cd /storage/appimg
citadel:/storage/appimg # ls -l
total 4
drwxrwxrwt 1 root root 154 Jun 11 13:37 base.appimg
lrwxrwxrwx 1 root root   7 Jun 17 13:37 default.appimg -> primary
drwxr-xr-x 1 root root  12 Jun 17 13:37 primary
```

You have a directory called `primary` and a symlink `default.appimg` pointing 
to the `primary` directory. Inside of primary is a directory called `rootfs`
When you boot your computer, whatever the symlink is pointing to is the apping 
that is started. To double check option `Citadel Terminal` and look at:

```shell
# machinectl
MACHINE   CLASS     SERVICE        OS     VERSION ADDRESSES
code      container systemd-nspawn debian -       172.17.0.3
main      container systemd-nspawn debian -       172.17.0.2
web       container systemd-nspawn debian -       172.17.0.3

3 machines listed.
```

To see details of the `main` realm, do the following 

```shell
# machinectl show main
...
RootDirectory=/storage/appimg/test/rootfs
```
