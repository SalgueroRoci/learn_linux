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