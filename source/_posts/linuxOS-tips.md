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

 ### command line >> lsblk

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

```
nvme0n1p1:
nvme0n1 is a naming convention used in the Linux system to represent NVMe (Non-Volatile Memory Express) devices. NVMe is an interface and protocol designed for connecting high-performance solid-state drives (SSDs). nvme0n1 denotes the first NVMe device in the system, where:

- nvme: Represents NVMe devices.
- 0: Represents the device's identifier, starting from 0.
- n1: Represents the first namespace (or partition) within the device.
- p1: Represents the first partition within the device.

Therefore, nvme0n1p1 represents the first partition of the first NVMe device in the system (typically an NVMe SSD). If there are multiple NVMe devices in the system, they might be named nvme0n1, nvme1n1, nvme2n1, and so on, following a similar pattern. If the devices have multiple partitions, they might be named nvme0n1p2, nvme0n1p3, and so forth.
```



### command line >> mount /dev/sdb1 usb/

```reStructuredText
For instance, make a new directory named usb in current directory, then run " mount    /dev/sdb1    usb/ "
```

```reStructuredText
If user-oriented, run fowllowing commands in order:
umount ./usb
mount /dev/sdb1 -o uid=? gid=? /dev/sdb1 ./usb/
```



### command line >> cp source_file(folder)  destination_folder  [-r]

```reStructuredText
mv source_file(folder) destination_folder
rm file(folder)_name [-r -f -v -i]
```



## How to compress or decompress in linux

### basic infos

```reStructuredText
.tar VS .tar.gz VS .tgz >> 
".tar": This is the most basic archive file format, which bundles multiple files or directories into a single file without compression. Therefore, .tar files are commonly referred to as tarballs or tar archives.

".tar.gz": This is a file format compressed using the gzip compression algorithm on top of the .tar format. It bundles multiple files or directories into a .tar file, which is then compressed using gzip to create a .tar.gz file.

Hence, .tar.gz and .tgz are the same format, with different file extensions, both representing a file that has been bundled with tar and compressed with gzip.
```

### compress

#### using tar and zip

```bash
tar -czvf ./archive.tar.gz /path/to/directory_or_file
```

```reStructuredText
-c: Create a compressed file.
-z: Use gzip compression.
-v: Display detailed output.
-f: Specify the name of the compressed file.

archive.tar.gz: The name of the compressed file.
/path/to/directory_or_file: The directory or file to be compressed.
```

#### Using zip

```bash
zip -r ./archive.zip /path/to/directory_or_file
```

```reStructuredText
-r: Recursively compress directories and their contents.

archive.zip: The name of the compressed file.
/path/to/directory_or_file: The directory or file to be compressed.
```





