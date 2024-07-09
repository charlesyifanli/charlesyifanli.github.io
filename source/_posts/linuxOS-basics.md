---
title: linuxOS-basics
date: 2024-03-08 20:17:10
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

## Set  Vim

create ~/.vimrc

```bash
set nu
```

```bash
. ~/.vimrc
```



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

```reStructuredText
dnf config-manager --add-repo URL+[name].repo
dnf install [name]
[systemctl enable --now [name]]
```

**Or**

1. Use `wget` to download the `.rpm` file to the system (or by browser or **USB drive**):

   ```bash
   wget [-O /path/to/destination/package.rpm] https://example.com/package.rpm
   ```

2. Use the `dnf` command to install the `.rpm` file:

   ```bash
   dnf install package.rpm
   ```

`dnf` will handle dependency resolution during the installation process and retrieve any necessary dependencies from configured software sources. Therefore, this is a convenient method to install `.rpm` files and their dependencies.



### rpm command

```bash
rpm -qa | grep name
```



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

- `Wget` is a command-line utility used to retrieve files from web servers using HTTP, HTTPS, FTP, and FTPS protocols.
- It is commonly used to download files, including software packages, from the internet to a local system.



## Environment variables

### recommended (for instance):

vim /etc/profile

append >> {

export JAVA_HOME=/root/Downloads/jdk1.8.0_181
export PATH=$PATH:$JAVA_HOME/bin
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar

export HADOOP_HOME=/root/Downloads/hadoop-3.2.4
export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin

}



### ~/.bashrc  && /etc/profile

```reStructuredText
`.bashrc` is a user-level configuration file that only affects the Bash environment of the current user. `/etc/profile` is a system-level configuration file that affects the Bash environment for all users.

`.bashrc` is executed when a user starts an interactive Bash shell, whereas `/etc/profile` is executed when a user logs in.

Users can customize their settings in `.bashrc`, while configurations in `/etc/profile` are typically managed by system administrators for consistency across all users.
```



## Copy-paste, move and remove file or folder

```bash
cp source_file(folder)  destination_folder  [-r]
```

```bash
mv source_file(folder) destination_folder

mv demo.txt test.txt //rename the file
```

```bash
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

#### Using tar and gzip:

```
tar -czvf ./archive.tar.gz /path/to/directory_or_file
```

- `-c`: Create a compressed file.
- `-z`: Use gzip compression.
- `-v`: Display detailed output.
- `-f`: Specify the name of the compressed file.
- `archive.tar.gz`: The name of the compressed file.
- `/path/to/directory_or_file`: The directory or file to be compressed.

#### Using zip:

```
zip -r ./archive.zip /path/to/directory_or_file
```

- `-r`: Recursively compress directories and their contents.
- `archive.zip`: The name of the compressed file.
- `/path/to/directory_or_file`: The directory or file to be compressed.



### decompress

#### Using tar and gzip:

```
tar -xzvf ./archive.tar.gz [-C /output]
```

- `-x`: Extract files.
- `-z`: Use gzip decompression.
- `-v`: Display detailed output.
- `-f`: Specify the file to be decompressed.
- `archive.tar.gz`: The name of the file to be decompressed.

#### Using unzip:

```
unzip ./archive.zip [-d /output]
```

- `archive.zip`: The name of the file to be decompressed.



##  Unbind process from current terminal

###  hang up

This method puts the command in the background, but if the terminal is closed, the command may receive the SIGHUP signal and be terminated.

```bash
command &
```



### no hang up

Using the `nohup` command redirects the output of the command to the file `nohup.out`, so even if the terminal is closed, the execution of the command will not be terminated.

``` bash
nohup command &
```



#### however,

When using the `nohup` command to run a process in the background, the `nohup.out` file is created by default in the current working directory. It is used to store the standard output and standard error messages of the process started by the `nohup` command.



#### select output path

```bash
nohup command > /path &
```



#### discard the `nohup.out` file

```bash
nohup command > /dev/null &
```





### kill the process in the background

#### View real-time system process information

```bash
top
```



#### Display the processes:

only current user
all users
detailed process information
a tree-like process list
***a specific process***

```bash
ps
ps -e
ps aux
ps auxf
ps -e | grep process_name
```



#### Close process

```bash
kill pid
```



## Use **vim** in linux

### Set row number

- `:set nu`
- `:set number`

### Enter Insert Mode:

- `i`: Insert text before the cursor.
- `a`: Insert text after the cursor.
- `o`: Open a new line below the current line and switch to insert mode.
- `I`: Insert text before the cursor on the current line.
- `A`: Append text after the cursor on the current line.
- `O`: Open a new line above the current line and switch to insert mode.

### Exit Insert Mode:

- `Esc`: Exit the current insert mode.

###  Save File:

- `:w`: Save the file without exiting Vim.
- `:wq` or `:x`: Save the file and quit Vim.

### Quit Without Saving:

- `:q!`: Quit without saving changes.

### Move Cursor:

- `h`: Move left one character.
- `j`: Move down one line.
- `k`: Move up one line.
- `l`: Move right one character.
- `gg`: Go to the beginning of the file.
- `G`: Go to the end of the file.

### Copy, Cut, and Paste:

- `yy`: Copy the current line.
- `dd`: Cut the current line.
- `p`: Paste the contents of the clipboard after the current position.

### Undo and Redo:

- `u`: Undo the last operation.
- `Ctrl + r`: Redo the last undone operation.

### Search and Replace:

- `/keyword`: Search for the specified keyword.
- `:%s/old/new/g`: Replace all occurrences of `old` with `new` throughout the file.

***It is recommended to use `vim` to edit something and use `less` to look through the text.***



## Allow remote connections using the root user

If you want to allow the root user to log in via SSH using a password, you can modify the `PermitRootLogin` parameter in the `/etc/ssh/sshd_config` file. Set it to `yes` to allow the root user to log in via SSH using a password.

Follow these steps to make the changes:

1. Open a terminal and log in to your server as the root user.
2. Use a text editor such as nano, vim, etc., to open the `/etc/ssh/sshd_config` file. 
3. Find the `PermitRootLogin` line and modify it to:
   ```reStructuredText
   PermitRootLogin yes
   ```
4. Save the file and exit the editor.
5. Reload the SSH service to apply the changes. You can do this by running the following command:
   ```bash
   systemctl reload sshd
   ```



## Permissions

### command

Each permission is represented by a number, ranging from 0 to 7, which represents the combination of read (4), write (2), and execute (1) permissions. 

```bash
chmod 755 file.txt
```

### info

1. **Owner Permissions**: Permissions held by the creator of the file or directory, controlling ownership and permission settings for the file.

2. **Group Permissions**: Specifies the permissions for the user group to which the file belongs. Besides the owner, a group of users is granted the same set of permissions.

3. **Others Permissions**: Specifies permissions for all other users.

These permissions are often represented by a string of characters, such as `rwxr-xr-x`, where:

- The first character represents the file type (`-` indicates a regular file, `d` indicates a directory, and so on).
