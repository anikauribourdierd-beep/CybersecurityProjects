# Network Setup & Enumeration Lab

## 🏁 Objective

This project focuses on building a functional network infrastructure from scratch in a virtualized environment. The lab covers DHCP and DNS service configuration, network connectivity verification, and basic network enumeration using command-line tools.

---

## 🛠️ Skills Practiced

- Virtual network configuration (VirtualBox Internal Network)
- Linux server configuration (Ubuntu Server)
- DHCP server setup and troubleshooting
- DNS server configuration with BIND9
- Static IP address assignment with Netplan
- Network connectivity testing and verification
- Network enumeration and scanning techniques
- CLI-based network diagnostics

---

## 🧰 Tools Used

**VirtualBox** – Virtualization platform used to create isolated lab environment with multiple VMs and custom network configurations

**Ubuntu Server** – Linux distribution used as the DHCP and DNS server platform

**isc-dhcp-server** – DHCP service that automatically assigns IP addresses to client machines in the 192.168.100.10-50 range

**BIND9** – DNS server software used to resolve domain names to IP addresses within the mylab.local domain

**Netplan** – Ubuntu's network configuration tool used to assign static IP addresses and manage network interfaces

**Kali Linux** – Client machine used for testing DHCP/DNS functionality and performing network enumeration

**Nmap** – Network scanning tool used to discover live hosts, open ports, and running services on the network

**dig** – DNS lookup utility for querying DNS records and testing DNS resolution

**nslookup** – Command-line tool for testing DNS name resolution

**ip** – Linux networking utility for viewing network interfaces, IP addresses, and routing tables

---

## 🧭 Methodology

### 1. 🖥️ Lab Planning & Setup

- Created VirtualBox Internal Network named "LabNet" for isolated testing environment
- Installed Ubuntu Server 22.04 LTS as the network server
- Installed Kali Linux as the client machine for testing and enumeration
- Configured dual network adapters on server (Internal Network + NAT for internet access)

#### 📸 Screenshots

- `screenshots/01-virtualbox-network-setup.png` – VirtualBox Internal Network configuration
- `screenshots/02-ubuntu-server-install.png` – Ubuntu Server installation
- `screenshots/03-kali-client-setup.png` – Kali Linux client VM setup

---

### 2. ⚙️ Static IP Configuration

- Configured static IP address 192.168.100.1/24 on server's enp0s3 interface using Netplan
- Set nameservers to 8.8.8.8 for external DNS resolution
- Configured enp0s8 adapter with DHCP for internet access
- Verified IP configuration with `ip addr` command

#### 📸 Screenshots

- `screenshots/04-netplan-config.png` – Netplan YAML configuration file
- `screenshots/05-static-ip-applied.png` – Static IP successfully applied to enp0s3
- `screenshots/06-dual-adapter-config.png` – Both network adapters configured

---

### 3. 🔧 DHCP Server Configuration

- Installed isc-dhcp-server package
- Configured DHCP to listen on enp0s3 interface
- Created subnet declaration for 192.168.100.0/24 network
- Set IP pool range from 192.168.100.10 to 192.168.100.50
- Configured DHCP options (router, DNS server, domain name)
- Tested configuration syntax with `dhcpd -t` command
- Started and enabled isc-dhcp-server service

#### 📸 Screenshots

- `screenshots/07-dhcp-install.png` – DHCP server package installation
- `screenshots/08-dhcpd-conf.png` – DHCP configuration file
- `screenshots/09-dhcp-interface-config.png` – Interface configuration in /etc/default/isc-dhcp-server
- `screenshots/10-dhcp-service-active.png` – DHCP server running successfully

---

### 4. 🌐 DNS Server Configuration

- Installed BIND9 DNS server packages
- Configured forward zone for mylab.local domain in named.conf.local
- Created zone file db.mylab.local with DNS records
- Added A records for server, ns1, and mylab.local domain
- Validated zone file syntax with `named-checkzone` command
- Validated main configuration with `named-checkconf` command
- Restarted BIND9 service

#### 📸 Screenshots

- `screenshots/11-bind9-install.png` – BIND9 installation
- `screenshots/12-named-conf-local.png` – Zone configuration file
- `screenshots/13-zone-file.png` – DNS zone file with records
- `screenshots/14-zone-syntax-check.png` – Zone file validation
- `screenshots/15-bind9-service-active.png` – DNS server running

---

### 5. ✅ Connectivity Testing & Verification

