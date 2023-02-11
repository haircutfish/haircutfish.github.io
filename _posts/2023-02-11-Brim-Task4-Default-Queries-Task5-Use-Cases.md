---
layout: "post"
title: "TryHackMe Brim — Task 4 Default Queries & Task 5 Use Cases"
categories: Brim
tags: TryHackMe, Brim, SOC Level One Path
---

_If you haven’t done tasks 1, 2, & 3 yet, here is the link to my write-up of them:_ [_Task 1 Introduction, Task 2 What is Brim?, & Task 3 The Basics._](https://haircutfish.com/posts/Brim-Task1-Intro-Task2-What-Is-Brim-Task3-The-Basics/)

## Getting the VM Started

Click the green button labeled Start Machine, at the top of Task 1.

![](https://miro.medium.com/max/567/0*wLF4Y5Cpd8WiNC4H.png)

The screen should split in half if it doesn’t go to the top of the page. You will see a blue button labeled Show Split View, click this button.

![](https://miro.medium.com/max/567/0*oxm1KQnRujiu2Zb3.png)

The screen should be split now, you have to wait for the VM to load. When it is finished loading it will look like it does below. You are ready to continue with the tasks ahead.On the desktop, double-click the Exercise-Files directory icon and Brim icon.

![](https://miro.medium.com/max/149/0*6RNEFSqQ2kQn6FWz.png)

When both open, click and drag the task4-sample-b.pcap file from the Exercise-Files directory to the Brim application.

![](https://miro.medium.com/max/630/1*9gnGaCch_WYfFDvuUVEiFQ.png)

Then Brim will start to import the file.

![](https://miro.medium.com/max/567/0*QN2-jttOzzcq-apV.png)

After the sample pcap loads, we first want to go to the view tab. It is the fourth tab on the right at the top of Brim. Click on it and a drop-down menu will appear, then click the Right Pane choice.

![](https://miro.medium.com/max/567/0*QSiBf2EvG8AavJK6.png)

You are now ready to move on to the takes ahead.

## Task 4 Default Queries

**Default Queries**

We mentioned that Brim had 12 premade queries in the previous task. Let’s see them in action! Now, open Brim, import the sample pcap and go through the walkthrough.

![](https://miro.medium.com/max/363/0*Uvom3_Dgo9zyqfYZ.png)

**Reviewing Overall Activity**

This query provides general information on the pcap file. The provided information is valuable for accomplishing further investigation and creating custom queries. It is impossible to create advanced or case-specific queries without knowing the available log files.

The image on the left shows that there are 20 logs generated for the provided pcap file.

**Windows Specific Networking Activity**

This query focuses on Windows networking activity and details the source and destination addresses and named pipe, endpoint and operation detection. The provided information helps investigate and understand specific Windows events like SMB enumeration, logins and service exploiting.

![](https://miro.medium.com/max/630/0*CT02pHJ44PqNc9Yk.png)

**Unique Network Connections and Transferred Data**

These two queries provide information on unique connections and connection-data correlation. The provided info helps analysts detect weird and malicious connections and suspicious and beaconing activities. The uniq list provides a clear list of unique connections that help identify anomalies. The data list summarises the data transfer rate that supports the anomaly investigation hypothesis.

![](https://miro.medium.com/max/630/0*a5Gkjnv8mkxFS1lW.png)

**DNS and HTTP Methods**

These queries provide the list of the DNS queries and HTTP methods. The provided information helps analysts to detect anomalous DNS and HTTP traffic. You can also narrow the search by viewing the “HTTP POST” requests with the available query and modifying it to view the “HTTP GET” methods.

![](https://miro.medium.com/max/630/0*CMl0x4AMblbVvTY9.png)

**File Activity**

This query provides the list of the available files. It helps analysts to detect possible data leakage attempts and suspicious file activity. The query provides info on the detected file MIME and file name and hash values (MD5, SHA1).

![](https://miro.medium.com/max/630/0*_UBiQkYIyavlm8Bi.png)

**IP Subnet Statistics**

This query provides the list of the available IP subnets. It helps analysts detect possible communications outside the scope and identify out of ordinary IP addresses.

![](https://miro.medium.com/max/630/0*0SF72Qtx9hQm6pLI.png)

**Suricata Alerts**

These queries provide information based on Suricata rule results. Three different queries are available to view the available logs in different formats (category-based, source and destination-based, and subnet based).

**Note:**  Suricata is an open-source threat detection engine that can act as a rule-based Intrusion Detection and Prevention System. It is developed by the Open Information Security Foundation (OISF). Suricata works and detects anomalies in a similar way to  [**Snort**](https://tryhackme.com/room/snort)  and can use the same signatures.

See image

![](https://miro.medium.com/max/621/0*S-g927YLIT_2zvKo.png)

## Answer the questions below

### Investigate the files. What is the name of the detected GIF file?

On the VM, look to the left side panel of Brim. On this panel, you will see Queries, inside this panel you will see File Activity. Click on File Activity.

![](https://miro.medium.com/max/211/1*SOG1md4y5dybWqWSowAhdQ.png)

Go to the center of Brim and you see all the instances that have to deal with files. Look down through the mime_type column till you find image/gif. Once you find it look to the row to the right, this is the answer to the question. Once you find it type the answer into the answer field on TryHackMe, then click submit.

![](https://miro.medium.com/max/630/1*Qa77PXXhQsIeJ2HtMZ3f-A.png)

**Answer:** c**at01_with_hidden_text.gif**

### Investigate the conn logfile. What is the number of the identified city names?

Heading back to Brim, we need to sort through some files similar to how we did it in Zeek. There is a search bar above the table in the middle of Brim, click on it. Type in the search bar  `_path=="conn"`, then press enter to search it. When it is finished, we need to look at the names of the columns to find the right one. Start scrolling to the right.

![](https://miro.medium.com/max/630/1*0Hn-9HK-_pdqEMePOX3flg.png)

Since we need to know how many city names were identified, I think geo.resp.city is a good start.

![](https://miro.medium.com/max/630/1*PhfYeVeXdJFLYxhb2LukSA.png)

Time to use some skills learned from the Zeek room, and using the column name we found, let's build the command out. So the command we want to use is  `_path=="conn" | cut geo.resp.city | sort | uniq -c`, then press enter to search with this command. We keep the first part of the command along (  `_path=="conn"`), we then pipe the result of the first part into cut. Using cut, we “cut” out the column that we specifically, in this case it is geo.resp.city, so that we can look at just that column (or any other that we would specify). We take the results from cut and pipe it through sort, this will sort the results alphabetically. The results of sort are then finally piped through uniq -c, this will take away any duplicates with the uniq then the -c counts them. After you have run this command through our pcap, you will be left with a result that all you need to do is count the number of city names you find. The answer is the number of city names that you counted. Type the answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/621/1*uD9JU10BrHELthNzdSXM7g.png)

**Answer: 2**

### Investigate the Suricata alerts. What is the Signature id of the alert category “Potential Corporate Privacy Violation”?

Heading back to the VM, and in Brim look to the left side of the application. You will see the Queries panel, click on any of the Suricata Alerts.

![](https://miro.medium.com/max/207/1*RS1OQwivXymguWJ1TpkOuA.png)

Move to the center of the Brim application you will see the search field has the syntax used to narrow down the alerts to information the query was looking for. So highlight everything from the first pipe ( | ) on the left to the end, then press delete to remove it. Press enter to search for  `event_type=="alert"`.

![](https://miro.medium.com/max/589/1*_pwVm-bMJuHMzJ4xd_uvPQ.png)

Time to scroll to the right looking that the column names for anything interesting.

![](https://miro.medium.com/max/630/1*QAgKstqdXXKGYt8TVBtDCg.png)

We found a column at looks interesting, the alert.signature_id. If you look we can see the answer below but lets see if we can declutter up the center display a bit.

![](https://miro.medium.com/max/630/1*f1Dw2PwcXJW777zSX6mGkw.png)

Go back up to the search field, type in the field  `| cut alert.category, alert.signature_id`, the press enter to run the search with these parameters.

![](https://miro.medium.com/max/495/1*cyP7q_ykMKgRcx61XadvbA.png)

Now that it looks cleaner, we can see the alert id that is related to Potential Corporate Privacy Violation. Once you find it, type the answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/598/1*ZhpCFIAShsFhovnW43sFYA.png)

**Answer: 2,012,887**

## Task 5 Use Cases

**Custom Queries and Use Cases**

There are a variety of use case examples in traffic analysis. For a security analyst, it is vital to know the common patterns and indicators of anomaly or malicious traffic. In this task, we will cover some of them. Let’s review the basics of the Brim queries before focusing on the custom and advanced ones.

**Brim Query Reference**

![](https://miro.medium.com/max/630/1*LbA82DuJXCUmFYlBDQN67Q.png)

![](https://miro.medium.com/max/630/1*FuVPeZvbOrF4p7XYRh8g9g.png)

**Note:** It is highly suggested to use field names and filtering options and not rely on the blind/irregular search function. Brim provides great indexing of log sources, but it is not performing well in irregular search queries. The best practice is always to use the field filters to search for the event of interest.

![](https://miro.medium.com/max/630/1*QoovHnoVettX--DfMddloA.png)

![](https://miro.medium.com/max/630/1*fSai9NTX8cpqQW5AtNgUjw.png)

![](https://miro.medium.com/max/630/1*5Lap9rqbkJi-81F6AYLzaA.png)

![](https://miro.medium.com/max/630/1*rbQTBIduTRcKPysSlHCRvA.png)

You have finished these tasks and can now move on to Task 6 Exercise: Threat Hunting with Brim | Malware C2 Detection.
