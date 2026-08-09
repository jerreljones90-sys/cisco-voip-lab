# Troubleshooting Notes

# Hyper-V VM not communicating with gateway.
-Went into Hyper-V reviewed current VM Host settings and noticed an issue with the vNIC. Plugged in an ethernet to the second network interface on the back of the server directly into the switch port on Access 2 switch. Logged into the switch via SSH placed this connection into VLAN 200, made sure the vNIC on the host is to DHCP. Logged into Debian 12 and executed the "ip address" command to get the IP to start testing connectivity. From the switch performed a ping, sourcing from VLAN 200 to the IP address of the server. Issue resolved. 
*Testing Resolution*
Performing a continuous ping from the switch to the VM Host and from the server to VM host. Successfully pings

# Debian 12 installed but phones are stuck in "Registering"
-What I noticed when after the install of Debian, I wasn't able to open the GUI for FusionPBX. After doing some research I noticed the application needs to be installed via the internet. Performing commands to download FusionPBX. FusionPBX application is now installed and has the IP of 10.0.0.140 /24. I am now able to log into the GUI successfully. 
*Testing Resolution*
Logged into 10.0.140 and credentials are working. 

# Phones are stuck in "Registering"
I was able to log into the phones IP address to view the status logs and noticed its looking for a particular file called "SEP501CB00C31CP.cnf.xml." TFTP timeout continues to show in the logs, at this point I started using Wireshark and mirror the port of the phone. In Wireshark I filter by "tftp" I notice the host 10.0.0.140 is constantly cycling through a few file extensions .tlv and .cnf.xml. On the VM host it not listening for port 69 after running through a few commands on the linux host. Allowed port 69 and now in Wireshark the IP Phone and VM host are sending TFTP message to each other. Wireshark is showing many Read Request packets and not any acknowledgments. After running into issues of the Debian 12 TFTP, I downloaded TFTPD64 installed on the server. Found the config file SEP501CB00C31CP.cnf.xml place it where TFTP can see and send it. Now in Wireshark it shows an Acknowlegment after see the file and starts installing the config file. 
Logging into the FusionPBX GUI went to Accounts >Extensions>Manually created extension 1000 and 1001. Went to Devices and added both both phones and made sure the password matched. Rebooted the IP Phone. Phone is now registered with FusionPBX. Repeating for second IP Phone. Both phones are registered.

*Testing Resolution *
- With Wireshark still running, from extension 1001 calling 1000. Successful call Wireshark is showing the RTP stream and SIP showing connected correctly before and after a call. Also just leaving a voicemail to make sure Wireshark shows "NOTIFY." 
