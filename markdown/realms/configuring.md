# Configuring Realms

Many aspects of this will eventually have graphical UIs built, but if if you are
eager to experiment with Citadel, you will have to manually create and edit
things in the `Citadel Terminal` for now.

## The config file

All of the curretly supported configuration options are listed below with their default values assigned.

    use-shared-dir = true
    use-sound = true
    use-x11 = true
    use-wayland = true
    use-gpu = false
    use-kvm = false
    use-network = true
    network-zone = "clear"

If you wish to change any of these options to something other than what is listed above add the
corresponding line to the file `/realms/realm-$name/config`

    citadel:~ # echo "use-gpu = true" > /realms/realm-games/config
    citadel:~ # realms shell games
    [+]: realm 'games' is not running, starting it.
    [+]: Started realm 'games'
    [+]: opening shell in realm 'games'
    games:~$ ls -l /dev/dri/renderD128
    crw-rw----+ 1 root video 226, 128 Mar 18 19:27 /dev/dri/renderD128

This will have added `use-gpu` support to the realm called 'games', from then on everything that runs in 
that realm has hardware graphics accelleration.


## Options 

`use-shared-dir` - Set to `false` to disable mounting the shared directory `/realms/Shared` into this realm at
`/home/user/Shared`.

`use-sound` - Set to `false` to prevent mounting pulse audio socket and sound device into this realm.

`use-x11` - Set to `false` to prevent mounting `/tmp/.X11-unix` into the realm. This is the socket for communicating
with the `XWayland` X11 compatibility daemon.

`use-wayland` - Set to `false` to prevent mounting the wayland display server socket `/run/user/1000/wayland-0`
 into the realm.

`use-gpu` - Set to `true` to mount the device `/dev/dri/renderD128` into the realm. Adding this
device will make hardware graphics acceleration available to applications running
in the realm.

`use-kvm` - Set to `true` to mount the device `/dev/kvm` into the realm.  This will make it
possible to run Qemu and other KVM based tools with hardware virtualization
inside the realm.

`use-network` - Set to `false` to disable configuring the realm with access to the internet.  The
realm instance will only have a localhost network interface.

`network-zone` - Setting a name here will create bridge device in citadel with the name vz-$name if
it doesn't already exist and attach this realm instance to that bridge.
