---
layout: "post"
title: "TryHackMe Zeek Exercises — Task 1 Introduction & Task 2 Anomalous DNS"
categories: Zeek-Exercises
tags: TryHackMe, Zeek, SOC Level One Path
---


Put your Zeek skills into practice and analyze network traffic.

## Task 1 Introduction

![](https://miro.medium.com/max/700/0*IXpeERiXS_utLnVu.png)

The room invites you a challenge to investigate a series of traffic data and stop malicious activity under different scenarios. Let’s start working with Zeek to analyze the captured traffic.

We recommend completing the  [**Zeek**](https://tryhackme.com/room/zeekbro)  room first, which will teach you how to use the tool in depth.

A VM is attached to this room. You don’t need SSH or RDP; the room provides a “Split View” feature. Exercise files are located in the folder on the desktop. Log cleaner script  **“clear-logs.sh”**  is available in each exercise folder.

![](https://miro.medium.com/max/613/0*IqMzHRMqJqN3vYn1.png)

## Getting the VM Started

Click the green button labeled Start Machine, at the top of Task 1.

![](https://miro.medium.com/max/700/1*MR8zOMfOAbI_wp0KS1WGnw.png)

The screen should split in half if it doesn’t go to the top of the page. You will see a blue button labeled Show Split View, click this button.

![](https://miro.medium.com/max/700/1*DrNsXyf808gtKEbP0nOy3g.png)

The screen should be split now, you have to wait for the VM to load. When it is finished loading it will look like it does below. You are ready to continue with the tasks ahead.

![](https://miro.medium.com/max/700/1*gTZHcAtc5xLjn7tT7RuhXg.png)

On the VM, you will see a terminal icon in the middle of the VM screen on the right. Click on it.

![](https://miro.medium.com/max/700/1*wwnycimx6mlGmTmPZkB_7Q.png)

A terminal window will pop-up, time to move to the Exercise-Files directory. To do this we will use the  `cd`  command, which stands for change directory. We will use this command in combination with Tab completion. With Tab complete, you only have to press Tab after starting to type, and if it only has one entry that matches, it will auto-complete it. So let’s type out the command  `cd Desktop/Exercise-Files/`, then press enter to run the command. Follow up with the  `ls`  command to see the contents of the directory.

![](https://miro.medium.com/max/700/1*9cSL5YvEVgPt3FDQVTdQYg.png)

## Task 2 Anomalous DNS

**An alert triggered:** “Anomalous DNS Activity”.

The case was assigned to you. Inspect the PCAP and retrieve the artifacts to confirm this alert is a true positive.

## Answer the questions below

First, move into the anomalous-dns directory with the  `cd`  command. So the command we are doing is  `cd anomalous-dns/`, then press enter to move into the directory. Then use  `ls`  to see the contents of the directory.

![](https://miro.medium.com/max/604/1*BUbmz3nmAypXV0qbdbE88A.png)

### Investigate the  **dns-tunneling.pcap**  file. Investigate the  **dns.log**  file. What is the number of DNS records linked to the IPv6 address?

So we want to use run Zeek against the pcap file. To do this we will use the command  `zeek -r dns-tunneling.pcap`, then press enter to run Zeek. Using  `ls`, will show the content and log files in the current directory.

![](https://miro.medium.com/max/700/1*AejSOiz9esFV33ckZL-ClQ.png)

Now let’s cat the dns log file and pipe it through less to see if we can figure out the name of the field we want to see it. Also, the question here wasn’t very clear so at first I was searching the IP addresses for an IPv6 address, and found one. But what they are asking for here is, a certain DNS record associated with the IPv6 address, and what is the number of occurrences of this DNS record are. So knowing this and looking at the hint that TryHackMe gives, we are looking for the quad A record (AAAA). Know all this let’s run the command  `cat dns.log | less`, then press enter to run. When you get in the dns log file through less press the right arrow key till reaching the quad A record.

![](https://miro.medium.com/max/700/1*YdfXwUBLbzAlt22zIA_cDA.png)

After looking at the fields and counting, I determined that the name of the field we are looking for is qtype_name. Press  `q`  to exit out of less.

![](https://miro.medium.com/max/700/1*2EcJIsivdjf6CEApzKmcsQ.png)

Knowing the field we need to zeek-cut, time to do a little Command-Line Kung-Fu! The command being  `cat dns.log | zeek-cut qtype_name | grep "AAAA" | uniq -c`, then press enter to run. After we zeek-cut the field out, we then pipe that into grep which we then pull out only quad A results. Then take the results from grep and pipe that into uniq and get rid of the duplicates and count the number of times it occurred. After this command runs we are left with the answer in the output, type it into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/700/1*KOigWlkSigzKK6RgaScsGA.png)

**Answer: 320**

### Investigate the  **conn.log**  file. What is the longest connection duration?

Now let’s cat the conn log file and pipe it through less to see if we can figure out the name of the field we want to see it. So the command we want to use is  `cat conn.log | less`, and press enter to run.

![](https://miro.medium.com/max/648/1*kOA9DZ3N8zDHZAljS1UrIA.png)

At a quick glance at the different fields, we see that one of the field names is duration. This seems to be the field we want to use, time to use some zeek-cut.

![](https://miro.medium.com/max/663/1*iJ6jx_y4gB-Bf2ZVBbI0Ng.png)

Time to use zeek-cut, sort, and tail with some pipes. The command that we want to use is  `cat conn.log | zeek-cut duration | sort -n | tail -1`, and press enter to run the code. We take the field and run it through zeek-cut, and pipe the results through sort. Sort has the dash/tick n for sorting numerically, then we pipe the results of sort through tail. Tail gives the last 10 results unless told otherwise, which we are telling it to with the dash/tick 1. After running the command, you are left with the result in the output of the terminal, type the answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/700/1*hxoeidXjrkD-i416auj9DQ.png)

**Answer: 9.420791**

### Investigate the  **dns.log**  file. Filter all unique DNS queries. What is the number of unique domain queries?

To start we will pipe the DNS log file into less to find the field we want to look at, to do this use the command  `cat dns.log | less`, press enter to run.

![](https://miro.medium.com/max/700/1*eFmc6SBBr28KbVWXWgNrzg.png)

At a quick glance at the different fields, we see that one of the field names is query. This seems to be the field we want to use, time to use some zeek-cut.

![](https://miro.medium.com/max/700/1*-LKc5-KGYSS_WD8STMWTCw.png)

Let’s use zeek-cut along with some new commands to find the answer. After trying multiple combinations, and finally looking at the hint the full command I used was  `cat dns.log | zeek-cut query | rev | cut -d '.' -f 1-2 | rev | sort | uniq`, and press enter to run. We take and zeek cut the query field out, then pipe the results through to rev. Rev then reverses the string of characters, which then get’s piped to cut. Cut will then work like zeek-cut and with the parameters of -d for the delimiter and we chose the period, the -f stands for field, and 1–2 is for the first and second field. Now the results of cut are piped back into rev to reverse the string of characters once more, aka they are now in the proper order. The results from rev are piped into sort, to sort them alphabetically. Finally, the results from sort are piped into uniq to remove any duplicates. After the command has run, you are left with a single output of each unique domain query. Count them to get your answer, once you have counted them type it into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/700/1*62bJQXPBlyK9MxXv3mImaw.png)

**Answer: 6**

### There are a massive amount of DNS queries sent to the same domain. This is abnormal. Let’s find out which hosts are involved in this activity. Investigate the  **conn.log**  file. What is the IP address of the source host?

To start we will pipe the conn log file into less to find the field we want to look at, to do this use the command  `cat conn.log | less`, press enter to run.

![](https://miro.medium.com/max/700/1*7qkzZtYIrRBg_QNX6YjMMA.png)

At a quick glance at the different fields, we see that two of the field names are id.orig_h and id.resp_h. This seems to be the field we want to use, time to use some zeek-cut.

![](https://miro.medium.com/max/700/1*44JIVqucqNwJON7ldtmubQ.png)

Time to use zeek-cut, sort, and uniq with some pipes. The command that we want to use is  `cat conn.log | zeek-cut id.orig_h id.resp_h | sort -n | uniq -c`, then press enter. We take the field and run it through zeek-cut, and pipe the results through sort. Sort has the dash/tick n for sorting numerically. Finally, the results from sort are piped into uniq to remove any duplicates. After you run the command you are left with the results, one of those results is over two thousand times. The answer is the source IP address from this row. Once you find it type it into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/700/1*aMV893-NZJ0RIEYkTJ-mUQ.png)

**Answer: 10.20.57.3**

You have finished these tasks, and can now move on to Task 3 Phishing, Task 4 Log4J, & Task 5 Conclusion.