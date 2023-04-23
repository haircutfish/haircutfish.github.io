---
layout: "post"
title: "TryHackMe Wireshark: The Basics —Task 1 Introduction & Task 2 Tool Overview"
categories: Wireshark
tags: TryHackMe, Wireshark, SOC Level One Path
---

## Getting The VM Started

Starting at Task 1, you will see the green _Start Machine_ button. Click this button to get the VM Started.

![](https://cdn-images-1.medium.com/max/800/1*y8rtV0zla6Iyr4olL3lc4g.png)

Scroll to the top where the banner is. On the right side of the page, you will see the blue _Show Split view_. Click this blue button.

![](https://cdn-images-1.medium.com/max/800/1*USlLYqlNAuGYNoRVu8Wavg.png)

The page will split, now just wait till the VM loads.

![](https://cdn-images-1.medium.com/max/800/1*u3P_a9Rs7ua8w0yoTWxKBw.png)

Once the VM loads, click the _View in Full Screen_ icon in the bottom left of the VM.

![](https://cdn-images-1.medium.com/max/800/1*NYfxvRusKvwKwI152fTkyw.png)

A new browser tab should open with the VM in it.

![](https://cdn-images-1.medium.com/max/800/1*p8Qr_qFiLe5T4dspGaImLQ.png)

Now depending on what you are doing, if you are following along with the screenshot, use _http1.pcapng_. If you are answering the questions, use _Exercise.pcapng_. Whichever you choose, right-click on the file, then on the drop-down menu click the _Open With Wireshark_.

![](https://cdn-images-1.medium.com/max/800/1*bB-oYIIWFqDD6Y1JIoFRJw.png)

This will open that file into Wireshark, and you will be ready to go!!

## Task 1 Introduction

Wireshark is an open-source, cross-platform network packet analyzer tool capable of sniffing and investigating live traffic and inspecting packet captures (PCAP). It is commonly used as one of the best packet analysis tools. In this room, we will look at the basics of Wireshark and use it to perform fundamental packet analysis.

**Note:** A VM is attached to this room. You don’t need SSH or RDP; the room provides a “Split View” feature. We suggest completing the [**Network Fundamentals**](https://tryhackme.com/module/network-fundamentals) module before starting working in this room.

There are two capture files given in the VM. You can use the “http1.pcapng” file to simulate the actions shown in the screenshots. Please note that you need to use the “Exercise.pcapng” file to answer the questions.

## Answer the questions below

All the answers can be found above, so I won’t be providing them here.

**Which file is used to simulate the screenshots?**

The Answer to this question can be found in the last paragraph of the above section. Once you find it, type the answer into the TryHackMe answer field and click submit.

![](https://cdn-images-1.medium.com/max/800/1*dCYCa53wtpYpfgYrTGR_-A.png)

  

**Which file is used to answer the questions?**

The Answer to this question can be found in the last paragraph of the above section. Once you find it, type the answer into the TryHackMe answer field and click submit.

![](https://cdn-images-1.medium.com/max/800/1*BM2he8rLk9_sdqe25l7cug.png)

  

## Task 2 Tool Overview

**Use Cases**

Wireshark is one of the most potent traffic analyzer tools available in the wild. There are multiple purposes for its use:

-   Detecting and troubleshooting network problems, such as network load failure points and congestion.
-   Detecting security anomalies, such as rogue hosts, abnormal port usage, and suspicious traffic.
-   Investigating and learning protocol details, such as response codes and payload data.

**Note:** Wireshark is not an Intrusion Detection System (IDS). It only allows analysts to discover and investigate the packets in depth. It also doesn’t modify packets; it reads them. Hence, detecting any anomaly or network problem highly relies on the analyst’s knowledge and investigation skills.

**GUI and Data**

Wireshark GUI opens with a single all-in-one page, which helps users investigate the traffic in multiple ways. At first glance, five sections stand out.

**Use Cases**

Wireshark is one of the most potent traffic analyzer tools available in the wild. There are multiple purposes for its use:

-   Detecting and troubleshooting network problems, such as network load failure points and congestion.
-   Detecting security anomalies, such as rogue hosts, abnormal port usage, and suspicious traffic.
-   Investigating and learning protocol details, such as response codes and payload data.

**Note:** Wireshark is not an Intrusion Detection System (IDS). It only allows analysts to discover and investigate the packets in depth. It also doesn’t modify packets; it reads them. Hence, detecting any anomaly or network problem highly relies on the analyst’s knowledge and investigation skills.

**GUI and Data**

Wireshark GUI opens with a single all-in-one page, which helps users investigate the traffic in multiple ways. At first glance, five sections stand out.

![](https://cdn-images-1.medium.com/max/800/1*GPJSKNuYRggjvPaVNXq7hg.png)

The below picture shows Wireshark’s main window. The sections explained in the table are highlighted. Now open the Wireshark and go through the walkthrough.

![](https://cdn-images-1.medium.com/max/800/0*KaNAplEirVp4GLlU.png)

**Loading PCAP Files**

The above picture shows Wireshark’s empty interface. The only available information is the recently processed “http1.cap” file. Let’s load that file and see Wireshark’s detailed packet presentation. Note that you can also use the **“File”** menu, dragging and dropping the file, or double-clicking on the file to load a pcap.

![](https://cdn-images-1.medium.com/max/800/0*M_GC7nk0Z1u8zhGK.png)

Now, we can see the processed filename, detailed number of packets and packet details. Packet details are shown in three different panes, which allow us to discover them in different formats.

![](https://cdn-images-1.medium.com/max/800/1*TXhmobF1_WFcvYsnZB-CUw.png)

**Coloring Packets**

Along with quick packet information, Wireshark also color packets in order of different conditions and the protocol to spot anomalies and protocols in captures quickly (this explains why almost everything is green in the given screenshots). This glance at packet information can help track down exactly what you’re looking for during analysis. You can create custom color rules to spot events of interest by using display filters, and we will cover them in the next room. Now let’s focus on the defaults and understand how to view and use the represented data details.

Wireshark has two types of packet coloring methods: temporary rules that are only available during a program session and permanent rules that are saved under the preference file (profile) and available for the next program session. You can use the “right-click menu” or **“View → Coloring Rules”** menu to create permanent coloring rules. The **“Colorize Packet List”** menu activates/deactivates the coloring rules. Temporary packet coloring is done with the “right-click menu” or **“View → Conversation Filter”** menu, which is covered in TASK-5.

The default permanent colouring is shown below.

![](https://cdn-images-1.medium.com/max/800/0*pG5EZvd1vdnOj2jD.png)

  

**Traffic Sniffing**

You can use the blue **“shark button”** to start network sniffing (capturing traffic), the red button will stop the sniffing, and the green button will restart the sniffing process. The status bar will also provide the used sniffing interface and the number of collected packets.

![](https://cdn-images-1.medium.com/max/800/0*_vzkfWS2hjgW90jf.png)

  

**Merge PCAP Files**

Wireshark can combine two pcap files into one single file. You can use the **“File → Merge”** menu path to merge a pcap with the processed one. When you choose the second file, Wireshark will show the total number of packets in the selected file. Once you click “open”, it will merge the existing pcap file with the chosen one and create a new pcap file. Note that you need to save the “merged” pcap file before working on it.

![](https://cdn-images-1.medium.com/max/800/0*ValzMXqnIzMn38lH.png)

  

**View File Details**

Knowing the file details is helpful. Especially when working with multiple pcap files, sometimes you will need to know and recall the file details (File hash, capture time, capture file comments, interface and statistics) to identify the file, classify and prioritize it. You can view the details by following “**Statistics → Capture File Properties”** or by clicking the **“pcap icon located on the left bottom”** of the window.

![](https://cdn-images-1.medium.com/max/800/0*f3gMu3f9Myw-PYaj.png)

## Answer the questions below

**Use the “Exercise.pcapng” file to answer the questions.**

If you haven’t already, scroll to the top of this write-up and follow the steps it takes to load the pcap file into Wireshark. Once you have done this, proceed to the questions.

**Read the “capture file comments”. What is the flag?**

Go to the toolbar at the top of Wireshark, and look for _Statistics._

![](https://cdn-images-1.medium.com/max/800/1*cLZPR1iz2X8zyHZ02QCdMg.png)

Either click on _Statistics_ or press the letter _S_ to have the drop-down appear. On the drop-down menu, click _Capture File Properties._

![](https://cdn-images-1.medium.com/max/800/1*aYc_mHJnMCYJeni_JZ5DxQ.png)

The _Wireshark — Capture File Properties_ window will pop up. Look at the bottom of this window for the _Capture File Comments_ section. Once you see it, scroll to the bottom.

![](https://cdn-images-1.medium.com/max/800/1*8N1YvCtfJAvw-xoHuQOaKA.png)

When you reach the bottom of this section, you will see _Flag:_ followed by the flag. Highlight the flag, then copy (ctrl +c) then paste (ctrl +v) the flag in the TryHackMe answer field and click submit.

![](https://cdn-images-1.medium.com/max/800/1*DwxTgyf5cl4hLIbXNsFvuw.png)

**Answer: TryHackMe_Wireshark_Demo**

  

**What is the total number of packets?**

Starting back on the main page of Wireshark, look at the bottom info bar. Look for the word _Packets:_, the answer will be to the right of this word. Highlight the number, then copy (ctrl +c) then paste (ctrl +v) the flag in the TryHackMe answer field and click submit.

![](https://cdn-images-1.medium.com/max/800/1*vdnf7D1-WK12QNFTCnMMiA.png)

**Answer: 58620**

  

**What is the SHA256 hash value of the capture file?**

Go to the toolbar at the top of Wireshark, and look for _Statistics._

![](https://cdn-images-1.medium.com/max/800/1*cLZPR1iz2X8zyHZ02QCdMg.png)

Either click on _Statistics_ or press the letter _S_ to have the drop-down appear. On the drop-down menu, click _Capture File Properties._

![](https://cdn-images-1.medium.com/max/800/1*aYc_mHJnMCYJeni_JZ5DxQ.png)

The _Wireshark — Capture File Properties_ window will pop up. Look in the _Details_ section for _Hash(SHA256):_, When you find it, you will see a long string of alphanumeric characters. This is the answer, highlight the hash, then copy (ctrl +c) then paste (ctrl +v) the flag in the TryHackMe answer field and click submit.

![](https://cdn-images-1.medium.com/max/800/1*xOb4IJCECo8IF11QGzLMnw.png)

**Answer: f446de335565fb0b0ee5e5a3266703c778b2f3dfad7efeaeccb2da5641a6d6eb**

  
You have finished these tasks and can now move on to Task 3 Packet Dissection & Task 4 Packet Navigation.