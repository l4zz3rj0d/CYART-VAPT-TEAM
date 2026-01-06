# Vulnerability Assessment and Penetration Testing 

## 1. Vulnerability Scanning Techniques

### 1.1 Introduction to Vulnerability Scanning
Vulnerability scanning is the process of identifying security weaknesses in
systems, networks, and applications using automated and manual techniques. It
helps organizations understand their attack surface and prioritize risks before
they are exploited by attackers. Vulnerability scanning is a foundational
activity in vulnerability assessment and penetration testing (VAPT).

---

### 1.2 Types of Vulnerability Scans

#### Network-Based Scanning
Network-based scanning focuses on identifying open ports, running services, and
service versions exposed on a target system. Tools such as **Nmap** are commonly
used to enumerate network services and detect potential entry points for
attackers.

#### Application-Based Scanning
Application scanning focuses on identifying vulnerabilities in web applications,
such as SQL Injection, Cross-Site Scripting (XSS), insecure configurations, and
outdated components. Tools such as **Nikto** and vulnerability scanners are used
to identify common web-related security issues.

#### Authenticated vs Unauthenticated Scanning
- **Unauthenticated scanning** simulates an external attacker without valid
  credentials and identifies publicly exposed vulnerabilities.
- **Authenticated scanning** uses valid credentials to perform deeper analysis
  and detect internal issues such as weak configurations and missing patches.

---

### 1.3 Vulnerability Scoring – CVSS
The **Common Vulnerability Scoring System (CVSS)** is used to assess the severity
of identified vulnerabilities. CVSS assigns a numerical score between **0.0 and
10.0**, helping organizations prioritize remediation efforts.

Severity levels:
- **Low:** 0.1 – 3.9  
- **Medium:** 4.0 – 6.9  
- **High:** 7.0 – 8.9  
- **Critical:** 9.0 – 10.0  

For example, **Remote Code Execution (RCE)** vulnerabilities often score High to
Critical due to their potential to fully compromise a system.

---

### 1.4 False Positives in Scanning
Automated vulnerability scanners may report issues that are not practically
exploitable, known as **false positives**. Therefore, scan results must be
validated manually through service interaction, configuration review, and
controlled exploitation attempts to confirm real security risks.

---

### 1.5 Objectives of Vulnerability Scanning
The primary objectives of vulnerability scanning are to:
- Identify exposed services and misconfigurations
- Assess risk using CVSS scoring
- Provide accurate input for penetration testing
- Support informed remediation and risk management decisions

---

## 2. Penetration Testing Techniques

### 2.1 Introduction to Penetration Testing
Penetration testing is a controlled and authorized security assessment that
simulates real-world attacks to evaluate the security posture of systems and
applications. Unlike vulnerability scanning, penetration testing involves
active exploitation to validate the impact of identified vulnerabilities.

---

### 2.2 Phases of Penetration Testing

#### Reconnaissance
Information gathering to identify exposed services, technologies, and potential
attack vectors using both network-based and web-based inspection techniques.

#### Scanning and Enumeration
Identifying open ports, running services, and service versions to expand the
attack surface and identify exploitable components.

#### Exploitation
Actively exploiting identified vulnerabilities to gain unauthorized access or
execute code on the target system.

#### Post-Exploitation
Evaluating the impact of access by performing privilege escalation, accessing
sensitive data, and validating the extent of system compromise.

#### Reporting
Documenting findings, severity, impact, and remediation recommendations in a
clear and structured manner.

---

### 2.3 Penetration Testing Methodologies
Standard methodologies provide structured guidance for penetration testing.
Commonly used methodologies include:
- **Penetration Testing Execution Standard (PTES)**
- **OWASP Web Security Testing Guide (WSTG)**

These methodologies ensure ethical, consistent, and repeatable testing
processes.

---

### 2.4 Ethics and Legal Considerations
Penetration testing must always be performed with explicit authorization and
within a defined scope. Unauthorized testing is illegal and unethical. Ethical
penetration testing ensures responsible disclosure and avoids unnecessary system
damage.

---

## 3. Exploit Development Basics

### 3.1 Introduction to Exploits
An exploit is a technique or piece of code used to take advantage of a
vulnerability. Exploits demonstrate the real-world impact of security
weaknesses and help validate the severity of vulnerabilities.

---

### 3.2 Common Types of Exploits

#### Buffer Overflow
Occurs when a program writes more data than allocated memory, potentially
allowing arbitrary code execution.

#### SQL Injection
Occurs when untrusted input is improperly handled in database queries, allowing
attackers to manipulate or retrieve sensitive data.

#### Cross-Site Scripting (XSS)
Occurs when user input is not properly sanitized, allowing malicious scripts to
execute in a victim’s browser.

---

### 3.3 Proof of Concept (PoC) Exploits
Public exploit repositories provide Proof of Concept (PoC) code to demonstrate
known vulnerabilities. These PoCs should only be used in controlled lab
environments for learning and validation purposes.

---

### 3.4 Security Mitigations
Modern systems implement multiple mitigations to reduce exploitability, such as:
- Address Space Layout Randomization (ASLR)
- Web Application Firewalls (WAF)
- Secure coding practices
- Regular patching and updates

These controls significantly reduce the likelihood of successful exploitation.

---

## 4. Conclusion
A strong understanding of vulnerability scanning, penetration testing
methodologies, and exploit fundamentals is essential for effective VAPT.
Accurate risk assessment, ethical conduct, and structured documentation are
critical components of professional cybersecurity practice.
