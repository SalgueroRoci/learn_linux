## What is Operating System
To understand what is OS, you need to understand hardware and how programs are ran on hardwares.
Here we use SCM (Single Chip Microcomputer) as an example.
How can multiple programs run on one chip?
Even if we have multiple programs running, how can we stop them intervene each others' memory?
How do we manage files?
What about interrupts?

Now we need something to operate these 'resources', which introduces us into Operating Systems.

### Kernel
To my understanding, kernel is the most essential part of an OS, which includes all necessary functions to "operate" the resources. But this is just a simple and partial description, you can read this.
[What is kernel](https://stackoverflow.com/questions/2013937/what-is-an-os-kernel-how-does-it-differ-from-an-operating-system)


### Shell
After you have a kernel, how would you interact with it? When you want to send commands to the kernel, you have your very OG user interface ---- the shell.
* [What is shell?](http://linuxcommand.org/lc3_lts0010.php)

### Boot Process
![boot image](./images/bootProcess.png)
Linux startup init services   
Boot loader both in kernel and initial RAM (initramfs) into memory so it can be used directly by the kernel    

### Linux Filesystem Overview

Hierarchy of directories (tree) used to organize files on a compute system
Filesystem Hierarchy Standard (FHS)   
Root directory top of the hierarchy which contains all other directories on the system Multiple drives and/or partitions are mounted as directories in the single filesystem (HDD)   Case-sensitive    
Conventional disk file systems: ext2/3/4, XFS, Btrfs, JFS, NTFS etc.  
Other database: flash etc  
![boot image](./images/filesystem.png)

Root directory marks the beginning /root or /
* Contains all the required executables and libraries to boot linux afterwards all other filesystems are mounted on the defined mount points
* /home - all users are placed under
* /bin directory contains executable binaries used to boot the system and essential command used by all users
* /sbin intended for essential binaries related to sys admin (fsck and shutdown) * /proc virtual files to view kernel data
* /dev contains device nodes used by most hardware and software devices (except network)
* /var contains files that are expected to change in size and content as the system is running (variables)
* /etc - directory is the home for the system config files
* /boot directory contains the few essentials files needed to boot the system Removable media such as USE drives and CD etc show up as mounted

### Linux Command Line 
* Sudo: to provide user the admin privileges when required. Allows users to run programs using the security privileges of another user,, generally root (superuser ) 
* Common:
https://maker.pro/linux/tutorial/basic-linux-commands-for-beginners http://www.pixelbeat.org/cmdline.html

Daemons - a computer program that runs as a background process, rather than being under the direct control of an interactive user
Kernel - Lowest level component between hardware and OS
Services - App or set of apps that runs in the background waiting to be used or carrying out essential tasks.

### Popular Distros, each has different package managers:
* Debian (Ubuntu, Linux MINT) = Debian Packages
* RedHat (Fedora, Mandriva, Oracle Linux) = RPM Packages Slackware Linux (SUSE)
* Enoch (Chrome OS)
* Arch (Arch Linux)
* Android