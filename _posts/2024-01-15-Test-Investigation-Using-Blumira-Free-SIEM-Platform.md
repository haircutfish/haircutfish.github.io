---
layout: "post"
title: "Test Investigation Using Blumira Free SIEM Platform"
categories: Blumira
tags: Blumira, SIEM, SOC, Investigation
---

----------

![](https://cdn-images-1.medium.com/max/640/0*ZH7ns9HmAmLUKlzx.jpg)

I first want to thank [Secure Point Solutions](https://www.secureps.net) for their aid in this investigation. They helped by allowing me access to their demo account. All alerts mentioned were randomly generated and not linked to any actual customer account. From the alerts, I have done an investigation and given my thought and remediation steps. Along with mapping to MITRE ATT&CK and NIST Password Policy. Enjoy!!

### Scanning for Vulnerabilities

**F-24–02–459B — Jan 8, 2024 11:20 AM EST — P2 — Reconnaissance Scanning from Known Threat:**

> An external to internal scan was detected based on Palo Alto Firewall traffic anomalies from 95.165.149.124 and 106.12.212.39 to 10.23.2.8, 10.23.2.10, and 10.23.2.12 over 3389, 1433, and 443 ports. This indicates that an external threat actor is attempting to determine which of your hosts are vulnerable. Additionally, the 95.165.149.124 and 106.12.212.39 were determined to be on at least one threat feed, Cisco Talos and Proofpoint Emerging Threats, at the time of scanning.

The attacker was using the Reconnaissance Tactic, and more specifically [MITRE ATT&CK ID T1595](https://attack.mitre.org/techniques/T1595/), Active Scanning. Which is used to find vulnerabilities within our systems. Additionally, said IP address have appeared on the Cisco Talos and Proofpoint Emerging Threats threat feeds.

### Remediation:

The ability to mitigate this issues is a difficult one, as if is outside the network and therefore outside your influence. But some steps you can take are limiting the traffic that goes to these ports. If they fit certain criteria (ie. ICMP packets, attacker sending only SYN packets, etc.), restricting access via a firewall to any unused ports, or since the IP address have appeared on the Threat Feed. Place them on the IP Blocklist.

----------

### Attempting Access to the System

**F-24–02–9459 — Jan 8, 2024 11:20 AM EST — P2 — Duo Access Denied — Likely Credential Compromise:**

> Blumira has detected a Duo Access Denied event for jsnow from RU. The user purposely denied the Push authentication request and selected User Marked Fraud after a successful primary authentication. This indicates that the jsnow’s primary credentials have likely been stolen and an attacker is attempting to access your systems.

**F-24–02-E88F — Jan 8, 2024 11:20 AM EST — P2 — G Suite Authentication Attempt from Geographically Unlikely Location:**

> Blumira has detected a G Suite sign-in by user from a location deemed unlikely for a user to travel to across two successive sign-in attempts. This may indicate that the user’s credentials have been stolen and an attacker is attempting to access your systems.

It appears that user credentials have become compromised, and the attacker is attempting to log in. Though, they are currently being stopped by 2FA. This doesn’t mean that they were completely unsuccessful. As it appears, multiple users credentials have been compromised. Furthermore, these alerts line up with the [MITRE ATT&CK ID T1621](https://attack.mitre.org/techniques/T1621/), Multi-Factor Authentication Request Generation. Which is where an attacker will attempt to bypass 2FA by either spamming the users with 2FA notifications or hope a user clicks the accept button out of habit or by accident.

### Remediation:

Using a more secure type of 2FA/MFA, where the user will need to put a code in to gain access. Enacting policies on 2FA where a check is made of the location of the attempt. If it does not match the usual location of the user or is in a different location than the 2FA device, it will be a denial automatically and logged.

In the case of the compromised passwords. Find out which users have potentially compromised passwords. Then inform them that they will have to change them in the next 7 days. If this is not possible, then they will need to contact the Help Desk to get their password reset. A way to help mitigate this issue is having a good password policy in place. Here is a link to the [NIST Password Guidelines 2023](https://www.auditboard.com/blog/nist-password-guidelines/), to aid you.

The other step that can be taken applies to by 2FA and User Credentials. Training End Users with the knowledge and know how needed to spot suspicious behavior can be the key to early detection. As well as mitigating account compromises. With regard to 2FA, tell the End User, unless they specifically are attempting to gain access or verify that it is in fact them. Always click Deny. For the latter, making sure that the end users know the password policies and the importance of a strong password.

----------

### Attacker Detected in the System

**F-24–02–244F — Jan 8, 2024 11:20 AM EST — P1 — Hacker Tool: Credential Stealing:**

> Host hq-dc1.phys.local at 10.1.2.2 was detected via endpoint AV logs executing the Hacker Tool Mimikatz. This detection indicates an attacker has gained access to hq-dc1.phys.local via jsmitha and is running Mimikatz in memory in an attempt to gain access to credentials.

The use of **Mimikatz** on this system indicated that the attacker was attempting to gain access to the credentials stored on the system. This is an indication of [MITRE ATT&CK ID T1555](https://attack.mitre.org/techniques/T1555/), Credentials From Password Stores. Once the attacker had the credentials of other users, they could potentially access their systems and either move laterally or elevate their privileges.

### Remediation:

Remove Mimikatz from the effected computer. End any active session, and force a password reset upon next log in. Additionally, create [ASR (Attack Service Reduction)](https://attack.mitre.org/mitigations/M1040/#:~:text=OS%20Credential%20Dumping-,On%20Windows%2010%2C%20enable%20Attack%20Surface%20Reduction%20%28ASR%29%20rules%20to%20secure%20LSASS%20and%20prevent%20credential%20stealing,-.%20%5B1%5D) rules to secure LSASS and prevent accounts from stealing credentials. Setting Defender or Anti-virus/malware software of choice to scan every download for known threats. If one is detected, then it is not downloaded. Furthermore, limiting the number of accounts and programs/services that are allowed to access the password stores. While also only allowing said accounts and programs/software to access the passwords stores it requires.

----------

### Data Exfiltration/Access

**F-24–02–0CF6 — Jan 8, 2024 11:20 AM EST — P3 — G Suite Document Was Shared Externally:**

> Blumira has detected the user account user has modified a document type of Google Sheets named ‘All Company HR Info’ from ‘Private’ to ‘Shared Externally’. This type of activity can expose internal documents and files to external entities as well as allow for data exfiltration for malicious purposes. Blumira recommends that file and share permissions within Google G Suite be audited on a regular basis and employees instructed on proper protocols and procedures regarding sensitive data.

This is a technique falls inline with [MITRE ATT&CK ID T1567](https://attack.mitre.org/techniques/T1567/), Exfiltration Over Web Service. As the attacker has changed the permissions for a company file to **_Shared Externally_**. It would give them access to this document from anywhere on the internet.

### Remediation:

Start by changing the permissions back to Private. Then only allowing accounts that need to have access to this document, to have access to this document. Ensuring that accounts use the least privileged required.

----------

Even though these alerts were randomly generated. It gives you a real glimpse at how attacker Recon, Access, Persist, and Exfil. These steps are part of the [Cyber Kill Chain](https://medium.com/@haircutfish/tryhackme-cyber-kill-chain-room-a0ebcff024a9). The Cyber Kill Chain is a Security Framework used to help understand attackers and the steps they take.

If you enjoyed this, check out my other write-ups here on medium or over on my personal webpage [Haircutfish.com](https://haircutfish.com)