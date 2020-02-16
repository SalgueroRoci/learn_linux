# Network
netstat - Monitor your network stats. Use grep to find a particular item netstat -tupnl | grep <port number>
Ways to check what ports are running and what process IDs

netstat -rn : should ip, and gateway.
dladm show-dev (solaris only?) : shows the speed of the network https://www.binarytides.com/linux-commands-monitor-network/ : other ways to find speed of network.


wget : Enables to retrieve document and store it locally, similar to cp command. --spider does not download the files and returns zero is resource found, or non-zero is not found. echo $? to see the results
curl : Designed to transfer files to/from servers. Default though curl just displays the retrieved file.

Networking Check Ports open lsof -i -P -n | grep LISTEN

Make sure bastion server allows the port forwarding open !!!
Firewalld version
https://www.thegeekdiary.com/5-useful-examples-of-firewall-cmd-command/
https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-using-firewalld- on-centos-7
firewall-cmd --list-all-zones
firewall-cmd --permanent --add-port=[YOUR PORT]/tcp
firewall-cmd --reload
Sudo firewall-cmd —zone=public — permanent —add-port=7001/tcp

Netstate -tupnl |grep 7001
#server running on that port number

ifconfig | grep "inet " | grep -v 127.0.0.1

tcpdump

https://www.hostinger.com/tutorials/iptables-tutorial
sudo yum install iptables
sudo iptables -L -v
sudo iptables -A INPUT -p tcp --dport 22 -s -j DROP

ifconfig - Can be used to check the network interface is up and running.
If ifconfig shows that your network interface is up but you can’t seem to access the network, try using an IP address rather than a hostname. (You can use host on another computer to look up a hostname, or you can try your router’s IP address.) If you can access a system by IP address but not by hostname, then the problem almost certainly lies with your DNS configuration—or perhaps your DNS server is down.
ping - Used for testing basic connectivity. Sends a simple packey to the system you name and waits for a response.
ping -c <n> : can ping certain amount of packets
By pinging systems on both local and remote networks, you can isolate where a network problem occurs. For instance, if you can ping local systems but not remote systems, the problem is most probably in your router configuration. If you can ping by IP address but not by name, the problem is with your DNS configuration.
Some computers are configured to ignore ping requests.
traceroute - Used to see the route of the packet. Sends a series of test packets to each computer between your system and specified target system.
traceroute -n <ip or hostname> : n option tells to display target computers IP addresses rather than hostnames.
As with ping, some routers are configured to drop packets from traceroute. Thus, the traceroute output may indicate dropped packets even though regular network traffic passes through these routers just fine.
netstat - Checking network status.
netstat -i : Returns info on network interfaces similar to ifconfig. netstat -r : returns the route table
Name Server Troubling
nslookup , host , dig - All can be used if you want to use another name server for testing the DNS.

hostname - can display the local machines hostname
telnet - Simple text-mode remote login program. Enables to connect to a remote system and run test-mode programs on it. (unencrypted and not recommended to use) instead use ssh
Still remains useful for connecting since you can pass a port number ei. telnet mail.example.com 25
Telnet isnt useful for protocols using UDP

In /etc/services - lists service names and the ports which they’re associated. Common ports to know:
20/21 FTP (file transfer protocol) 22 SSH (Secure Shell)
23 Telnet
25 SMTP
53 DNS
67 DHCP
69 TFTP
80 HTTP
109/110 POP
113 auth/ident
389 LDAP
443 HTTPS
3306 MYSQL
5800-5899 VNC via HTTP
