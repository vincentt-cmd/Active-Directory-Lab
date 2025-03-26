# Part 3
Objective: Install and configure Sysmon and Splunk on the Windows Target Machine and Windows Server in order to start collecting telemetry and sending logs to the Splunk Server

1. Create a custom NAT network in VMware, named it AD-Project, set the network address to 192.168.10.0/24, configured the gateway IP as 192.168.10.1, and enabled DHCP with a range from 192.168.10.2 to 192.168.10.100, allowing automatic IP assignment to devices on the network while ensuring the gateway remains reserved.
