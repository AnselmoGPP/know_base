# Linux in VirtualBox

## Table of Contents
+ [Install VirtualBox](#install-virtualbox)
+ [Install Ubuntu](#install-ubuntu)
+ [Share data](#share-data)
+ [Fullscreen](#fullscreen)
+ [Links](#links)


## Install VirtualBox

1. **Download** [VirtualBox](https://www.virtualbox.org/) and install it.
2. Open VirtualBox and create a new virtual machine (**new** button).
3. **Configure** virtual machine: Location (where to install), machine name, OS, RAM (size), processors, hard disk (size, location, and others. Recommended: virtual hard disk drive, VisualBox disk image, dynamically allocated storage).


## Install Ubuntu

1. **Download** the [Ubuntu](https://ubuntu.com/download) iso.
2. Boot the virtual machine (**start** button) and load the Ubuntu iso.
3. **Install** Ubuntu (normal installation type, erase disk option) and **reboot**.

## Guest additions

Installing **guest additions** is required for sharing data and enabling fullscreen. Installing procedure:

- Guest menu > `Devices` > `Insert guest additions CD image`.
- This loads a CD in the guest, so open it, run the commands below, and restart Ubuntu.

```
sudo apt update
sudo apt upgrade
./autorun.sh
```

### Fullscreen

1. Guest > `View` > `Auto-resize guest display`
2. Guest > `View` > `Full-screen mode`

### Share data

Sharing data between host and guest can be configured in:

- VirtualBox manager > Guest > `settings` > 
  - `General` > `Advanced` > `Shared clipboard` (optional: `Enable clipboard file transfers`).
  - `General` > `Advanced` > `Drag and Drop`
  - `Shared folders` (select `Auto-mount`)


## Links

- [How to install Ubuntu on VirtualBox](https://www.geeksforgeeks.org/how-to-install-ubuntu-on-virtualbox/)