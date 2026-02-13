# 🛡 Active Directory Penetration Testing Lab

![Platform](https://img.shields.io/badge/Platform-Kali%20Linux-blue)
![Target](https://img.shields.io/badge/Target-Windows%20Server%202019-red)
![Environment](https://img.shields.io/badge/Environment-Active%20Directory-green)
![Purpose](https://img.shields.io/badge/Purpose-Penetration%20Testing-orange)

---

## 📌 Project Overview

This project simulates a real-world enterprise Active Directory environment to demonstrate **end-to-end penetration testing**, from reconnaissance to full **Domain Admin compromise**.

The objective was to begin as an external attacker and escalate privileges within a corporate network by identifying and exploiting Active Directory misconfigurations.

---

## 🏗 Lab Architecture

### Attacker Machine
- Kali Linux

### Target Machines
- Windows Server 2019 (Domain Controller)
- Windows 10 Client Machine

### Domain Information

| Component | Value |
|---------|--------|
| Domain Name | corp.local |
| Network Range | 192.168.10.0/24 |
| Domain Controller | 192.168.10.10 |
| Client Machine | 192.168.10.20 |
| Attacker Machine | 192.168.10.30 |

---

## 🛠 Tools Used

| Tool | Purpose |
|-----|---------|
| Nmap | Network scanning and service detection |
| Enum4Linux | SMB enumeration |
| CrackMapExec | SMB and credential validation |
| Responder | Credential harvesting |
| BloodHound | Active Directory privilege analysis |
| Neo4j | BloodHound database backend |
| Impacket | Credential dumping and lateral movement |
| Wireshark | Packet analysis |

---

## 🔎 Attack Methodology

### Phase 1 – Reconnaissance

- Identified open ports and services using Nmap
- Discovered critical services such as:
  - SMB (445)
  - LDAP (389)
  - Kerberos (88)

---

### Phase 2 – Enumeration

- Enumerated domain users via SMB
- Identified shared resources and misconfigurations
- Gathered domain information

---

### Phase 3 – Credential Harvesting

- Captured NTLM hashes using Responder
- Analyzed captured authentication attempts
- Identified reusable credentials

---

### Phase 4 – Active Directory Enumeration

- Collected domain data using BloodHound
- Mapped relationships between users, groups, and systems
- Identified privilege escalation paths

---

### Phase 5 – Exploitation

- Extracted credential hashes using Impacket
- Performed Pass-the-Hash attacks
- Authenticated to Domain Controller

---

### Phase 6 – Privilege Escalation

- Escalated privileges to Domain Admin
- Demonstrated full domain compromise
- Verified administrative access

---

## 🎯 Final Outcome

- Successfully escalated privileges to Domain Admin
- Demonstrated lateral movement across systems
- Compromised entire Active Directory domain
- Documented vulnerabilities and remediation recommendations

---

## 🛡 Defensive Recommendations

To mitigate such attacks, organizations should:

- Disable LLMNR and NBT-NS
- Enforce SMB signing
- Implement Least Privilege Principle
- Monitor suspicious Windows Event IDs:
  - 4624 – Logon events
  - 4625 – Failed logon
  - 4672 – Admin logon
- Enable strong password policies
- Deploy SIEM monitoring solutions

---

## 📚 Key Learnings

- Understanding Active Directory attack methodology
- Real-world credential harvesting techniques
- Privilege escalation strategies in enterprise environments
- Importance of secure Active Directory configuration
- Detection and mitigation of credential-based attacks

---

## 📸 Screenshots

Screenshots available in `/Screenshots` folder:

- Network scan results
- Credential capture proof
- BloodHound privilege graph
- Domain Admin compromise proof

---

## ⚠ Disclaimer

This project was conducted in a controlled lab environment for educational and ethical purposes only.

---

## 👤 Author

**Raghav Nuwal**  
Cybersecurity Enthusiast | Risk Consultant | Penetration Testing Learner

---
