# 9 - Network and Configuration
> To learn a lot more about layers (and networks in general), see Andrew S. Tanenbaum and David J. Wetherall’s Computer Networks, 5th edition (Prentice Hall, 2010)

## 9.1 - Network Basics
* host - machine connected to network
* router - host that can move data between networks
* Local area network (LAN) - collection of hosts on the same network
* Wide area network (WAN)

## 9.2 - Packets
* packets - small chunks of data transmitted by a machine
    * header - identifying information such as the source and destination host machines and transmission protocol
    * payload - application data
    * why packets - simultaneous communication to several hosts at once (alternate receiver), easier to compensate for errors in transmission

## 9.3 - Network Layers
* Network stack - set of network layers
* Internet Stack -
    * Application layer - contains language that apps and servers use to communicate; usually a high level protocol like HTTP, TLS, FTP, HTTPS
    * Transport Layer - defines data transmission characteristics of the application layer
        * Includes data integrity checks, src and dest ports, specifications for breaking app data into packets and reassembling them
        * TCP, UDP
    * Network/Internet Layer - defines how packets move from src host to dest host
        * Internet Protocol (IP) - packet transit rule for the internet
        * More examples: IPv4, IPv6, IPX, AppleTalk
    * Physical Layer - defines how to send raw data across a physical medium suchas ethernet or a modem

## 9.4 - The Internet Layer
* Internet layer - 
    * meant to be a software network, not dependent upon a paticular hardware or OS
    * toptology - decentralized; made up of smaller networks called subnets
* Router - a host that connects to multiple subnets; gateway
    * two addresses - local subnet address and link to internet
* IP address - a.b.c.d; dotted-quad sequence more human readable and writable than 4 bytes
    * should be unique across the entire internet but private networks and network address translation (NAT) make this confusing

### 9.4.1 - Viewing IP Addresses
`ip address show` - see addresses active on machine

### 9.4.2 - Subnets
* subnet - connected group of hosts with IP addresses in a paticular range
    * network prefix - part common to all addresses in the subnet
    * subnet mask - marks bit loactions in an IP address that are common to the subnet
    * ex. IP 10.23.2.1 and mask 255.255.255.0, subnet defined as 10.23.2.0/24 meaning first 24 bits are the network adress of the subnet and the remaining 8 bits are for the hosts of the subnet.

### 9.4.3 - Common Subnet Masks and CIDR Notation
* Classless Inter-Domain Routing (CIDR) notation - `10.23.2.0/24`
* basic calculator - `echo "ibase=16; 1A3" | bc` -> `419`

## 9.5 - Routes and the Kernel Routing Table
* Connecting internet subnets is a process of sending data through hosts connected to more than one subnet
* `ip route show` - show routing table; each line of output is a routing rule

## 9.6 - The Default Gateway
* `default` - routing table entry that matches any address on the internet.
    * in CIDR notation, it is `0.0.0.0/0` for IPv4
    * when no other rules match, the default route always does, and the default gateway is where you send messages when there is no other choice.
* how the kernel chooses a route?
    * longest matching destination prefix - default is always last since `/0` is no prefix

## 9.7 - IPv6 Addresses and Networks
* IPv6 address - 128 bits `2001:0db8:0a0b:12f0:0000:0000:0000:8b6e`
    * shortening - leave out leading 0s and only one set of contiguous zero groups can become `::` - `2001:db8:a0b:12f0::8b6e`
* global unicast address - address for host that is valid across the internet
* link local address - `fe80::/10` prefix, followed by an all zero 54 bit network ID, followed by 64 bit interface ID

### 9.7.1 - Viewing IPv6 Configuration on Your System
* `ip -6 address show`
* `ip -6 route show`

### 9.7.2 - Configuring Dual Stack Networks
* Dual stack network - configure hosts and networks to run both IPv4 and IPv6

## 9.8 - Basic ICMP and DNS Tools
* Internet Control Message protocol (ICMP) - helps root out problems with connectivity and routing
    * transport layer protocol, does not carry any true user data and thus no application layer above it
* Domain Name Service (DNS) - maps host names to IP addresses
    * application layer protocol

## 9.8.1 - `ping`
* sends ICMP echo request packets to a host that asks the recipient to return the packet to the sender
* if there is no way to reach the dest, the final router to see the packet will return an ICMP "host unreachable" packet to `ping`

### 9.8,2 - DNS and host
* `host www.example.com`
    * can also use host in reverse - give an IP address to return a host name; not reliable as some IP addresses can be associated with multiple host names and admin of the host needs to manually set up the reverse lookup

## 9.9 - The Physical Layer and Ethernet
* ethernet -
    * all devices have a Media Access Control (MAC) address, sometimes called a hardware address; independent of a host's IP address; ex. `10:78:d2:eb:76:97`
    * devices on an ethernet network send messages in frames which are wrappers around the data containing the origin and destination MAC addresses
    * ethernet does not attempt to go beyond hardware on a single network, but even though a frame cannot leave one physical network, a router can take the data out of a frame, repackage it, and sed it to a host on a different physical network, which is what happens on the internet

## 9.10 - Understanding Kernel Network Interfaces
* kernel network interface - communication standard for linking the physical and internet layers

## 9.11 - Intro to Network Interface Configuration
* Connecting a Linux machine to the internet:
    1. Connect network hardware and ensure kernel has a driver for it. `ip address show` should include an entry for the device.
    2. Perform additional pysical layer setup such as choosing a network name and password
    3. Assign IP addresses and subnets to the kernel network interface
    4. Add any additional routes, including the default gateway.