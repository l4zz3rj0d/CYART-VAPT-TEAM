# Vulnerability Assessment and Penetration Testing (VAPT) – Week 2

## Overview
This repository documents a structured Vulnerability Assessment and Penetration
Testing (VAPT) workflow carried out in an authorized and controlled lab
environment. The objective is to demonstrate practical security testing skills,
methodology, and proper technical documentation.

The workflow covers network-level assessment, manual exploitation, post-
exploitation validation, web application testing, and automated vulnerability
scanning.

---

## Scope and Authorization
- Target Type: Deliberately vulnerable systems
- Testing Type: Educational / Authorized lab assessment
- Scope: Network services, system-level vulnerabilities, and web application
  vulnerabilities
- All activities were performed strictly for learning and demonstration purposes

---

## VAPT Workflow Summary

1. Network Scanning and Enumeration  
2. Vulnerability Identification  
3. Exploitation  
4. Post-Exploitation  
5. Web Application VAPT (DVWA)  
6. Automated Vulnerability Scanning 

---

## Phase 1: Network Scanning and Enumeration

**Tool Used:** Nmap  

### Activities
- Full TCP port scanning
- Service and version detection
- Identification of exposed and potentially vulnerable services

###  Command Used
```
nmap -sC -sV -p- <target-ip>
Outcome
Multiple network services were identified running outdated or insecure versions,
indicating a broad attack surface for further assessment.

Evidence Location

swift
Copy code
Week 2/Scanning/
Phase 2: Vulnerability Identification
Based on enumeration results, identified services were analyzed for known
weaknesses and misconfigurations.

Key Observations
Insecure and legacy services exposed to the network

Weak authentication mechanisms

Services commonly associated with publicly known exploits

A vulnerability mapping table was created to correlate services with risk level
and potential impact.

Documentation

bash
Copy code
Week 2/Scanning/vulnerability_table.md
Phase 3: Exploitation
Tool Used: Metasploit Framework

Activities
Selection of exploit modules based on identified services

Successful exploitation of vulnerable service

Shell access obtained on the target system

Result
The target system was successfully compromised, and root-level access was
achieved due to critical security misconfigurations. This confirms a high to
critical severity impact.

Evidence Location

swift
Copy code
Week 2/Exploitation/
Phase 4: Post-Exploitation
Activities
Verification of privilege level

Confirmation of full system compromise

Collection of evidence to validate impact

Outcome
Post-exploitation confirmed complete system control, validating the severity of
the identified vulnerabilities.

Evidence Location

swift
Copy code
Week 2/Post-Exploitation/
Phase 5: Web Application VAPT (DVWA)
Application Tested: Damn Vulnerable Web Application (DVWA)

Vulnerability Identified
SQL Injection due to improper input validation

Exploitation Method
Authenticated SQL Injection testing was performed using automated tooling.

bash
Copy code
sqlmap -u "http://<target-ip>/vulnerabilities/sqli/?id=1&Submit=Submit#" \
--cookie="security=low; PHPSESSID=<session-id>" \
-D dvwa -T users --dump
Results
Backend DBMS identified as MySQL

Databases and tables enumerated successfully

Sensitive user information extracted from the users table

Multiple SQL Injection techniques confirmed:

Boolean-based

Error-based

Time-based

UNION-based

Evidence Location

swift
Copy code
Week 2/Capstone/
Phase 6: Automated Vulnerability Scanning (OpenVAS)
Tool: OpenVAS / Greenbone Vulnerability Manager

Status
Scanner environment configured

Vulnerability feeds synchronized

Automated scan execution pending due to tool stabilization issues in the lab
environment

Automated scan results will be added once execution is completed. Manual testing
and exploitation were prioritized to ensure continuity of the VAPT workflow.

Reserved Directory

swift
Copy code
Week 2/OpenVAS/
Repository Structure
nix
Copy code
Week 2/
├── Scanning/
├── Exploitation/
├── Post-Exploitation/
├── Capstone/
├── OpenVAS/
└── README.md
Key Takeaways
Manual enumeration is essential for accurate vulnerability discovery

Exploitation validates real-world impact beyond automated scan results

Authenticated web application testing exposes critical vulnerabilities

Automated tools support, but do not replace, structured methodology

Disclaimer
All activities documented in this repository were performed in authorized and
controlled lab environments for educational purposes only.
