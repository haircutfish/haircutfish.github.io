---
layout: "post"
title: "Sigma Rule Scenario - Antisyphon SOC Summit 2026"
categories: Sigma
tags: Sigma, SOC, Antisyphon, BHIS
---

# The Scenario

## Security Alert: Arasaka Corp targeted by "Flaming Donkey" in localized Cyberattack

**Night City — March 15, 2026**

Arasaka Corp, a leading multinational entity, has confirmed it is investigating a targeted security breach within its accounting department. Digital forensics teams identified the "Flaming Donkey" threat group as the primary orchestrator behind the intrusion.

The compromise originated from a single workstation assigned to an employee identified as Carl. Investigators believe the initial access was achieved through a deceptive social engineering campaign that bypassed traditional perimeter defenses. Once the system was infected, the threat actors utilized native Windows utilities to establish persistence and prepare for data staging.

Security researchers tracking Flaming Donkey note that while the group is known for elaborate and complex cyber attacks, their technical execution in this instance was relatively straightforward. The group focused on executing unauthorized scripts via the Windows Command Processor to modify system configurations.

Early detection of the anomalous activity prevented the actors from moving laterally into Arasaka’s more sensitive research and development networks. The company has since isolated the affected hardware and issued a mandatory credential reset for the entire accounting branch.

---

# The IOCs and TTPs

## Incident Summary and Indicators

The following TTPs (Tactics, Techniques, and Procedures) and IOCs (Indicators of Compromise) were observed during the investigation. Security teams are encouraged to hunt for these specific patterns within their own telemetry.

### Observed TTPs
- Execution: Use of cmd.exe to run hidden batch scripts from temporary directories.
- Persistence: Creation of a scheduled task to ensure the malicious script remains active after a reboot.
- Defense Evasion: Renaming of common tools to mimic legitimate system files.

### Indicators of Compromise (IOCs)
- File Path: C:\Users\Carl\AppData\Local\Temp\update.bat
- Process Command Line: cmd.exe /c "echo flaming_donkey > C:\pwned.txt"
- Network: Outbound connection attempt to 192.168.1.200 on port 4444.

---

# The Goal

You are a SOC analyst, your manager has tasked you with creating a Sigma rule that can be converted into the SIEM solution your organization uses.  Your goals are as follows:
- Use the template below to craft several Sigma rules that detects the observed TTPs and IOCs
- Use tools like [sigma-cli](https://github.com/SigmaHQ/sigma-cli/tree/main) (command line tool) or [sigconverter.io](https://sigconverter.io/) (online gui version) to validate the syntax and structure is correct
- Using the same tools listed above, convert the Sigma Rule into you SIEM query langauge of choice

### Sigma Rule Template
```
title:
id: 
description: 
author: 
date: 
logsource:
    category: 
    product:
detection:
    selection:
    condition: 
level: 
```

### Helpful Links

- [Installation and configuration of *sigma-cli*](https://sigmahq.io/docs/guide/getting-started.html#or-from-source)
- [Online UUID Generator(version 4)](https://www.uuidgenerator.net/version4)
- [List of Available Sigma Field Modifiers](https://sigmahq.io/docs/basics/modifiers.html#sigma-frontmatter-title)
- [Sigma Conditions](https://sigmahq.io/docs/basics/conditions.html)
- [List of Available Sigma Log Sources](https://sigmahq.io/docs/basics/log-sources.html#available-logsources)
- [sigconverter.io](https://sigconverter.io/)

<details>
	<summary>Flaming Donkey File Tampering</summary>
<pre>title: Flaming Donkey File Tampering<br>id: ffc1869f-40c8-4703-99ce-8769ef816510<br>description: Detects the command line execution used by Flaming Donkey to create a proof-of-compromise file.<br>author: HaircutFish<br>date: 2026-03-15<br>logsource:<br>    category: process_creation<br>    product: windows<br>detection:<br>    selection_payload:<br>        Image|endswith: '\cmd.exe'<br>        CommandLine|contains|all:<br>            - '/c'<br>            - 'echo'<br>            - 'flaming_donkey'<br>            - 'pwned.txt'<br>    condition: selection_payload<br>level: High</pre>
</details>

<details>
	<summary>Testing 2</summary>
	```
	title: Flaming Donkey File Tampering
	id: ffc1869f-40c8-4703-99ce-8769ef816510
	description: Detects the command line execution used by Flaming 	Donkey to create a proof-of-compromise file.  
	author: HaircutFish
	date: 2026-03-15
	logsource:
	    category: process_creation
	    product: windows
	detection:
	    selection_payload:
	        Image|endswith: '\cmd.exe'
	        CommandLine|contains|all:
	            - '/c'
	            - 'echo'
	            - 'flaming_donkey'
	            - 'pwned.txt'
	    condition: selection_payload
	level: High
	```
</details>