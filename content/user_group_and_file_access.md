# User, Group & File Access

## Managing Users

```zsh
# How to add a user 
$ useradd -m <user name>
$ useradd -m -d <path for home directory> <username>
$ useradd -m -s <shell path> -u <id> <username>

# alternative to adding a user, will ask for information.
$ adduser <username> [--disabled-password] 

# switch users
$ sudo su - <username> 
$ sudo su -

# delete a users
$ userdel 
$ userdel -r <username>

# change user password. Must be root or sudo
$ passwd <username>

# modify the user from username change to lock/unlock passwords 
$ usermod 

# find out who is currently logged in
$ who 
$ w

# find out who's logged into your computer last number of days
last -<number of days>

# show who you're currently logged in as 
$ whoami 

# broadcast the file to all users logged on
$ wall <file name>
```

### User Groups 
Users can also be added to groups. Folders have acces permissions based on groups too.
```bash
# show groups and which groups users are apart of
$ groups
$ groups <username>

# create a new group
$ groupadd <group name>
$ groupadd -g <group ID> <group name>

# modify group
$ groupmod -n <newgroupname> <oldgroupname> 
# change the group password 
$ gpasswd

# add users to group
$ addgroup <username>
$ usermod -G groupa,groupb <username>
```

Certain files manage users, groups, and permissions.
| File | Description |
|-|-|
| /etc/passwd | file has linux users and information. |
| /etc/sudoers | file has all users who have sudo priviledge|
| /etc/group | file contains all linux groups |

#### Sudo  

Sudo allows users to run commands as superuser. Root user having the highest permissions, sudo can grant other users similar superuser access.  

```bash
# add a user to sudoers
$ usermod -aG sudo username
$ tail -n 10 /etc/sudoers
```

## Permissions
Each file and folder has permissions for users, groups, and others.  
* Users - owner of the file / directory. default creator
* Group - all users belonging to group will have access  
* Other - Other users not owners or part of the group   

Example:
```bash
$ ls -l
> drwxr-xr-x  1 <user> <group>  2694 Dec  5 16:42 <filename>
```

| Dir, Link, or File bit | User | Group | Other |
|-|-|-|-|
|d|rwx|r-x|r-x|

**permissions**
* r - read - 1
* w - write - 2
* x -  execute - 4

add the numbers and concet for user , group, others example:  
rwxr-xr-x = (1+2+3)+(1+4)+(1+4) = 755

```bash
# changes the permissions for owner, group, others. Can use numbers from binary numbers or ugo+rwx
$ chmod <permission> <filename> 
$ chmod ugo+r <filename>
$ chmod o+x <filename>
$ chmod 600 <filename>
$ chmod -R +r <directory>           # recursive

# Changes the owner of the file.
$ chown <new owner>:<new group> <filename> 
$ chown user:root <filename>
$ chown -R user:root <directory>    # recursive

# change the group of the file 
$ chgrp <group> <filename> 
```