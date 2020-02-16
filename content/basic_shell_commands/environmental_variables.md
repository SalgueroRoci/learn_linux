Setting Environmental Variables
virtual location of the program and the resources available to it. Useful for multiple
programs, for one use program configuration
echo <variable> : shows the value of the variable. Example echo $SHELL shows the current shell location.
echo $PATH : path environment
example: export PATH=$PATH:/opt/bin
Common Variables: USER, SHELL, PWD, HOSTNAME, PATH, HOME, LD_LIBRARY_PATH, PS1, PAGER, NNTPSERVER, TERM, DISPLAY, EDITOR, PRINTER

View your environment variables:
env | less
set | less
<Variable name>=“value” : create a variable for the environment echo $<variable name>
export $<variable name> : will be exported to all environments but will vanish when you log out machine.

