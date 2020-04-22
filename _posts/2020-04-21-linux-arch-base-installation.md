---
title: Arch Linux Base Installation - Supplemental Steps
description: The Arch Wiki is a great resource but it is missing a couple of important steps.
image: /assets/images/archlinux-logo-dark-scalable.svg

header:
   teaser: /assets/images/archlinux-logo-dark-scalable.svg

keywords: Linux Arch
permalink: /linux/arch/arch-linux-base
toc: true
---


The [Arch Linux Wiki][2] does a fantastic job of describing the essential steps to install Arch Linux to the point of having a working, base installation. However, it misses out a few steps necessary to get to a functional, networked installation.

![Arch Linux](/assets/images/archlinux-logo-dark-scalable.svg)

This post extends the official [Arch Linux Installation Guide][1] with a few extra steps necessary to get networking and user permissions up and running.

# What's missing from the Arch Installation Wiki?
After you've completed the [Arch Linux Installation Guide][1], don't reboot yet. There are some extra steps to take to simplify your next boot into Arch base install.

## Common packages
Needed for next steps.

```bash
pacman -S vim sudo grub dhcpcd
```

## Networking
When you reboot after completing installation according to the Wiki, you will have no internet connection. This is because, by default, DHCP is not enabled.

## Non root user is not installed / granted permissions.

# Essential Extra Steps for Arch Linux Base

## Networking
By default, DHCP is not enabled.

Enable as follows:

```bash
systemctl enable dhcpcd
```


## Non root user
This step may not apply to you if you choose to run Arch as root (not recommended).

```bash
useradd -m {yourusername}
passwd {yourusername}
usermod -aG wheel,audio,video,optical,storage {yourusername}
```

### Add non root user to sudoers

```bash
visudo
```

Uncomment the line that starts with '%wheel ...' as follows:

```bash
## Uncomment to allow members of the group wheel to execute any command
# %wheel ALL=(ALL) ALL
```

## GRUB boot loader
This is documented in the Arch Wiki, but not on the main installation guide page.

Included here for completeness.

```bash
grub-install /dev/sda
grub-mkconfig -o /boot/grub/grub.cfg
```

# Reboot
Now go ahead and reboot for an installation that has working networking and a non-root user enabled. Don't forget to remove the installation media before doing so!

[1]: https://wiki.archlinux.org/index.php/Installation_guide "Arch Linux Installation Guide"
[2]: https://wiki.archlinux.org "Arch Linux Wiki"
