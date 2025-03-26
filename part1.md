# Part 1
Objective: Create a diagram for the lab before starting in order to better understand how everything is connected.

Components:
- Splunk Server: Central log analysis and monitoring. Allows you to monitor, search, and visualize data from sources such as the AD server and client machines.
- Active Directory Server: Identity management within the network. Controls who can log in and access what on the network, and also enforces security policies and configurations across the domain.

--
- Splunk Universal Forwarder: Lightweight agent installed on servers and clients to forward log data from the Active Directory Server and Windows 10 client. Includes system, application, security logs, and more.
- Sysmon: Windows tool that provides detailed logs of system activity, such as process creation, network connections, etcetera. Crucial for detecting suspicious activity, such as malware execution and privilege escalation. These logs are forwarded to Splunk for analysis.
- Atomic Red Team: Collection of simple, modular tests designed to simulate real-world attack techniques. Used to test monitoring and detection capabilities on systems. Useful for evaluating security infrastructure, such as Splunk's ability to detect on malicious behavior.

--
- Windows 10 Client: Acts as a client within the network that is apart of the Active Directory domain. Testing ground for tools such as Sysmon and Atomic Red Team.
- Kali Linux Client: Linux distribution used for penetration testing. Used to test the security of the network and systems.

--
- Switch: Connects all servers and client machines on the same local network. Facilitates communication between devices within the network, but does not route data outside of the network.
- Router: Connects the local network to the external internet, enabling the ability to download updates, access external sites, etcetera.  Allows configuration of port forwarding and other network security settings.

![image](https://github.com/user-attachments/assets/6cf63b18-b0f8-4e50-99bf-ca85858d1821)
