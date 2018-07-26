# Tor Networking

Creating realms which route traffic through Tor is easy.

*Additional realms based on the stb appimg required this*

```
su -i
chown -R user:user /home/user/.config
env TOR_CONTROL_PORT=9051 /usr/bin/sandboxed-tor-browser
```

*On older versions you need to do this in Citadel Terminal*

```
sysctl kernel.grsecurity.chroot_deny_pivot=0
```

Citadel should switch you into that realm and you should be good to go

## Enable Apt Packages

Add the following rule to the file `/etc/iptables/rules.v4`

```shell
-A OUTPUT -m owner --uid-owner _apt -j ACCEPT
```

Then stop and restart that realm in Citadel

```shell
realms stop realm-name
realms current realm-name
``` 

This realm will now allow apps to route via tor, but `apt` 
packages will install normally over clearnet.
