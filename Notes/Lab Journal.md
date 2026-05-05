# Home-Lab-Network

###### 

###### \# Day 0 (31/3/26):

* Downloaded and installed VirtualBox and GitHub Desktop.
* Downloaded and installed VirtualBox Extension Pack.
* Outlined project goals, tools, and broader project steps in README.





###### \# Day 1 (1/4/26):

* Downloaded Ubuntu v24.04.4 LTS .ISO file.
* Created initial setup of new server VM that runs Ubuntu v24.04.4 LTS. (ubuntu-lab-server)
RAM: 4GB.
CPU: 4 vCPU cores.
Disk: 25GB, dynamically allocated.



* ubuntu-lab-server fully installed.
* Adapter 1 automatically attached to NAT.
* Successfully installed OpenSSH Server for future secure remote access, encrypted communications and authentication.
* Used 'ip a' to confirm device IP address and confirm network connectivity.
* Used 'ping 127.0.0.1' to ping loopback address.
* Used 'ping google.com' to ping google.com to test external connectivity.





###### \# Day 2 (2/4/26):

* Created initial setup of new client VM that runs Ubuntu v24.04.4 LTS. (ubuntu-lab-client)
RAM: 4GB.
CPU: 4 vCPU cores.
Disk: 25GB, dynamically allocated.



* ubuntu-lab-client fully installed.
* Adapter 1 automatically attached to NAT.
* Discovered issue with VM not re-sizing to full screen - See Day 2/Issue 1 in Troubleshooting.
* Successfully installed OpenSSH Client for future secure remote access, encrypted communications and authentication.
* Successfully epeated 'ip a' and ping tests from Day 1 for client.



* In VirtualBox Settings -> Network for both VMs - Changed Adapter 1 from NAT to Internal Network.
* Established lab-net internal network.
* Logged into both VMs and network connection has failed - as expected with the change to internal network.



* Logged onto Server and entered the YAML file in the etc/netplan/ directory.
* Changed renderer from NetworkManager to networkd - networkd is more ideal for smaller, static configurations.
* Disabled DHCP to prevent DHCP attempting to assign an IP, and risking duplicate IPs.
* Statically assigned server with IP address 192.168.10.10/24.
* Ran 'sudo netplan apply' to apply changes to IP.



* Error message appeared when trying to apply changes to YAML file - See Day 2/Issue 2 in Troubleshooting.
* Ran 'sudo chmod 600' to change file permissions, enabling changes in YAML file to be applied.
* 'sudo netplan apply' ran successfully.
* Used 'ip a' to confirm new IP address of 192.168.10.10/24.



* Repeated 'sudo chmod 600' in client.
* Repeated above steps to statically assign client IP address 192.168.10.20/24.



* From client, successfully ran a ping to server.
* From server, successfully ran a ping to client.



* Entered /etc/hosts/ of both VMs and added the new IP addresses with associated host names.
* Successfully pinged client from server using its hostname.
* Successfully pinged server from client using its hostname.





###### \# Day 3 (27/4/26):

* Used 'ip route' on both VMs, confirming they are both part of lab-net 192.168.10.0/24.
* Used 'ping 192.168.10.99' from client, which, as expected, resulted in all packets dropped and "Destination Host Unreachable" error.
* Changed client IP address to 192.168.20.20/24 to test subnet.
* Used 'ping 192.168.10.10' from client, which, as expected, resulted in "Network is unreachable" error.
* Changed clientIP address back to 192.168.10.20/24.



* Added default route 192.168.10.1 as a simulated gateway to client for testing.
* Used modern Netplan route configuration instead of deprecated 'gateway4' notation.
* Use 'ip route' to confirm 'default via 192.168.10.1' is returned.
* Removed simulated gateway.





###### \# Day 4 (29/4/26):

* Downloaded Netgate Installer v1.1.1 (pfSense) .ISO file.
* Created initial setup of new router VM that runs pfSense. (pfsense-lab-router)
RAM: 2GB.
CPU: 2 vCPU cores.
Disk: 16GB, dynamically allocated.
* Enabled Adapter 1 for lab-router - NAT (for WAN capabilities).
* Enabled Adapter 2 for lab-router - Internal Network (lab-net for LAN capabilities).



* Unable to confirm installation of pfSense as rebooting the VM returns me to the installation screen - See Day 4/Issue 1 in Troubleshooting.
* Dismounting the VM's ISO Image file prior to rebooting pfSense fixed the problem.



* pfSense successfully installed on lab-router with LAN IP address 192.168.1.1/24.
* Statically assigned server's IP address as 192.168.1.10. (Same subnet as router).
* Statically assigned client's IP address as 192.168.1.20. (Same subnet as router).
* Successfully pinged router from server.
* Successfully pinged router from client.
* Successfully pinged google.com from server.
* Successfully pinged google.com from client.



* Completed general setup for pfsense-lab-router.
* Assigned IP address pool as 192.168.1.100 - 192.168.1.199.
* Downloaded pfsense-lab-router config XML file.



###### \# Day 5 (4/5/26):

* On client, changed the Netplan YAML file to enable DHCP.
* 'ip a' confirms dynamically assigned IP address of 192.168.1.100/24, from the DHCP address pool.
* Reset VM and ran 'ip a' again - resulted in expected IP address of 192.168.1.100/24.
* Used 'ping google.com' to confirm DNS is working via router.
* Statically assigned a DHCP reservation IP address to client VM of 192.168.1.20.



###### \# Day 6 (5/5/26):

* Updated README and Network Configuration files for easier readability.

