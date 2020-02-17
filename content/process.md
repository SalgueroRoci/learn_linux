# Process

Processes are programs running on your linux machine

### Look at your processes
```bash
$ ps 
$ ps -ef | grep cron        # search if cron is running 
$ ps -auf <process>         # searches all the processes similar name to cron
$ ps -u <user> —forest      # shows the process tree for user.
```

### Killing Processes
```bash
$ kill -l                     # to see the linux signals
$ kill -s <signal> <pid>      # kill a specific process
$ killall <name>              # kill all processes with name.
```

### Background Jobs
When you run a program, so you can use your terminal after running command you can run the process in the background. 

Controlling Foreground and Background Processes  
| Command | Description |
|-|-|
|Ctrl + Z  | stops the process|
| fg <job id> | Makes the job go onto the foreground |
| bg <job id> | Makes the job go onto the background |
| jobs | Shows all the jobs displayed and their numbers|
| <program starting command> & | will make the program launch to the background |
| nohup <command> & | Run a Command or Shell-Script Even after You Logout unlike background which will kill the process after you logout|
| nohup command >/dev/null 2>&1 | Doesn't create nohup.out |


### Monitoring System Statistics
__iostat__ - Gives you information about the disk. Disk addresses, cpu wait times, and network. Monitory disk input output stats.  
__vmstat__ - Gives your information on memory and swap.  
__prstat__ - Information about processors and lists by CPU usage.  
__prstat -Z__ - displays the Zones and how much cpu each zone is using.  
__pmap -x <process id>__ - Check memory usage.  

### Chron information
Cron helps with scheduling tasks to run at specified times to handle such issues.
Chron is a daemon, which means that it runs continuously, looking for events that cause it to spring into action.
```bash
$ crontab -l      # See all the cron jobs.
$ crontab -e      # to edit the cron job file correctly.
$ /etc/crontab    # file controls system cron jobs
```

### Restricting Processes’s CPU use
nice: to launch the program with a specific priority renice: to alter the priority of the running program example:
```bash
nice -12 number-crunch data.txt
nice -n 12 number-crunch data.txt
nice —adjustment=12 number-crunch data.txt renice 7 16580 -u pdavison tbaker
```