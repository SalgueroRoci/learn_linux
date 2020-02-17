# Network

Common network linux commands for network monitoring, troubleshooting, and configuration.

## Network Monitoring

Find out information on network interface
```bash
# print out network interface card information, such as private ip
$ ifconfig
# Shows private ip of machine
$ ifconfig | grep "inet " | grep -v 127.0.0.1
```

Some programs also run on different ports locally. To check if a port is taken by a program use the following comamnds: 
```bash
# netstat to check if port is being used
$ netstat -vanp tcp | grep 3000

# lsof can also show the PID (process id) running on the port
$ sudo lsof -i tcp:3000 

# can also check which ports are open or connection established
$ lsof -i -P -n | grep LISTEN
$ lsof -i -P -n | grep ESTABLISH

# If you want to terminate the program using the port
$ kill -9 <PID>
```

#### Network Sniffers
If you want to get network information, tcpdump shows packet and traffic information of your machine. 
[tcpdump information](https://www.tecmint.com/12-tcpdump-commands-a-network-sniffer-tool/)

Can also use __WireShark__ to monitor traffic. [link](https://www.wireshark.org/)

## Connectivity
Common network commands to check connectivity between machines. 

#### ping 
Ping is used for testing basic connectivity. Sends a simple packet to the system and waits for a response.

By pinging systems on both local and remote networks, you can isolate where a network problem occurs. For instance, if you can ping local systems but not remote systems, the problem is most probably in your _router configuration._ If you can ping by IP address but not by name, the problem is with your _DNS configuration._   
`ping ip_or_hostname`

#### telnet
telnet is a simple text-mode remote login program. Enables to connect to a remote system and run test-mode programs on it. **(unencrypted and not recommended to use, instead use ssh)**    
Still remains useful for connecting since you can pass a port number. examples:  
```
$ telnet mail.example.com 25
$ telnet host_ip 80 
$ telnet hodt_ip 22
```
* Telnet isnt useful for protocols using UDP
* Useful if ping if disabled or blocked


#### traceroute 
Is used to see the route of the packet. Sends a series of test packets to each computer between your system and specified target system.  
```bash
$ traceroute ip_or_hostname
$ traceroute -n ip or hostname    # n option tells to display target computers IP addresses rather than hostnames.
```
* As with ping, some routers are configured to drop packets from traceroute. Thus, the traceroute output may indicate dropped packets even though regular network traffic passes through these routers just fine.

#### DNS Name Server Troubleshooting
DNS is used to have human friendly names mapped to IPs, rather than having to remember hundreds of ips.  

Our local machines has its own local DNS file. 
```bash
# show the local hostname of the machine
$ hostname  

# Local DNS hostname. Add hostname and ip in the file for local DNS.
$ vi /etc/hostname
> 120.2.1.20  example.com
```

The following commands are useful for troubleshooting DNS
| Command |
| - |
| nslookup |
| host |
| dig |

## WGET and Curl 
|Command|Description|
|-|-|
|wget url_file_download | Enables to retrieve document and store it locally, similar to cp command. Can also use for checking download speed.|  
| wget --spider url_file_download | --spider does not download the files and returns zero is resource found, or non-zero is not found. |
| curl | Designed to transfer files to/from servers. Default though curl just displays the retrieved file. |

## Security

Linux has a firewall that blocks or allows packets based on ip, ports, or both. In order to access certain services such as a website (port 80) then the firewall must allow http traffic.  

**iptables** are firewalls for linux. [Read more about it here](https://www.ibm.com/support/knowledgecenter/STXKQY_5.0.4/com.ibm.spectrum.scale.v5r04.doc/bl1adv_firewallportopenexamples.htm), but common commands here: 

```bash
# install iptables for your OS
$ sudo yum install iptables
$ sudo apt-get install iptables
# check status
$ sudo iptables -L -v

# allow port 80
$ sudo iptables -A INPUT -p tcp --dport 80 -s -j Accept
# restrict port 22
$ sudo iptables -A INPUT -p tcp --dport 22 -j DROP

# filter packets based on source 
$ sudo iptables -A INPUT -s 192.168.1.3 -j ACCEPT
$ sudo iptables -A INPUT -m iprange --src-range 192.168.1.100-192.168.1.200 -j DROP
```

**Firewall-cmd** is another firewall in linux. To read more about it [here.](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-using-firewalld-on-centos-7)

Common firewall-cmd commands
```bash
# Install and show status
$ sudo yum install firewalld
$ sudo firewall-cmd --state
$ sudo firewall-cmd --list-all-zones

# Modify ports allowed 
$ sudo firewall-cmd --permanent --add-port=[YOUR PORT]/tcp
$ sudo firewall-cmd --permanent --add-port=8000/tcp
$ sudo firewall-cmd —zone=public —permanent —add-port=7001/tcp
$ sudo firewall-cmd --zone=public --permanent --add-service=http

# reload and list the ports allowed
$ sudo firewall-cmd --reload
$ sudo firewall-cmd --list-all
```
## Protocols

In __/etc/services__ lists service names and the ports which they’re associated.  
Common ports to know:
| Port Number | Protocol |
|-|-|
|20/21 |FTP (file transfer protocol) |
|22 |SSH (Secure Shell)|
| 23 |Telnet|
| 25 |SMTP |
| 53 |DNS |
| 67 | DHCP| 
| 69 |TFTP|
|80 |HTTP|
|109/110 |POP|
|113 |auth/ident|
|389 |LDAP|
|443 |HTTPS|
|1521| Oracle Database|
|3306 |MYSQL|
|5800-5899 | VNC via HTTP|








 









