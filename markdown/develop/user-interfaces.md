# User Interfaces

The various graphical user interfaces that interact with `Citadel` and allow a
user to control their `Realms` are [Gnome Shell Extensions](https://wiki.gnome.org/Projects/GnomeShell/Extensions) 
that is controlled by Citadel. Like the `Gnome Shell` these extensions are 
written in JavaScript.

## Adding An Extension To Citadel

Open `Citadel Terminal` become root and make it writable:

```
$ su
# mount -o remount,rw /
```

Copy the code from `your-extension` folder to the following and restart `gdm`

```
# cp -r /realm/realm-code/home/your-extension /usr/share/gnome-shell/extensions/
# gnome-shell-extension-tool -e your_extension@company.com
# systemctl restart gdm
```

*NOTE: Restarting `gdm` will quit all currently running applications inside it.*

You can also reload `gnome-shell` as user `citadel` with the following.
However, this option is really laggy and not the most helpful.

```
$ gnome-shell -r --nested
```

Once `gdm` has reloaded, go into `Gnome Tweak Tool` then `Extensions` pane. You 
should see your extension in the list. Toggle the switch to enable it. Your 
extension should now be accessible however you expect it to be.

**Debugging**

In `Citadel Terminal` you can monitor your extension for bugs as you develop it 
by running the following command:

```
journalctl -xe /usr/bin/gnome-shell
```

## Helpful Links

Developing *Gnome Shell Extensions* is not the most inuitive and easy process. 
Here are a few links to get started:

- [gnome-shell](https://github.com/GNOME/gnome-shell/) codebase
- [GNOME Developer Center](https://developer.gnome.org/)
- [GNOME Wiki: Extensions](https://wiki.gnome.org/Projects/GnomeShell/Extensions)
- [Tutorial: How I developed my first Gnome Shell Extension](https://www.abidibo.net/blog/2016/03/02/how-i-developed-my-first-gnome-shell-extension/)
