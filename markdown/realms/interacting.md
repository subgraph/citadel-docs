# Interacting with Realms

Soon there will be user friendly interfaces for creating, editing, and
switching between realms, but for now Citadel provides the command-line tool
accesible in the `Citadel Terminal` by typing `realms` you will see a list of
existing realms.

```shell
citadel:~ $ realms

   REALMS     bold: current, colored: running, (default) starts on boot
   ------

 > main          (default)
   web          
   chat        
   work
```` 


By typing `realms help` you can see a list of all the commands available that
control your realms.

To perform any actions like starting or stoping realms, you need to become root.
Then you can type commands like `stop`

```shell
$ su
# realms stop main
```

### The `default` realm

One realm is always selected to be the `default` realm.  This realm
starts automatically when the system boots.  The `realms` utility can be used
to change which realm is the default realm. Switching the default realm changes
the symlink `/realm/default.realm` to point to a different realm instance directory.

```shell
citadel:~ # realms default
Default Realm: main

citadel:~ # realms default project
[+] default realm changed from 'main' to 'project'

citadel:~ # realms default
Default Realm: project
```

### The `> current` realm

Multiple realms may be launched at once but the Gnome Desktop is only associated with
one of the running realms.  This realm is called the `current` realm.

When displaying applications available to launch from the desktop, Gnome will only
be aware of applications that are installed in the realm which is set as `current`
and any application launched from the desktop will run inside this current realm.

Setting another realm as current does not affect any applications that are already running.
Changing the current realm only means that any further applications which are launched
will now run in the newly chosen realm.

Changing or querying the current realm is done with the `realms current` command, and
if you choose a realm which is not currently running it will be automatically started.
