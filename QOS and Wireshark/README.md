# Project Objective

This is a basic QoS configuration designed to verify traffic classification and marking using Wireshark.

Voice and Data will be the two traffic classes being marked:
- Voice traffic: DSCP EF (46)
- Data traffic: DSCP AF21 (18)

Configure a local SPAN port to mirror traffic on Phone 1001. 
Wireshark will be used to capture and inspect the traffic to verify that the expected DSCP markings are being applied.

(Network Topology can be folder in this folder name Basic QOS Topology)
