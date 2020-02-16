# Conventional Paths

Since Unix/Linux systems have existed for decades, users start to form conventions about how to organize files. You might have been confused by /usr/bin or ~/.ssh folders. But do not worry, they are just conventions.

You can read this -> [Conventional Paths](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard)  

Common File System hierarchy  
![boot image](../images/filesystem.png)

| Path | Description |
| - | - |
|/ |(root partition) used by Linux to install and boot. Holds the root directory tree (all files on the computer)  |
|/etc | contains all system related configuration files in here or in its sub-directories. A "configuration file" is defined as a local file used to control the operation of a program | 
| /bin | is a standard subdirectory of the root directory in Unix-like operating systems that contains the executable (i.e., ready to run) programs  |

### Getting Help on a Command:
Many Linux commands have a lot of option flags and usage. To find out information or help page of linux commands use these: 
```bash
<command> --help 
man <command> 
info <command> 
which <command>     # focused search on exactly which command is running.
whereis <command>   # searches in the OS where the command is.
whereis <command>
```

These options can also output help information:  
```bash
<command> -v            # verbose 
<command> --help
<command> --version
```
 
## Alias
In linux if you have certain commands that you use commonly, you can create aliases to create shorter versions of the commands and options. Set up a customized command for the commands or can make an alias for a set of commands.
```bash
# alias <newvalue>='<command>'
alias ls ='ls -la'
# unalias remove alias
unalias ls 
```
