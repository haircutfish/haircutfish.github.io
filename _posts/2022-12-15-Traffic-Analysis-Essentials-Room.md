---
layout: "post"
title: "TryHackMe Traffic Analysis Essentials Room"
categories: Traffic-Analysis-Essentials
tags: TryHackMe, Traffic Analysis, SOC Level One Path
---



Learn Network Security and Traffic Analysis foundations and take a step into probing network anomalies.

## Task 1 Introduction

Network Security is a set of operations for protecting data, applications, devices and systems connected to the network. It is accepted as one of the significant subdomains of cyber security. It focuses on the system design, operation and management of the architecture/infrastructure to provide network accessibility, integrity, continuity and reliability. Traffic analysis (often called Network Traffic Analysis) is a subdomain of the Network Security domain, and its primary focus is investigating the network data to identify problems and anomalies.

This room will cover the foundations of Network Security and Traffic analysis and introduce the essential concepts of these disciplines to help you step into Traffic/Packet Analysis. We suggest completing the “[**Network Fundamentals**](https://tryhackme.com/module/network-fundamentals)” module before starting working in this room.

## Task 2 Network Security and Network Data

![](https://miro.medium.com/max/630/0*5S50Vnq8w1M3stLw.png)

### Network Security

The essential concern of Network Security focuses on two core concepts: authentication and authorization. There are a variety of tools, technologies, and approaches to ensure and measure implementations of these two key concepts and go beyond to provide continuity and reliability. Network security operations contain three base control levels to ensure the maximum available security management.

**Base Network Security Control Levels:**

![](https://miro.medium.com/max/630/1*5FTtLAoVbafARkO5LOeaww.png)

There are two main approaches and multiple elements under these control levels. The most common elements used in network security operations are explained below.

**The main approaches:**

![](https://miro.medium.com/max/630/1*eJOIixkvoos3BhuSe2YEdA.png)

**The key elements of Access Control:**

![](https://miro.medium.com/max/630/1*ELOotN7ICXMNQIuZ6N3_EA.png)

**The key elements of Threat Control:**

![](https://miro.medium.com/max/630/1*QEKT9BpvMFbchxgSks27wg.png)

**Typical Network Security Management Operation is explained in the given table:**

![](https://miro.medium.com/max/630/1*jsFxgBUc_w2hQGYDcf86Iw.png)

### Managed Security Services

Not every organisation has enough resources to create dedicated groups for specific security domains. There are plenty of reasons for this: budget, employee skillset, and organisation size could determine how security operations are handled. At this point, Managed Security Services (MSS) come up to fulfil the required effort to ensure/enhance security needs. MSS are services that have been outsourced to service providers. These service providers are called Managed Security Service Providers (MSSPs). Today, most MSS are time and cost effective, can be conducted in-house or outsourced, are easy to engage, and ease the management process. There are various elements of MSS, and the most common ones are explained below.

![](https://miro.medium.com/max/630/1*zpkkNNHQJdaKg2vYuL5Acw.png)

## Answer the questions below

Since the answer can be found above, I won’t be posting the answers below. Follow along to help find the answer.

### Which Security Control Level covers contain creating security policies?

Go up to the Base Network Security Control Levels table, in this table you will find the answer, just read through. Once you find it, Highlight copy (ctrl + c) and paste (ctrl + v) or type, the answer into the TryHackMe answer Field, then click submit.

![](https://miro.medium.com/max/630/1*YGIMpEAVGYYoCpBhu27dAw.png)

### Which Access Control element works with data metrics to manage data flow?

Scroll up to The Key Elements of Access Control table, in this table you will find the answer, manage data flow is the key. Once you find it, Highlight copy (ctrl + c) and paste (ctrl + v) or type, the answer into the TryHackMe answer Field, then click submit.

![](https://miro.medium.com/max/630/1*aA03GaHRJWnGjSPkktty9g.png)

### Which technology helps correlate different tool outputs and data sources?

Scroll up to The Key Elements of Threat Control table, the answer can be found towards the bottom of this table. TryHackMe is looking for the acronym for the answer. Once you find it, Highlight copy (ctrl + c) and paste (ctrl + v) or type, the answer into the TryHackMe answer Field, then click submit.

![](https://miro.medium.com/max/630/1*Z6gKsr5T3D1yOlVgO-BSAA.png)


## Task 3 Traffic Analysis

![](https://miro.medium.com/max/630/0*Tk7qSMyJe-4yDuhX.png)

### Traffic Analysis / Network Traffic Analysis

Traffic Analysis is a method of intercepting, recording/monitoring, and analysing network data and communication patterns to detect and respond to system health issues, network anomalies, and threats. The network is a rich data source, so traffic analysis is useful for security and operational matters. The operational issues cover system availability checks and measuring performance, and the security issues cover anomaly and suspicious activity detection on the network.

Traffic analysis is one of the essential approaches used in network security, and it is part of multiple disciplines of network security operations listed below:

-   Network Sniffing and Packet Analysis (Covered in  [**Wireshark room**](https://tryhackme.com/room/wiresharkthebasics))
-   Network Monitoring (Covered in  [**Zeek room**](https://tryhackme.com/room/zeekbro))
-   Intrusion Detection and Prevention (Covered in  [**Snort room**](https://tryhackme.com/room/snort))
-   Network Forensics (Covered in  [**NetworkMiner room**](https://tryhackme.com/room/networkminer))
-   Threat Hunting (Covered in  [**Brim room**](https://tryhackme.com/room/brim))

There are two main techniques used in Traffic Analysis:

![](https://miro.medium.com/max/630/1*-APJRQB6c6d2g7DC4y1IlA.png)

Benefits of the Traffic Analysis:

-   Provides full network visibility.
-   Helps comprehensive baselining for asset tracking.
-   Helps to detect/respond to anomalies and threats.

### Does the Traffic Analysis Still Matter?

The widespread usage of security tools/services and an increasing shift to cloud computing force attackers to modify their tactics and techniques to avoid detection. Network data is a pure and rich data source. Even if it is encoded/encrypted, it still provides a value by pointing to an odd, weird or unexpected pattern/situation. Therefore traffic analysis is still a must-to-have skill for any security analyst who wants to detect and respond to advanced threats.

Now you know what Traffic Analysis is and how it operates. Now use the static site to simulate a traffic analysis operation and find the flags.

## Answer the questions below

At the top of the task, click the green View Site button.

![](https://miro.medium.com/max/238/1*Be36jz9H20uPVSdCISnbZA.png)

The screen will split, and you will be ready to start.

![](https://miro.medium.com/max/630/1*2XAChB9tH13zzQNeOv2NUA.png)

### **Level-1**  is simulating the identification and filtering of malicious IP addresses.

Click the black Start Network Traffic button.

![](https://miro.medium.com/max/630/1*FHRAPwsAmv_HUpW5j5OuXw.png)

You will see traffic running across the network, but uh-no we got malware!!! So a black button labeled Restore the Network and record the traffic for further investigation, click this button.

![](https://miro.medium.com/max/630/1*PQ0gwn2Cn_uCxRK3Zx6qag.png)

So we will have traffic run over the network again, this time we are getting logs of what is running over it. Once we have enough logs, you will be instructed to analyze the data to find two IP addresses to filter through the firewall. Looking through the IDS/IPS system, we can see a couple of suspicious IP addesses.

![](https://miro.medium.com/max/577/1*Bdpboz2_qZkpjNpwLlNnpw.png)

Highlight copy (ctrl + c) and paste (ctrl + v) or type the IP addresses into the Filter box, then click the blue Add to Filter.

![](https://miro.medium.com/max/577/1*dLsb-s5EZCSftkLwzH67Kg.png)

Once you have added both of them, you will have a black Restart Network Traffic Button. Click it.

![](https://miro.medium.com/max/472/1*pksn1yKhY561iR2OOYk6Jw.png)

After restarting the Network Traffic, you will have successfully block the malware. You will get a pop-up window, this window will contain the first flag. Type the answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/290/1*f_YmjzkMUW2UQX3kJKNCEA.png)

### What is the flag?

**Answer: THM{PACKET_MASTER}**

### **Level-2**  is simulating the identification and filtering of malicious IP and Port addresses.

Now we are tasked with blocking destination ports, we need to get these from the Traffic Analyzer table. If we look at the sus IP addresses from the previous question, along with number five, since it is labeled as Suspicious ARP Behavior. We can see the destination ports they correlate to in the Traffic Analyzer table on the right.

![](https://miro.medium.com/max/510/1*qMAt5mkBV88DsdJTxW3abg.png)

Since we only need the port numbers, Highlight copy (ctrl + c) and paste (ctrl + v) or type, the port number into the Filter box, then click the blue Add to Filter.

![](https://miro.medium.com/max/510/1*1ph5M39ndJ8W-dHrMG1aYw.png)

Once you have added all the ports, a black Restart Network Traffic button will apper. Click it.

![](https://miro.medium.com/max/499/1*v1D815nH-ZcOJT0yZKVScg.png)

After restarting the Network Traffic, you will have successfully block the malware. You will get a pop-up window, this window will contain the first flag. Type the answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/258/1*oo-Qck0etqJvL4rUXqfb4g.png)

### What is the flag?

**Answer: THM{DETECTION_MASTER}**

## Task 4 Conclusion

**Congratulations!** You just finished the “Traffic Analysis Essentials” room.

In this room, we covered the foundations of the network security and traffic analysis concepts:

-   Network Security Operations
-   Network Traffic Analysis

Now, you are ready to complete the  **“Network Security and Traffic Analysis”**  module.

🎉🎉🎉CONGRAT!!!! You completed the Traffic Analysis Essentials Room🎉🎉🎉