# Cisco VoIP Enterprise Lab

#Network Topology#
Document name "Network Topology.PDF

## Project Overview ##

This project documents the design, deployment, and troubleshooting of a Cisco VoIP environment within my enterprise home lab. The objective is to deploy 2 Cisco IP phones with Fusion PBX and to successfully make calls to each other while using Wireshark to view packets in real time and for troubleshooting. Rather than focusing only on successful configuration, this project also documents the troubleshooting process used to identify issues with phone provisioning and SIP registration.

## Technologies Used 
Cisco 8845 IP Phones,

Fusion PBX (VM Host),

Hyper-V,

Wireshark, 

TFTP Server (TFTPD64),

DHCP,

DHCP Option 150, 

SIP,

RTP,

Debian Linux,

Cisco IP Phones, 

Cisco IOS Switching,  

QOS / DSCP,


## Current Network Equipment in this lab ##

2 - Cisco 3560 -POE (24 port switches),

1 Cisco Catalyst 3750 series- POE (24 port),

1 Cisco Catalyst 3750 series- POE (48 port),

3- Cisco 2821 ,

1- Hewlett Packard Proliant DL360 Gen 10 Server,

1- Palo Alto 220 Firewall ,

2- Cisco 8845 IP Phones , 

## Lab Objectives ## 
Create subnet and VLAN for Voice VLAN on Distribution A (Vlan 200)
For lab purposes create a DHCP Scope on Distribution A (In production the server would hand out DHCP)
Place both IP on Access 2 into Voice VLAN 200
Place server port 2 into VLAN 200
Configure Hyper-V for Debian 12 with the correct vNIC.
Once debian 12 downloads successfully, deploy FusionPBX application / FreeSwitch.
Set up a separate TFTP server from FusionPBX using TFTPD64. 
Both phones must obtain an IP address via DHCP 
Both phones must register will FusionPBX.
Establish extension-to-extension calling
Capture and analyze VoIP traffic
Validate QoS markings using Wireshark
Troubleshoot phone registration and provisioning issues

Wireshark was used throughout the troubleshooting to verify network behavior such DHCP DORA process, TFTP, SIP and RTP stream traffic or application. This was used to isolate each problem that occurred. 
