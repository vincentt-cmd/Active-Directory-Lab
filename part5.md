# Part 5
Objective: Use Kali Linux to perform a brute force attack on users, view telemetry via Splunk, setup, install, and run Atomic Red Team tests

1. Set static IP to 192.168.10.250, as reflected in the diagram created in Part 1
![image](https://github.com/user-attachments/assets/83efe972-a8ab-4f32-944d-4841ea7ef78e)

---
2. Update the package list and upgrade all installed packages to the latest versions
![image](https://github.com/user-attachments/assets/a7299ad3-b400-4fd0-9fd4-b5199bd8f02d)

---
3. Create a new directory on the desktop to organize all files used in this part

![image](https://github.com/user-attachments/assets/06c45064-e145-4caf-b6bb-64184a22fddf)

---
4. Install Crowbar, a brute-force tool in designed for cracking remote authentication services
![image](https://github.com/user-attachments/assets/a4d09e8e-ea95-4dc3-9d4b-55e7bbdbb054)

---
5. Extract rockyou.txt.gz, which contains a password wordlist included in Kali Linux, commonly used for brute-force attacks and password cracking

![image](https://github.com/user-attachments/assets/19d8b97e-1a6c-4dc3-bf63-85274817a551)

---
6. Copy rockyou.txt to a new document containing only 20 lines/passwords (the original document is large)
![image](https://github.com/user-attachments/assets/73bd5fee-81e5-4214-a7a8-0bc2ddb32aa3)

---
7. To target a specific password, add the password used previously for the machines to the document (actually WindowsRocks!9)
![image](https://github.com/user-attachments/assets/9aee588e-e437-439a-833e-ebf2619cfa5e)

---
8. Enable remote connections on the Target Machine and users
![image](https://github.com/user-attachments/assets/074dec3b-80af-4435-b8de-3720cab868a9)

---
9. Install Hydra, another brute-force tool since Crowbar didn't work for me


- Crowbar not working for me
![image](https://github.com/user-attachments/assets/4d6d1b08-7aa1-4698-8cf2-28b793a6848f)

---
10. Run a brute-force attack on the RDP service at 192.168.10.100 using the username jpork and testing passwords from the passwords.txt file
    ![image](https://github.com/user-attachments/assets/fe2cfb71-a634-43a6-90b1-40a3ae49233a)

---
11. Targeted search in Splunk to identify and analyze logs related to the user jpork
![image](https://github.com/user-attachments/assets/397b81c2-b871-4f5d-ac6e-e3c221c31a86)

---
- Multiple instances of EventCode 4625 in Splunk indicate a series of failed authentication attempts, which may signal a potential brute-force attack or other unauthorized access attempts.
![image](https://github.com/user-attachments/assets/8b396037-df87-4b68-9724-860cad696543)

![image](https://github.com/user-attachments/assets/e30a8824-8e2e-4b44-8d01-e186feaaa578)

---
12. Modify the PowerShell execution policy for the Target Machine to allow unrestricted script execution, bypassing security restrictions for running potentially untrusted scripts
![image](https://github.com/user-attachments/assets/dbcc5383-5d85-4759-bba3-7d17dc0134ad)

---
13. Add the C:/ Drive as an excluded folder from Windows Defender, as it might remove files from Atomic Red Team
![image](https://github.com/user-attachments/assets/46f8fba9-cd96-49fa-8ad5-9fd938b7471f)

---
14. Install Atomic Red Team
![image](https://github.com/user-attachments/assets/a04c04ca-8049-4262-8606-67f51f619780)

---
15. Execute the Invoke-AtomicTest command to simulate the T1136.001 - Create Account technique from the MITRE ATT&CK framework, which tests the ability to create a new local user account on the system as part of adversary emulation for persistence
![image](https://github.com/user-attachments/assets/a4b5fd14-1632-40df-a1eb-3f675cb62d0a)

---
- Atomic Red Team's T1136.001, which simulates the creation of a new local user account, verified that the endpoint monitoring effectively detected the event, indicating that there are no gaps in the logging or detection capabilities for local account creation activities. 
![image](https://github.com/user-attachments/assets/e27d3497-cb64-4467-bb02-0a0cc769508f)
















