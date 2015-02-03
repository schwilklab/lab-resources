Computers and Network
=====================

author: Dylan Schwilk

## Lab computers ##

TODO.  Standard os is Kubuntu

## Ethernet at TTU ###

The TTU ethernet network is finicky and there are undocumented requirements.  We have both "old" (100Mb/s) and "new" (1000Mb/s) ports in the lab. I will label all "new" ports witha  red sharpie.
These ports require different network settings in the operating system. My instructions below assume that entwork manager has been uninstalled and that we are using the older debian method of setting ethernet options in /etc/network/interfaces

So my tentative conclusions on required settings

### "Old" ports: ###

Must be set manually 100Mb/s.  On Debian and Ubuntu flavors (assuming network manager is uninstalled/disabled), use ethtool in a pre-up hook, eg this stanza in /etc/network/interfaces:

```
auto eth0
iface eth0 inet dhcp
pre-up /sbin/ethtool -s eth0 autoneg off speed 100 duplex full
```

### "new" ports ###

#### NIC pre-up hook should be: ####

```
pre-up /sbin/ethtool -s eth0 autoneg on
```

#### ipv6 must be disabled on the machine. ####

 - add the following lines to /etc/sysctl.conf:

```
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv6.conf.lo.disable_ipv6 = 1
```

 - Modify grub settings to add option ipv6.disabled=1

   GRUB_CMDLINE_LINUX_DEFAULT="ipv6.disabled=1 quiet"

   then update-grub

#### Autonegotiation MUST be used on the new ports, manual setting of any speed fails ####

