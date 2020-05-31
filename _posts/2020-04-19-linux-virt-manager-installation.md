---
title: virt-manager Installation
description: How to install virt-manager on Linux
image: /assets/images/lib-vert-manager-800x450.png
header:
   teaser: /assets/images/lib-vert-manager-800x450.png
keywords: virt-manager linux
permalink: /linux/virt-manager-installation
toc: true
images:
  - url: /assets/images/lib-vert-manager-800x450.png
    alt: virt-manager
    title: virt-manager
    height: 450
    width: 800
---

[virt-manager][1] is a virtual machine manager for Linux and can run both Linux and Windows virtual machines. Its main advantage is speed.

![virt-manager](/assets/images/lib-vert-manager-800x450.png){:style="width:800px;height:450px;"}

If you're using Linux did you know that the Linux kernel already has virtual machine capability built in? You don't need VM Ware, Virtual Box or any other hyper visor. The Linux Kernel can run your Linux or Windows virtual machines right out of the box.

# Why use virt-manager?
virt-manager is built to manage QEMU/KVM hyper visor. The QEMU hyper visor can access hardware virtualisation natively via the Linux kernel which means that virtualisation should be a faster and more efficient than some thing like, say, Virtual Box

# What do you need?
KVM will work on any Linux distribution but you need CPU hardware virtualisation support enabled. Use the following command to check that CPU virtualisation is enabled:

```bash
LC_ALL=C lscpu | grep Virtualization
```
A positive response of a value is what you're looking for. For example, for Intel systems the following:

```bash
Virtualization:                  VT-x
```
If nothing is shown, you need to enable CPU virtualisation in your BIOS.

# How to install virt-manager

## Install packages
The following is for Debian/Ubuntu based systems.

```bash
sudo apt install libvirt qemu virt-manager ebtables
```

## Enable and start services

```bash
sudo systemctl enable libvirtd
sudo systemctl start libvirtd
```

## Check the status of service
```bash
sudo systemctl start libvirtd
```

Should return something like:

```
ibvirtd.service - Virtualization daemon
   Loaded: loaded (/lib/systemd/system/libvirtd.service; enabled; vendor preset: enabled)
   Active: active (running) since Sun 2020-04-19 11:21:43 BST; 1 day 3h ago
     Docs: man:libvirtd(8)
           https://libvirt.org
 Main PID: 2067 (libvirtd)
    Tasks: 19 (limit: 32768)
   Memory: 59.9M
   CGroup: /system.slice/libvirtd.service
           ├─2067 /usr/sbin/libvirtd
           ├─2290 /usr/sbin/dnsmasq --conf-file=/var/lib/libvirt/dnsmasq/default.conf --leasefile-ro --dhcp-script=/usr/lib/libvirt/libvirt_leaseshelper
           └─2291 /usr/sbin/dnsmasq --conf-file=/var/lib/libvirt/dnsmasq/default.conf --leasefile-ro --dhcp-script=/usr/lib/libvirt/libvirt_leaseshelper
```

## Set permissions
To run virt-manager, your user needs to be a member of the libvert group.

```bash
sudo usermod -aG libvirt {your user}
```

# How to run virt-manager
Now simply run virt-manager from your desktop launcher.

[1]: https://virt-manager.org "virt-manager"
