# Process

Processes
Look at your processes
ps, ps -ef | grep (like a search tool) cron , ps -auf: searches all the processes similar name to cron
Linux processes have parents and leading back to init the first program that Linux runs.

Ways to check the processes running
ps -u <user> —forest : Shows the process tree for user.
Restricting Processes’s CPU use
nice: to launch the program with a specific priority renice: to alter the priority of the running program example:
nice -12 number-crunch data.txt
nice -n 12 number-crunch data.txt
nice —adjustment=12 number-crunch data.txt renice 7 16580 -u pdavison tbaker
Killing Processes
kill -l : to see the linux signals
kill -s <signal> <pid>
killall <name> : kill all processes with name.
Controlling Foreground and Background Processes Ctrl + Z : stops the process
fg <job id> : Makes the job go onto the foreground bg <job id> :
jobs : shows all the jobs displayed and their numbers
<program starting command> & : will make the program launch to the background.
Unix Nohup: Run a Command or Shell-Script Even after You Logout
Description: When you execute a Unix job in the background (using &, bg command), and logout from the session, your process will get killed. You can avoid this using several methods — executing the job with nohup, or making it as batch job using at, batch or cron command. nohup command-with-options &
nohup command >/dev/null 2>&1 # doesn't create nohup.out https://linux.101hacks.com/unix/nohup-command/

Linux Information and Monitoring
psrinfo (solaris) - Gives you processor information and online for how long. psrinfo -pv (solaris)- gives you more information about the processor lscpu (Linux) - listing out cpu information
/user/sbin/prtconf | head (solaris) : gives you information of memory and processor
Monitoring System Statistics
iostat - Gives you information about the disk. Disk addresses, cpu wait times, and network. Monitory disk input output stats.
vmstat - Gives your information on memory and swap
prstat (not working on oracle linux) - Information about processors and lists by CPU usage.
prstat -Z : displays the Zones and how much cpu each zone is using.

sar - Useful for tracking down the source of system slowdowns. Examine load on memory, CPU, devices, and so on.
install: sudo <packages install like apt-get> install sysstat
edit: edit the file /etc/default/sysstat and change to ENABLED=“true" start: sudo service sysstat start
Check memory usage:
pmap -x <process id>

Chron information
scheduling tasks to run at specified times to handle such issues.
Chron is a daemon, which means that it runs continuously, looking for events that cause it to spring into action.
crontab -l : See all the cron jobs.
crontab -e : to edit the cron job file correctly.
/etc/crontab file controls system cron jobs.