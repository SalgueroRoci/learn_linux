ln [option] <source> <link> : creates hard links and soft links (symbolic links)

Managing Disks
Tutorial: https://www.tecmint.com/parted-command-to-create-resize-rescue-linux-disk- partitions/
Create a Partition
1. Create Partition:
df -k (kilo) -h (giga) : See all the filesystems in the machine and the mount points. Only shows the logical partitions for the user.
fdisk -l : See the sector start and end, blocks, and ID etc. also used to partition
fdisk /dev/sdb - Also used for partitioning. m for commands.
lsblk : Shows all the logical disks and mount points
free: Shows the memory info in more human readable format than using /proc/meminfo. Used to show free swap space
fsck <filesystem> : Used to check bugs on a filesystem.
(Linux) parted : used to format the disk.
Create a new partition:
print/print free : displays all the disks and free space
select <disk> : select the right disk to partition
mkpart : creates a new partition. Provide info ex. (primary) , ext2 start, end. Uses
megabytes (MB). Can use GB is typed.
print : to show the partition and formatting worked.

Exit quit -> then
Next:
2. Create file system :
1. mkfs.ext4 <disk> : Used to format the disk , in this case formats to extension
type and creates a file system for it
1. Check to see if the partition is created using (parted) print
2. lsblk : Quit and check for listed disks
3. Make directory to mount to
1. mkdir <new directory>
2. mount <block-device> </mount/point>
3. df -h to check successful mount
4. umount to unmount filesystems
5. cat /etc/fstab edit to mount the filesystem on each reboot
——— —
Resize a Linux Disk
1. In Parted used resizepart, choose partition number, and size of the new resize.
Delete a Linux Partition
1. In Parted use the rm <disk number> to delete a partition.
Rescue a Linus Partition
1. rescue utility helps you recover a lost partition between a starting and ending point. If partition between range, it will attempt to restore it
Change Partition Flag
1. Use set command within partition: set <partition number> <flag name> <on or off>
——— —
Create a swap file
1. Create an empty file used for swap of desired size. Do this by copying bytes from /dev/zero to an empty file.
sudo dd if=/dev/zero of=/swapfile bs=1024 count=1000000
      
2. Set the correct permissions. Only root user should be able to write/read the swap: sudo chmod 600 /swapfile
3. Set up a linux swap area. Init the swap file for use: sudo mkswap /swapfile
4. Enable the swap to begin using the swap: sudo swapon /swapfile
5. To make the changes permanent change the /etc/fstab append: /swapfile swap swap defaults 0 0
6. Verify swap status:
sudo swapon --show
sudo free -h
Alternative:
1. Can create a partition and make a new swap space using: mkswap <disk>
Set the swapiness: https://linuxize.com/post/create-a-linux-swap-file/ Remove Swap file
1. First Deactivate the swap: sudo swapoff -v /swapfile
2. Remove the file entry in /etc/fstab.
3. Finally delete the actual swap file:
sudo rm /swapfile

Change swap size on linux
https://www.techpaste.com/2016/07/increase-swap-space-linux/
Using Fdisk to partition
fdisk <disk>
Command (m for help): p - prints the partition table Command (m for help): n - adds a new partition
L - Asks for logical or primary
First Cylinder : default
Last Cylinder: +2G - size of the partition
Command (m for help): w - writes changes to disk and exit Command (m for help): q - will quit without saving if needed.
Using GNU Parted to Create Partitions
parted <disk>
(parted) print - prints the disks and partition tables
(parted) mkpartfs - used to make a file system. Will ask for partition type, file system type, and start, end. Unlike fdisk which uses cylinders, parted uses Bytes for size calculations.

Creating new File Systems
Also known as formatting a partition. fdisk doesn’t format you can use mkfs tool to format. mkfs.ext3 <disk> or mkfs.fstype
mkdosfs for FAT partition

