# Hacks & Fixes

The following are various hack fixes to issues you may encounter that we are
aware of an working towards resolving.

## Permission Errors With Apt

While running `apt upgrade` or `apt install` in a `Realm` you may come across a 
permissions error such as the following:

```shell
dpkg: error while cleaning up:
 unable to remove newly-extracted version of '/usr/share/themes/Default/gtk-2.0-key/gtkrc': Read-only file system
```

A hacky fix to do the following for each directory containing files that throw 
the above error from the `Terminal` for that realm.

```shell
$ sudo mount -ttmpfs tmpfs /usr/share/themes/Default/gtk-2.0/
```

## Missing App Icons

In `Citadel Terminal` become root and make it writable

```shell
$ su
# mount -o remount,rw /
```

In `Citadel Terminal` copy icons like `app.png` to the following paths

```shell
/usr/share/icons/hicolor/512x512/app-name.png
/usr/share/icons/hicolor/256x256/app-name-png
/usr/share/icons/hicolor/128x128/app-name.png
```

Check that value of `Icon` matches the name of the icon you just copied in 
the `.desktop` file. This is located in the `Realm`

```shell
$ sudo vim /usr/share/applications/foo-app.desktop
```

You should see the following with `Icon=foo-app` value

```shell
[Desktop Entry]
Name=FooCorp App
Exec=foo-app
Icon=foo-app
Type=Application
Categories=GTK;GNOME;Utility;
```

That should fix the app icon issue.
