# Disk Management


## Common commands for disk information

| Command | Description |
|-|-|
|ln [option] source link |creates hard links and soft links (symbolic links) |
| df -h | See all the filesystems in the machine and the mount points. Only shows the logical partitions for the user. Options -k display sotrage in KB, -h will display in GB. |
| fdisk -l | See the sector start and end, blocks, and ID etc. also used to partition. |
| fdisk /dev/sdb |  Also used for partitioning. m for help with command. |
| lsblk | Shows all the logical disks and mount points. | 
| free | Shows the memory info in more human readable format than using /proc/meminfo. Used to show free swap space |
| fsck filesystem | Used to check bugs on a filesystem. |
| parted | used to format the disk. More information [here](https://www.tecmint.com/parted-command-to-create-resize-rescue-linux-disk-partitions/) |


## Devices and File systems
### Partitions
In linux block devices are shown as paths.  
Hard Disks identified as either ATA (/dev/hdx) and SCSI (/dev/sdx)  
| | |
|-|-|
| Primary Partitions | original partition types |
| Extended Partitions | Special type of primary partition that serves as a placeholder for the next type |
| Logical Partitions | Which reside within an extended partition |

**Special /dev/ types:**
| | | 
|-|-|
|/dev/null | device not connected to anything. |
| /dev/zero | file generates an endless stream of 0 values. This is sometimes useful when you want to create a blank file.  
| | Example: dd if=/dev/zero of=empty.file bs=1024 count=1024|
| /dev/random & /dev/urandom | generate streams of random bnumbers based on “noise” from hardware. |
 
### Filesystems
There are different filesystems types that Linuc supports. Most common ones:  
| | |
|-|-|
|EXT4 | Most common linuc file system. Previous ext3, ext2|
|journaling filesystems | file system keeps a record of changes it’s about to make in a special journal log file. Used for unexpected crash. ext3fs and ext4fs are common linux filesystems with journaling. Others: ReiserFS, XFS (extended fs) , JFS (journaled filesystem) |
|FAT (File Allocation Table) | used by DOS and Windows|
|NTFS (New Technology Filesystem) |NTFS is a proprietary journaling file system developed by Microsoft.|

### UUID 
Each filesystem have their own UUID ( Universally unique identifier ) and specified in **/etc/fstab/**.  

__/etc/fstab/__ is used to keep track of filesystems and their corresponding mount point.
[more information](https://www.linux.org/threads/etc-fstab-explained.10901/)
```bash
# Find all UUID in VM:
$ sudo mount -a
$ cat /etc/fstab
> # Swap space
> /dev/sda6  none  swap  defaults  0 0 
>
> # ext filesystem
> UUID=b85df913-580f-461c-844f-546d8cde4646 /home/projects ext4 defaults 0 0
> UUID=e1929239-5087-44b1-9396-53e09db6eb9e /home/backups ext4 defaults 0 0
>
> # /
> UUID=7c08c477-0ed4-4794-b847-982bce578592  /  ext4  errors=remount-ro  0 1
```

## Partitioning

When you attach new block storage to your linux machine, you need to format it, and mount it to be able to use it.  

__Option 1__ Parted. [information here](https://www.tecmint.com/parted-command-to-create-resize-rescue-linux-disk-partitions/)

1. New partition and filesystem:
```bash
# print out the disks available. Look for one not mounted
$ lsblk

# if you want to format the whole disk into 1 partition
$ sudo mkfs.ext4 /dev/sdb 

# Otherwise start parted to partition the disk. /dev/<disk name>
$ sudo parted               # or
$ sudo parted /dev/sda
(parted) print free         # displays all the disks and free space. Type fix for any errors.
(parted) select /dev/sda    # select the right disk to partition if didn't select before
(parted) p                  # creates a new partition. Provide info ex. (primary) , ext2 start, end. Uses megabytes (MB). Can use GB is typed.
(parted) print              # to show the partition and formatting worked.
(parted) quit 
$ sudo mkfs.ext4 /dev/sda4

# show the new partitioned disk
$ lsblk
```

2. Mount Disk
```bash
# Make a new directory 
$ mkdir ~/mnt

# Mount to the directory 
$ mount /dev/sda4 ~/mnt

# check to see if successfully mounted
$ df -h 

# to unmount filesystems
$ umount /dev/sda4
```

3. Add perminantly to fstab for reboots
```bash
# find the UUID of the block volume
$ ls -l /dev/disk/by-uuid

# Add the following to /etc/fstab
$ vi /etc/fstab
> UUID=c607a317-ea9e-46c6-b023-82a7eebcf88a  /home/user/mnt  xfs  defaults,_netdev,_netdev 0 0

# save and exit
```

__Option 2__ Fdisk  
Similar process except using fdisk instead of parted to partition disk 
```bash
$ fdisk /dev/sdb
# prints the partition table 
> Command (m for help): p 

# adds a new partition
> Command (m for help): n 
> primary or extended : 
> First Cylinder : default
> Last Cylinder : +2G  

# writes changes to disk
Command (m for help): w 

# exit / q will quit without saving if needed.
Command (m for help): q 

# add a filesystem 
$ sudo mkfs.ext4 /dev/sdb2

# do steps 2 and 3 from above
```

__Misc__ 
* Resize a Linux Disk - In Parted used resizepart, choose partition number, and size of the new resize.
* Delete a Linux Partition - In Parted use the rm <disk number> to delete a partition.
* Rescue a Linux Partition - rescue utility helps you recover a lost partition between a starting and ending point. If partition between range, it will attempt to restore it

## Swap 
Swap is a space on a disk that is used when the amount of physical RAM memory is full. When a Linux system runs out of RAM, inactive pages are moved from the RAM to the swap space. [x](https://linuxize.com/post/create-a-linux-swap-file/)

### Change Swap size
Steps on how to increase the swap space after the Linux OS has been installed. 

```bash
# Create an empty file used for swap of desired size. 
# Do this by copying bytes from /dev/zero to an empty file. 1 GB file
$ sudo dd if=/dev/zero of=/swapfile bs=1024 count=1000000
      
# Set the correct permissions. Only root user should be able to write/read the swap.
$ sudo chmod 600 /swapfile

# Set up a linux swap area. Init the swap file for use.
# save the UUID 
$ sudo mkswap /swapfile

# Enable the swap to begin using the swap: 
$ sudo swapon /swapfile

# To make the changes permanent change the /etc/fstab append: 
$ vi /etc/fstab
> /swapfile swap swap defaults 0 0          # or
> UUID=998b3800-ab9a-4c3e-82df-ae96aaaac2fa swap swap defaults,_netdev,x-initrd.mount 0 0

# Verify swap status:
$ sudo swapon --show
$ sudo free -h

# Alternative:
# Can create a partition and make a new swap space using: 
$ mkswap <disk>
```

### Swapiness

Set the swapiness [here](http://gentooexperimental.org/~patrick/weblog/archives/2009-11.html#e2009-11-10T20_18_46.txt) 

### Remove Swap file
You can remove the previous swap file to decrease swap. 
```bash
# First Deactivate the swap: 
$ sudo swapoff -v /swapfile 

# Remove the file entry in /etc/fstab:
$ vi /etc/fstab

# Finally delete the actual swap file:
$ sudo rm /swapfile
```

## File Sharing

You can share files between machines even from linux to Windows and vice versa: [info](https://www.howtogeek.com/176471/how-to-share-files-between-windows-and-linux/)