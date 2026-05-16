# Troubleshooting



##### \# Day 2:

###### Issue 1:

* VM not resizing in full screen (VirtualBox)
* Symptoms:

Fullscreen mode enabled but display not resizing

* Cause:

Guest Additions not installed on client VM

* Fix:

Installed VirtualBox Guest Additions and rebooted

* Result:

Fullscreen auto-resize working correctly



###### Issue 2:

* Unable to run 'sudo netplan apply' to apply changes to YAML file.
* Symptoms:

Error message in Terminal: "Permissions for /etc/netplan/01-network-manager-all.yaml are too open.
Netplan configuration should NOT be accessible by others."
Unable to apply changes.

* Cause:

File permissions set too strict for editing.

* Fix:

Run 'sudo chmod 600' command to change file permissions for the YAML file.

* Result:

'sudo netplan apply' now runs successfully and my static IP has been implemented.





##### \# Day 4

###### Issue 1:

* After installing pfSense onto its VM, rebooting the VM leads me back to the installation setup screen.
* Symptoms:

Selecting 'Reboot' following pfSense installation leads me back to the pfSense installation screen, with no sign that the installation was successful.

* Cause:

Not removing the Netgate Installer ISO file from the VM's ISO Image file within VirtualBox.
The VM will boot up the installer image each time it is rebooted.

* Fix:

Unmounting the ISO Image File from the 'Devices' menu in VirtualBox, and then resetting the VM, following installation of pfSense.

* Result:

pfSense VM boots up to the main pfSense home screen.





##### \# Day 7

###### Issue 1:

* Attempted 'curl' command on client VM terminal but command could not be found.
* Symptoms:

After attempting 'curl google.com' in the client terminal, terminal responded with 'Command 'curl' could not be found'.

* Cause:

The 'curl' command did not come as default with my installation of Linux and must be installed first.

* Fix:

Used 'sudo apt update' and 'sudo apt upgrade' to download and install updates.
Used 'sudo apt install curl' to install curl functionality.

* Result:

Used 'curl -version' to verify installation.
Using 'curl google.com' now runs as expected, displaying the HTML information of google.com homepage in the terminal.



###### Issue 2:

* Attempted pinging google.com from client VM terminal but command would not resolve.
* Symptoms:

After attempting 'ping google.com' in the client terminal, terminal responded with 'Temporary failure in name resolution'.

* Cause:

Temporarily disabling 'Default Allow LAN to Any' rule in the firewall has stopped DNS from resolving.

* Fix:

Pinging 192.168.1.1 does resolve, with no packet delivered. (As expected with Block ICMP rule).

Created a new rule in firewall - 'Allow DNS', which enables traffic to TCP/UDP/53.

* Result:

Pinging google.com now resolves, with no packets delivered.

Using 'curl google.com' returns the HTML file as expected.





##### \# Day 9

###### Issue 1:

* Attempted pinging google.com from client VM terminal but packets were dropped following DNS resolution.
* Symptoms:

After attempting 'ping google.com' in the client terminal, the google.com name was resolved, but terminal responded with '100% packet loss'.

* Cause:

Lack of explicit 'ICMP Allow Any' rule results in an implicit deny of ICMP traffic.

* Fix:

Created a new rule in firewall - 'ICMP Allow Any', which explicitly allows ICMP traffic.

* Result:

Pinging google.com now resolves with 0% packet loss.



###### Issue 2:

* Attempted pinging google.com from client VM terminal to capture DNS packets in Wireshark, but DNS packets were not appearing in Wireshark.
* Symptoms:

After attempting 'ping google.com' in the client terminal while Wireshark was filtered to capture DNS packets, no DNS packets were appearing in Wireshark's capture display.

* Cause:

The DNS resolution for google.com was cached by the client, so DNS lookup was not performed by ping.

* Fix:

Run 'nslookup google.com' instead to explicitly request a name resolution from the DNS server.

* Result:

'nslookup google.com' was successful, and Wireshark captured DNS packets for google.com correctly.



