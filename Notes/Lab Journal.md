# Home-Lab-Network

###### 

###### \# Day 0 (31/3/26):

* Downloaded and installed VirtualBox and GitHub Desktop.
* Downloaded and installed VirtualBox Extension Pack.
* Outlined project goals, tools, and broader project steps in README.md.





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
* Used 'ping -c 4 google.com' to ping google.com URL 4 times to test external connectivity.





###### \# Day 2 (2/4/26):

* Created initial setup of new VM that runs Ubuntu v24.04.4 LTS. (ubuntu-lab-client)
RAM: 4GB.
CPU: 4 vCPU cores.
Disk: 25GB, dynamically allocated.



* ubuntu-lab-client fully installed.
* Adapter 1 automatically attached to NAT.
* Discovered issue with VM not re-sizing to full screen - See Issue 1 in Troubleshooting.md.
Successfully installed OpenSSH Client for future secure remote access, encrypted communications and authentication.
Used 'ip a' to confirm device IP address and confirm network connectivity.
Used 'ping 127.0.0.1' to ping loopback address.
Used 'ping -c 4 google.com' to ping google.com URL 4 times to test external connectivity.



* In VirtualBox Settings -> Network for both VMs - Changed Adapter 1 from NAT to Internal Network.
* Established lab-net internal network.
* Logged into both VMs and network connection has failed - as expected with the change to internal network.



* Logged onto Server and entered the YAML file in the etc/netplan/ directory.
* Changed renderer from NetworkManager to networkd - networkd is more ideal for smaller, static configurations.
* Disabled DHCP to prevent DHCP attempting to assign an IP, and risking duplicate IPs.
* Assigned the Server VM with IP address 192.168.10.10/24.
* Ran 'sudo netplan apply' to apply changes to IP.



* Error message appeared when trying to apply changes to YAML file - See Issue 2 in Troubleshooting.md.
* Ran 'sudo chmod 600' to change file permissions, enabling changes in YAML file to be applied.
* 'sudo netplan apply' ran successfully.
* Used 'ip a' to confirm new IP address of 192.168.10.10/24.



* Logged onto Client and ran 'sudo chmod 600' to change file permissions, enabling changes in YAML file to be applied.
* Entered the YAML file in the etc/netplan/ directory.
* Changed renderer from NetworkManager to networkd.
* Disabled DHCP.
* Assigned the Client VM with IP address 192.168.10.20/24.
* Ran 'sudo netplan apply' to apply changes to IP.
* 'sudo netplan apply' ran successfully.
* Used 'ip a' to confirm new IP address of 192.168.10.20/24.



* From Client, successfully ran a ping to Server's new IP address.
* From Server, successfully ran a ping to Client's new IP address.



* Entered /etc/hosts/ of both VMs and added the new IP addresses with associated host names.
* Successfully pinged Client VM from Server VM using its host name.
* Successfully pinged Server VM from Client VM using its host name.





###### \# Day 3 (27/4/26):

* Used 'ip route' on both VMs, confirming they are both part of lab-net 192.168.10.0/24.
* Used 'ping 192.168.10.99' from Client VM, which, as expected, resulted in all packets dropped and "Destination Host Unreachable" error.
* Changed Client VM IP address to 192.168.20.20/24 to test subnet.
* Used 'ping 192.168.10.10' from Client VM, which, as expected, resulted in "Network is unreachable" error.
* Changed Client VM IP address back to 192.168.10.20/24.



* Added default route 192.168.10.1 as a simulated gateway to Client VM for testing.
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



* Unable to confirm installation of pfSense as rebooting the VM returns me to the installation screen.
* Dismounting the VM's ISO Image file prior to rebooting pfSense fixed the problem.



* pfSense successfully installed on lab-router with LAN IP address 192.168.1.1/24.
* Changed Server's IP address to 192.168.1.10. (Same subnet as router).
* Changed Client's IP address to 192.168.1.20. (Same subnet as router).
* Successfully pinged router from server.
* Successfully pinged router from client.
* Successfully pinged google.com from server.
* Successfully pinged google.com from client.



* Completed general setup for pfsense-lab-router.
* Assigned IP address pool as 192.168.1.100 - 192.168.1.199.
* Downloaded pfsense-lab-router config XML file.

