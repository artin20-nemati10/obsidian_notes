# Basic Network Configurations
## Basic network config with "ifconfig"
###### Show all (disabled/enabled) network interface cards (NICs):
```
$ ifconfig -a
```
---
###### Disable/Enable network cards:
```
$ ifconfig enp0s8 up or down
```
---
###### Set an IP address, set broadcast & change MAC address of NICs:
```
ifconfig enp0s8 192.168.1.2 netmask 255.255.255.0 up
```
---
###### Assign multiple IP addresses (Aliases) to a single NIC:
```
ifconfig enp0s8:0 192.168.1.3 netamsk 255.255.255.0 up
ifconfig enp0s8:3 down
```
---
## Basic Network config with "ip"
###### Show all (disabled/enabled) network interface cards (NICs):
```
$ ip address show
```
---
###### Disable/Enable network cards:
```
$ ip link set enp0s8 up or down
```
---
###### Set an IP address, set broadcast & change MAC address of NICs:
```
ip address add 192.168.1.2/24 dev enp0s8
```
---
###### Assign multiple IP addresses (Aliases) to a single NIC:
```
ip address add 192.168.1.3/24 dev enp0s8 label enp0s8:1
ip address del 192.168.1.3/24 dev enp0s8 label enp0s8:1
```

## Manage Routing Table with "ifconfig" & "ip"
###### Display routing table of Linux: 
```
route -n
ip route show
```
---
###### Add a static route with a range of IP addresses:
```
route add -net 10.10.20.0/24 gw **10.10.20.1** enp0s8
ip route add 10.10.20.0/24 via **10.10.20.1** dev enp0s8
```
---
###### Add a default gateway route to Linux:
``` 
route add default gw 192.168.1.1 enp0s8
ip route add default via 192.168.1.1 dev enp0s8
```
---

# YAML Introduction
## Why learn YAML?
- Configuration files mostly written YAML.
- Pretty widely used format.
- USed to different DevOps tools & Applications.
---
## What is YAML?
- YAML is a data seialization Language.
#### What is Serialization Language?!
- It means that applications which written with different technologies languages can transfer data to each other using standard formats like, YAML.JSON & XML.
- YAML : Yet Another Markup Language
---
## Yaml Format Comparison
- YAML is super-human-readable and intuitive.
- YAML = Superset of JSON: any valid JsON file is a valid YAML fijle.
- YAML has line sepration & indentations.
---
## YAML Syntax
- Key value pairs:
    -  No difference to use ' or " or none.
    - Just if string has special characters, then use "" needed.
- Comments:
	-  Ech line started with #, will be considered as comment.
- Objects:
	- Each group of key values can be intended into an object.
- Lists:
	- If there are more objects in one group dash can be used.
- Boolean values:
	- In value of each keys can use true/false, yes/no, on/off.

###### Example :
```
artin@host:~# vi /etc/netplan/00-installer-config.yaml
network:
  ethernets:
	ens33:
	  dhcp4: false
	    addresses:
		- 192.168.1.100/24
		gateway4: 192.168.1.1
		nameservers:
	      addresses:
		  - 192.168.1.1
		  - 8.8.8.8
		routes:
		- to: 192.168.1.0/24
		  via: 192.168.1.1
  version: 2
artin@host:~# netplan apply
```

---
# Ping & Traceroute
## Ping & Ping6
###### Use ping command to test the connection of the between two servers:
```
$ ping -c 4 192.168.1.9
$ ping -s 1024 192.168.1.9
$ ping -I ens33 192.168.1.9
$ ping -i 3 192.168.1.9
$ ping -6 ::1
$ ping6 ::1
```
---
## Traceroute & Traceroute6 
###### Use traceroute command to check the route of between two servers:
```
# apt install traceroute
$ traceroute -n www.google.com
$ traceroute -i ens33 192.168.1.9
$ traceroute -p 32 192.168.1.9
$ traceroute -6 ::1
$ traceroute6 ::1
```
---
## Display Current Network Connections -netstat

|      Options      |                         Description                         |
|:-----------------:|:-----------------------------------------------------------:|
|  -p , --program   | Display PID & name of program to which each socket belongs. |
|   -e , --extend   |               Display additional information.               |
|  -n , --numeric   |           Do not resolve hostnames or portnames.            |
|    -t , --tcp     |               Display active TCP connections.               |
|    -u , --udp     |               Display active UDP connections.               |
|    -a , --all     |       Display all listening & non-listening sockets.        |
| -l , --listening  |               Display only listening sockets.               |
| -i , --interfaces |               Display all network interfaces.               |
|   -r , --route    |       Display routing tables (netstat -rn = route -n)       |

