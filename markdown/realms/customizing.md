# Customizing Realms

## Default Files

If you want custom `.bashrc` files or any other `.dotfiles` in a `Realm` simply 
copy those files to the following location via `Citadel Terminal`

```shell
$ su
# mount -o remount,rw /
# cp /path/to/custom/bashrc /realms/skel/.bashrc
```

Then whenever a new realm is created the `.bashrc` file and any other files in
the `skel` directory will copied into the new realm's home directory.
