---
layout: "post"
title: "Wireshark: Packet Operations — Task 1 Introduction & Task 2 Statistics | Summary"
categories: Wireshark
tags: TryHackMe, Wireshark, SOC Level One Path
---


![](https://cdn-images-1.medium.com/max/640/1*0A9UR_NQdVWPXmD7BbgvnQ.png)

## Task 1 Introduction

In this room, we will cover the fundamentals of packet analysis with Wireshark and investigate the event of interest at the packet-level. Note that this is the second room of the Wireshark room trio, and it is suggested to visit the first room ([**Wireshark: The Basics**](https://tryhackme.com/room/wiresharkthebasics)) to practice and refresh your Wireshark skills before starting this one.

In the first room, we covered the basics of the Wireshark by focusing on how it operates and how to use it to investigate traffic captures. In this room, we will cover advanced features of the Wireshark by focusing on packet-level details with Wireshark statistics, filters, operators and functions.

**Note:** A VM is attached to this room. You don’t need SSH or RDP; the room provides a “Split View” feature. Access to the machine will be provided in-browser and will deploy in Split View mode in your browser. If you don’t see it, use the blue Show Split View button at the top right of this room page to show it. **DO NOT** directly interact with any domains and IP addresses in this room. The domains and IP addresses are included for reference reasons only.

## Getting the VM Started

Starting at Task 1, you will see the green _Start Machine_ button. Click this button to get the VM Started.

![](https://cdn-images-1.medium.com/max/640/1*h-AdoKC80XbGXhpdao3EnA.png)

Scroll to the top where the banner is. On the right side of the page, you will see the blue _Show Split view_. Click this blue button.

![](https://cdn-images-1.medium.com/max/640/1*pbK8eA7x_V7f0osS1krfuw.png)

The page will split, now just wait till the VM loads.

![](https://cdn-images-1.medium.com/max/640/1*Izh42-5VdeId9YSS-5CLlA.png)

Once the VM loads, click the _View in Full Screen_ icon in the bottom left of the VM.

![](https://cdn-images-1.medium.com/max/640/1*BjlNIoZFdwAxwTqXhzD9IA.png)

A new browser tab should open with the VM in it.

![](https://cdn-images-1.medium.com/max/640/1*uYEybxyxC-Q-qR9jJo9iJA.png)

Right-click on _Exercise.pcapng_, then on the drop-down menu click the _Open With Wireshark_.

![](https://cdn-images-1.medium.com/max/640/1*1cgaqgrtnACJ8-5z6YoNsA.png)

While Wireshark loads, head back to the THM Task Tab. At the bottom of the VM you will see a minus ( — ), this represents _Exit Split View_. Click the — to allow the THM task to incapsilate the entire window. This won’t close out of your VM instance, it will just be on the other tab.

![](https://cdn-images-1.medium.com/max/640/1*hB_yDzjivMvgyHB2UOOpdA.png)

Now head back to the broswer tab that the VM instance is in. Wireshark should be open and ready to use.

![](https://cdn-images-1.medium.com/max/640/1*sD5wFph3XXuEkriXT6g7Hg.png)

----------

## Task 2 Statistics | Summary

### **Statistics**

This menu provides multiple statistics options ready to investigate to help users see the big picture in terms of the scope of the traffic, available protocols, endpoints and conversations, and some protocol-specific details like DHCP, DNS and HTTP/2. For a security analyst, it is crucial to know how to utilise the statical information. This section provides a quick summary of the processed pcap, which will help analysts create a hypothesis for an investigation. You can use the **“Statistics”** menu to view all available options. Now start the given VM, open the Wireshark, load the “Exercise.pcapng” file and go through the walkthrough.

### **Resolved Addresses**

This option helps analysts identify IP addresses and DNS names available in the capture file by providing the list of the resolved addresses and their hostnames. Note that the hostname information is taken from DNS answers in the capture file. Analysts can quickly identify the accessed resources by using this menu. Thus they can spot accessed resources and evaluate them according to the event of interest. You can use the **“Statistics → Resolved Addresses”** menu to view all resolved addresses by Wireshark.

![](https://cdn-images-1.medium.com/max/640/0*QlbUgbwhH1-VcYPp.png)

### **Protocol Hierarchy**

This option breaks down all available protocols from the capture file and helps analysts view the protocols in a tree view based on packet counters and percentages. Thus analysts can view the overall usage of the ports and services and focus on the event of interest. The golden rule mentioned in the previous room is valid in this section; you can right-click and filter the event of interest. You can use the **“Statistics → Protocol Hierarchy”** menu to view this info.

![](https://cdn-images-1.medium.com/max/640/0*EwXg8I8TC5-45KsF.png)

### **Conversations**

Conversation represents traffic between two specific endpoints. This option provides the list of the conversations in five base formats; ethernet, IPv4, IPv6, TCP and UDP. Thus analysts can identify all conversations and contact endpoints for the event of interest. You can use the **“Statistic → Conversations”** menu to view this info.

![](https://cdn-images-1.medium.com/max/640/0*DVpRNuC5fEKxSJA-.png)

### **Endpoints**

The endpoints option is similar to the conversations option. The only difference is that this option provides unique information for a single information field (Ethernet, IPv4, IPv6, TCP and UDP ). Thus analysts can identify the unique endpoints in the capture file and use it for the event of interest. You can use the **“Statistics → Endpoints”** menu to view this info.

Wireshark also supports resolving MAC addresses to human-readable format using the manufacturer name assigned by IEEE. Note that this conversion is done through the first three bytes of the MAC address and only works for the known manufacturers. When you review the ethernet endpoints, you can activate this option with the **“Name resolution”** button in the lower-left corner of the endpoints window.

![](https://cdn-images-1.medium.com/max/640/0*N9DdiwVf_1UmQQBg.png)

Name resolution is not limited only to MAC addresses. Wireshark provides IP and port name resolution options as well. However, these options are not enabled by default. If you want to use these functionalities, you need to activate them through the **“Edit → Preferences → Name Resolution”** menu. Once you enable IP and port name resolution, you will see the resolved IP address and port names in the packet list pane and also will be able to view resolved names in the “Conversations” and “Endpoints” menus as well.

![](https://cdn-images-1.medium.com/max/640/0*-PrnEArLJW1CZTGU.png)

Endpoint menu view with name resolution:

![](https://cdn-images-1.medium.com/max/640/0*kVZL_hU1iKBpQuTi.png)

Besides name resolution, Wireshark also provides an IP geolocation mapping that helps analysts identify the map’s source and destination addresses. But this feature is not activated by default and needs supplementary data like the GeoIP database. Currently, Wireshark supports MaxMind databases, and the latest versions of the Wireshark come configured MaxMind DB resolver. However, you still need MaxMind DB files and provide the database path to Wireshark by using the **“Edit → Preferences → Name Resolution → MaxMind database directories”** menu. Once you download and indicate the path, Wireshark will automatically provide GeoIP information under the IP protocol details for the matched IP addresses.

![](https://cdn-images-1.medium.com/max/640/0*I5XArJ9DoZMdtfsn.png)

Endpoints and GeoIP view.

![](https://cdn-images-1.medium.com/max/640/0*gGVvSF2D3ALTP7Sh.png)

**_Note: You need an active internet connection to view the GeoIP map. The lab machine doesn’t have an active internet connection!_**

## Answer the questions below

### Investigate the resolved addresses. What is the IP address of the hostname starts with “bbc”?

At the top of the Wireshark window, click on _Statistics_ from the menu bar. In the drop-down, click on _Resolved Addresses._

![](https://cdn-images-1.medium.com/max/640/1*3UJ2DVIK91AwJa7Ja_oC_g.png)

The _Wireshark — Resolved Addresses_ window will pop-up. At the top of this window is a search field labeled _Search for entry (min 3 characters)._ Type _bbc_ into this search field.

![](https://cdn-images-1.medium.com/max/640/1*_vpaYDUTa7ebdkuYW8hQ1g.png)

After you have typed _bbc_ into the search field. It will auto filter any matches. There should be only one Hostname that matches to the query. The address that was resolved from this Hostname is the answer to the question. You can click on the _IP Address_, and use copy (_CTRL+C)._ Then paste (_CTRL+V_) the answer into the THM answer field, and click submit.

![](https://cdn-images-1.medium.com/max/640/1*QXk_JBtjoSb2rfZbZfuvCw.png)

**Answer:** 1**99.232.24.81**

  

### What is the number of IPv4 conversations?

Go back up to the Menu bar and click _Statistics_ again. This time click on the _Conversations_ option from the drop-down menu.

![](https://cdn-images-1.medium.com/max/640/1*ajyxJFWsqoI6hy9aDIIRBQ.png)

The _Conversations_ window will pop-up. You can see the different tabs at the top of this window. The tab that pertains to this question is the _IPv4_ tab. Look at the number on this tab, this is the answer to this question. Type it into the answer field on THM, and then click submit.

![](https://cdn-images-1.medium.com/max/640/1*9-IeRkGXOIJt8o0tdJta2g.png)

**Answer: 435**

  

### How many bytes (k) were transferred from the “Micro-St” MAC address?

Once again, head back up to the menu bar and click _Statistics_. On the drop-down menu click _Endpoints_.

![](https://cdn-images-1.medium.com/max/640/1*OqXIX5VoI8S6iCY2Ge1h0w.png)

The _Endpoints_ window will pop-up. Look at the bottom left of the window. Click the checkbox next to _Name Resolution_.

![](https://cdn-images-1.medium.com/max/640/1*fF7nGFkUrt6sqY9fqaljAw.png)

After checking the _Name Resolution_ checkbox, the MAC address will now display the resolved Name. Looking down through the list, you need to find the name _Micro-St_. Once you find it look across the row till you get to the _Bytes_ column, displaying the amount of _Bytes_ that were transferred from that Name/MAC Address. Once you have found the answer, type it into the THM answer field, then click submit.

![](https://cdn-images-1.medium.com/max/640/1*2ZRXsM3z6UHaKF-twimB3A.png)

**Answer:** 7474

  

### What is the number of IP addresses linked with “Kansas City”?

You are going to stick with the _Endpoints_ window for this question. Going back to it, you will want to click on the tab labeled _IPv4_.

![](https://cdn-images-1.medium.com/max/640/1*fOHkSX0RXS9f4kkeJ76dnQ.png)

You will now be presented with the IPv4 Endpoints from the pcapng file in the table format. Look for the column labeled _City_, and click on it to alphabitize them.

![](https://cdn-images-1.medium.com/max/640/1*qNDENQc5wac7IkUoZB4J3Q.png)

Scroll down till you find _Kansas City_.

![](https://cdn-images-1.medium.com/max/640/1*YiI_QIkhVKdd3TdxOrslXg.png)

Once you have found it, count the number of times it appears and you will have your answer. Type your answer into the THM answer field, and then click submit.

![](https://cdn-images-1.medium.com/max/640/1*lgCt1W0HgUmAxQxZxolbWg.png)

**Answer:** **4**

  

### Which IP address is linked with “Blicnet” AS Organisation?

One last time, head back to the _Endpoints_ window. This time you are going to want to scroll to the right until you see the column _As Organization._

![](https://cdn-images-1.medium.com/max/640/1*Sn8DhIvLhhnlkrUyfdCyKg.png)

Like before, when you find the column _As Organization._ Click on it to alphabatize it.

![](https://cdn-images-1.medium.com/max/640/1*ApG9Js5ZUr5i4tPS5NpfUQ.png)

Scroll up till you see _Blicnet_ in the _As Organization column._

![](https://cdn-images-1.medium.com/max/640/1*ca3OkFIHovmxoInYzuXTjg.png)

When you find it, click on the row to highlight it. Then scroll to the left till you see the _Address_ column.

![](https://cdn-images-1.medium.com/max/640/1*m-FeTzHr-askEJzOPb7bhw.png)

Once you reach the _Address_ column, you will see the IPv4 address associated with _Blicnet_ and thus the answer. Type it into the THM answer field, and then click submit.

![](https://cdn-images-1.medium.com/max/640/1*M7oQSNDCn1XUUv8CiM0tsg.png)

**Answer: 188.246.82.7**

----------

You have finished these tasks and can now move on to [Task 3 Statistics | Protocol Details, Task 4 Packet Filtering | Principles, & Task 5 Packet Filtering | Protocol Filters](https://haircutfish.com/posts/Wireshark-Packet-Operations-Task-3-Statistics-Protocol-Details-Task-4-Packet-Filtering-Principles-&-Task-5-Packet-Filtering-Protocol-Filters).