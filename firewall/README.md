# Firewall

In computing a firewall is a network security system that monitors and controls incoming and outgoing network 
traffic based on predetermined security rules.

A firewall typically establish a barrier between a trusted network and a untrusted network 
such as internet.

# Type of firewall

1) software firewall:

Such type of firewall is either operating system built in or can be enabled by installing a software in the computer
e.g. antivirus software, total protection software, internet security software etc.

A software firewall is install on an individual computer and it protect that single device. If multiple computer 
need protection, the software must be installed on each device.

2) Hardware firewall:

A hardware firewall is physical device similar to a server that filter traffic to a computer. insted of 
plugging the network cable into the server, it is connected to the firewall, positioning the firewall between 
the uplink and the computer.

Hardware firewall allow you to protect your entire network from the outside world with a single physical device.
this device is installed between your computer network and the internet. A hardware firewall monitors packets of data as they are transmitted.

# Working Of Firewall:

. firewall is used to control incoming & outgoing traffic in any device or network

. firewall decide which traffic come in machine(network) & which can go out of it.

. firewall can be found at every level in any network e.g - computer,router,server and other networking device.

. firewall can also forward packets to next machine(network) which are coming from other machines(network), if your 
  machine working as router.

. Both types of traffic incoming as well as outgoing can be controlled with firewall

. Generally no restrictions are there on outgoing traffic on your machine(pc), by default firewall
  does not block all outgoing traffic. We manage outgoing traffic with the help of proxy server in network.

. firewall controls or restricts all incoming traffic except the traffic that is coming in response 
  of any requests, by default on clients(pc) it does not allow any unattended traffic to come in. it drop such traffic

# firewall zones in linux:

The predefined zones are stored in usr/lib/firewalld/zones directory and can be instantly applied to any
available network interface. These files are copied to the /etc/firewalld/zones/ directory only after they are
modified. the default setting of the predefined zones are as follow:

Block:

Any incoming network connections are rejected with an icmp-host prohibited message for ipv4 and icmp6-adm 
-prohibited for ipv6. only network connection initiated from with in the system are possible.

DmZ:

for computers in your demilitarized zone that are publicly accessible with limited access to your internal 
network. only selected incoming connections are selected

Drop:

Any incoming network packets are dropped without any notifications. only outgoing network connections are possible.

External:

for use on external networks with masquerading enabled, especially for routers. you do not trust the other computers
on the network to not harm your computer. only selected incoming connections are selected.

Home:

for use at home when you mostly trust the other computers on the network. only selected incoming connections are 
selected.

Internal:

for user on internal network when you mostly trust the other computers on the network. only selected incoming 
connections are accepted.

Trusted:

All network connections are accepted.

 

