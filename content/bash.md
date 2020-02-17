## Using Shell Scripts

Are plain text files and begin with:
```
#!/bin/sh 
```

The first two characters are a special code that tells the Linux kernel that this is a script and to use the rest of the line as a pathname to the program that’s to interpret the script.  

For shell scripts you need to modify to be executable using chmod. 
To run: ./<filename> or bash <filename> or sh <filename>
```
$ chmod +x mybash.sh
$ ./mybash
$ sh mybash.sh
``` 

Following command you can run remote command to another user:  
`sudo runuser -l root -c 'sudo echo JAVA_HOME="/home/opc/jdk1.8.0_191" >> /etc/environment;sudo echo APP_JAVA_HOME="/home/opc/jdk1.8.0_191" >> /etc/environment'`

Reference
https://bash.cyberciti.biz/guide/Main_Page
