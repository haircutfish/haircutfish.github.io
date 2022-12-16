---
layout: "post"
title: "TryHackMe Snort — Task 1 Introduction, Task 2 Interactive Material and VM, & Task 3 Introduction to IDS/IPS"
---

# TryHackMe Snort — Task 1 Introduction, Task 2 Interactive Material and VM, & Task 3 Introduction to IDS/IPS

Learn how to use Snort to detect real-time threats, analyse recorded traffic files and identify anomalies.

## Task 1 Introduction

![](https://miro.medium.com/max/630/0*K9Cq35gBJ9ZI5je9.png)

This room expects you to be familiar with basic Linux command-line functionalities like general system navigation and Network fundamentals (ports, protocols and traffic data). The room aims to encourage you to start working with Snort to analyse live and captured traffic.

Before joining this room, we suggest completing the  [‘Network Fundamentals’](https://tryhackme.com/module/network-fundamentals)  module. If you have general knowledge of network basics and Linux fundamentals, you will be ready to begin! If you feel you need assistance in the Linux command line, you can always refer to our “Linux Fundamentals” rooms (here  [1](https://tryhackme.com/room/linuxfundamentalspart1)  [2](https://tryhackme.com/room/linuxfundamentalspart2)  [3](https://tryhackme.com/room/linuxfundamentalspart3));

SNORT is an  **open-source, rule-based**  Network Intrusion Detection and Prevention System  **(NIDS/NIPS)**. It was developed and still maintained by Martin Roesch, open-source contributors, and the Cisco Talos team.

[**The official description**](https://www.snort.org/)**:**  _“Snort is the foremost Open Source Intrusion Prevention System (IPS) in the world. Snort IPS uses a series of rules that help define malicious network activity and uses those rules to find packets that match against them and generate alerts for users.”_

## Task 2 Interactive Material and VM

![](https://miro.medium.com/max/630/0*6dmjXBzcdJu7Q18i.png)

**Interactive material and exercise setup**

Deploy the machine attached to this task; it will be visible in the  **split-screen**  view once it is ready. If you don’t see a virtual machine load, click the  **Show Split View**  button.

![](https://miro.medium.com/max/630/0*PWxPdrf4HcLMbwWQ.png)

Once the machine had fully started, you will see a folder named “**Task-Exercises**” on the Desktop. Each exercise has an individual folder and files; use them accordingly to the questions.

Everything you need is located under the “**Task-Exercises**” folder.

There are two sub-folders available;

-   Config-Sample **—** Sample configuration and rule files. These files are provided to show what the configuration files look like. Installed Snort instance doesn’t use them, so feel free to practice and modify them. Snort’s original base files are located under  **/etc/snort** folder.
-   Exercise-Files **—** There are separate folders for each task. Each folder contains pcap, log and rule files ready to play with.

![](https://miro.medium.com/max/630/0*qJAnkyUepb8R6frU.png)

**Traffic Generator**

The machine is offline, but there is a script (**traffic-generator.sh**) for you to generate traffic to your snort interface. You will use this script to trigger traffic to the snort interface. Once you run the script, it will ask you to choose the exercise type and then automatically open another terminal to show you the output of the selected action.

**Note that each traffic is designed for a specific exercise. Make sure you start the snort instance and wait until to end of the script execution. Don’t stop the traffic flood unless you choose the wrong exercise.**

Run the  **“traffic generator.sh”**  file by executing it as sudo.

executing the traffic generator script

user@ubuntu$ sudo ./traffic-generator.sh

General desktop overview. Traffic generator script in action.

![](https://miro.medium.com/max/630/0*hn1lY099jtNamPjv.png)

Once you choose an action, the menu disappears and opens a terminal instance to show you the output of the action.

![](https://miro.medium.com/max/630/0*OLYA3ZtAU3VCnRLB.png)

## Answer the questions below

### Navigate to the Task-Exercises folder and run the command “./.easy.sh” and write the output

Click the small terminal icon, in the top left of the VM.

![](https://miro.medium.com/max/630/1*y83d2Zy3AT4OBOS2o_qqqw.png)

In the window that pops up type, cd Desktop/Task-Exercises/ . Then press enter to navigate to this directory.

![](https://miro.medium.com/max/530/1*rDJteOCR8WXd2c6vUP_oqg.png)

Type the command, given to you by the question, into the terminal. The output is going to be the answer. Type it into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/390/1*QIK58Wqr-IXdPUYVyTPelw.png)

**Answer: Too Easy!**

## Task 3 Introduction to IDS/IPS

![](https://miro.medium.com/max/630/0*ggmoPUy2JqM4Dk_y.png)

Before diving into Snort and analysing traffic, let’s have a brief overview of what an Intrusion Detection System (IDS) and Intrusion Prevention System (IPS) is. It is possible to configure your network infrastructure and use both of them, but before starting to use any of them, let’s learn the differences.

### **Intrusion Detection System (IDS)**

IDS is a passive monitoring solution for detecting possible malicious activities/patterns, abnormal incidents, and policy violations. It is responsible for generating alerts for each suspicious event.

**There are two main types of IDS systems;**

-   **Network Intrusion Detection System (NIDS) —** NIDS monitors the traffic flow from various areas of the network. The aim is to investigate the traffic on the entire subnet. If a signature is identified,  **an alert is created**.
-   **Host-based Intrusion Detection System (HIDS) —** HIDS monitors the traffic flow from a single endpoint device. The aim is to investigate the traffic on a particular device. If a signature is identified,  **an alert is created.**

### **Intrusion Prevention System (IPS)**

IPS is an active protecting solution for preventing possible malicious activities/patterns, abnormal incidents, and policy violations. It is responsible for stopping/preventing/terminating the suspicious event as soon as the detection is performed.

**There are four main types of IPS systems;**

-   **Network Intrusion Prevention System (NIPS) —** NIPS monitors the traffic flow from various areas of the network. The aim is to protect the traffic on the entire subnet. If a signature is identified, **the connection is terminated**.
-   **Behaviour-based Intrusion Prevention System (Network Behaviour Analysis — NBA) —** Behaviour-based systems monitor the traffic flow from various areas of the network. The aim is to protect the traffic on the entire subnet. If a signature is identified,  **the connection is terminated.**

Network Behaviour Analysis System works similar to NIPS. The difference between NIPS and Behaviour-based is; behaviour based systems require a training period (also known as “baselining”) to learn the normal traffic and differentiate the malicious traffic and threats. This model provides more efficient results against new threats.

The system is trained to know the “normal” to detect “abnormal”. The training period is crucial to avoid any false positives. In case of any security breach during the training period, the results will be highly problematic. Another critical point is to ensure that the system is well trained to recognise benign activities.

-   **Wireless Intrusion Prevention System (WIPS) —** WIPS monitors the traffic flow from of wireless network. The aim is to protect the wireless traffic and stop possible attacks launched from there. If a signature is identified,  **the connection is terminated**.
-   **Host-based Intrusion Prevention System (HIPS) —** HIPS actively protects the traffic flow from a single endpoint device. The aim is to investigate the traffic on a particular device. If a signature is identified,  **the connection is terminated.**

HIPS working mechanism is similar to HIDS. The difference between them is that  **while HIDS creates alerts for threats,**  **HIPS stops the threats by terminating the connection.**

### **Detection/Prevention Techniques**

There are three main detection and prevention techniques used in IDS and IPS solutions;

![](https://miro.medium.com/max/630/1*zKgoSNP9-pQ2PECApmXHVQ.png)

### **Summary**

**Phew!** That was a long ride and lots of information. Let’s summarise the overall functions of the IDS and IPS in a nutshell.

-   **IDS** can identify threats but require user assistance to stop them.
-   **IPS** can identify and block the threats with less user assistance at the detection time.

**Now let’s talk about Snort.** [**Here is the rest of the official description**](https://www.snort.org/) **of the snort;**

_“Snort can be deployed inline to stop these packets, as well. Snort has three primary uses: As a packet sniffer like tcpdump, as a packet logger — which is useful for network traffic debugging, or it can be used as a full-blown network intrusion prevention system. Snort can be downloaded and configured for personal and business use alike.”_

SNORT is an  **open-source**,  **rule-based**  Network Intrusion Detection and Prevention System  **(NIDS/NIPS)**. It was developed and still maintained by Martin Roesch, open-source contributors, and the Cisco Talos team.

**Capabilities of Snort;**

![](https://miro.medium.com/max/551/0*9zJ9HNAnxhjSql37.png)

-   Live traffic analysis
-   Attack and probe detection
-   Packet logging
-   Protocol analysis
-   Real-time alerting
-   Modules & plugins
-   Pre-processors
-   Cross-platform support! (Linux & Windows)

**Snort has three main use models;**

-   **Sniffer Mode —** Read IP packets and prompt them in the console application.
-   **Packet Logger Mode —** Log all IP packets (inbound and outbound) that visit the network.
-   **NIDS (Network Intrusion Detection System) and NIPS (Network Intrusion Prevention System) Modes —** Log/drop the packets that are deemed as malicious according to the user-defined rules.

## Answer the questions below

Since the answers can be found above, I won’t be sharing them here. Follow along to help better locate them if you can’t find them.

### Which snort mode can help you stop the threats on a local machine?

From the question, we are stopping threats, so we want to look at an IPS (Intrusion Prevention System). Scroll up to the IPS section, we see that there are four different types of IPS, read the bottom two. One of these holds the answer, also TryHackMe wants the acroymn of the name for the answer. Once you figure it out, highlight copy (ctrl + c) and paste (ctrl + v) or type, the answer in the TryHackMe answer field.

![](https://miro.medium.com/max/630/1*R6bvM4DJNpN8TP9kFhkNqw.png)

### Which snort mode can help you detect threats on a local network?

From the question, we are detecting threats, so we want to look at an IDS (Intrusion Detection System). Scroll up to the IDS section, with the IDS section we only have two to look at. The one we are looking for works on a network. One of these holds the answer, also TryHackMe wants the acroymn of the name for the answer. Once you figure it out, highlight copy (ctrl + c) and paste (ctrl + v) or type, the answer in the TryHackMe answer field.

![](https://miro.medium.com/max/630/1*Il_iJzRVRDL8m92N7LlyIQ.png)

### Which snort mode can help you detect the threats on a local machine?

From the question, we are detecting threats, so we want to look at an IDS (Intrusion Detection System). Scroll up to the IDS section, with the IDS section we only have two to look at. The one we are looking for works on a single endpoint. One of these holds the answer, also TryHackMe wants the acroymn of the name for the answer. Once you figure it out, highlight copy (ctrl + c) and paste (ctrl + v) or type, the answer in the TryHackMe answer field.

![](https://miro.medium.com/max/630/1*fZlX3_SfDOFcmTTa7CWz-A.png)

### Which snort mode can help you stop the threats on a local network?

From the question, we are stopping threats, so we want to look at an IPS (Intrusion Prevention System). Scroll up to the IPS section, we see that there are four different types of IPS, read the top two. We are looking for network traffic protection. One of these holds the answer, also TryHackMe wants the acroymn of the name for the answer. Once you figure it out, highlight copy (ctrl + c) and paste (ctrl + v) or type, the answer in the TryHackMe answer field.

![](https://miro.medium.com/max/630/1*7rBFfnB0cNTNuCaE56LlkA.png)

### Which snort mode works similar to NIPS mode?

Scroll back up to the section you were just at, read the NIPS bullet point. After you have done reading, read the bullet point under it. You will found out it is quite similar. TryHackMe wants the acroymn of the name for the answer. Once you figure it out, highlight copy (ctrl + c) and paste (ctrl + v) or type, the answer in the TryHackMe answer field.

![](https://miro.medium.com/max/630/1*RYURj9iE3N3Db5BazcoKsw.png)

### According to the official description of the snort, what kind of NIPS is it?

Reading through the qoute that TryHackMe gives on, look for network intrusion prevention system, this is NIPS. The word before network is the answer. Once you figure it out, highlight copy (ctrl + c) and paste (ctrl + v) or type, the answer in the TryHackMe answer field.

![](https://miro.medium.com/max/630/1*GMy_eDPEPQZnPAQRPrMP6Q.png)

### NBA training period is also known as …

Scroll up to the paragraph under the first two IDS, this is where you can find the answer to this question. Once you figure it out, highlight copy (ctrl + c) and paste (ctrl + v) or type, the answer in the TryHackMe answer field.

![](https://miro.medium.com/max/630/1*gQblkhOgwjvqHvjXoUdwQQ.png)

You have finished these tasks, and can now move onto Task 4 First Interaction with Snort, Task 5 Operation Mode 1: Sniffer Mode, & Task 6 Operation Mode 2: Packet Logger Mode.