# USB Devices

## Mounting Storage Devices

Currently, USB storage devices need to be mounted manually from the terminal. 
Plug in the USB device and open `Citadel Terminal`

```shell
$ su
# mkdir /realms/realm-main/home/YourDrive
# chown -R user:user /realms/realms-main/home/YourDrive
# mount /dev/sdb1 /realms/realm-main/home/YourDrive
```

You can also mount `YourDrive` to the `Shared` directory so that is available 
to all realms which have a `Shared` directory.

```shell
# mount /dev/mapper/YourDrive /realms/Shared/YourDrive
```

## Mounting Encrypted Storage Devices

If your storage device is LUKS encrypted, you need to do the following from
within `Citadel Terminal`

```shell
$ su
# cryptsetup luksOpen /dev/sdb1 YourDrive
# mkdir /realms/Shared/YourDrive
# mount /dev/mapper/YourDrive /realms/Shared/YourDrive
```

Your encrypted drive should then be mounted in `Shared`
