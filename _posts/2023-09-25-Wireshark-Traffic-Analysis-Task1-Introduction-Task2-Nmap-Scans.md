---
layout: "post"
title: " TryHackMe Wireshark:Traffic Analysis — Task 1 Introduction & Task 2 Nmap Scans"
categories: Wireshark
tags: TryHackMe, Wireshark, SOC Level One Path
---

Learn the basics of traffic analysis with Wireshark and how to find anomalies on your network!

# Task 1 Introduction

In this room, we will cover the techniques and key points of traffic analysis with Wireshark and detect suspicious activities. Note that this is the third and last room of the Wireshark room trio, and it is suggested to visit the first two rooms stated below to practice and refresh your Wireshark skills before starting this one.

-   [**Wireshark: The Basics**](https://tryhackme.com/room/wiresharkthebasics)
-   [**Wireshark: Packet Operations**](https://tryhackme.com/room/wiresharkpacketoperations)

In the first two rooms, we have covered how to use Wireshark and do packet-level searches. Now, it is time to investigate and correlate the packet-level information to see the big picture in the network traffic, like detecting anomalies and malicious activities. For a security analyst, it is vital to stop and understand pieces of information spread in packets by applying the analyst’s knowledge and tool functionality. This room will cover investigating packet-level details by synthesising the analyst knowledge and Wireshark functionality for detecting anomalies and odd situations for a given case.

**Note:** A VM is attached to this room. You don’t need SSH or RDP; the room provides a “Split View” feature. **DO NOT** directly interact with any domains and IP addresses in this room. The domains and IP addresses are included only for reference reasons.

## Getting the VM Started

Starting at Task 1, you will see the green _Start Machine_ button. Click this button to get the VM Started.

![](https://cdn-images-1.medium.com/max/640/1*oTHapUvW_k7C0d9XHu4cPA.png)

Scroll to the top where the banner is. On the right side of the page, you will see the blue _Show Split view_. Click this blue button.

![](https://cdn-images-1.medium.com/max/640/1*hA7I8debkGEAIALzeiM3_Q.png)

The page will split, now just wait till the VM loads.

![](https://cdn-images-1.medium.com/max/640/1*wBbomFA5apQCFKeDJtfz6A.png)

Once the VM loads, click the _View in Full Screen_ icon in the bottom left of the VM.

![](https://cdn-images-1.medium.com/max/640/1*3LTzdWlKsWpxqEod82lKsQ.png)

A new browser tab should open with the VM in it.

![](https://cdn-images-1.medium.com/max/640/1*MdWpir7vVaTyBABGjLuuPw.png)

Double-Click on the e_xercise-pcap_ folder to open it.

![](https://cdn-images-1.medium.com/max/640/1*CjufqwTyhW7vIbR6a9Kebg.png)

While folder opens, head back to the THM Task Tab. At the bottom of the VM you will see a minus ( — ), this represents _Exit Split View_. Click the — to allow the THM task to incapsilate the entire window. This won’t close out of your VM instance, it will just be on the other tab.

![](https://cdn-images-1.medium.com/max/640/1*u6W5IWPah0c1Tiq2SbShhg.png)

Heading back to the browser tab that the VM is in. The folder should be open. Inside this folder will be other folders containing the files needed for the tasks ahead. The folders are named accordingly to the task they are associated with.

![](https://cdn-images-1.medium.com/max/640/1*iz9rYeuhdRVKU3N1f8pFBg.png)

----------

## Task 2 Nmap Scans

### **Nmap Scans**

Nmap is an industry-standard tool for mapping networks, identifying live hosts and discovering the services. As it is one of the most used network scanner tools, a security analyst should identify the network patterns created with it. This section will cover identifying the most common Nmap scan types.

-   TCP connect scans
-   SYN scans
-   UDP scans

It is essential to know how Nmap scans work to spot scan activity on the network. However, it is impossible to understand the scan details without using the correct filters. Below are the base filters to probe Nmap scan behaviour on the network.

**TCP flags in a nutshell.**
![](https://cdn-images-1.medium.com/max/640/1*llXPgrU_To_KRbq77_0yXQ.png)

## **TCP Connect Scans**

**TCP Connect Scan in a nutshell:**

-   Relies on the three-way handshake (needs to finish the handshake process).
-   Usually conducted with `nmap -sT` command.
-   Used by non-privileged users (only option for a non-root user).
-   Usually has a windows size larger than 1024 bytes as the request expects some data due to the nature of the protocol. ![](https://cdn-images-1.medium.com/max/640/1*lHNl1_VqWLSFF2W5OtrNtA.png)

The images below show the three-way handshake process of the open and close TCP ports. Images and pcap samples are split to make the investigation easier and understand each case’s details.

**Open TCP port (Connect):**

![](https://cdn-images-1.medium.com/max/640/0*RvvmYQe0js4AByqp.png)

**Closed TCP port (Connect):**

![](https://cdn-images-1.medium.com/max/640/0*QU9hCpq0U4BI5tsd.png)

The above images provide the patterns in isolated traffic. However, it is not always easy to spot the given patterns in big capture files. Therefore analysts need to use a generic filter to view the initial anomaly patterns, and then it will be easier to focus on a specific traffic point. The given filter shows the TCP Connect scan patterns in a capture file.

`tcp.flags.syn==1 and tcp.flags.ack==0 and tcp.window_size > 1024`

![](https://cdn-images-1.medium.com/max/640/0*rvy___C4oy2py7SP.png)

## **SYN Scans**

**TCP SYN Scan in a nutshell:**

-   Doesn’t rely on the three-way handshake (no need to finish the handshake process).
-   Usually conducted with `nmap -sS` command.
-   Used by privileged users.
-   Usually have a size less than or equal to 1024 bytes as the request is not finished and it doesn’t expect to receive data.

![](https://cdn-images-1.medium.com/max/640/1*RocDjDlfYh1h4N0gsyc3yw.png)

**Open TCP port (SYN):**

![](https://cdn-images-1.medium.com/max/640/0*Lt7YeYMqetEIcwfP.png)

**Closed TCP port (SYN):**

![](https://cdn-images-1.medium.com/max/640/0*jjKOjex6FCmmzrnN.png)

The given filter shows the TCP SYN scan patterns in a capture file.

`tcp.flags.syn==1 and tcp.flags.ack==0 and tcp.window_size <= 1024`

![](https://cdn-images-1.medium.com/max/640/0*9MsZ0XI1N8jAOP9U.png)

## **UDP Scans**

**UDP Scan in a nutshell:**

-   Doesn’t require a handshake process
-   No prompt for open ports
-   ICMP error message for close ports
-   Usually conducted with `nmap -sU` command.

![](https://cdn-images-1.medium.com/max/640/1*bc8gc0gh68ROmsWFsrJxcg.png)

**Closed (port no 69) and open (port no 68) UDP ports:**

![](https://cdn-images-1.medium.com/max/640/0*7xJ7PvGlzSdtDiZC.png)

The above image shows that the closed port returns an ICMP error packet. No further information is provided about the error at first glance, so how can an analyst decide where this error message belongs? The ICMP error message uses the original request as encapsulated data to show the source/reason of the packet. Once you expand the ICMP section in the packet details pane, you will see the encapsulated data and the original request, as shown in the below image.

![](https://cdn-images-1.medium.com/max/640/0*zmUvINxy1_ZRBQh5.png)

The given filter shows the UDP scan patterns in a capture file.

`icmp.type==3 and icmp.code==3`

![](https://cdn-images-1.medium.com/max/640/0*Kl63qV6U3x-LW20E.png)

Detecting suspicious activities in chunked files is easy and a great way to learn how to focus on the details. **Now use the exercise files to put your skills into practice against a single capture file and answer the questions below!**

## Answer the questions below

### **Use the “Desktop/exercise-pcaps/nmap/Exercise.pcapng” file.**

Inside the _exercise-pcaps_ folder, double-click on the _nmap_ folder.

![](https://cdn-images-1.medium.com/max/640/1*AoLitFQ8_Fsuy7TdBnmd6g.png)

Inside the nmap folder you will see the _Exercise.pcap_ file. Right-click on it, then choose _Open With Wireshark_ from the drop-down menu.

![](https://cdn-images-1.medium.com/max/640/1*esbEOozPKRNCQulisu4X-w.png)

You are now ready to answer the following questions.

### What is the total number of the “TCP Connect” scans?

The command needed to find the answer is given above. But I am going to explain what exactly the command is looking for. In short this command looks for the TCP Connect Scan that results in a Closed Port. The `tcp.flags.syn == 1` looks for the _SYN_ flag being set on a TCP packet. Then the `tcp.flags.ack == 0` is looking for any packet that doesn’t have the _ACK_ flag set. Finally it is also looking for any packet that has a size greater than 1024 bytes. After we put together the command, it will be `tcp.flags.syn==1 and tcp.flags.ack==0 and tcp.window_size > 1024` . Type this into the mint green filter bar, then press enter to use this filter on the pcapng.

![](https://cdn-images-1.medium.com/max/640/1*wGL0saCHGnk7LitRXnyX8A.png)

Look at the bottom right of the Wireshark window. You are looking for the word _Displayed:_. The numbers to the right of _Displayed_, is the answer. Type the answer in the THM answer field, and then click submit.

![](https://cdn-images-1.medium.com/max/640/1*368K4eCsJsyHHAYWppJzGQ.png)

**Answer: 1000**

  

### Which scan type is used to scan the TCP port 80?

Since we want to know that we are looking at port 80 via TCP. Click on the mint green filter bar, and use the filter `tcp.port == 80`. This will filter out and display only packets that travel over TCP to port 80. Press enter to use apply this filter.

![](https://cdn-images-1.medium.com/max/640/1*zt8m-QXHgBe6n4A-6xC_mg.png)

You will be left with 7 results. Looking at the first 4 results we can see that they are all part of the same stream by the connecting bracket. So next we want to move down to the _Info section_, to figure out what type of scan this could be.

![](https://cdn-images-1.medium.com/max/640/1*QXLY6IG3fWmDqfEyqDonng.png)

Taking a look at the different flags that were used, we see _SYN, SYN ACK, ACK, RST ACK_. It looks like the process of a _Three-way Handshake_. Knowing this, along with what we read above, we can figure out what type of scan this is. Once you figure it out, type the answer in the THM answer field, and then click submit.

![](https://cdn-images-1.medium.com/max/640/1*KXfuqcNVn7_YZk4PUCfHpg.png)

**Answer: tcp connect**

  

### How many “UDP close port” messages are there?

The command needed to find the answer is given above. But I am going to explain what exactly the command is looking for. With the filter we are looking at both the _ICMP type_ and _code_, both of which is _3_. We know this by the information given to us by THM above in the table. So the filter is `icmp.type == 3 and icmp.code == 3`. Once you have typed the filter into the mint green filter bar, press enter to use it.

![](https://cdn-images-1.medium.com/max/640/1*xrJyIrFiZzHbyW8d1KTpkg.png)

Look at the bottom right of the Wireshark window. You are looking for the word _Displayed:_. The numbers to the right of _Displayed_, is the answer. Type the answer in the THM answer field, and then click submit.

![](https://cdn-images-1.medium.com/max/640/1*I-0SVNpdkUiOAYEuRRLq3A.png)

**Answer: 1083**

  

### Which UDP port in the 55–70 port range is open?

The question is looking to find out which UDP port is open amongst the port range. To be honest, I had to do some searching to figure out the correct syntax for the filter. Huge shout out to Chris Greer, and his [YouTube Short](https://www.youtube.com/shorts/R4L5ONvznmQ) that shows how to properly create this filter. Since we are looking for a UDP protocol port, we start the filter with `udp.port`. Then we are looking at the ports `in` a port range, we add the `in` operator. Now it’s time for the port range, to achieve this we need to use the curly brackets (`{ }`). We then put the port range in between the curly bracket with a double period between the numbers, `55..70`. Let’s put it all together, `udp.port in {55..70}`. Type the filter into the mint green filter bar, then press enter to use.

![](https://cdn-images-1.medium.com/max/640/1*vfdk1lZMOU-Tw0zTuxgpng.png)

As we can see from the search results, the first UDP attempts met a closed port. But upon the third try, an open port was found. Once you see the open port. Type the answer in the THM answer field, and then click submit.

![](https://cdn-images-1.medium.com/max/640/1*Y78Ty6cMkgPWWeyQ7NGk3A.png)

**Answer: 68**

----------

### You have finished these tasks and can now move on to Task 3 ARP Poisoning & Man In The Middle and Task 4 Identifying Hosts: DHCP, NetBIOS and Kerberos