\# Day 2:
Issue 1:

* VM not resizing in full screen (VirtualBox)
Symptoms:
* Fullscreen mode enabled but display not resizing
Cause:
* Guest Additions not installed on client VM
Fix:
* Installed VirtualBox Guest Additions and rebooted
Result:
* Fullscreen auto-resize working correctly



Issue 2:

* Unable to run 'sudo netplan apply' to apply changes to YAML file.
Symptoms:
* Error message in Terminal: "Permissions for /etc/netplan/01-network-manager-all.yaml are too open. Netplan configuration should NOT be accessible by others." Unable to apply changes.
Cause:
* File permissions set too strict for editing.
Fix:
* Run 'sudo chmod 600' command to change file permissions for the YAML file.
Result:
* 'sudo netplan apply' now runs successfully and my static IP has been implemented.

