# Active-Directory-Penetration-Testing-Lab
📌 Project Overview

This project simulates a real-world enterprise Active Directory environment to demonstrate end-to-end penetration testing — from reconnaissance to full Domain Admin compromise.

The objective was to start as an external attacker and escalate privileges within a corporate network.

🏗 Lab Architecture

Attacker Machine:

Kali Linux

Target Machines:

Windows Server 2019 (Domain Controller)

Windows 10 Client Machine

Domain Name:

corp.local


Network:

192.168.10.0/24

🛠 Tools Used

Nmap

Enum4Linux

CrackMapExec

Responder

BloodHound

Neo4j

Impacket

Wireshark

🔎 Attack Methodology
Phase 1 – Reconnaissance

Identified open ports and services using Nmap.

Discovered SMB, LDAP, Kerberos services.

Phase 2 – Enumeration

Enumerated domain users via SMB.

Identified accessible shares and misconfigurations.

Phase 3 – Credential Harvesting

Captured NTLM hashes using Responder.

Performed offline password analysis.

Phase 4 – Active Directory Enumeration

Collected AD data using BloodHound.

Identified privilege escalation paths.

Phase 5 – Exploitation

Extracted password hashes using Impacket.

Conducted pass-the-hash attacks.

Phase 6 – Privilege Escalation

Achieved Domain Admin access.

Demonstrated full domain compromise.

🎯 Final Outcome

✔ Successfully escalated privileges to Domain Admin
✔ Demonstrated lateral movement
✔ Documented vulnerabilities and remediation steps

🛡 Defensive Recommendations

Disable LLMNR & NBT-NS

Enforce SMB signing

Implement least privilege access

Monitor suspicious Event IDs

Enable strong password policies

📚 Key Learnings

Understanding of AD attack paths

Credential-based attacks in enterprise networks

Real-world red team simulation experience

Importance of proper AD hardening
