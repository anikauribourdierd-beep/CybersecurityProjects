# Penetration Testing Home Lab Using Kali Linux and Metasploitable2

## 🏁 Objective
The goal of this lab is to simulate a basic penetration test in a controlled environment. The lab demonstrates:
- Network discovery  
- Service enumeration
- Exploitation of known vulnerabilities
- Documentation of findings and remediation suggestions

---

## 🖥 Lab Setup
**Virtual Machines:**
- **Kali Linux** (Attacker VM) - KaliLinuxSetup
- **Metasploitable2** (Target VM). –    Metrasploitable2Setup
  - Pre-configured vulnerable machine

**Network Configuration:**
- VirtualBox NAT Network.    (KaliLinuxadAdapter1. --- Metasploitable2Adapter1
- Both VMs on the same subnet.  (Both machines subnet 
- Isolated from untrusted networks.   (give an explanation on why is isolated)

**Tools Used:**
- **Nmap:** This command is a network scanning tool. The purpose is to identify open ports and identify which are exposed.  This command was used to map the attack surface of the machine and identify which ports were not insecure.
- **Metasploit:** This is an open-source penetration testing framework used to develop, test, and run exploits against vulnerable systems. It helps security professionals validate and automate the exploitation of identified weakness.
- **Telnet:** This is a remote access protocol that allows user to connect to a system over a network. This was used on this lab to demonstrate exploitation by logging in with default credential and gain remote access to the target machine 
- **Burp Suite:** Is a security testing tool used to intercept and analyze http traffic. The purpose of this was to inspect and test the web services running on the target system.

---

## 📸 Screenshots & Where to Add Them
All screenshots are stored in the `/screenshots` folder.

1. **Network Discovery**  
   - **Screenshot Name:** `network_scan.png`  
   - **Command Used:** `nmap -sn 192.168.56.0/24`  
   - **Purpose:** Show that you discovered the Metasploitable VM IP.  

2. **Port Scanning**  
   - **Screenshot Name:** `port_scan.png`  
   - **Command Used:** `nmap -sS -sV -A <target_ip>`  
   - **Purpose:** Display open ports, running services, and versions.  

3. **Service Enumeration**  
   - **Screenshot Name:** `service_enum.png`  
   - **Command Used:** `nmap -sV -A <target_ip>`  
   - **Purpose:** Highlight the attack surface (FTP, SSH, HTTP, etc.).  

4. **Exploitation Run**  
   - **Screenshot Name:** `exploit_run.png`  
   - **Command Used:** Metasploit vsftpd exploit  
     ```bash
     use exploit/unix/ftp/vsftpd_234_backdoor
     set RHOSTS <target_ip>
     run
     ```  
   - **Purpose:** Show exploit execution.  

5. **Access Confirmation**  
   - **Screenshot Name:** `access_confirm.png`  
   - **Command Used:** `whoami` / `uname -a`  
   - **Purpose:** Confirm successful access to the target VM.

---

## 🧭 Methodology

1. **Network Discovery**
   - Identified live hosts on the network using Nmap ping scan.
   - Verified target IP.

2. **Port Scanning**
   - Performed TCP SYN scan and service version detection.
   - Recorded open ports and potential vulnerabilities.

3. **Service Enumeration**
   - Analyzed running services (FTP, SSH, HTTP, MySQL).
   - Determined which services were exploitable.

4. **Exploitation**
   - Selected vsftpd 2.3.4 backdoor exploit in Metasploit.
   - Configured target IP and ran exploit.
   - Verified access with `whoami`.

5. **Documentation**
   - Captured screenshots at each step.
   - Noted key findings and potential risks.

---

## ⚠️ Findings & Security Risks
- **Open FTP with backdoor (vsftpd 2.3.4):** Can allow remote code execution.  
- **Open SSH with default credentials:** Could allow unauthorized access.  
- **Other services (HTTP, MySQL):** Potential for misconfiguration or weak passwords.  

> **Remediation Suggestions:**
> - Disable or patch vulnerable services.
> - Change default credentials.
> - Use firewalls to restrict access.

---

## ✅ Key Takeaways
- Successfully demonstrated a penetration testing workflow.
- Learned practical skills in:
  - Host discovery
  - Service enumeration
  - Exploitation in a safe environment
- Documented findings professionally for GitHub showcase.

---

## 📂 Optional: Burp Suite Web Testing
- Intercepted HTTP requests to the Metasploitable web server.
- Observed request/response headers.
- Screenshot can be added as `burp_intercept.png`.

---

## ⛰️ Challenges Faced and How I Overcame Them 
**VirtualBox network configuration issues**
The Kali and Metasploitable machines initially could not communicate due to incorrect adapter settings. This was resolved by properly configuring NAT for internet access and a Host only adapter for the lab network, then verifying connectivity using ip addr, ip route, and ping.

**Confusion between IP addresses and network interfaces**
Multiple IP ranges caused uncertainty about which address to scan. I overcame this by identifying the correct interface and IP using ip link and confirming the target IP through successful ping tests.

**Nmap scans hanging or returning limited results**
Some scans appeared to stall or showed all ports closed. This was resolved by adjusting scan types, running scans with elevated privileges, and narrowing scans to specific ports to improve reliability.

**Exploit attempts not working as expected**
The FTP backdoor exploit did not trigger despite the vulnerable version being identified. I overcame this by pivoting to another exposed service and successfully exploiting Telnet using default credentials.

**Script and package errors in Kali**
Issues with Nmap scripts and package updates occurred due to repository and connectivity problems. These were resolved by fixing network access and confirming internet connectivity before retrying updates.

**Virtual machine usability issues (mouse/pointer not working)**
The Metasploitable virtual machine had persistent mouse and pointer issues that prevented proper interaction. After researching solutions through online resources such as technical articles and community forums, the issue was partially addressed. Ultimately, switching to a laptop and reinstalling both virtual machines from scratch resolved the problem and allowed Metasploitable to function correctly.

**Understanding when to stop scanning and move forward**
It was initially unclear when a phase was complete. This was overcome by clearly separating discovery, enumeration, and exploitation phases and progressing only after each objective was met.

#
