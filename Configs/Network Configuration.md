# Network Configuration



###### \# Internal Network

* Hostname: lab-net
* Subnet: 192.168.1.0/24



###### \# Devices

* ubuntu-lab-server: 192.168.1.10 (Static)
* ubuntu-lab-client: 192.168.1.20 (DHCP reservation)



###### \# Router (pfSense)

* Hostname: pfsense-lab-router
* Domain: lab.lan
* LAN IP: 192.168.1.1 (Default gateway)

###### 

###### \# DHCP

* DHCP Pool: 192.168.1.100 - 192.168.1.199
* Reservations: ubuntu-lab-client -> 192.168.1.20



###### \# DNS

* DNS Servers:

\- Primary: 1.1.1.1

\- Secondary: 8.8.8.8

* Resolver: 192.168.1.1 (pfsense-lab-router)



###### \# Firewall Rules (LAN)

1. Anti-Lockout (TCP/80, TCP/443)
2. Allow DNS (TCP/UDP/53)
3. Allow HTTPS (TCP/443)
4. Allow HTTP (TCP/80)
5. Allow Internal Traffic (Within subnet)
6. Block ICMP to Any (Temporary)
7. Default Allow LAN IPv4 to Any (Disabled)
8. Default Allow LAN IPv6 to Any (Disabled)

