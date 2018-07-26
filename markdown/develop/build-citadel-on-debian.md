# Build Citadel on Debian

Alternatively, if you prefer to not use Docker, here are instructions for building Citadel on a basic Debian machine.

## Install Dependencies

Currently there are some rather unreliable scripts to make it possible
to turn build output into something that you can install and run. Very
soon these scripts will be replaced by an actual installer that you can
just build by running a make target, but that doesn't quite exist yet.

Run the following command to install the build dependenices on Debian

```shell
$ sudo apt update && apt install -y gawk wget git-core diffstat unzip texinfo gc-multilib build-essential chrpath socat cpio python python3 python3-pip python3-pexpect xz-utils debianutils iputils-ping locales libgmp-dev libmpc-dev libelf-dev nano sudo debootstrap inkscape file
```

Now go into the directoy and do the following:

```shell
$ cd citadel/
$ make update-submodules
$ make install-build-deps
```

The end goal is you will be to create a file `installpack.tar` but before doing
that some artifacts must exist in the `build/images/` directory:

- `make citadel-image` creates `images/citadel-image-intel-corei7-64.ext2`
- `make citadel-kernel` creates `images/bzImage`
- `make bootloader` creates `images/systemd-bootx64.efi`
- `make build-appimg` creates `appimg/appimg-rootfs.tar.xz`

After all of those components have been built you can run:

```shell
$ scripts/create_install_pack
```

And this will create a file in the current directory called `installpack.tar`

You can then unpack this tarball somewhere and run a script inside of it
called `install.sh` to install to a USB stick (do this first, at least
until you understand the process) or to install to internal disk drive.

```shell
$ tar xvf installpack.tar
$ cd installpack
$ sudo ./install.sh /dev/sdb
```

The `install.sh` script redirects all output from the commands it runs
to a file install.log in the current directory. If the last line of
output does not say:

**"Install completed successfully"**

Then something failed and you should look in `install.log` for information about
what went wrong. The script itself does not print any output when it fails, it
will just stop at one of the steps and it appears as if everything worked since
there is no error output.
