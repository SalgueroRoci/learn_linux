# Navigate
Before we start navigating the file system, we need to have the concept about working directory, file system, as well as physical path and relative path.

## Home Directory
If you start your terminal, you will be in a directory. This directory is your "Home Directory". 
In shell, "~" is used to represent your home directory. 
([Teleport](http://www.linfo.org/home_directory.html))

## Working Directory
After you log into your system, your working directory is your home directory. 
After you navigate to different directories, the working directory will be the directory you are in.   

## Brief Intro to File system
1. Everything in Linux is file.
2. Each file has a path.
3. The file system is like a tree (hierarchical directory structure) with links here and there, but generally a tree.
4. The root (path) of the file system is '/' aka root directory.

## Physical Path and Relative Path
Physical path is the relative path of the file with the root directory (need double check).
|Command | Description|
| ----- |------|
| / | is the root directory or absolute directory|
|~ | is the home directory of the user, users home directory|
| . | current folder. |
| .. or ../ | previous directory, parent directory. |
| ../../ | two folders up. |
| .././ | one folder up and current folder, which in total is one folder up. |
| /usr/../usr/./ | you are actually in /usr/ |

### Other common symbols
| | |
|-|-|
| > or < | redirects to a new command or file. |
| '|' |is pipe to a new command. Output as input. |
| ; | if you want to execute two commands in sequence but don’t want to pipe them together.|

### Wildcards
| | |
|-|-|
| ? | represents a single character|
|* | matches any char or set of characters including no char |

### Shell Types
| | |
|-|-|
| $ or > |for ordinary users |
| # | for root users|

## Commands
These commands will help you move around in shell.
### pwd
Shows your working directory, which is your current directory.

```
user:~$ pwd
/home/usr
```

### cd (change directory)
In order to change your directory, you might want to read [_show files_](./navigate.md/#List-Contents) section in the file section.

Change directory

| | |
|-|-|
| cd - | change to the previous working directory. |
| cd ~ | change to home directory. |
| cd / | change to root directory. |
| cd /some/path | change to /some/path |
| cd .. | change to upper directory |
| cd . | change to current directory |


```
Tip: use tab to auto complete, click tab twice will show you the contents in entered path.
```

### List Contents
List the contents of the directory, options allow to display different information.

```
# outputs folders and files in current directory   
$ ls
# outputs folders and files in /home/user/Downloads directory  
$ ls ~/Downloads
# shows file or directory, size, modified date and time, file or folder name and owner of file and its permission. 
$ ls -l 
> -rw-r--r--. 1 root root   683 Aug 19 09:59 0001.pcap
# shows hidden files in the current directory 
$ ls -a 
# shows sizes in human readable format.
$ ls -lh 
> -rw-r--r--. 1 root root  683 Aug 19 09:59 0001.pcap
# will shows latest modification file or directory date as last. l file info, t time modified, r reverse order
$ ls -ltr
```

### Find Files
Sometimes its hard to find a particular file in linux. Use these commands to locate files.  
Searching
find <location> -name “what to find”
locate <search string>
whereis
grep [option] pattern [file] : helps search in the files or outputs


### Clear your terminal 
Free up your terminal screen using clear
```
 $ clear
```

### Shell Ctrl commands
```
Ctrl + R : reverse search on the shell (ctrl + g to get out) Ctrl + A : Move cursor to front of the line
Ctrl + E : Move to the end of the line
Option + Arrow : Move by word
Ctrl + K : Deletes from cursor to end of line
Ctrl + U: deletes from cursor to beginning of line
ESC + U : Converts all letters form cursor to end of work to upper case ESC + L : for lower case
history : shows the history of the terminal.
```

