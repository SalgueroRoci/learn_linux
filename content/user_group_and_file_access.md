# User, Group & File Access
Managing Users
How to add a user
useradd -m <user name>
useradd -m -d <path for home directory> <username>
adduser <username> [--disabled-password] :alternative to adding a user, will ask for information.
groupadd <group name>
sudo su - <username> : Used to switch users.
userdel : delete a user. userdel -r <username>
passwd <username>: changes the password of the user on their behalf must be root. usermod : Can be used to modify the user from username change to lock/unlock passwords groupmod [-n newgroupname] <oldgroupname> : modifies existing groups s
gpasswd : Way to add a user to a group without affecting existing group memberships. changes the group password
chage : enables you to modify account settings relating to account expiration. Two conditions: passwords change in specified time, or a specified system date for a predetermined time.
chage [-l] [-m mindays] [-M maxdays] [-d lastday] [-I inactivedays]➥ [-E expiredate] [-W warndays] username


who or w: Displays info on who is currently logged in.
last -<num> : Find out whos logged into your computer last number of days. whoami : Displays who you're currently logged in as.


User Definitions
    
                 
User Private Groups : scheme is used by RedHat and other distros. Creates a one-to-one mapping of users and groups. When a new user is added a new group is created.
Project Groups: Create a group for a specific purpose
Shadow: Message Digest 5 (MD5) $1$ or Secure Hash Algorithm (SHA) $5$ or $6$
/etc/pam.d/passwd file controls the Pluggable Authentication Modules (PAM) configuration for the passwd utility.

Check the run level of your machine
who -r : to see run level.
reboot: to reboot your machine.
wall <file name> -a (no -a): broadcast the file to all users logged on.

