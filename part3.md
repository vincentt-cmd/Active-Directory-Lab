# Part 3
Objective: Install and configure Sysmon and Splunk on the Windows Target Machine and Windows Server in order to start collecting telemetry and sending logs to the Splunk Server


1. Create a custom NAT network in VMware, named it AD-Project, set the network address to 192.168.10.0/24, configured the gateway IP as 192.168.10.1, and enabled DHCP with a range from 192.168.10.2 to 192.168.10.100, allowing automatic IP assignment to devices on the network while ensuring the gateway remains reserved.
![image](https://github.com/user-attachments/assets/49254983-3da1-4af9-9c4c-cd06bcfef5a6)

---
2. Assign all the machines to the new NAT network that was created so that they can all communicate with each other.
![image](https://github.com/user-attachments/assets/8980db4f-d108-435e-8f67-21c35f01ed40)

---
3. Create a Netplan configuration file for the Splunk server to set a static IP address and configure network settings. The file specifies that the enp0s3 network interface uses static IP addressing by disabling DHCP for IPv4. Set the server’s IP address to 192.168.10.10 with a /24 subnet mask (as reflected in the diagram made in Part 1) and define 8.8.8.8 (Google) as the DNS server for name resolution. Additionally, configure the default gateway as 192.168.10.1 to enable the server to reach external networks.
![image](https://github.com/user-attachments/assets/1e229fdc-d166-42c1-adac-797726425f42)

---
4. Run `sudo netplan apply` to apply changes made to the network configuration
![image](https://github.com/user-attachments/assets/010a6333-309f-41a2-b13a-8da1b2696f0b)

---

Windows Server Static IP has been set to `192.168.10.10`
![image](https://github.com/user-attachments/assets/4a6a29cf-9c7a-46e0-a872-96c66b6ffc31)

---
5. Download Splunk Enterprise 9.4.1 for Linux
![image](https://github.com/user-attachments/assets/5467cc9a-08e4-4e18-a549-2939e7c0516a)

6. Install open-vm-tools and open-vm-tools-desktop to enable VMware integration features, specifically clipboard sharing (for next steps).

---
7. Enable shared folders to be able to transfer files easily (alternative that might've been better is SSH)
![image](https://github.com/user-attachments/assets/125eddaa-5729-4a74-a1c0-8b963b0ade2e)

---

- Had to manually mount the folder to /mnt/hgf using `sudo mount -t fuse.vmhgfs-fuse .host:/ /mnt/hgfs -o allow_other`

---
8. Install Splunk onto Ubuntu Server
Login: joe / Windowsrocks!9

![image](https://github.com/user-attachments/assets/d38151c4-b872-4068-9d1a-020d10d9bced)

---
License Agreement for Splunk
![image](https://github.com/user-attachments/assets/915d5377-73c4-4eb1-8296-b99fe0152839)

---

9. Configure Splunk to automatically start during system boot and run it under the user splunk, ensuring Splunk starts as a background service when the server is rebooted
    
![image](https://github.com/user-attachments/assets/d214f8a6-a2a7-406e-8873-73c81d96a11c)

---

10. Set Windows Machine (Target PC) static IP to 192.168.10.100
    
![image](https://github.com/user-attachments/assets/07d0ba3a-c05d-4597-ae67-d0e9c0096a00)

---
11. Download Splunk Universal Forwarder on Windows Machine
![image](https://github.com/user-attachments/assets/3b2df4a9-1d79-4074-9eeb-3def8173a5d4)

---
12. Download Olaf Sysmon configuration (comes with pre-configured rules, widely adopted, etc.)
![image](https://github.com/user-attachments/assets/d4281456-a4a5-4bcd-bf41-2f4774af2251)

---
13. Create an inputs.conf file in the Splunk Universal Forwarder directory to collect Windows Event Logs (Application, Security, System) and Sysmon Operational logs, indexing them into the endpoint index with Sysmon logs rendered as XML.
![image](https://github.com/user-attachments/assets/201cbd88-45a6-4525-a507-456fc2df1f3c)

---
14. Log into Splunk dashboard (192.168.10.10:8000)
![image](https://github.com/user-attachments/assets/3589d25c-a81e-4aac-8e67-301a78125d87)

---
15. Create a new index called `endpoint` to organize and store the event data
![image](https://github.com/user-attachments/assets/9473ae06-d2d7-471a-a5a8-5decb34b4038)

---
16. Search for event logs within the index `endpoint`
![image](https://github.com/user-attachments/assets/400f0c83-1a15-4716-a071-a6639ad5ef05)

---
16. Repeat the process to install Splunk Universal Forwarder and Sysmon for the Windows Server (AD)
![image](https://github.com/user-attachments/assets/1af4d608-8cbc-4db3-9bf5-c701e785e344)

---
Issues I ran into during this part:
- In VMware, a file called 50-cloud-init.yaml was created under the /etc/netplan/ directory, which I initially expected to be 00-installer-config.yaml, where I intended to configure a static IP address for the Splunk server. I first attempted to set the static IP directly in 50-cloud-init.yaml, but encountered an issue where the static IP would reset every time the server was rebooted. To resolve this, I created my own 00-installer-config.yml file with a different format for manual network configuration. This new file successfully applied the static IP configuration and prevented it from resetting upon reboot.
