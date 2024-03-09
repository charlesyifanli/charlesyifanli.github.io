---
title: linuxOS-tips
date: 2024-03-08 09:01:29
tags: linux
categories:
- linux config
---

## How to set terminal shortcuts

```reStructuredText
click on "settings"
```

```reStructuredText
click on "Customize Shortscuts" in Keyboard Shortcuts
```

```reStructuredText
click on "Custom Shortcuts"
```

```reStructuredText
name: terminal
Command: /usr/bin/gnome-terminal
Shortcut: Ctrl + Alt + L
```

###    

##  Handle block device like USB drive

 ### Command line:

```bash
lsblk
```



```bash
mount /dev/sdb1 ./usb/
```



If user-oriented, run fowllowing commands in order:

```bash
umount ./usb
mount /dev/sdb1 -o uid=? gid=? /dev/sdb1 ./usb/
```



### Explanation

```reStructuredText
sda:
The naming convention for storage devices in Linux, such as hard drives, solid-state drives, and USB drives, uses "sda" and "sdb". This convention consists of the following parts:

"sd": Represents SCSI devices. Although called SCSI devices, they are not necessarily true SCSI devices but rather follow a naming convention.
"a", "b", etc.: Represents the device's identifier, starting from "a" and incrementing.

Therefore, "sda" represents the first SCSI device in the system, typically the primary hard drive, while "sdb" represents the second SCSI device, typically another hard drive or external device like a USB drive. Following this pattern, "sdc", "sdd", and so on represent the third, fourth, and subsequent SCSI devices in the system, respectively.
```

```reStructuredText
sr0:
In the Linux system, "sr0" is a naming convention used to represent optical disc drives. It typically denotes the first optical disc drive in the system, where:

- "sr": Represents SCSI CD-ROM devices. Despite being referred to as SCSI devices, they may not necessarily be true SCSI devices but rather follow a naming convention.
- "0": Represents the device's identifier, starting from 0.

Therefore, "sr0" signifies the first CD-ROM or DVD-ROM drive in the system.
```

```reStructuredText
nvme0n1p1:
nvme0n1 is a naming convention used in the Linux system to represent NVMe (Non-Volatile Memory Express) devices. NVMe is an interface and protocol designed for connecting high-performance solid-state drives (SSDs). nvme0n1 denotes the first NVMe device in the system, where:

- nvme: Represents NVMe devices.
- 0: Represents the device's identifier, starting from 0.
- n1: Represents the first namespace (or partition) within the device.
- p1: Represents the first partition within the device.

Therefore, nvme0n1p1 represents the first partition of the first NVMe device in the system (typically an NVMe SSD). If there are multiple NVMe devices in the system, they might be named nvme0n1, nvme1n1, nvme2n1, and so on, following a similar pattern. If the devices have multiple partitions, they might be named nvme0n1p2, nvme0n1p3, and so forth.
```



## Package manager  in versions like fedora

### suggested downloading and installing approach

1. Use `wget` to download the `.rpm` file to the system (or by browser or USB drive):
   ```bash
   wget [-O /path/to/destination/package.rpm] https://example.com/package.rpm
   ```

2. Use the `dnf` command to install the `.rpm` file:
   ```bash
   dnf install package.rpm
   ```

`dnf` will handle dependency resolution during the installation process and retrieve any necessary dependencies from configured software sources. Therefore, this is a convenient method to install `.rpm` files and their dependencies.



### rpm

`rpm` (Red Hat Package Manager) is a low-level tool used to install, upgrade, and remove software packages on RPM-based Linux systems. RPM **operates directly on local .rpm files but does not involve package downloading or dependency resolution**. It is primarily used for direct management of local software packages, **requiring manual resolution of package dependencies**.



### yum

`yum` (Yellowdog Updater Modified) is an advanced package management tool built on top of rpm. It is an **automated package manager** capable of handling package downloads, **dependency resolution**, installation, updates, and removal. yum utilizes pre-configured software repositories to obtain packages and can **automatically resolve dependencies between packages**, making package management more convenient and efficient.



### dnf

`dnf` (Dandified Yum) is **the successor to yum**, designed to be **a replacement for yum**. dnf uses different dependency resolution algorithms and has made improvements in performance, stability, and functionality compared to yum. It provides faster package management capabilities and is easier to use.



###  comparation

#### rpm & yum

Compared to rpm, **yum has an additional feature of automatically resolving dependencies**. The method yum uses to resolve dependencies is by automatically downloading them.



#### rpm & wget

- Wget is a command-line utility used to retrieve files from web servers using HTTP, HTTPS, FTP, and FTPS protocols.
- It is commonly used to download files, including software packages, from the internet to a local system.



## Environment variables

