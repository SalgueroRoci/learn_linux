# Manipulate Files
In Linux, everything is file this includes Configurations, Sockets, Process ids, etc. Hence, knowing how to interact with file system is crucial for you. Here we separate the actions into different categories.

### Creating a folder 
```bash
$ mkdir 

# Creating a folder and it's parent directory if it doesn't exist
$ mkdir -p /grandparent/parent/child

# Create and change folder permission, similar to chmod
$ mkdir -m a=rwx /folder
``` 

## Show Files
### ls
Before we create or remove any file, we need to see what we have in your current working directory.

_ls_ is the command for listing files in your working directory.
### List Contents
List the contents of the directory, options allow to display different information. 

```bash
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
  
**Hidden files**  
The files starting with "."  
You need "-a" to show the hidden fields.

* read about file permissions [here](../user_group_and_file_access.md#Permissions)

## Create Files

### touch
This might be the easiest way to create a file in Linux.
```bash
# touch creates a new file in the current directory
$ touch file

# or create multiple files
$ touch file1 file2 file3
```
* Alternatively, one can use [pipeline redirection](./file.md#TextStreams) or editors([vim](../content/vim.md)) to create a new file.

[Here](http://www.linfo.org/touch.html) is a more detailed instruction of touch.

## Remove

### rm
After you created a file, you should be able to delete it. The command to remove something in the file system is 'rm'.
```bash
# remove one file
$ rm <file name>

# remove multiple files
$ rm <file name 1> <file name 2> <file name 3>

# remove a folder
$ rm -r <folder name>

# remove directories and children
$ rmdir <directory>

# remove files by force, use cautiously
$ rm -f <file name>

```
> __IMPORTANT:__ do double check before you remove things

> __IMPORTANT:__ careful when using rm -rf / not recommended  

## Copy
### cp
You can also copy files and directories.
```bash
# copy files 
$ cp <source file> <target file>
$ cp <source file 1> <source file 2> <target directory>

# copy recursively 
$ cp -R <source directory> <target directory>
```

### pbcopy 
pbcopy can also be used to copy outputs from termincal to clipboard. 
[info](https://www.ostechnix.com/how-to-use-pbcopy-and-pbpaste-commands-on-linux/)
```bash
$ echo "Hello World!" | pbcopy 
$ cat ~/.ssh/id_rsa.pub > pbcopy
$ pbcopy < file_name

```

## Move
### mv
Move files to different directories or locations. 

```bash
# move files to new directory, also used to rename a file
$ mv <source> <target>
$ mv <orig_file> <new_file>
$ mv <directory> <new destination>

# can also move multiple directories
$ mv -v dir1 dir2 <destination_path> 

```

## Read
### cat
Concatenate and print files
```bash
# to simply print a file
$ cat file

# to concatenate files
$ cat file1 file2
# to concatenate files and save them to a new file 
$ cat file1 file2 > file3

# write to a file until using EOF signal, ctrl + d. Everything willed be saved onto the file
$ cat > file 
``` 
There are other tools to help read long files, especially log files. The following will show common commands for each.

### less
Helps you read files in chunks. View the file without opening.
```bash
$ less <filename> 

# press 'f' will let your read more. 
# press 'b' move page up
# press 'g' move to the beginning 
# type /<pattern> to find a pattern/word in the file
# press 'q' to quit
```

### more
more is primitive version of less
```bash
$ more <filename> 
```

### head
head only prints out the top of the file
```bash
# print the first 10 lines
$ head <filename>

# print n numbers of lines
$ head -n <num> <filename>

# print lines from 10 to 15. head prints 15 lines, pipe to tail to print lines after line 10
$ head -n 15 agatha.txt | tail -n +10
```

### tail
tail prints out the ending of a file

```bash
# prints the last ten lines
$ tail -f

# print N last number of lines
$ tail -n <num> <filename>

# monitor files in realtime and will auto update
$ tail -f <filename>

# can also see last lines form outputs of other commands
$ ls -latr | tail -n3
``` 

## TextStreams
We've been using standard outputs/inputs with commands to "pass" commands to other linux commands. The following shows stdout > or |, stdin < , and strerr &>  

__stdout__  
```bash
# > redirection operator 
$ echo Hello World > file.txt 
$ ls /path/directory > directory.txt  


# >> will append to the file instead of overriding it
$ cat file1.txt >> file2.txt 

# pipe also get output of command and input into a new command (stdin)
$ ls -la /etc | less 
```
__stdin__
```bash
# redirected to cat then banana.txt
$ cat < peanuts.txt > banana.txt 
```
__stderr__ 
```bash
# redirects any errors to the file using &
$ ls /fake/directory &> peanuts.txt 
```

## Archive Files
Unarchive and archive files that are zip, and tar
```bash
$ tar --extract --verbose --gunzip --file samba-3.2.11.tar.gz 
$ tar xvzf samba-3.2.11.tar.gz

# making a tar file
$ tar cvzf my-stuff.tgz my-stuff-dir 

$ unzip archive.zip
```

## Advanced File Manipulation
The following commands help with more advanced file manipulations.

|command | description|
|-|-|
|cut| helps with cutting out text from a file|
|sort| sort in alphabetical order, combined with uniq to show unique values|
|uniq| removes duplicates in a file and can count with -c flag|
|join| joins files based on a common column field|
|paste| command is similar to the cat command, it merges lines together in a file|
|split| split files into smaller parts |
|wc and nl| outputs word count and number lines|
|**grep**| used to search files and outputs. Common for pipe outputs from other commands|
|tr| translate |
|sed| stream editor used fro find and replace|

following are common examples: 
```bash
# show only text files
$ ls /directory | grep '.txt$'
$ ls /directory | grep -i '.TXT$'   # not text sensitive

# Cut by delimiter for a file - cut -d[separator] -f1 [file name]
# cat the file, and cut out the usernames, and show line numbers called usernames
$ cat /etc/passwd | cut -d: -f1 | nl > usernames 
$ cat /etc/passwd | cut -d: -f5 | nl > fullnames

# find a specific user exists
$ cat /etc/passwd | grep -i <user>

# output the word count of file
$ wc -w testfile

#will convert all lowercase to uppercase
$ cat file.txt | tr a-z A-Z  

# substitute values in a file
$ cat file.txt | sed s/[value to replace]/[value to replace with]

# output unique values in a file
$ sort file.txt | uniq 

# get the fifth line and output the second word in a space sperated file.txt
$ head -n 5 file.txt | tail -n +5 | cut -d ' ' -f2
```
 




 



