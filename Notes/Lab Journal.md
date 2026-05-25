# Home-Lab-Network

###### 

###### \# Day 0 - Installation and Setup:

* Downloaded and installed VirtualBox and GitHub Desktop.
* Downloaded and installed VirtualBox Extension Pack.
* Outlined project goals, tools, and broader project steps in README.





###### \# Day 1 - Creating First Virtual Machine:

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





###### \# Day 2 - Creating Second Virtual Machine and LAN Subnet:

* Created initial setup of new client VM that runs Ubuntu v24.04.4 LTS. (ubuntu-lab-client)
RAM: 4GB.
CPU: 4 vCPU cores.
Disk: 25GB, dynamically allocated.



* ubuntu-lab-client fully installed.
* Adapter 1 automatically attached to NAT.
* Discovered issue with VM not re-sizing to full screen - See Day 2/Issue 1 in Troubleshooting.
* Successfully installed OpenSSH Client for future secure remote access, encrypted communications and authentication.
* Successfully repeated 'ip a' and ping tests from Day 1 for client.



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





###### \# Day 3 - Testing Subnet:

* Used 'ip route' on both VMs, confirming they are both part of lab-net 192.168.10.0/24.
* Used 'ping 192.168.10.99' from client, which, as expected, resulted in all packets dropped and "Destination Host Unreachable" error.
* Changed client IP address to 192.168.20.20/24 to test subnet.
* Used 'ping 192.168.10.10' from client, which, as expected, resulted in "Network is unreachable" error.
* Changed clientIP address back to 192.168.10.20/24.



* Added default route 192.168.10.1 as a simulated gateway to client for testing.
* Used modern Netplan route configuration instead of deprecated 'gateway4' notation.
* Use 'ip route' to confirm 'default via 192.168.10.1' is returned.
* Removed simulated gateway.





###### \# Day 4 - Creating and Installing Virtual Router:

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





###### \# Day 5 - Enabling DNS, DHCP, and Assigning Static IP Address:

* On client, changed the Netplan YAML file to enable DHCP.
* 'ip a' confirms dynamically assigned IP address of 192.168.1.100/24, from the DHCP address pool.
* Reset VM and ran 'ip a' again - resulted in expected IP address of 192.168.1.100/24.
* Used 'ping google.com' to confirm DNS is working via router.
* Statically assigned a DHCP reservation IP address to client VM of 192.168.1.20.





###### \# Day 6 - Updating Documentation:

* Updated README and Network Configuration files for easier readability.





###### \# Day 7 - Enabling Firewall Rules:

* Default Firewall rules for LAN:
* Anti-Lockout Rule (Ports 80 and 443)
* Default Allow LAN to Any
* Default Allow LAN IPv6 to Any
* Adding Block ICMP test rule to firewall:
* Action: Block
* Interface: LAN
* Protocol: ICMP
* Destination: Any
* Pinged google.com from client - As expected, ping fails.
* Unable to run 'curl google.com' - See Day 7/Issue 1 in Troubleshooting.
* After installing curl functionality, used 'curl google.com' to confirm HTTP requests are working.



* Created two new firewall rules - Allow HTTP (TCP/80) and Allow HTTPS (TCP/443).
* Temporarily disabled Default Allow LAN to Any firewall rules.
* Pinging google.com results in resolution failure - See Day 7/Issue 2 in Troubleshooting.
* After creating a new Allow DNS (TCP/UDP/53) rule, ping now resolves as expected.
* Using 'curl google.com' was successful, so HTTP/HTTPS traffic is flowing as expected.





###### \# Day 8 - Deploying Web Server:

* Ran 'sudo apt update' and 'sudo apt upgrade' on server.
* Ran 'sudo apt install apache2' to install Apache web server.
* Ran 'systemctl status apache2' to verify Apache status - Active (running).
* Ran 'sudo apt install curl' to install curl functionality.
* Ran 'curl localhost' to display Apache server HTML output.



* From client, Ran 'curl 192.168.1.10' to display server VM's Apache server HTML output.
* In router, added firewall rule 'Allow Internal Traffic', intentionally allowing internal communication between LAN devices.
* From client, ran 'http://192.168.1.10', and was able to connect to the server's Apache Default Page.
* From server, ran 'sudo nano /var/www/html/index.html' to enter the Apache Default Page's HTML layout.
* Ran 'sudo cp /var/www/html/index.html /var/www/html/index.html.bak' to create a backup copy of the Apache Default Page.
* Created basic HTML web page within index file.
* From client, ran 'http://192.168.1.10' again and my web page loaded as expected.





###### \# Day 9 - Installing and Using Wireshark:

* Ran 'sudo apt install wireshark' on client to install Wireshark.
* Ran 'sudo usermod -aG wireshark $USER' to add the client's user to Wireshark.



* Pinging google.com results in dropped packets following name resolution - See Day 9/Issue 1 in Troubleshooting.
* After creating a new Allow Any ICMP rule, ping now resolves as expected and Wireshark successfully captured ICMP packets.



* Pinging google.com resulted in no DNS packets being captured by Wireshark - See Day 9/Issue 2 in Troubleshooting.
* After using 'nslookup google.com', Wireshark successfully captured DNS packets.
* Ran 'curl 192.168.1.10' to display Apache server HTML output.
* Wireshark successfully captured HTTP packets.
* Ran 'curl https://google.com' to display Google HTML.
* Wireshark successfully captured encrypted HTTPS packets.





###### \# Day 10 - Simulating Failures and Troubleshooting:

* Ran ping, curl, and nslookup tests - All functioning as expected.



* Edited Netplan YAML file to list unconnected DNS server 10.10.10.10.
* Ran 'nslookup amazon.com' - Lookup timed out and returned non-authorative response.
* Wireshark captured outgoing DNS request packets.
* Deleted new DNS configuration.



* Edited Netplan YAML file to list default gateway as incorrect address 192.168.1.254.
* Resulted in no Internet access.
* nslookup times out.
* Deleted new default gateway configuration.



* Added a Block HTTP rule to router firewall.
* Ran 'curl google.com', which failed as expected.
* Ran 'ping google.com', which succeeded as expected.
* Wireshark captured outgoing HTTP request packets.
* Deleted new Block HTTP rule.

* Ran 'sudo systemctl stop apache2' in server to disable Apache web server.
* Ran 'curl 192.168.1.10' in client, which failed as expected.
* Ran 'ping 192.168.1.10' in client, which succeeded as expected.
* Wireshark captured outgoing HTTP request packets.
* 'sudo systemctl start apache2' to re-enable Apache.
* Ran 'systemctl status apache2' to verify Apache status - Active (running).











