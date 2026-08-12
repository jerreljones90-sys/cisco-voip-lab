# Project Objective: Setup VM through Hyper-V and download FusionPBX

Click Troubleshooting Notes for Screenshots of VM and CLI Settings 

[
](https://github.com/jerreljones90-sys/cisco-voip-lab/blob/36d778ab3670b33fa916e1da6accd8fadfe988bb/VM%20Setup%20for%20Linux/Troubleshooting%20Notes/VM%20Setup%20%20New%20subnet%20setup%20-%20Troubleshooting%20.pdf)
# Description:
Create a virtual machine using Microsoft Hyper-V with the recommended hardware and network settings to install Debian 12 and successfully deploy FusionPBX. 
FusionPBX will serve as the VoIP call-control/PBX platform used to register and provide calling services for Cisco IP phones.

# Technology Used for this lab 
- HP Proliant DL360 Gen10 server
- Debian 12 ISO  
- Cisco IP Phones
- TFTP
- Wireshark

# VM Setup 
-2 CPU's
-4GB of RAM 
-50 GB of space 
-vNIC (hardwired and setup for VLAN 200) 
-Removing Secureboot in the security options 
-Selection Generation 2 for VM 
-Attaching the .iso file as the image
(After configuring all above options, running the VM) 
  
  # Troubleshooting 
  VM/ issue with IP 
  
  Issue: After VM setup was completed in Hyper-V, as I was running through the Debian 12 setup it failed on the network detect screen. I currently have a static address setup on this machines as 10.147.59.126 /25.
  I need to go back into Linux under nano /etc/network/interfaces screen and change this to DHCP and connect this to the internet and not my lab environment. 

  Fix: Setup the Linux VM as DHCP and plugged directly into my home router. VM now has a DHCP address of 10.0.0.140 and I can ping 8.8.8.8. Running through the setup for Debian 12.
  Validation: After network detection its now successful and it installed the correct packages. 

  FusionPBX keeps old static IP.
  Issue: After navigating through linux I notice that FusionPBX continues to keep the old IP address of 10.147.59.126 /25. Which is causing issues when trying to log in as admin. 

  Troubleshooting: 
  Went into ip settings on Linux (nano /etc/network/interfaces) made sure it was set to static. Verified the IP settings, rebooted the VM and check network settings again. Still has the static IP of 10.147.59.126, logging into FusionPBX with the admin credentials.
  "Authentication Failed" message. In FusionPBX in the Linux screen it still showing that the application is tied to 10.0.0.140 from when I connected to the internet.
  -Going into the Linux network settings, setting password to 10.0.0.140 for test purposes. 
  -Creating a SVI for a new VLAN 10 (TestVoice) 10.0.0.1 /24.
  -Creating a DHCP scope on the router. (Testing purposes only before moving to the server to host DHCP)
  - using TFTP file on the server and not Linux for ease of use to import the .cnf.xml file for phones.

    Fix: Once I changed the Linux IP to 10.0.0.140, I am not able to log into FusionPBX successfully.

    -Validation: Logged into FusionPBX, created 2 Extensions and devices. The IP Phones successfully received a DHCP address. I can ping the IP for the phones from the switch and the server. Switching the IP to 10.0.0.140 /24 fixed the issue with FusionPBX login. 

  
  
