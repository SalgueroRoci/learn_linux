# Environment Variables
Are variables stored in your linux shell, usually to help customize system or ehavior of applications.  

## Setting Environmental Variables
Virtual location of the program and the resources available to it. Useful for multiple
programs, for one use program configuration
```bash
# create a variable for the environment 
$ KEY=value
$ KEY="Some other value"
$ KEY=value1:value2
```
* The names of the variables are case-sensitive. By convention, environment variables should have **UPPER CASE names.**
* When assigning multiple values to the variable they must be separated by the colon : character.
* There is no space around the equals = symbol.
* Common Variables: USER, SHELL, PWD, HOSTNAME, PATH, HOME, LD_LIBRARY_PATH, PS1, PAGER, NNTPSERVER, TERM, DISPLAY, EDITOR, PRINTER

## Exporting Variables
After the Environment Variable been set can display or use: 
```bash
# shows the value of the variable. Example echo $SHELL shows the current shell location.
$ echo <variable> 

# PATH is used to tell shell where to locate executable files
$ echo $PATH 

# The export command is used to set Environment variables
# Will be exported to all environments but will vanish when you log out machine.
$ example: export PATH=$PATH:/opt/bin
$ export PATH="$HOME/bin:$PATH"

# To load the new environment variables into the current shell session use the source
$ source ~/.bashrc
$ source <env variable>
```

View your environment variables:
```bash
$ env | less
$ set | less
```
