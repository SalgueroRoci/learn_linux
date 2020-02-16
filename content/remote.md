# ssh
[What is SSH](https://www.ssh.com/ssh/protocol/)

 Adding a new user for SSH (AWS)
https://aws.amazon.com/premiumsupport/knowledge-center/new-user-accounts-linux- instance/
sudo adduser <new_user> or sudo adduser <new_user> --disabled-password : create new user
sudo su - <new user> : change to new user
mkdir .ssh : Make an .ssh directory
chmod 700 .ssh : Change the folder permissions
touch .ssh/authorized_keys : create file for keys
chmod 600 .ssh/authorized_keys : change the permission to key file
cat >> .ssh/authorized_keys : Copy and paste your public key onto the instance.

chmod go-rwx <private key>

Remote Access
telnet is the unencrypted remote access utility
ssh (Secure Shell) port 22 - Encrypted way to remotely access your machine.
ssh <username>@<IP or hostname>
ssh -i <path to key file> <username>@<IP or hostname>
ssh -verbose <username>@<IP or hostname> : used to see the outputs of connecting to the server
scp (Secure Copy) port 22 - used to secure copy from a local machine to a remote.
From local to remote: scp <file path> <username>@<hostname or IP>:<remote directory to add it to>
From remote to local: scp <username>@<IP or Hostname>:<text file> ./
sftp (Secure File Transfer Protocol) Port 20/21 - Secure version of ftp also used for file transfer.
sftp [-oPort=custom_port] <username>@<hostname> : then you’ll be prompted with sftp> and have access to put (, get, dir or ls, cd, lcd (change directory on local system), lls (local directory listing), exit and quit.
Use help for more options. Example: put <local file path>
Generating SSH Keys
ssh-keygen -q -t rsa -f ~/.ssh/id_rsa -C ‘’ -N ''
Omitting the -N ‘’ will prompt for password which would be necessary when you access system.
cat id_rsa.client >> authorized_keys : to add your public keys to the remote system. Never share your private key since that is your identification.
       
Using X Programs Remotely
Setting up for X11 Port forwarding for GUI Programs
Use xTerm or xQuartz
#Set display variable =========
# the variable should auto set
# when you ssh -Y oracle@ip
sudo yum install unzip bind-utils bc rng-tools xauth xterm xdpyinfo dbus-x11 -y
# Enable X11 forwarding in /etc/ssh/sshd_config sudo grep ‘^X11’ /etc/ssh/sshd_config
# these should be the settings
# X11Forwarding yes
# X11UseLocalhost no
# if you don’t get above settings, edit sshd_config sudo vi /etc/ssh/sshd_config
# reload
sudo systemctl reload sshd
ps -ef | grep sshd
# use the pid from above command’s result sudo kill -HUP <pid>
#=======END Set display variable =====
SSH and using GUI based application. Can use this command to enable: ssh -Y <user>@<remote host address>
ssh -XY <user>@<remote host address>
Run Graphical Programs Remotely from a linux server
https://uisapp2.iu.edu/confluence-prd/pages/viewpage.action?pageId=280461906
xterm
install: sudo apt-get update -y sudo apt-get install -y xterm run: ssh -X <user>@<host ip>
xQuartz for Mac similar to xterm.
 Terminal emulator fot the X windows system.
   
Tunneling SSH forwarding / Port forwarding
            
https://www.skyverge.com/blog/how-to-set-up-an-ssh-tunnel-with-putty/ https://medium.com/faun/aws-setup-bastion-host-ssh-tunnel-f5ec5cf10524
How to do this in Putty use a new session: https://blog.avmconsulting.net/posts/2017-11-23-easy-ssh-tunneling-and-port-forwarding/
VNC server One hop no bastion server:
ssh -i <private/key> -L 5901:localhost:5901 opc@<ip address> -N & Browser/VNC: localhost:5901
Mac/Linux version localmachine -> bastion -> app server:
ssh -L 7001:<ebs private IP>:7001 opc@<Bastion server IP>
ssh -L <localport>:<private private IP>:<destination port on application> <user>@<Bastion server IP>
Then navigate to using browser: http://localhost:7001 http://localhost:<localport>

Add SSH Keys
vim ~/.ssh/authorized_keys
cat ~/.ssh/id_rsa.pub | pbcopy

SSL