```
$ netstat -pentual
$ ss -tulpne
```
---
# DNS Client Configuration
## DNS Client-side Configuration
- DNS is a protocol for converting Name to IP and vice versa.

| DNS Config Files | Description                                                                                                                                                                                                                                  |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| /etc/resolv.conf | Lists nameservers that are used by your host for DNS resolution.<br>If using DHCP, this file automatically filled with DNS records by DHCP.                                                                                                  |
| /etc/hosts       | Mapping between IP addresses & hostnames, for name resolution                                                                                                                                                                                |
| /etc/nsswitch    | It defined order of resolution.<br>Who should it consult first for resolution, a DNS or a host file?<br>For example, if there is hosts: files dns, then /etc/hosts file first will be<br>checked for resolution, then DNS will be consulted. |

---

## DNS Client Tools --> nslookup
###### Use the nslookup tool to map domain name and IP address to each other:
```
$ nslookup sematec-co.com
	Name:
	sematec-co.com
Address: 178.22.121.148
$ nslookup -querytype=mx yahoo.com
$ nslookup -querytype=soa yahoo.com
$ nslookup -querytype=any yahoo.com
$ nslookup miscrosoft.com 8.8.8.8
$ nslookup -debug sematec-co.com
```
---
## DNS Client Tools --> dig
###### Use the newer dig tool to resolve DNS names:
```
$ dig
$ dig sematec-co.com
$ dig sematec-co.com +nostats
$ dig sematec-co.com +short
$ dig yahoo.com MX
$ dig @4.2.2.4 microsoft.com
```
---
## Firewall Configuration
###### Operating firewall management using ufw tool:
```
# apt install ufw
# ufw enable / disable
 ufw default deny incoming
# ufw default allow outgoing
# ufw allow ssh / ftp / http / ...
# ufw status verbose
# ufw delete allow ssh / ftp / http
```
---
# Executing Commands Remotely
## Executing Commands Remotely
- Telnet and FTP are popular remote access and communication services.
- The disadvantage of these two services is the transfer of information in plain text.
- The OpenSSH service is a good alternative to previous services with data encryption.
- The OpenSSH service is a set of tools: SSH, SCP and SFTP.

>[!tip] 
>❖ SSH (Secure Shell) : a tool for remote control of the destination system and commandin the Shell environment.
❖ SCP (Secure Copy) : a tool for copying secure files to a remote system.
❖ SFTP (Secure FTP) : is the same as FTP only with higher security and encryption.

## Install & Start OpenSSH Service (Daemon)
- First we need to install the openssh-server package on our Linux.
- Then after installation, we have to launch its service (Daemon).
###### Deamon management in Linux:
```
# systemctl start sshd
# systemctl stop sshd
# systemctl status sshd
# systemctl restart sshd
# systemctl enable sshd
# systemctl disable sshd
# systemctl mask sshd
# systemctl unmask sshd
```
---
## Transfer Files between Servers (SCP)
###### Transfer files frjom one server to anothe r one with scp command:
```
$ scp <local-file> <username>@<host>:<remote-path>
$ scp test.txt artin@192.168.1.10:/tmp/dir1
```
###### Copy the file from remote machine to the local system in reverse:
```
$ scp <username>@<host>:<remote-path> <local-file>
$ scp artin@192.168.1.10:/tmp/dir1/test.txt /root/dir2
```
---
## Transfet Files between Servers (SFTP)

|  SFTP Command   |                        Description                         |
|:---------------:|:----------------------------------------------------------:|
|       pwd       |             Display current remote directory.              |
|      lpwd       |              Display current local directory.              |
| cd \<dir-name>  |              Change current remote directory.              |
| lcd \<dir-name> |              Change current local directory.               |
|       ls        |          List files in current remote directory.           |
|       lls       |           List files in current local directory.           |
|   get \<file>   | Download \<file> from current remote to current local dir. |
|  mget \<files>  |                  Download multiple files.                  |
|   put \<file>   |        Upload local file to the current remote dir.        |
|  mput \<files>  |  Upload multiple local files to current remote directory.  |
|      exit       |          Close connection to SSH server and exit.          |
# Connect to a Sever without Password
- Using PubKeyAuthentication instead of PasswordAuthentication.
```
$ ssh-keygen
$ ssh-copy-id ububntu@host-2
$ ssh ubuntu@host-2
```