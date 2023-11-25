---
layout: "post"
title: "TryHackMe Wireshark:Traffic Analysis - Task 5 Tunneling Traffic: DNS and ICMP & Task 6 Cleartext Protocol Analysis: FTP"
categories: Wireshark
tags: TryHackMe, Wireshark, SOC Level One Path
---

----------

_If you haven’t done tasks 3 and 4 yet, here is the link to my write-up of them: [Task 3 ARP Poisoning & Man In The Middle and Task 4 Identifying Hosts: DHCP, NetBIOS and Kerberos](https://haircutfish.com/posts/Wireshark-Traffic-Analysis-Task-3-ARP-Poisoning-&-Man-In-The-Middle-and-Task-4-Identifying-Hosts-DHCP-NetBIOS-and-Kerberos/)_

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

## Task 5 Tunneling Traffic: DNS and ICMP

#### **Tunnelling Traffic: ICMP and DNS**

Traffic tunnelling is (also known as **“port forwarding”**) transferring the data/resources in a secure method to network segments and zones. It can be used for “internet to private networks” and “private networks to internet” flow/direction. There is an encapsulation process to hide the data, so the transferred data appear natural for the case, but it contains private data packets and transfers them to the final destination securely.

Tunnelling provides anonymity and traffic security. Therefore it is highly used by enterprise networks. However, as it gives a significant level of data encryption, attackers use tunnelling to bypass security perimeters using the standard and trusted protocols used in everyday traffic like ICMP and DNS. Therefore, for a security analyst, it is crucial to have the ability to spot ICMP and DNS anomalies.

**ICMP Analysis**

Internet Control Message Protocol (ICMP) is designed for diagnosing and reporting network communication issues. It is highly used in error reporting and testing. As it is a trusted network layer protocol, sometimes it is used for denial of service (DoS) attacks; also, adversaries use it in data exfiltration and C2 tunnelling activities.

**ICMP analysis in a nutshell:**

Usually, ICMP tunnelling attacks are anomalies appearing/starting after a malware execution or vulnerability exploitation. As the ICMP packets can transfer an additional data payload, adversaries use this section to exfiltrate data and establish a C2 connection. It could be a TCP, HTTP or SSH data. As the ICMP protocols provide a great opportunity to carry extra data, it also has disadvantages. Most enterprise networks block custom packets or require administrator privileges to create custom ICMP packets.

A large volume of ICMP traffic or anomalous packet sizes are indicators of ICMP tunnelling. Still, the adversaries could create custom packets that match the regular ICMP packet size (64 bytes), so it is still cumbersome to detect these tunnelling activities. However, a security analyst should know the normal and the abnormal to spot the possible anomaly and escalate it for further analysis.

![](https://cdn-images-1.medium.com/max/640/1*1flk4qumyMc4BgfK0rz4Tg.png)

![](https://cdn-images-1.medium.com/max/640/0*4JXT5f_R4hqEFWHq.png)

#### **DNS Analysis**

Domain Name System (DNS) is designed to translate/convert IP domain addresses to IP addresses. It is also known as a phonebook of the internet. As it is the essential part of web services, it is commonly used and trusted, and therefore often ignored. Due to that, adversaries use it in data exfiltration and C2 activities.

**DNS analysis in a nutshell:**

Similar to ICMP tunnels, DNS attacks are anomalies appearing/starting after a malware execution or vulnerability exploitation. Adversary creates (or already has) a domain address and configures it as a C2 channel. The malware or the commands executed after exploitation sends DNS queries to the C2 server. However, these queries are longer than default DNS queries and crafted for subdomain addresses. Unfortunately, these subdomain addresses are not actual addresses; they are encoded commands as shown below:

**“encoded-commands.maliciousdomain.com”**

When this query is routed to the C2 server, the server sends the actual malicious commands to the host. As the DNS queries are a natural part of the networking activity, these packets have the chance of not being detected by network perimeters. A security analyst should know how to investigate the DNS packet lengths and target addresses to spot these anomalies.

![](https://cdn-images-1.medium.com/max/640/1*JYGoMFwUcilMAM0fC5Y1rw.png)

![](https://cdn-images-1.medium.com/max/640/0*XENzgZsetsuOEyMJ.png)

Detecting suspicious activities in chunked files is easy and a great way to learn how to focus on the details. **Now use the exercise files to put your skills into practice against a single capture file and answer the questions below!**

## Answer the questions below

#### **Use the “Desktop/exercise-pcaps/dns-icmp/icmp-tunnel.pcap” file.**

Inside the _exercise-pcaps_ folder, double-click on the _dns-icmp_ folder.

![](https://cdn-images-1.medium.com/max/640/1*UGQbpSSQQ4Gr9LSH5EzgYg.png)

Inside the dns-icmp folder you will see the _Exercise.pcap_ file. Right-click on it, then choose _Open With Wireshark_ from the drop-down menu.

![](https://cdn-images-1.medium.com/max/640/1*n4EgAla8jva0Rbt-mWtEVQ.png)

### Investigate the anomalous packets. Which protocol is used in ICMP tunneling?

Reading through the ICMP section, a regular size of a ICMP packet is 64 bytes. So to investigate this issue, we should start by looking for packets that are sized greater than 64 bytes. To do so, THM gave us a great filter to use, `data.len > 64 and icmp`. This will filter for any packets that have a data length of greater than 64 bytes. Once it’s in the mint green filter bar, press enter to use it.

![](https://cdn-images-1.medium.com/max/640/1*bGDDt8_Mw0XjXoiodaauUQ.png)

Now it’s time to play investigate. In the Hexadecimal section in the bottom right of Wireshark, we can see what it translates to in ASCII. Make sure you have click on the first packet. Then, using the down arrow, you can cycle down through the packets. As you do, keep watching the ASCII output for any signs of the type of protocol that the attacker used to connect to the system.

![](https://cdn-images-1.medium.com/max/640/1*PUIqUGjiox_uxTs39iEz2g.png)

You will reach a point where the protocol the attacker used will be obvious. Keep in mind how an attacker or even you may easily connect to a server if you have the right credentials. Once you find it, type the answer in the THM answer field, and click submit.

![](https://cdn-images-1.medium.com/max/640/1*CR1CUIzxNN85skB6X6s6Lw.png)

**Answer: ssh**

  

### **Use the “Desktop/exercise-pcaps/dns-icmp/dns.pcap” file.**

Going back to the dns-icmp folder, right-click on the _dns.pcap_ file. From the drop-down menu, click on _Open With Wireshark_.

![](https://cdn-images-1.medium.com/max/640/1*iqUcrsqK4e_tt__ZkZiJsg.png)

### Investigate the anomalous packets. What is the suspicious main domain address that receives anomalous DNS queries? (Enter the address in defanged format.)

To be able to detect anomalous traffic, we want to look for anything out of the ordinary. A dead give away that data is being exfiltrated is in DNS queries or responses. You may see a domain with a large string of Alpha Numerical Characters followed by a domain name or even the top level domain. THM explains it pretty good above, along with giving a great filter to start with.

![](https://cdn-images-1.medium.com/max/640/1*ZzC2KB2T26VROiqYPFTj3A.png)

Since we know what the filter we want to start with is, let’s break it down. The first part of the filter is `dns.qry.name.len > 15`, this will filter for any DNS query that has a character length of greater than 15. Then we want to use the `and` operator to make the filter match both filter queries. Lastly, using the `!mdns` to remove any Local Link device queries from the results. Once you have the filter typed out in the mint green filter bar, press enter to use it.

![](https://cdn-images-1.medium.com/max/640/1*YK8YXU-Pw1_INMsKOqhaLg.png)

WOW we still have 91.5%. Lets take a quick peak at the info section to see if we can find any suspicious activity. We can see the first MX record instance looks interesting, as it looks like a long encoded string. Looks like the attacker is trying to exfil the data via quering the MX record. Click on the Packet so we can investigate it further.

![](https://cdn-images-1.medium.com/max/640/1*pai6tUjCCPeBPuqUnDsi6A.png)

Taking a look in the Details section on the bottom right of Wireshark. We can see the Full Encoded string for this packet, and at the end you see what looks like a domain name. The domain looks quite suspicious. Let’s submit it using the format *********[.]***. After you have typed the answer into the THM answer field, click submit.

![](https://cdn-images-1.medium.com/max/640/1*xbWGOqrb85Xb5_pKdzFdMg.png)

**Answer: dataexfil[.]com**

----------

## Task 6 Cleartext Protocol Analysis: FTP

#### **Cleartext Protocol Analysis**

Investigating cleartext protocol traces sounds easy, but when the time comes to investigate a big network trace for incident analysis and response, the game changes. Proper analysis is more than following the stream and reading the cleartext data. For a security analyst, it is important to create statistics and key results from the investigation process. As mentioned earlier at the beginning of the Wireshark room series, the analyst should have the required network knowledge and tool skills to accomplish this. Let’s simulate a cleartext protocol investigation with Wireshark!

#### **FTP Analysis**

File Transfer Protocol (FTP) is designed to transfer files with ease, so it focuses on simplicity rather than security. As a result of this, using this protocol in unsecured environments could create security issues like:

-   MITM attacks
-   Credential stealing and unauthorised access
-   Phishing
-   Malware planting
-   Data exfiltration

**FTP analysis in a nutshell:**

![](https://cdn-images-1.medium.com/max/640/1*gPNadfmi3SCNmAL280dMzw.png)

![](https://cdn-images-1.medium.com/max/640/1*DehwBZf1U9m5SNs5Gl1BaA.png)

![](https://cdn-images-1.medium.com/max/640/0*KQJw1ILTFBbRZODk.png)

Detecting suspicious activities in chunked files is easy and a great way to learn how to focus on the details. **Now use the exercise files to put your skills into practice against a single capture file and answer the questions below!**

## Answer the questions below

### Before you start!

Here is a resource I found that helped to identify the different commands used on an FTP server. Use it to better understand what is going on and what the attacker may be doing

[https://en.wikipedia.org/wiki/List_of_FTP_commands](https://en.wikipedia.org/wiki/List_of_FTP_commands)

#### **Use the “Desktop/exercise-pcaps/ftp/ftp.pcap” file.**

Going back to the folder where the pcapng file is located. Click on the _Back_ button in the upper left of the dns-icmp folder’s window.

![](https://cdn-images-1.medium.com/max/640/1*gncMi71IKTbC79xT2ycAQA.png)

Now being in the exercise-pcaps folder, double-click on _ftp_ folder to open it.

![](https://cdn-images-1.medium.com/max/640/1*KT-ISCc7NteJLHIXfXdgQw.png)

Now being inside the ftp folder, right-click on the _ftp.pcap_ file. From the drop-down menu, click on _Open With Wireshark_.

![](https://cdn-images-1.medium.com/max/640/1*DeKUGo6ZBhNQTMdOTGcSoQ.png)

### How many incorrect login attempts are there?

Taking a look up in the text THM give us some good filters to attempt. We want to look at the `ftp.response.code`. Since the question is looking for incorrect login attempts, 430 and 530 look like a great place to start.

![](https://cdn-images-1.medium.com/max/640/1*mrZvoU5SuEx3BaDx-e1j5w.png)

Heading into Wireshark, lets create of filter in the mint green filter bar. As stated we want to start with `ftp.response.code` then we want to add `== 430` to indicate that we are looking for response code of 430. Next we want the `or` operator so it can either be response code 430 or 530. Then repeat the process, but this time with `ftp.response.code == 530`. Now that you have that all typed into the filter bar. Hit enter to filter for it.

![](https://cdn-images-1.medium.com/max/640/1*WwPXFCossPgMsipKuP9Omg.png)

Once the filtering is done you can find the answer in the bottom right of Wireshark. To the right of the word _Displayed_. Once you find it, type the answer into the THM answer field and click submit.

![](https://cdn-images-1.medium.com/max/640/1*g0Q5eIOZN8VdSfNnSxJNRw.png)

**Answer: 737**

  

### What is the size of the file accessed by the “ftp” account?

The question gives us some information, the account we need to look for first is the `ftp` account. To find the acount we want to start out with the filter that THM shared above. That filter being `ftp.request.arg ==`. We just need to add `"ftp"` to the end. What this filter does is we are looking for when the user uses the username _ftp_. So we can start investigating. Now once you have the filter typed in, press enter to use it.

![](https://cdn-images-1.medium.com/max/640/1*7EBXK-iSLJEyT6fY7LJf7w.png)

We are left with two results. One using _ftp_ for the USER request and the other for the PASS. Since we want to find the size of the file the account accessed, we can find it by following the stream. To do this you will right-click on the first Packet. From the drop down, move your mouse to _Follow_. From the new drop down click on _TCP Stream_.

![](https://cdn-images-1.medium.com/max/640/1*uRQpDCKElOaYjji75tB3lw.png)

The _TCP Stream_ window will pop up. Reading down through we can see that the user ended up checking SIZE of the file _resume.doc._ Since we can see the size of the file, it sounds like it fits the description of the question. Let’s type the answer over in the THM answer field, and click submit.

![](https://cdn-images-1.medium.com/max/640/1*5f5KzV4ycEvVEhC2TyhEow.png)

**Answer: 39424**

  

### The adversary uploaded a document to the FTP server. What is the filename?

This question feeds directly off the previous question. After checking the size. The attacker proceeds to use RETR which is used to download a copy of a file onto the server. We can see to the right of this command what the name of the file is. Once you have found it, type the answer into the THM answer field and click submit.

![](https://cdn-images-1.medium.com/max/640/1*1PPXUKHA4XPGTiVqMuRV_Q.png)

**Answer: resume.doc**

  

### The adversary tried to assign special flags to change the executing permissions of the uploaded file. What is the command used by the adversary?

We can see what command the Attacker used by scrolling down and following the entire stream.

![](https://cdn-images-1.medium.com/max/640/1*tojGBmGvQT8EqcAaTnyf1g.png)

Once you reach the bottom, you can see where the attacker was trying to run a linux command to change the files permissions. Once you see it, type the answer in the THM answer field, then click submit.

![](https://cdn-images-1.medium.com/max/640/1*lnbU9DgTAr2UAo36YMAITg.png)

  

**Answer: chmod 777**

  

----------

### You have finished these tasks and can now move on to Task 7 Cleartext Protocol Analysis: HTTP & Task 8 Encrypted Protocol Analysis: Decrypting HTTPS.