- Tested DHCP on Kali client machine
- Verified client received IP 192.168.100.10 from DHCP pool
- Tested DNS resolution using nslookup and dig commands
- Verified server.mylab.local resolves to 192.168.100.1
- Tested ping connectivity between client and server
- Confirmed both forward DNS (name to IP) and basic connectivity work

#### 📸 Screenshots

- `screenshots/16-client-dhcp-ip.png` – Kali client receiving DHCP address
- `screenshots/17-dns-nslookup-test.png` – DNS resolution with nslookup
- `screenshots/18-dns-dig-test.png` – DNS resolution with dig
- `screenshots/19-ping-test-by-name.png` – Ping server by hostname
- `screenshots/20-ping-test-by-ip.png` – Ping server by IP address

---

### 6. 🔍 Network Enumeration

- Viewed network configuration with `ip addr` and `ip route` commands
- Checked ARP cache with `ip neigh` to see discovered hosts
- Performed network-wide ping scan with `nmap -sn 192.168.100.0/24`
- Scanned server for open TCP ports with `nmap 192.168.100.1`
- Performed service detection scan with `nmap -sV 192.168.100.1`
- Discovered DNS service running on port 53
- Performed DNS zone transfer test with `dig axfr`
- Attempted reverse DNS lookup (documented PTR record absence)

#### 📸 Screenshots

- `screenshots/21-ip-addr-route.png` – Network interface and routing information
- `screenshots/22-arp-cache.png` – ARP neighbor table
- `screenshots/23-nmap-ping-scan.png` – Network-wide host discovery
- `screenshots/24-nmap-port-scan.png` – TCP port scan results
- `screenshots/25-nmap-service-scan.png` – Service version detection
- `screenshots/26-dns-zone-transfer.png` – DNS zone transfer test
- `screenshots/27-reverse-dns-test.png` – Reverse DNS lookup attempt

---

## 🧗‍♀️ Challenges Faced & How I Overcame Them

**Network adapter configuration issues:** The Ubuntu Server VM had no internet access to install packages. I fixed this by adding a second network adapter (NAT) in VirtualBox settings while keeping Adapter 1 on Internal Network for the isolated lab.

**Netplan YAML indentation errors:** When configuring static IP addresses, netplan threw "expected mapping" and "unknown key" errors. I resolved this by carefully following YAML spacing rules and ensuring nameservers was properly indented at the same level as addresses with correct multi-line format.

**DHCP server refusing to start:** The isc-dhcp-server service failed with "no subnet declaration for enp0s3" errors. I fixed this by specifying `INTERFACESv4="enp0s3"` in `/etc/default/isc-dhcp-server` and ensuring the subnet block was added to `dhcpd.conf`.

**Missing subnet configuration in dhcpd.conf:** I initially added global DHCP options but forgot the actual subnet block. I resolved this by adding the complete subnet 192.168.100.0 declaration with range, routers, and DNS options.

**dhcpd.conf syntax errors:** Encountered "semicolon expected" and "configuration file error" messages due to typos and missing semicolons. I fixed this by running `sudo dhcpd -t -cf /etc/dhcp/dhcpd.conf` to identify exact line numbers and correcting the syntax.

**Static IP not applying to interface:** The netplan configuration didn't apply the 192.168.100.1 address to enp0s3 initially. I verified this using `ip a` and reapplied the configuration with `sudo netplan apply` after fixing YAML formatting issues.

**BIND9 DNS server failing to start:** The named service failed with "'masters' unexpected" error in named.conf.local. I used `sudo named-checkconf` to identify the syntax issue on line 10 and corrected the zone configuration format.

**Client VM DHCP tool not available:** Kali Linux client didn't have `dhclient` command installed by default. I worked around this by using NetworkManager restart and verifying the client successfully received IP 192.168.100.10 from the DHCP pool.

**Reverse DNS lookup failing:** Running `nslookup 192.168.100.1` returned NXDOMAIN because reverse DNS (PTR records) weren't configured. I documented this as a learning point demonstrating the difference between forward and reverse DNS zones.

**DHCP port not visible in basic nmap scan:** Port 67 (DHCP) didn't appear in standard TCP nmap scans because DHCP uses UDP protocol. I resolved this by running `sudo nmap -sU -p 67 192.168.100.1` to specifically scan UDP ports.

**File saving issues in nano editor:** Configuration changes weren't persisting because I wasn't properly saving files in nano. I fixed this by ensuring I pressed Ctrl+X, then Y to confirm save, then Enter to write the file.
