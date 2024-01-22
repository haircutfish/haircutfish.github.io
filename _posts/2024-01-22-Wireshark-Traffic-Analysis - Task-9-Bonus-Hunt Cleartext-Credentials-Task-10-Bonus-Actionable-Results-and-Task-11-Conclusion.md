---
layout: "post"
title: "TryHackMe Wireshark:Traffic Analysis — Task 9 Bonus: Hunt Cleartext Credentials!, Task 10 Bonus: Actionable Results!, and Task 11 Conclusion"
categories: Wireshark
tags: TryHackMe, Wireshark, SOC Level One Path
---


----------

### TryHackMe Wireshark:Traffic Analysis — Task 9 Bonus: Hunt Cleartext Credentials!, Task 10 Bonus: Actionable Results!, and Task 11 Conclusion

_If you haven’t done tasks 7 and 8 yet, here is the link to my write-up of them: [Task 7 Cleartext Protocol Analysis: HTTP & Task 8 Encrypted Protocol Analysis: Decrypting HTTPS](https://haircutfish.com/posts/Wireshark-Traffic-Analysis-Task-7-Cleartext-Protocol-Analysis-HTTP-&-Task-8-Encrypted-Protocol-Analysis-Decrypting-HTTPS/)_

## Getting the VM Started

Starting at Task 1, you will see the green _Start Machine_ button. Click this button to get the VM Started.

![](https://cdn-images-1.medium.com/max/640/0*_BHceNJ1VRtlLk4v.png)

Scroll to the top where the banner is. On the right side of the page, you will see the blue _Show Split view_. Click this blue button.

![](https://cdn-images-1.medium.com/max/640/0*jlhlxhqcQ6NR9wbK.png)

The page will split, now just wait till the VM loads.

![](https://cdn-images-1.medium.com/max/640/0*xUXjf8i_J27b7mq4.png)

Once the VM loads, click the _View in Full Screen_ icon in the bottom left of the VM.

![](https://cdn-images-1.medium.com/max/640/0*97XpuRfEtO3OuuJO.png)

A new browser tab should open with the VM in it.

![](https://cdn-images-1.medium.com/max/640/0*RI7TVGri4r5-xWpX.png)

Double-Click on the e_xercise-pcap_ folder to open it.

![](https://cdn-images-1.medium.com/max/640/0*L68OBAvwqGMaPoAb.png)

While folder opens, head back to the THM Task Tab. At the bottom of the VM you will see a minus ( — ), this represents _Exit Split View_. Click the — to allow the THM task to incapsilate the entire window. This won’t close out of your VM instance, it will just be on the other tab.

![](https://cdn-images-1.medium.com/max/640/0*MBV7FEHAo0KjNnZC.png)

Heading back to the browser tab that the VM is in. The folder should be open. Inside this folder will be other folders containing the files needed for the tasks ahead. The folders are named accordingly to the task they are associated with.

![](https://cdn-images-1.medium.com/max/640/0*nJ2FtDPbbBUQVVvT.png)

----------

## Task 9 Bonus: Hunt Cleartext Credentials!

### **Bonus: Hunt Cleartext Credentials!**

Up to here, we discussed how to inspect the packets for specific conditions and spot anomalies. As mentioned in the first room, Wireshark is not an IDS, but it provides suggestions for some cases under the expert info. However, sometimes anomalies replicate the legitimate traffic, so the detection becomes harder. For example, in a cleartext credential hunting case, it is not easy to spot the multiple credential inputs and decide if there is a brute-force attack or if it is a standard user who mistyped their credentials.

As everything is presented at the packet level, it is hard to spot the multiple username/password entries at first glance. The detection time will decrease when an analyst can view the credential entries as a list. Wireshark has such a feature to help analysts who want to hunt cleartext credential entries.

Some Wireshark dissectors (FTP, HTTP, IMAP, pop and SMTP) are programmed to extract cleartext passwords from the capture file. You can view detected credentials using the **“Tools → Credentials”** menu. This feature works only after specific versions of Wireshark (v3.1 and later). Since the feature works only with particular protocols, it is suggested to have manual checks and not entirely rely on this feature to decide if there is a cleartext credential in the traffic.

Once you use the feature, it will open a new window and provide detected credentials. It will show the packet number, protocol, username and additional information. This window is clickable; clicking on the packet number will select the packet containing the password, and clicking on the username will select the packet containing the username info. The additional part prompts the packet number that contains the username.

![](https://cdn-images-1.medium.com/max/640/0*5-TYukJrYOCNYw4k.png)

## Answer the questions below

### **Use the “Desktop/exercise-pcaps/bonus/Bonus-exercise.pcap” file.**

Inside the _exercise-pcaps_ folder, double-click on the _bonus_ folder.

![](https://cdn-images-1.medium.com/max/640/1*kV7vYW3SDzzujBgBIR4_SA.png)

Inside the bonus folder you will see the _Bonus-exercise.pcap_ file. Right-click on it, then choose _Open With Wireshark_ from the drop-down menu.

![](https://cdn-images-1.medium.com/max/640/1*CTNMfLxPy5IyxFbkznQU1A.png)

  

### What is the packet number of the credentials using “HTTP Basic Auth”?

Click on the _Tools_ drop-down menu at the top of the Wireshark window. From the drop-down, click on _Credentials_.

![](https://cdn-images-1.medium.com/max/640/1*ey_f11aPIXtrGDARdlmwRg.png)

The Wireshark Credentials window will pop up. Looking through the Protocols, we can see one _HTTP_ Packet. Looking at the _Packet Number_ to the left we have our answer. Type the _Packet Number_ into the TryHackMe answer field, then click _Submit_.

![](https://cdn-images-1.medium.com/max/640/1*nPphRv31eyAHQ3PuQ6j0AA.png)

**Answer: 237**

  

### What is the packet number where “empty password” was submitted?

Time to do some investigating! In the Wireshark Credentials Window, click on the _Packet Number_. You will see that the _Packet Details_ change to the _Packet Number_ you clicked on. Looking at the _Request arg:_ will show you the password that was used. Now click down through the _Packet Numbers_ till you don’t see _Request arg:_, this means that no password was submitted. Once you find this Packet, you have found the _Packet Number_ that is the answer. Type this answer into the TryHackMe answer field, then click the _Submit_ button.

![](https://cdn-images-1.medium.com/max/640/1*2UfS-dMODW3CZsNTn5IGkA.png)

**Answer: 170**

  

----------

## Task 10 Bonus: Actionable Results!

### **Bonus: Actionable Results!**

You have investigated the traffic, detected anomalies and created notes for further investigation. What is next? Not every case investigation is carried out by a crowd team. As a security analyst, there will be some cases you need to spot the anomaly, identify the source and take action. Wireshark is not all about packet details; it can help you to create firewall rules ready to implement with a couple of clicks. You can create firewall rules by using the **“Tools → Firewall ACL Rules”** menu. Once you use this feature, it will open a new window and provide a combination of rules (IP, port and MAC address-based) for different purposes. Note that these rules are generated for implementation on an outside firewall interface.

Currently, Wireshark can create rules for:

-   Netfilter (iptables)
-   Cisco IOS (standard/extended)
-   IP Filter (ipfilter)
-   IPFirewall (ipfw)
-   Packet filter (pf)
-   Windows Firewall (netsh new/old format)

![](https://cdn-images-1.medium.com/max/640/0*4FIGX7D1bC6hGebp.png)

## Answer the questions below

### **Use the “Desktop/exercise-pcaps/bonus/Bonus-exercise.pcap” file.**

You will use the same _Bonus-exercise.pcap_ file you opened in the previous Task.

### Select packet number 99. Create a rule for “IPFirewall (ipfw)”. What is the rule for “denying source IPv4 address”?

Let’s start by filtering for only Packet 99. Using the _frame.number_ filter we used before, adding _== 99_. So that the filter is _frame.number == 99_, then press enter to run the filter.

![](https://cdn-images-1.medium.com/max/640/1*1q8ht2yfDdGMTKSlPix2tA.png)

Click on the _Tools_ drop-down menu at the top of the Wireshark window. From the drop-down, click on _Firewall ACL Rules_.

![](https://cdn-images-1.medium.com/max/640/1*N2JazeUnqsA96lyH3pUsEw.png)

The Wireshark Firewall ACL Rules window will pop up. At the bottom of the window we can see _Create Rules For_ with a drop-down menu to the right. Click the down carot to expand this menu.

![](https://cdn-images-1.medium.com/max/640/1*mkXPi6WCYVc9WdlUHp1b7A.png)

The drop-down will expand. Look for _IPFirewall (ipfw)_, once you find it, click on it. This will select it.

![](https://cdn-images-1.medium.com/max/640/1*9lU6PeVl_n-wbIbM8Y23fg.png)

The _IPFirewall (ipfw)_ rules will be loaded in the window now. As we can see, the rule for _denying IPv4 source address_ is at the top of the list. Highlight the rule and copy (ctrl + c), then paste it in the TryHackMe answer field. Then click _Submit_.

![](https://cdn-images-1.medium.com/max/640/1*SfOq30pvOy8DPhebpZK6sg.png)

**Answer: add deny ip from 10.121.70.151 to any in**

  

### Select packet number 231. Create “IPFirewall” rules. What is the rule for “allowing destination MAC address”?

Close out the Wireshark Firewall ACL Rules window using the _Close_ button in the bottom right of the window.

![](https://cdn-images-1.medium.com/max/640/1*7nY0iY6p5lRse_aRD8Q6Iw.png)

Now change the _Frame Number_ from _99_ to _231_. So that the filter will look like _frame.number == 231_, then press enter to run it.

![](https://cdn-images-1.medium.com/max/640/1*YFztliBbL-usqU6o1JCM2A.png)

Click on the _Tools_ drop-down menu at the top of the Wireshark window. From the drop-down, click on _Firewall ACL Rules_.

![](https://cdn-images-1.medium.com/max/640/1*N2JazeUnqsA96lyH3pUsEw.png)

The Wireshark Firewall ACL Rules window will pop up. At the bottom of the window we can see _Create Rules For_ with a drop-down menu to the right. Click the down carot to expand this menu.

![](https://cdn-images-1.medium.com/max/640/1*mkXPi6WCYVc9WdlUHp1b7A.png)

The drop-down will expand. Look for _IPFirewall (ipfw)_, once you find it, click on it. This will select it.

![](https://cdn-images-1.medium.com/max/640/1*9lU6PeVl_n-wbIbM8Y23fg.png)

One final thing we need to do is _uncheck_ the _deny_ box in the bottom right of the window. This will change the rules to be _allow_ instead of _deny_.

![](https://cdn-images-1.medium.com/max/640/1*uM2SYrb1lbYkkczvdkuMvw.png)

Now scroll down till you see _MAC destination address._ Once you spot it, highlight and copy (ctrl + c) the rule. Then paste (ctrl + v) the answer into the TryHackMe answer field, then click _Submit_.

![](https://cdn-images-1.medium.com/max/640/1*YBT2KDoFz107-NwDyJFpwQ.png)

**Answer: add allow MAC 00:d0:59:aa:af:80 any in**

  

----------

## Task 11 Conclusion

**Congratulations!** You just finished the “Wireshark: The Traffic Analysis” room.

In this room, we covered how to use the Wireshark to detect anomalies and investigate events of interest at the packet level. Now, we invite you to complete the Wireshark challenge room: [**Carnage**](https://tryhackme.com/room/c2carnage), **Warzone 1** and **Warzone 2**.

Wireshark is a good tool for starting a network security investigation. However, it is not enough to stop the threats. A security analyst should have IDS/IPS knowledge and extended tool skills to detect and prevent anomalies and threats. As the attacks are getting more sophisticated consistently, the use of multiple tools and detection strategies becomes a requirement. The following rooms will help you step forward in network traffic analysis and anomaly/threat detection.

-   [**NetworkMiner**](https://tryhackme.com/room/networkminer)
-   [**Snort**](https://tryhackme.com/room/snort)
-   [**Snort Challenge — The Basics**](https://tryhackme.com/room/snortchallenges1)
-   [**Snort Challenge — Live Attacks**](https://tryhackme.com/room/snortchallenges2)
-   [**Zeek**](https://tryhackme.com/room/zeekbro)
-   [**Zeek Exercises**](https://tryhackme.com/room/zeekbroexercises)
-   [**Brim**](https://tryhackme.com/room/brim)

----------

## 🎉🎉🎉Congrats!!! You completed the TryHackMe Wireshark:Traffic Analysis room, Awesome Job!!!🎉🎉🎉