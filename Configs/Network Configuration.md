# Network Configuration



###### \# Internal Networks

* lab-clients | 192.168.10.0/24
* lab servers | 192.168.20.0/24



###### \# Devices

* ubuntu-lab-client: 192.168.10.10 (DHCP Reservation)
* ubuntu-lab-server: 192.168.20.10 (Static)



###### \# Router (pfSense)

* Hostname: pfsense-lab-router
* Domain: lab.lan
* WAN Address: 10.0.2.15
* WAN Default Gateway: 10.0.2.2

###### 

###### \# DHCP

* lab-clients DHCP Pool: 192.168.10.100 - 192.168.10.199



###### \# DNS

* DNS Servers:

\- Primary: 1.1.1.1

\- Secondary: 8.8.8.8

* lab-clients Resolver: 192.168.10.1
* lab-servers Resolver: 192.168.20.1



###### \# Firewall Rules (lab-clients)



|DESCRIPTION|SOURCE|DESTINATION|PROTOCOL + PORT|
|-|-|-|-|
|Anti-Lockout|Any|CLIENTS address|Any/80|
|Allow DNS|CLIENTS subnets|This Firewall (self)|TCP/UDP/53|
|Allow HTTP to Apache Server|CLIENTS subnets|192.168.20.10|TCP/80|
|Block Any to SERVERS|CLIENTS subnets|SERVERS subnets|Any|
|Allow HTTP to Internet|CLIENTS subnets|Any|TCP/80|
|Allow HTTPS to Internet|CLIENTS subnets|Any|TCP/443|
|Allow Internal Traffic|CLIENTS subnets|CLIENTS subnets|Any|
|Allow Any ICMP|CLIENTS subnets|Any|ICMP|
|Block Any ICMP \[DISABLED]|CLIENTS subnets|Any|ICMP|
|Default Allow LAN IPv4 to Any \[DISABLED]|CLIENTS subnets|Any|Any|
|Default Allow LAN IPv6 to Any \[DISABLED]|CLIENTS subnets|Any|Any|



###### \# Firewall Rules (lab-servers)



|Allow DNS|SERVERS subnets|This Firewall (self)|TCP/UDP/53|
|-|-|-|-|
|Allow HTTP to Internet|SERVERS subnets|Any|TCP/80|
|Allow HTTPS to Internet|SERVERS subnets|Any|TCP/443|
|Allow Any ICMP|SERVERS subnets|Any|ICMP|
|Block Any to CLIENTS|SERVERS subnets|CLIENTS subnets|Any|
|Allow Internal Traffic|SERVERS subnets|SERVERS subnets|Any|
|Block Any ICMP \[DISABLED]|SERVERS subnets|Any|ICMP|
|Default Allow LAN IPv4 to Any \[DISABLED]|SERVERS subnets|Any|Any|
|Default Allow LAN IPv6 to Any \[DISABLED]|SERVERS subnets|Any|Any|



