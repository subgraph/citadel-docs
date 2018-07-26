# Taking Screenshots

In a realm of you choice install the `gnome-screenshot` application

```shell
$ sudo apt install gnome-screenshot
```

Then in `Citadel Terminal` become `root` and make root filesystem writable

```shell
$ su
# mount -o remount,rw /
```

Now copy over the schema for `gnome-screenshot` application

```shell
# cp /realms/realm-main/rootfs/usr/share/glib-2.0/schemas/org.gnome.gnome-screenshot.gschema.xml /usr/share/glib-2.0/schemas
```

In `Citadel Terminal` as `root` compile the schema you just copied, then become
user `citadel` and run screenshot tool

```shell
# glib-compile-schemas /usr/share/glib-2.0/schemas
# exit
$ /realms/realm-main/rootfs/usr/bin/gnome-screenshot -i
```
