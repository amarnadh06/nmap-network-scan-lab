Nmap TCP SYN Scan Lab Report
1. Scan Overview
Command Executed: nmap -sS 192.168.55.130/24 -oN scan_results.txt -oX scan_results.xml
Target Subnet: 192.168.55.0/24 (VMware Virtual Network)
Total Hosts Scanned: 256 IP addresses (4 hosts up)
2. Discovered Hosts and Open Ports
192.168.55.1 (VMware Host OS Adapter): Port 3306/tcp (mysql) OPEN; 999 ports filtered.
192.168.55.2 (VMware NAT Gateway): Port 53/tcp (domain) FILTERED; 999 ports closed.
192.168.55.254 (VMware DHCP Server): All 1,000 scanned TCP ports FILTERED.
192.168.55.130 (Kali Linux Scanner VM): All 1,000 scanned TCP ports FILTERED.
3. Service Analysis & Security Risks
MySQL (3306/tcp on 192.168.55.1): Runs a relational database server on the host OS. Exposing this port across the virtual interface creates risks of credential brute-forcing, unencrypted traffic sniffing, and potential VM-to-host database compromise.
DNS (53/tcp on 192.168.55.2): Resolves domain names for the NAT subnet. Port 53/tcp is filtered, preventing unauthorized DNS zone transfers.
4. Remediation
Bind the MySQL service strictly to localhost (127.0.0.1) in the database configuration file.
Block inbound TCP port 3306 on the host firewall for virtual network adapters.
5. Repository Files
scan_results.txt - Standard Nmap text output
scan_results.xml - Nmap XML structured output
scan_results.html - Browser-viewable HTML report
