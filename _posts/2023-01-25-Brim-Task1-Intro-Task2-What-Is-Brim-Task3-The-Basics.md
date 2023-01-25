---
layout: "post"
title: "TryHackMe Brim — Task 1 Introduction, Task 2 What is Brim?, & Task 3 The Basics"
categories: Brim
tags: TryHackMe, Brim, SOC Level One Path
---


Learn and practice log investigation, pcap analysis and threat hunting with Brim.

## Task 1 Introduction

[BRIM](https://www.brimdata.io/)  is an open-source desktop application that processes pcap files and logs files. Its primary focus is providing search and analytics. In this room, you will learn how to use Brim, process pcap files and investigate log files to find the needle in the haystack! This room expects you to be familiar with basic security concepts and processing Zeek log files. We suggest completing the “[**Network Fundamentals**](https://tryhackme.com/module/network-fundamentals)” path and the “[**Zeek room**](https://tryhackme.com/room/zeekbro)” before starting working in this room.

A VM is attached to this room. You don’t need SSH or RDP; the room provides a  **“Split View”**  feature. Exercise files are located in the folder on the desktop.  
**NOTE: DO NOT**  directly interact with any domains and IP addresses in this room.

![](https://miro.medium.com/max/700/0*hgdY6XwrvFO2y4Aj.png)

## Getting the VM Started

Click the green button labeled Start Machine, at the top of Task 1.

![](https://miro.medium.com/max/700/1*Eh5q4mIdkQbLw-fwUvIxmw.png)

The screen should split in half if it doesn’t go to the top of the page. You will see a blue button labeled Show Split View, click this button.

![](https://miro.medium.com/max/700/1*Tv-QW9P-WK9y8xfwhVKEfQ.png)

The screen should be split now, you have to wait for the VM to load. When it is finished loading it will look like it does below. You are ready to continue with the tasks ahead.

![](https://miro.medium.com/max/700/1*SeZjDMN2f0NWpkBCRISppg.png)

## Task 2 What is Brim?

![](https://miro.medium.com/max/700/0*g3ufI2rrsk3CY9ZU.png)

**What is Brim?**

Brim is an open-source desktop application that processes pcap files and logs files, with a primary focus on providing search and analytics. It uses the Zeek log processing format. It also supports Zeek signatures and Suricata Rules for detection.

It can handle two types of data as an input;

-   **Packet Capture Files:** Pcap files created with tcpdump, tshark and Wireshark like applications.
-   **Log Files:** Structured log files like Zeek logs.

Brim is built on open-source platforms:

-   **Zeek:**  Log generating engine.
-   **Zed Language:**  Log querying language that allows performing keywoırd searches with filters and pipelines.
-   **ZNG Data Format:**  Data storage format that supports saving data streams.
-   **Electron and React:**  Cross-platform UI.

**Why Brim?**

Ever had to investigate a big pcap file? Pcap files bigger than one gigabyte are cumbersome for Wireshark. Processing big pcaps with tcpdump and Zeek is efficient but requires time and effort. Brim reduces the time and effort spent processing pcap files and investigating the log files by providing a simple and powerful GUI application.

**Brim vs Wireshark vs Zeek**

While each of them is powerful and useful, it is good to know the strengths and weaknesses of each tool and which one to use for the best outcome. As a traffic capture analyser, some overlapping functionalities exist, but each one has a unique value for different situations.

**The common best practice is handling medium-sized pcaps with Wireshark, creating logs and correlating events with Zeek, and processing multiple logs in Brim.**

![](https://miro.medium.com/max/700/1*gJNvTC4MRmgK2F7lENInbQ.png)

## Task 3 The Basics

**Landing Page**

Once you open the application, the landing page loads up. The landing page has three sections and a file importing window. It also provides quick info on supported file formats.

-   **Pools:** Data resources, investigated pcap and log files.
-   **Queries:** List of available queries.
-   **History:**  List of launched queries.

**Pools and Log Details**

Pools represent the imported files. Once you load a pcap, Brim processes the file and creates Zeek logs, correlates them, and displays all available findings in a timeline, as shown in the image below.

![](https://miro.medium.com/max/700/0*U4R6axqPIdr24bzV.png)

The timeline provides information about capture start and end dates. Brim also provides information fields. You can hover over fields to have more details on the field. The above image shows a user hovering over the Zeek’s conn.log file and uid value. This information will help you in creating custom queries. The rest of the log details are shown in the right pane and provides details of the log file fields. Note that you can always export the results by using the export function located near the timeline.

![](https://miro.medium.com/max/470/0*mjPNL29YXOmhyZ6E.png)

You can correlate each log entry by reviewing the correlation section at the log details pane (shown on the left image). This section provides information on the source and destination addresses, duration and associated log files. This quick information helps you answer the “Where to look next?” question and find the event of interest and linked evidence.

You can also right-click on each field to filter and accomplish a list of tasks.

-   Filtering values
-   Counting fields
-   Sorting (A-Z and Z-A)
-   Viewing details
-   Performing whois lookup on IP address
-   Viewing the associated packets in Wireshark

The image below demonstrates how to perform whois lookup and Wireshark packet inspection.

**See image**

![](https://miro.medium.com/max/700/0*bpmPcdopZksBFP9c.png)

**Queries and History**

Queries help us to correlate finding and find the event of the interest. History stores executed queries.

![](https://miro.medium.com/max/491/0*xLNlUzAAsVvyLkJB.png)

The image on the left demonstrates how to browse the queries and load a specific query from the library.

Queries can have names, tags and descriptions. Query library lists the query names, and once you double-click, it passes the actual query to the search bar.

You can double-click on the query and execute it with ease. Once you double-click on the query, the actual query appears on the search bar and is listed under the history tab.

The results are shown under the search bar. In this case, we listed all available log sources created by Brim. In this example, we only insert a pcap file, and it automatically creates nine types of Zeek log files.

Brim has 12 premade queries listed under the “Brim” folder. These queries help us discover the Brim query structure and accomplish quick searches from templates. You can add new queries by clicking on the “+” button near the “Queries” menu.

![](https://miro.medium.com/max/556/0*AGsOmvDwSLHD7I8A.png)

### Answer the questions below

### Process the “sample.pcap” file and look at the details of the first DNS log that appear on the dashboard. What is the “qclass_name”?

On the desktop, double-click the Exercise-Files directory icon and Brim icon.

![](https://miro.medium.com/max/185/1*QwEVVmFwHWhduHrtaSzYKA.png)

When both open, click and drag the sample.pcap file from the Exercise-Files directory to the Brim application.

![](https://miro.medium.com/max/700/1*EPTR6BgE3wTW2h52v38DkA.png)

Then Brim will start to import the file.

![](https://miro.medium.com/max/700/1*ypxCJXxnyyUuIM3HwqUMbw.png)

After the sample pcap loads, we first want to go to the view tab. It is the fourth tab on the right at the top of Brim. Click on it and a drop-down menu will appear, then click the Right Pane choice.

![](https://miro.medium.com/max/700/1*E1w-48lq-pnzOHIUURrLTg.png)

Now that the Right Pane is visible, look at the dashboard in the middle of Brim. We want to look for the DNS entry, it can be found in the seventh result down. Once you find it, click on the entry.

![](https://miro.medium.com/max/700/1*16pgMSvpacK6mXlmypgNdw.png)

After you have clicked on the DNS entry, look at the Right Pane which is the Log Details. In the Log Details, we are looking for the qclass_name in the left column. Look down through till you find it, once you do the answer will be found in the column on the right. Type the answer into the TryHackMe answer field, then type submit.

![](https://miro.medium.com/max/700/1*QsraEGjPIsOdj5lmjwwFRw.png)

**Answer: C_INTERNET**

### Look at the details of the first NTP log that appear on the dashboard. What is the “duration” value?

Head back to the VM and in the dashboard look for NTP, once you find it click on the entry. The details of this entry will show up in the Log Details on the right panel. Go to the Log Details and scroll to the bottom.

![](https://miro.medium.com/max/700/1*Ufa1hfgWW0pEVAGLlp4_4A.png)

Once you reach the bottom, you will see the Duration column. To the right of this column is the answer. Once you find it, type the answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/272/1*bbmyWvFy5j-I5s0q7E8P1A.png)

**Answer: 0.005**

### Look at the details of the STATS packet log that is visible on the dashboard. What is the “reassem_tcp_size”?

Head back to the VM and in the dashboard scroll down till find STATS.

![](https://miro.medium.com/max/700/1*nGYXM7J2bcbyZYtR_Dd7Kw.png)

Once you find STATS, click on it. Then look to the Log Details panel on the right. Watching the column on the left as you scroll for the label, reassem_tcp_size.

![](https://miro.medium.com/max/700/1*0u-7a1GjhgAtGo2JvgqENw.png)

Once you find the column labeled reassem_tcp_size, look to the right of this column and you will see the answer. Once you find it, type the answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/249/1*jX62kQl8ijqRjsugjbgqZg.png)

**Answer: 540**

You have finished these tasks and can now move on to Task 4 Default Queries & Task 5 Use Cases.