Device Files
/dev/null : device not connected to anything.
/dev/zero : file generates an endless stream of 0 values. This is sometimes useful when you want to create a blank file.
Example: dd if=/dev/zero of=empty.file bs=1024 count=1024
/dev/random & /dev/urandom : generate streams of random bnumbers based on “noise” from hardware.
(very old systems) mknod <name> <type b: block c /u : char device , p : FIFO> : used to make a file system.
—— —
Hard Disks identified as either ATA (/dev/hdx) and SCSI (/dev/sdx)
Primary Partitions : original partition types
Extended Partitions : Special type of primary partition that serves as a placeholder for the next type
Logical Partitions : Which reside within an extended partition.

RAID (Redundant Array of Independant Disks : partitions on a separate physical hard disks are combined together to provide faster performance, greater reliability, or both.
Types of RAID:
Linear (append) : Combine partitions from multiple hard disks into a larger virtual partition. RAID 0 (striping): Similar to linear but interleaf between physical disks - combined partition consists of small strips of each disk.
RAID 1 (mirroring) : array uses one disk to exactly duplicate the data on another disk—when you write data to the first disk, the data is actually written to both disks.
RAID 4/5/6: These RAID types combine the features of RAID 0 and RAID 1: they spread data across multiple disks and provide redundancy.


journaling filesystems : file system keeps a record of changes it’s about to make in a special journal log file. Used for unexpected crash. ext3fs and ext4fs are common linux filesystems with journaling. Others: ReiserFS, XFS (extended fs) , JFS (journaled filesystem)
FAT (File Allocation Table) - used by DOS and Windows
NTFS (New Technology Filesystem) , HPFS, UFS, HFS, UDF

Find all UUID in VM:
— — - — — — —-
How to Manage and Create LVM Using vgcreate, lvcreate and lvextend Command
https://www.tecmint.com/manage-and-create-lvm-parition-using-vgcreate-lvcreate-and- lvextend/
Logical Volume Management - Allows logical divisions to be resized (reduced or increased)

Structure:
One or more entire HD are configured as physical volumes
Volume group is created using one or more physical volumes. VG as a single storage unit
Multiple logical volumes can be
Creating Physical Volumes, Volume Groups, and Logical Volumes
Physical volumes :
pvcreate /dev/sdb /dev/sdc - creates a new physical volume pvs lists newly created PVs
pvdisplay /dev/sdX - get detaild info of each PV
To create a volume group named vg00 using /dev/sdX vgcreate vg00 /dev/sdb
vgdisplay vg00 - view information about this volume group
Logical Volumes
lvcreate -n vol_projects -L 10G vg00 lvcreate -n vol_backups -l 100%FREE vg00 lvs - list logical volumes with basic info lvdisplay - for more detailed information lvdisplay vg00/vol_projects

Next we can make filesystem as ext4 since it allows resizing. mkfs.ext4 /dev/vg00/vol_projects
mkfs.ext4 /dev/vg00/vol_backups
Resizing Logical Volumes/Extending
Example on resizing to have vol_backups have more space while reducing vol_projects
# lvreduce -L -2.5G -r /dev/vg00/vol_projects
# lvextend -l +100%FREE -r /dev/vg00/vol_backups
The - and + while resizing logical volumes.
vgextend vg00 /dev/sdd
vgdisplay vg00 - Will show the new extension
Mounting LV on Boot and on Demand Requires UUID. To get the UUID use
blkid /dev/vg00/vol_projects blkid /dev/vg00/vol_backups
Create the mount points for each LV mkdir /home/projects
mkdir /home/backups
   
Edit the fstab file
UUID=b85df913-580f-461c-844f-546d8cde4646 /home/projects ext4 defaults 0 0 UUID=e1929239-5087-44b1-9396-53e09db6eb9e /home/backups ext4 defaults 0 0
mount -a

Mounting a Disk to instance
iSCSI commands
See disks attached: lsblk
Create file system: fdisk -l
Mkfs -t ext4 /dev/sdb
Create directory: mkdir /mnt/home
Mounting device: mount /dev/sdb /mnt/home