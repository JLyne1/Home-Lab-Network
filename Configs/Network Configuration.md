# Network Configuration



###### \# Internal Network

Hostname: lab-net

Subnet: 192.168.1.0/24



###### \# Devices

ubuntu-lab-server: 192.168.1.10

ubuntu-lab-client: 192.168.1.20 (DHCP reservation)



###### \# pfSense Configuration

Hostname: pfsense-lab-router

Domain: lab.lan

LAN IP: 192.168.1.1 (Gateway)

DHCP Pool: 192.168.1.100 - 192.168.1.199

DNS Servers: 1.1.1.1; 8.8.8.8

