# 🧱 Network Traffic Filtering & Firewall Configuration Lab (Task 4)

## 📌 1. Project Overview
[cite_start]This project focuses on configuring and testing basic firewall rules to monitor and filter network traffic. [cite_start]The primary objective is to understand how firewalls secure systems by explicitly allowing or blocking traffic on specific communication ports based on standard enterprise security policies. [cite_start]In this lab, I implemented inbound rule blocking for **Port 23 (Telnet)** and allowed traffic for **Port 22 (SSH)** using **UFW (Uncomplicated Firewall)** on Linux[cite: 54, 58, 60].




----------------------------------------------------------------------------------------------------------------------------




## ⚙️ 2. Lab Environment & Technical Methodology
* **Operating System:** Linux (Ubuntu/Debian-based distribution)
* [cite_start]**Firewall Utility Used:** UFW (Uncomplicated Firewall) [cite: 54]
* **Target Network Ports:**
  * [cite_start]**Port 23 (Telnet):** Configured to block inbound traffic due to cleartext transmission risks[cite: 58, 70].
  * [cite_start]**Port 22 (SSH):** Configured to explicitly allow secure remote management sessions.

### 📋 Execution Steps & Commands Log:

1. **Verify Firewall Current Status:**
   [cite_start]Audited the active firewall rules and baseline configurations before making changes:
   ```bash
   sudo ufw status verbose

2. **Enable the Firewall Service:**
   Activated the firewall to enforce policy filtering on system boot:
   ```Bash
   sudo ufw enable
   
3. **Block Inbound Telnet Traffic (Port 23):**
Injected a rule to drop all incoming TCP packets attempting to connect via Telnet:
```Bash
sudo ufw deny in 23/tcp
```

4. **Allow Secure Shell Traffic (Port 22):**
Added an explicit rule to permit encrypted administrative access over SSH:
```Bash
sudo ufw allow 22/tcp
```

5. ***Verify Applied Rule Matrix:***
Generated a numbered list of the live rules to ensure correct enforcement and order:
```Bash
sudo ufw status numbered
```

Removed the temporary Telnet block rule to safely restore the host back to its default state:
```Bash
sudo ufw delete deny in 23/tcp
```



------------------------------------------------------------------------------------------------------------------------




📊 3. **How a Firewall Filters Traffic***
A firewall functions as a perimeter barrier separating a trusted internal network from untrusted external traffic. It acts as a packet filter that inspects every transit layer frame headers in real-time. The filtering criteria consist of checking: 

**Source & Destination IP Addresses:*** Identifying the exact node initiating the request.
**Protocols:** Inspecting transport rules like TCP, UDP, or ICMP network packets.
**Port Numbers:** Evaluating the destination application service endpoint (e.g., Port 22, 23, 80).

When a packet hits the interface, the firewall scans its rules from top to bottom. If a match is found, it executes the corresponding action (Allow/Accept or Deny/Drop), effectively hardening the system against network-based exploits. 



----------------------------------------------------------------------------------------------------------------------------



**4. Interview Q&A**

**Q1. What is a firewall?**
**Answer:**  A firewall is a software or hardware-based network security system that monitors and filters incoming and outgoing network traffic based on an organization's previously established security policies.  


**Q2. Difference between stateful and stateless firewall?** 
**Answer:** **Stateless Firewall:** Inspects individual network packets dynamically in isolation based on fixed parameters like source/destination IP and port numbers without tracking the session state. 
     **Stateful Firewall:** Monitors and keeps track of the entire state of active network connections and handshakes. It safely allows returning traffic belonging to an established session without requiring explicit standalone rules. 


**Q3. What are inbound and outbound rules?**
**Answer:** **Inbound Rules:** Security configurations that filter incoming traffic originating from external networks attempting to access services on the local machine.  
        **Outbound Rules:** Security configurations that filter outgoing traffic originating from the local machine attempting to reach external web servers or remotes.


**Q4. How does UFW simplify firewall management?**
**Answer:** UFW (Uncomplicated Firewall) acts as a high-level command-line frontend interface that abstracts the highly complex and verbose syntax of Netfilter's raw iptables rules into simple, human-readable English commands (e.g., ufw allow 22). 


**Q5. Why block port 23 (Telnet)?**
**Answer:** Port 23 is used by Telnet, which is an obsolete, highly insecure protocol that transmits session tokens, user IDs, and passwords in unencrypted plain text over the wire. This makes it vulnerable to packet sniffing attacks (e.g., via Wireshark). It should always be blocked and replaced by encrypted alternatives like SSH (Port 22). 


**Q6. What are common firewall mistakes?**
**Answer:** Common operational misconfigurations include setting overly permissive rules (like allow any any), placing specific rules below broad rules in priority order, forgetting to clean up temporary testing exceptions, and omitting outbound logging which hinders effective threat hunting during incident response.



**Q7. How does a firewall improve network security?**
**Answer:** A firewall improves security by reducing the overall attack surface, blocking unauthorized network probes on sensitive open ports, mitigating lateral movement during internal compromises, preventing unauthorized data exfiltration, and maintaining logs of blocked malicious events. 



**Q8. What is NAT in firewalls?**
**Answer:**  NAT (Network Address Translation) is a technique where a firewall translates multiple internal private IP addresses into a single public IP address before routing traffic onto the internet. This hides the internal network topology from external actors, providing an additional layer of security.  




----------------------------------------------------------------------------------------------------------------------------




**5. Key Concepts & Tools Used** 
**Primary Scanner:** UFW (Uncomplicated Firewall). 
**Core Concepts:** Packet Inspection, Port Hardening, Access Control Lists (ACLs), TCP Networking.  
