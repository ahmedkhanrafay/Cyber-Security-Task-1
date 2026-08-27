# Cyber Security Internship – Task 1: Network Reconnaissance
### Introduction
As part of the first phase of my cybersecurity internship, I conducted a practical network reconnaissance exercise. The activity focused on actively mapping a local network environment to identify live hosts and active services. This foundational task simulates the initial steps a security analyst or penetration tester takes when evaluating a network's attack surface.

### Objective
The primary objective of this task was to perform a network sweep to discover active devices and identify open ports. By uncovering these exposed network services, the goal was to analyze potential security risks, understand network exposure, and explore remediation strategies for securing local environments.  

### Tool Used
Nmap (Network Mapper): An industry-standard, open-source utility utilized for network discovery and security auditing.  

### Network Details
The reconnaissance was performed on a local Wi-Fi network with the following configuration:

Target IP Address Detected: 192.168.0.7

Subnet Mask: 255.255.255.0

Network Range Scanned: 192.168.0.0/24

Scan Type: TCP SYN Scan (Stealth Scan)

### Command Used
Bash
nmap -sS 192.168.0.0/24 -oN nmap_scan.txt
The -sS flag instructs Nmap to perform a TCP SYN scan, which sends a SYN packet and tears down the connection before completion to bypass basic logging mechanisms.  

The -oN flag outputs the scan results directly into a text file for documentation.

### Scan Results
The scan successfully probed 1000 ports on the local network. Below are the specific open TCP ports identified on the active host (192.168.0.7):

### IP Address Port & Protocol	State	Service
192.168.0.7	   135/tcp	        Open	msrpc
192.168.0.7	   139/tcp	        Open	netbios-ssn
192.168.0.7	   445/tcp	        Open	microsoft-ds
192.168.0.7	   3306/tcp	        Open	mysql

### Service and Security Analysis
Each exposed port represents a specific service running on the target machine, which carries its own set of potential security implications.  

### Port 135 (MSRPC):
Microsoft Remote Procedure Call is used for client-server network applications. Risk: If exposed externally, attackers can query this port to map out internal network services and launch targeted RPC exploits.

### Port 139 (NetBIOS-SSN):
A legacy Windows service used for file and printer sharing. Risk: Can allow unauthorized users to enumerate system information, discover domain details, and potentially access unauthenticated shared resources.

### Port 445 (Microsoft-DS):
Modern Server Message Block (SMB) file sharing. Risk: This is a historically vulnerable port; unpatched SMB services were the entry point for massive ransomware campaigns like WannaCry. Mitigation: Requires strict patching and blocking at the network edge.

### Port 3306 (MySQL):
The default port for MySQL databases. Risk: Exposure to the wider network invites brute-force credential attacks and unauthorized data exfiltration. Mitigation: Should be restricted to allow-listed IP addresses only.

### Security Observations
The presence of an open port simply indicates that a service is listening; it does not guarantee a vulnerability. However, every open port expands the system's attack surface. During this scan, the discovery of database and file-sharing ports on a local machine highlights the importance of internal network segmentation. Services that are not strictly necessary should be disabled. For required services, robust firewall rules must be implemented to restrict access exclusively to trusted network traffic.  

### What I Learned
Through the successful completion of this task, I developed practical skills in:

Determining local network ranges and identifying active IP allocations.  

Executing and analyzing TCP SYN scans using command-line interface tools.  

Mapping raw port numbers to their corresponding network services and protocols.  

Evaluating the security posture of Database Management Systems by identifying exposed backend infrastructure.

Understanding the crucial role network security plays when developing and deploying software, ensuring that future Java applications and databases are configured with network safety in mind.

Documenting technical reconnaissance data for formal security reporting.  

### Files Included
* `nmap_scan.txt` – Saved Nmap scan results
* `nmap_scan_result.png` – Screenshot of the scan results

nmap_scan_result.png – Visual documentation of the terminal scan results.
