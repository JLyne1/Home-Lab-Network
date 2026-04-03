# Home-Lab-Network

\# Day 0 (31/3/26):
Downloaded and installed VirtualBox and GitHub Desktop.

Downloaded and installed VirtualBox Extension Pack.
Outlined project goals, tools, and broader project steps in README.md.



\# Day 1 (1/4/26):
Downloaded Ubuntu v24.04.4 LTS .ISO file.
Created initial setup of new server VM that runs Ubuntu v24.04.4 LTS. (Ubuntu-Lab-Server)
RAM: 4GB.
CPU: 4 vCPU cores.

Disk: 25GB, dynamically allocated.



Ubuntu-Lab-Server fully installed.

Adapter 1 automatically attached to NAT.

Successfully installed OpenSSH Server for future secure remote access, encrypted communications and authentication.

Used 'ip a' to confirm device IP address and confirm network connectivity.
Used 'ping 127.0.0.1' to ping loopback address.
Used 'ping -c 4 google.com' to ping google.com URL 4 times to test external connectivity.



\# Day 2 (2/4/26):
Created initial setup of new VM that runs Ubuntu v24.04.4 LTS. (Ubuntu-Lab-Client)
RAM: 4GB.
CPU: 4 vCPU cores.
Disk: 25GB, dynamically allocated.



Ubuntu-Lab-Client fully installed.
Adapter 1 automatically attached to NAT.

Discovered issue with VM not re-sizing to full screen - See Issue 1 in Troubleshooting.md.
Successfully installed OpenSSH Client for future secure remote access, encrypted communications and authentication.
Used 'ip a' to confirm device IP address and confirm network connectivity.
Used 'ping 127.0.0.1' to ping loopback address.
Used 'ping -c 4 google.com' to ping google.com URL 4 times to test external connectivity.



In Settings -> Network for both VMs - Changed Adapter 1 from NAT to Internal Network.
Established lab-net internal network.

Logged into both VMs and network connection has failed - as expected with the change to internal network.



Logged onto Server and entered the YAML file in the etc/netplan/ directory.

Changed renderer from NetworkManager to networkd - networkd is more ideal for smaller, static configurations.

Disabled DHCP to prevent DHCP attempting to assign an IP, and risking duplicate IPs.

Assigned the Server VM with IP address 192.168.10.10/24.

Ran 'sudo netplan apply' to apply changes to IP.

Error message appeared when trying to apply changes to YAML file - See Issue 2 in Troubleshooting.md.

Ran 'sudo chmod 600' to change file permissions, enabling changes in YAML file to be applied.
'sudo netplan apply' ran successfully.

Used 'ip a' to confirm new IP address of 192.168.10.10/24.



Logged onto Client and ran 'sudo chmod 600' to change file permissions, enabling changes in YAML file to be applied.

Entered the YAML file in the etc/netplan/ directory.

Changed renderer from NetworkManager to networkd.

Disabled DHCP.

Assigned the Client VM with IP address 192.168.10.20/24.

Ran 'sudo netplan apply' to apply changes to IP.

'sudo netplan apply' ran successfully.

Used 'ip a' to confirm new IP address of 192.168.10.20/24.



From Client, successfully ran a ping to Server's new IP address.

From Server, successfully ran a ping to Client's new IP address.



