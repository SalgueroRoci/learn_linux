# Manipulate Files
In Linux, everything is file this includes Configurations, Sockets, Process ids, etc. Hence, knowing how to interact with file system is crucial for you. Here we separate the actions into different categories.

### Creating a folder 
```
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

**Hidden files**  
The files starting with "."  
You need "-a" to show the hidden fields.

## File Management

### touch
This might be the easiest way to create a file in Linux.
```
# usage
touch file
# or
touch file1 file2 file3
```
Alternatively, one can use [pipeline redirection](../content/pipeline.md) or editors([vim](../content/vim.md)) to create a new file.

[Here](http://www.linfo.org/touch.html) is a more detailed instruction of touch.

## Remove

### rm
After you created a file, you should be able to delete it. The command to remove something in the file system is 'rm'.
```
# usage
# to remove one file
rm <file name>
# to remove multiple files
rm <file name 1> <file name 2> <file name 3>
# to remove a folder
rm -r <folder name>
```
> __IMPORTANT:__ do double check before you remove things

> __IMPORTANT:__ do not do rm -rf /
rm - remove a file. rm -rf (recursive/forced) or rmdir to remove directories
rmdir 

## Copy
### cp
```
# usage
cp <source file> <target file>
cp <source file 1> <source file 2> <target directory>
# copy recursively 
cp -R <source directory> <target directory>
```

## Move
### mv
```
mv source target
mv source ... directory
mv <source> <destination> - used to move to rename the file into something new.
```

## Read
### cat
Concatenate and print files
```
# usage
# to simply print a file
cat file
# to concatenate files
cat file1 file2
# to concatenate files and save them to a new file 
cat file1 file2 > file3

# ctrl + d is the EOF signal, so you can use this
cat > file
# you can copy paste your file to the stdin at this time and hit ctrl + d to have everything casted into the file
```
### pbcopy 

here we mentioned [pipeline redirection](), you can click on the link to 
### less
http://man7.org/linux/man-pages/man1/less.1.html
### head
http://man7.org/linux/man-pages/man1/head.1.html
### tail
http://man7.org/linux/man-pages/man1/tail.1.html
```
# usage
# this is very useful for reading logs
tail -f
```
more <filename> : results in a screen by screen display of filenames contents.
less <filename> : view the file instead of opening. Pressing F will let your read more of the end of file. :e <nonexistant filename> will reload current file.
tail -n <filepath> : View the last 10 lines of a file.
tail -f <file path> : Will auto update the output if the file changes.
tail: Shows the last 10 lines. -n to change line amount. -f to follow the file as it grows. expand/unexpand:
file <filename> : shows the file type os the file.

## Archive Files
Zip and Backup Utilities:
Tar files:
tar --extract --verbose --gunzip --file samba-3.2.11.tar.gz : extracting files tar xvzf samba-3.2.11.tar.gz
tar cvzf my-stuff.tgz my-stuff-dir : making a tar file

## Permissions 
chmod <permission> <filename> : changes the permissions for owner, group, others. Can use numbers from binary numbers or ugo+rwx
chown <new owner>:<new group> <filename> : Changes the owner of the file.
chgrp <group> <filename> : change

## Outputs
cat

### More Text Manipulation
stdout: $ echo Hello World > peanuts.txt : > redirection operator >> will append to the file instead of overriding it
stdin: $ cat < peanuts.txt > banana.txt redirected to cat then banana.txt
stderr: $ ls /fake/directory &> peanuts.txt redirects stderr and stdout
$ ls /fake/directory 2> peanuts.txt to redirect stderr to a file peanut.txt

pipe and tee: $ ls -la /etc | less allows us to get the stdout of a command and make that the stdin to another process.

cut: helps with cutting out text from a file


paste: command is similar to the cat command, it merges lines together in a file.

join/split: files
sort: can sort content in text files
tr (translate)
uniq: removes duplicates in a file and can count with -c flag
wc and nl: word count and number lines
grep: used to search files and outputs. Common for commands like $ ls /somedir | grep ‘.txt$’

File commands.
echo [words] > [file name] : can echo and redirect to a file. cat [file name]
wc [file name] : gives you file word count.
wc -w testfile : shows you word count.
nl [file name] : Show line numbers in a file. Similar to the cat command (cat -n) cut -d[separator] -f1 [file name]
   
Advanced:
cat /etc/passwd | cut -d: -f1 | nl > usernames :
cat the file, and cut out the usernames, and show line numbers called usernames
cat /etc/passwd | cut -d: -f5 | nl > fullnames
Join command
and redirect to a file
join [file1] [file2] -j [field number] > joinednames
paste [file1] [file2] > joinednames2: connects both files in separate columns.
expand [file] -t [number of characters] : expands each word to number of characters.
unexpand [filename] -t [character count] : reduce the char count.

Sort command:
sort [file name] : sorts in alphabetical order.
sort [file name] | uniq : to show sorted file and unique only

Separate a file into separate parts:
split -l [number of lines] [file name] [new file name starting number] : Will split a file into separate ones.
Substitute values of a file:
cat birthdays | sed s/[value to replace]/[value to replace with]
Translating characters in a file. Example:
cat [filename] | tr a-z A-Z (will convert all lowercase to uppercase)
To redirect error codes:
cat [filename] >2 [filename] : outputs the error codes only
Append to a file:
cat [filename 1 ] >> [file name2]
Tee command shows the file contents and also creates a new file cat [filename] | tee [output file]

Search in a file:
grep <value> or grep -i <value not case sensitive> cat /etc/passwd | grep -i <value>




