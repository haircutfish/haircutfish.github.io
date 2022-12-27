---
layout: "post"
title: "TryHackMe Snort Challenge — The Basics — Task 4 Writing IDS Rules (PNG) & Task 5 Writing IDS Rules (Torrent Metafile)"
categories: Snort-Challenge-TheBasics
tags: TryHackMe, Snort, SOC Level One Path
---

_If you haven’t done task 1, 2, & 3 yet, here is the link to my write-up of it: [Task 1 Introduction, Task 2 Writing IDS Rules (HTTP), & Task 3 Writing IDS Rules (FTP).](https://haircutfish.com/posts/Snort-Challenge-Basics-Task1-Intro-Task2-Writing-IDS-Rules-Task3-Writing-IDS-Rules/)_

## Opening the VM

Click the green Start Machine button in the top of Task 1.

![](https://miro.medium.com/max/630/1*x6zAWPFYlAEuB1ExR5r4lg.png)

The screen will split in half, with the VM on the right and the Tasks on the left. If the screen didn’t split in half go to the next step, if it did split in half skip the next step.

![](https://miro.medium.com/max/630/1*XHM98kiz9OIbW0c5EvkjLg.png)

Scroll to the top of the page, you will see a blue bottom labeled Show Split View, click this button to split the page in half.

![](https://miro.medium.com/max/630/1*JnVGkE_NtXty6nxBBsiVBg.png)

Now that we have our screen split and we have our VM, we need a terminal to work in. At the top left of the VM is a terminal icon, it is hard to see, click this icon to open a terminal window.

![](https://miro.medium.com/max/342/1*vJqkLpwjhViMNKuvIqtYVw.png)

Once you have your terminal window, you are good to go with the tasks ahead.

![](https://miro.medium.com/max/531/1*5saQgr92ghWRq6CF7JvMNw.png)

## Task 4 Writing IDS Rules (PNG)

Let’s create IDS Rules for PNG files in the traffic!

## Answer the questions below

### **Navigate to the task folder.**

Use command  `cd Desktop/Exercise-Files/TASK-4\ \(PNG\)/`, then press enter to run the command. You are now in the correct directory, using the command  `ls`  will list the contents of the directory so we know what the name of the pcap and rules file is.

![](https://miro.medium.com/max/560/1*9S63zAMVE2GSy4E_U9gB9w.png)

### Use the given pcap file.

### Write a rule to detect the PNG file in the given pcap.

Before we write our rule we need to go get a number, to start we need to go to  [wiki](https://en.wikipedia.org/wiki/List_of_file_signatures)  that hold the list of file signatures. Click on the link for the  [wiki](https://en.wikipedia.org/wiki/List_of_file_signatures), and once there we are going to use the find (ctrl + f) feature of our browser to find png. When the search bar opens, type png and you will have 4 results.

![](https://miro.medium.com/max/372/1*q9W3zmQoc2U8KMFlXuj0yA.png)

Go to the second or third result and you will see the PNG magic number we need.

![](https://miro.medium.com/max/630/1*Dp534YxHAWicnQ-WS7gmYg.png)

Start by opening the text editor with  `sudo gedit local.rules`, and press enter.

![](https://miro.medium.com/max/630/1*mYNj4V3864ZT4RIihfgC1A.png)

We can see that they already have a rule inside the rule file, so we will leave it alone for the time being. But we will borrow from it, highlight and copy (ctrl + c) the rule on line 8, press enter to start a new line and paste (ctrl + v) the rule on line 9.

![](https://miro.medium.com/max/630/1*KwVDOn7A4QoNyLcPl9Hgpg.png)

Now let’s change some things up on the new rule. First thing to change is the protocol to tcp from icmp. The second thing to change would be the msg:, we want to change it to “PNG file detected”. Then the sid we can increment it one 1. Finally we need to add a content: section, this is where we are going to put that magic number from earlier into. You can copy (ctrl + c) and paste (ctrl + v) or type the hex value in, but the command should look like this,  `alert tcp any any <> any any (msg:"PNG file Detected"; content:"|89 50 4A 47 0D 0A 1A 0A|"; sid:100002; rev:1;)`, once we have this typed out we can save it. We use the pipes between to tell snort that this is a binary or a hex value inside here.

![](https://miro.medium.com/max/630/1*KzNujq9WrOOdtbN2NvM4Hg.png)

Save (ctrl + s) and X out of the text editor window, and your back in the terminal.

![](https://miro.medium.com/max/630/1*ZXb9QVrWIv4H1j2dLgXlXQ.png)

Time to run our rule through, snort against the pcap file. We will set it up as we did in the previous room, the command will be  `sudo snort -c local.rules -A full -l . -r mx-3.pcap`. We get the name of the pcap file from running the  `ls`  command earlier. So after typing the command in, press enter to run it.

![](https://miro.medium.com/max/630/1*ECJh-CBMG7f3IPoTaLbHqA.png)

After snort is done running, we can use  `ls`  again, and see that now we have an alert and log file.

![](https://miro.medium.com/max/533/1*aA8hIsJ_oE_fZ6Apv5QpBg.png)

### Investigate the logs and identify the software name embedded in the packet.

Let’s look at the log file, to do this we can use the snort command we learned in the previous room,  `sudo snort -r snort.log.1671814047 -X`. The name of your log file may be different, that is ok, just make sure it is named properly. Then press enter to run the command.

![](https://miro.medium.com/max/630/1*IE74Zjk7JD8Ktb79spomQA.png)

There is only one result, scroll up till you get almost to the top. Look to the text next to the hex output. A program name should standout, this is the answer. Once you find it, type this answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/630/1*yKhjzbnrFGoK47Ddt2s5-g.png)

**Answer: Adobe ImageReady**

### **Clear the previous log and alarm files.**

Let’s remove the log file first, to do this we can use the command  `sudo rm snort.log.1671814047`, then press enter. If it is ready for you to add another command, then you entered it correctly.

![](https://miro.medium.com/max/630/1*siT3aIvV8ED-oubH7vp5KQ.png)

For the alarm file, we can use  `gedit`. The command will be  `sudo gedit alert`, then press enter to open the alert file in gedit.

![](https://miro.medium.com/max/567/0*tM8nJhSPDgndWnq7.png)

Click anywhere inside the alert file, then use the keyboard shortcut to select all, ctrl + a . The text editor should fill up blue, meaning that all the text is selected.

![](https://miro.medium.com/max/567/0*hAshpTMASFchBIO5.png)

Press the Deleted button on the keyboard, everything will be gone.

![](https://miro.medium.com/max/567/0*Y3ttPNpTlarNq8sL.png)

Save (ctrl + s) and X out of the text editor window, and your back in the terminal.

![](https://miro.medium.com/max/567/0*2axg2SNjqajiRqJQ.png)

### Deactivate/comment on the old rule.

Open the rule file with the command,  `sudo gedit local.rules`.

![](https://miro.medium.com/max/630/1*Fxgs-V59q7RM6zkr12cVng.png)

To Deactivate/comment out the rule, just put a # symbol at the beginning of the line.

![](https://miro.medium.com/max/630/1*zx3LWq94Oj95TMV_BlVZzw.png)

### Write a rule to detect the GIF file in the given pcap.

Before we write our rule, head back to the  [List of File Signatures Wiki](https://en.wikipedia.org/wiki/List_of_file_signatures)  page. Once there, we are going to use the browser find (ctrl + f) feature. In the search bar type GIF, and you will get 4 result all of which are going to be in the same row.

![](https://miro.medium.com/max/383/1*VdhNZek7HiK01HBv-yY-EA.png)

I will say, after some trail and error, I came up with this being the only code that would yield results. So now we have our number.

![](https://miro.medium.com/max/630/1*HTUjTpmWGnW1mMffYbZlKQ.png)

Time to write a rule to detect GIF files, to do so it is going to be much like the previous rule. I am going to type out the rule then explain it,  `alert tcp any any <> any any (msg:"GIF File Detected"; content:"GIF89A"; sid:100003; rev:1;)`. So before the parentheses we are keeping the same, so we go to msg: to start our changes. In the msg: section we change it to “GIF File Detected”. The content: section we will go back to the  [wiki](https://en.wikipedia.org/wiki/List_of_file_signatures), to get the GIF code and place that in here. Then the sid: section with once again be incremented by one, and the rev will be left along.

![](https://miro.medium.com/max/630/1*4zatcIvmUOzYU4o6qNUHVw.png)

Save (ctrl + s) and X out of the text editor window, and your back in the terminal.

![](https://miro.medium.com/max/567/0*2axg2SNjqajiRqJQ.png)

Time to run our rule through, snort against the pcap file. We will set it up as we did in the previous room, the command will be  `sudo snort -c local.rules -A full -l . -r mx-3.pcap`. We get the name of the pcap file from running the  `ls`  command earlier. So after typing the command in, press enter to run it.

![](https://miro.medium.com/max/630/1*ECJh-CBMG7f3IPoTaLbHqA.png)

After snort is done running, we can use  `ls`  again, and see that now we have an alert and log file.

![](https://miro.medium.com/max/580/1*hzkoXA9StrMcWWXOoyooDg.png)

### Investigate the logs and identify the image format embedded in the packet.

Let’s look at the log file, to do this we can use the snort command we learned in the previous room,  `sudo snort -r snort.log.1671817766 -X`. The name of your log file may be different, that is ok, just make sure it is named properly. Then press enter to run the command.

![](https://miro.medium.com/max/630/1*Dcp44djyAWWMTt2j-0H5cA.png)

Scroll up, looking at the text next to the hex output. Something should stand out to be in everyone, that is also something that you put in your rule. Once you figure it out/find it, type this answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/628/1*oHCxDafSLqAmTDmTnuMFRg.png)

**Answer: GIF89A**

## Task 5 Writing IDS Rules (Torrent Metafile)

Let’s create IDS Rules for torrent metafiles in the traffic!

## Answer the questions below

### **Navigate to the task folder.**

Let’s move back and then forward again from the Task 4 directory to the Task 5 directory. To do this use the command  `cd ..`, this backs you out of your current directory. The next command is  `cd TASK-T\ \(TorrentMetafile\)/`, this will move you forward into the Task 5 directory. Finish up with,  `ls`  to view the contents of the current directory.

![](https://miro.medium.com/max/630/1*hepfUgTb-MlNa8Hjwg-ivw.png)

### Use the given pcap file.

### Write a rule to detect the torrent metafile in the given pcap.

Time to write a rule to detect Torrent Metafiles, let’s go simple with this one. First open the text editor with  `sudo gedit local.rules`.

![](https://miro.medium.com/max/630/1*D86oPJIEZ8jac1P_60LpIg.png)

Writing out the command it is  `alert tcp any any <> any any (msg:"Torrent MetaFile Detected"; content:"torrent"; sid:100001; rev:1;)`. Let’s break it down, we start it off like we have been  `alert tcp any any <> any any`. Then we get to the msg: section, we make it  `msg:"Torrent MetaFile Detected"`. The content: section we want to search for any instance of torrent. Then sid: 10001, and rev:1 as always. Once you have it all typed out, you are ready to save your rule.

![](https://miro.medium.com/max/630/1*s4hgqmTEdPuSpkZZ0BlKrw.png)

Save (ctrl + s) and X out of the text editor window, and your back in the terminal.

![](https://miro.medium.com/max/630/1*RWj7nDP_OYZf6hZw25wWkA.png)

### What is the number of detected packets?

Time to run our rule through, snort against the pcap file. We will set it up as we did in the previous room, the command will be  `sudo snort -c local.rules -A full -l . -r mx-3.pcap`. We get the name of the pcap file from running the  `ls`  command earlier. So after typing the command in, press enter to run it.

![](https://miro.medium.com/max/630/1*wpfdTC5u1_OebjoP9ke7Tw.png)

After snort is done running, we can use  `ls`  again, and see that now we have an alert and log file.

![](https://miro.medium.com/max/630/1*-fyP4RAjiiUPD2b-HsvfuQ.png)

When snort is done outputting the log file, you will see Total, if you look to the right in the Total row you will see a number. This number is the answer to the question. Type this answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/409/1*6bqRoTKZaitqqGdmYfbcYg.png)

**Answer: 2**

### Investigate the log/alarm files.

Go back to the log where you just got the answer from in the previous question. You will just need to scroll up to the packet section.

![](https://miro.medium.com/max/630/1*d9cw1ouUgKZI2hTgomLLOA.png)

### What is the name of the torrent application?

Now that you are up in the Packet section, look in the text next to the hex values, this is where you are going to find the answer. It is in both packets, and can be found just under halfway down through the text. Once you find it, type this answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/630/1*VSSNz1hIc2RuJKNk_8jl5A.png)

**Answer: bittorrent**

### Investigate the log/alarm files.

Stay where you are!!!!

### What is the MIME (Multipurpose Internet Mail Extensions) type of the torrent metafile?

This answer is easier to find once you have found the previous answer. It has the previous answer in it, but it starts before the previous answer. Once you find it, type this answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/630/1*hlCNO5SXiu74Enxf3Skh7w.png)

**Answer: application/x-bittorrent**

### Investigate the log/alarm files.

Stay where you are!!!!

### What is the hostname of the torrent metafile?

Going back for the last time, look for Host:, the answer can be found right after this. Once you find it, type this answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/630/1*qiSXV_Yn1lQ3q0z0Am66ZA.png)

**Answer: tracker2.torrentbox.com**

### You have finished these tasks, and can now move onto Task 6 Troubleshooting Rule Syntax Errors.