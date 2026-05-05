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

