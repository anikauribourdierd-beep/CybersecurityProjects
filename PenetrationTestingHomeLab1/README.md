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
- Nmap 
- Metasploit
- Telnet (optional)
- Burp Suite (optional)

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

## 💡 Tips for GitHub Presentation
- Include clear **descriptive filenames** for screenshots.  
- Use Markdown syntax to embed images:

```markdown
![Network Scan](screenshots/network_scan.png)
