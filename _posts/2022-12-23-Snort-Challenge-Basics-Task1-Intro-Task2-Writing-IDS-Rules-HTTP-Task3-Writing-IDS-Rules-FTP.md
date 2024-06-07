---
layout: "post"
title: "TryHackMe Snort Challenge — The Basics — Task 1 Introduction, Task 2 Writing IDS Rules (HTTP), & Task 3 Writing IDS Rules (FTP)"
categories: Snort-Challenge-TheBasics
tags: TryHackMe, Snort, SOC Level One Path
---



Put your snort skills into practice and write snort rules to analyze live capture network traffic.

## Task 1 Introduction

![](https://miro.medium.com/max/630/0*PV0e0vWIYh6D1hy0.png)

The room invites you a challenge to investigate a series of traffic data and stop malicious activity under two different scenarios. Let’s start working with Snort to analyze live and captured traffic.

We recommend completing the  [Snort](https://tryhackme.com/room/snort)  room first, which will teach you how to use the tool in depth.

![](https://miro.medium.com/max/630/0*FdFLM1v7wHv9wGlU.png)

Exercise files for each task are located on the desktop as follows;

![](https://miro.medium.com/max/630/0*nnfDPFEV0gVbZwpX.png)

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

## Task 2 Writing IDS Rules (HTTP)

Let’s create IDS Rules for HTTP traffic!

## Answer the questions below

### **Navigate to the task folder.**

We can get to the Task folder with  `cd Desktop/Exercise-Files/Files/TASK-2\ \(HTTP\)/`. Then I use  `ls`, to see the contents of the directory. You are now in the proper directory to get started.

![](https://miro.medium.com/max/465/1*UeLgftNojtkBwiPPF4WYWA.png)

### Use the given pcap file.

### Write rules to detect “**all TCP port 80 traffic**” packets in the given pcap file.

So we want to open a text editor, so use the command  `sudo gedit local.rules`, then press enter to open it.

![](https://miro.medium.com/max/630/1*IY2UyT62BOvjnl9oj4YUKw.png)

So from going through the previous room, we learned that we will start with alert. Then from what THM wants us to write, it is a tcp protocol with port 80. Then we create a message that is descriptive, followed by the sid and the rev. So our rule should be  `alert tcp any 80 <> any any (msg:”TCP port 80 found”; sid:100001; rev:1;)`, we need to create the rule again with the port in the destination side as well, so it would look like this,  `alert tcp any any <> any 80(msg:”TCP port 80 found”; sid:100002; rev:1;)`

![](https://miro.medium.com/max/630/1*XaJ1IkT1Z9SukKM7vrmNpw.png)

Save (ctrl + s) and X out of the text editor window, and your back in the terminal.

![](https://miro.medium.com/max/630/1*AC5PGXZlQGadHiV8ZWUsqA.png)

### What is the number of detected packets?

### Note: You must answer this question correctly before answering the rest of the questions in this task.

Time to run our rule through, snort against the pcap file. We will set it up as we did in the previous room, the command will be  `sudo snort -c local.rules -A full -l . -r mx-3.pcap`. We get the name of the pcap file from running the  `ls`  command earlier. So after typing the command in, press enter to run it.

![](https://miro.medium.com/max/630/1*DFp6EJBW47T-BSYpDk34pg.png)

After snort is done running, we can use  `ls`  again, and see that now we have an alert and log file.

![](https://miro.medium.com/max/625/1*YAfrUkJxOHXZUr8zhumV1A.png)

Let’s look at the log file, to do this we can use the snort command we learned in the previous room,  `sudo snort -r snort.log.1671720080`. The name of your log file may be different, that is ok, just make sure it is named properly. Then press enter to run the command.

![](https://miro.medium.com/max/630/1*F25ZoDvoZh0gs8w_JBUvqg.png)

When snort is done outputting the log file, you will see Total, if you look to the right in the Total row you will see a number. This number is the answer to the question. Type this answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/604/1*AZauFQKtUndVXWgKWBFsNA.png)

**Answer: 164**

### Investigate the log file.

### What is the destination address of packet 63?

Time to pick and choose packets to investigate, to do this once again we go back to what we learned in the previous room. We use the command from the previous question, but end it with -n 63, this will show us the first 63 packets. So the command is  `sudo snort -r snort.log.1671720080 -n 63`, then press enter to run it.

![](https://miro.medium.com/max/630/1*ur0G8iXtkyoRte-aqotJSw.png)

When it is done running, we want to scroll up to the last packet being displayed.

![](https://miro.medium.com/max/630/1*5hCOpVH6yIGMQIIn99S0kQ.png)

Once we reach the packet, you can find the destination IP as it the second IP address in the second row. Once you find it, type this answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/630/1*AFhDkXIWjiqf1vc4Cv-3eA.png)

**Answer: 145.254.160.237**

### Investigate the log file.

### What is the ACK number of packet 64?

So head back to your terminal, and press the up arrow to bring back the previous command. Then delete the number 63 and type in the number 64.

![](https://miro.medium.com/max/598/1*7SlYa5rqZ50DFWegF9q6pA.png)

Now that we have the correct number in, press enter for snort to read the first 64 packets from the log file.

![](https://miro.medium.com/max/630/1*UTHXD6KijoyIIPFF8X9lYw.png)

As before, when it is done running, we want to scroll up to the last packet being displayed.

![](https://miro.medium.com/max/439/1*N3f4SJgiPj06ZKUIglJ_cg.png)

Once we reach the packet, you can find the Ack in the last row around the middle of the packet. Once you find it, type this answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/542/1*LFTT1ObSXaO6YufOP_6izw.png)

**Answer: 0x38AFFFF3**

### Investigate the log file.

### What is the SEQ number of packet 62?

Go back to the terminal and if you look two packets up you are at 62. The Seq number is right before the Ack in the last row, and the Seq number will look familiar. Once you find it, type this answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/590/1*s22OOEagJnNQZKqieDRMAw.png)

**Answer: 0x38AFFFF3**

### Investigate the log file.

### What is the TTL of packet 65?

So head back to your terminal, and press the up arrow to bring back the previous command. Then delete the number 64 and type in the number 65.

![](https://miro.medium.com/max/630/1*KZfknUMm9ueOHRCbX267rg.png)

Now that we have the correct number in, press enter for snort to read the first 65 packets from the log file.

![](https://miro.medium.com/max/630/1*I9YJOLUkw2jUjEVnVrIUGw.png)

As before, when it is done running, we want to scroll up to the last packet being displayed.

![](https://miro.medium.com/max/512/1*RuNsrTyQrFReLNnQb2KCnA.png)

Once we reach the packet, you can find the TTL: in the middle row, the number after the colon is the answer. Once you find it, type this answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/571/1*hLAQpP4CoDMX8QZpoGn94A.png)

**Answer: 128**

### Investigate the log file.

### What is the source IP of packet 65?

Heading back to packet 65, look to the second row and look for the first IP address. This is the source IP address, and the answer to this question. Once you find it, type this answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/571/1*Gp1LJ8KBXVmf-YOijYNOvg.png)

**Answer: 145.254.160.237**

### Investigate the log file.

### What is the source port of packet 65?

Heading back, one last time, to packet 65, look at the end of the first IP address for the number after the colon. This is the port number, and the answer to this question. Once you find it, type this answer into the TryHackMe answer field, then click submit.

**Answer: 3372**

## Task 3 Writing IDS Rules (FTP)

Let’s create IDS Rules for FTP traffic!

## Answer the questions below

### **Navigate to the task folder.**

Time to move over to the Task 3 directory, to do so we first need to move back a directory, we do this with  `cd ..`. Now we are in the Exercise-Files directory, to move forward into the Task 3 directory we use the command  `cd TASK-3\ \(ftp\)/`. Then we use the  `ls`  command to list the contents of the directory.

![](https://miro.medium.com/max/480/1*nHbJR4gWdujjdZGalk_wAA.png)

### Use the given pcap file.

### Write rules to detect “**all TCP port 21**” traffic in the given pcap.

Let’s open the text editor, use the command  `sudo gedit local.rules`. Press enter to run the command.

![](https://miro.medium.com/max/630/1*myegmdmuuZdDFMqZjUXwZw.png)

I set it up similar to the previous task, catching traffic on both the source and the destination side. Then the message, I differentiated which side it is on. So the rules are written like this,  `alert tcp any 21 <> any any (msg:"src:FTP found"; sid:100001; rev:1;)`  &  `alert tcp any any <> any 21 (msg:"des:FTP found"; sid:100002; rev:1;)`. Once you have them written out, it’s time to save.

![](https://miro.medium.com/max/514/1*x5NYkHZRQtSVRl_x0XsYRg.png)

Save (ctrl + s) and X out of the text editor window, and your back in the terminal.

![](https://miro.medium.com/max/630/1*-GA6tXtwmrykpXDCBY6MWw.png)

### What is the number of detected packets?

Time to run our rule against the ftp pcap that THM gave us. Just like in the previous task, the command is the same except the file at the end. The command is  `sudo snort -c local.rules -A full -l . -r ftp-png-gif.pcap`, after typing this in, press enter and let Snort do it’s work.

![](https://miro.medium.com/max/630/1*mnCPmjRRN0M67ZRBbOFEWA.png)

When Snort is done running, we can use the  `ls`command to view the contents of the current directory. As we can see, we have our alert and log file now.

![](https://miro.medium.com/max/460/1*cP9mw8UZADg9w7HRmtHNpg.png)

Let’s take a look at the log file with the command,  `sudo snort -r snort.log.1671731339`, and press enter for snort to read and output it to the terminal.

![](https://miro.medium.com/max/630/1*mZMxNNcyCFtuQ8Lq8s_YLw.png)

When snort is done outputting the log file, you will see Total, if you look to the right in the Total row you will see a number. This number is the answer to the question. Type this answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/521/1*7Ts7OaurGKgy0tJFeCr9ew.png)

**Answer: 614**

### Investigate the log file.

### What is the FTP service name?

Head back to the terminal, since we don’t want to search through 500+, let’s start with 10, and let’s add a little information to them as well. We can do this with the  `-X`  parameter, so the command is  `sudo snort -r snort.log.1671731339 -X -n 10`. Press enter to run this command.

![](https://miro.medium.com/max/630/1*nSyXQWczhPWXlCprMP3ySw.png)

Scroll back to the top, and as you can see, we have more information. Scroll down through the 10 packets, looking for FTP service, as the question is asking.

![](https://miro.medium.com/max/550/1*Eh1_I_GCHhaLQxqLs_b8Ug.png)

After scrolling down through you should reach about packet 7 and 8, you should see it. Once you find it, type this answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/492/1*ZQsdKGZ0t1mUgZqeKbFAeQ.png)

**Answer: Microsoft FTP service**

### **Clear the previous log and alarm files.**

Let’s remove the log file first, to do this we can use the command  `sudo rm snort.log.1671731339`, then press enter. If it is ready for you to add another command, then you entered it correctly.

![](https://miro.medium.com/max/599/1*qIDwEnGIfv9yvm4cmjQnJw.png)

For the alarm file, we can use  `gedit`. The command will be  `sudo gedit alert`, then press enter to open the alert file in gedit.

![](https://miro.medium.com/max/630/1*moVuKZ3j2SipKTD0M9R7hg.png)

Click anywhere inside the alert file, then use the keyboard shortcut to select all, ctrl + a . The text editor should fill up blue, meaning that all the text is selected.

![](https://miro.medium.com/max/630/1*1xU90Rv7Jx51ueCboqgumA.png)

Press the Deleted button on the keyboard, everything will be gone.

![](https://miro.medium.com/max/630/1*AW5E0uz24xR92bMiUFrl3g.png)

Save (ctrl + s) and X out of the text editor window, and your back in the terminal.

![](https://miro.medium.com/max/630/1*HLEEBQMbBV3dO3gdcTLSJA.png)

### Deactivate/comment on the old rules.

Open the rule file with the command,  `sudo gedit local.rules`.

![](https://miro.medium.com/max/630/1*lcfpG7o55sI-n9iInGpOfQ.png)

To Deactivate/comment out the rule, just put a # symbol at the beginning of the line.

![](https://miro.medium.com/max/490/1*2Dos-rSXFjJYfKAXdeBDGg.png)

### Write a rule to detect failed FTP login attempts in the given pcap.

Let’s write the rules to catch failed FTP login attempts on our system. Start off, we can type the first part of the first alert  `alert tcp any 21 <> any any`. Then when it comes to the msg: section I am going to change to  `msg:"Detected Failed FTP Login";`. The sid: area is going to be  `sid:100003`, and rev is going to stay the same.But before the sid: section we are going to add a content: section, and that will be  `content:"530 User";`  . So the full rule should look like this,  `alert tcp any 21 <> any any (msg:"Detectected Failed FTP Login"; content:"530 User"; sid:100003; rev:1;)`

![](https://miro.medium.com/max/630/1*f3kFtopQfWdKsqsSkDL_Iw.png)

Save (ctrl + s) and X out of the text editor window, and your back in the terminal.

![](https://miro.medium.com/max/630/1*HLEEBQMbBV3dO3gdcTLSJA.png)

The reason I went the route I did above is because I couldn’t figure out why “Failed” didn’t work so I looked at the hint and this is why. But doing a quick research I don’t know where it came from so I have to do more research on the topic

![](https://miro.medium.com/max/347/1*mt6h-6ApFx2xyyD3D2i8VQ.png)

### What is the number of detected packets?

Time to run our rule against the ftp pcap that THM gave us. Just like in the previous task, the command is the same except the file at the end. The command is  `sudo snort -c local.rules -A full -l . -r ftp-png-gif.pcap`, after typing this in, press enter and let Snort do it’s work.

![](https://miro.medium.com/max/630/1*xOq9TkYzkhZ2LROfeNhSnQ.png)

When Snort is done running, we can use the  `ls`command to view the contents of the current directory. As we can see, we have our alert and log file now.

![](https://miro.medium.com/max/434/1*BuX2kQCsVA7-4aiGqrjhpA.png)

Let’s take a look at the log file with the command,  `sudo snort -r snort.log.1671736484`, and press enter for snort to read and output it to the terminal.

![](https://miro.medium.com/max/630/1*BgFl8atFS7KP57zf1mUxzQ.png)

When snort is done outputting the log file, you will see Total, if you look to the right in the Total row you will see a number. This number is the answer to the question. Type this answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/448/1*LQlysHYcTAT3hkTevcntEg.png)

**Answer: 41**

### **Clear the previous log and alarm files.**

Let’s remove the log file first, to do this we can use the command  `sudo rm snort.log.1671736484`, then press enter. If it is ready for you to add another command, then you entered it correctly.

![](https://miro.medium.com/max/606/1*ubhd8uF-r8r2ITrJfQKqWg.png)

For the alarm file, we can use  `gedit`. The command will be  `sudo gedit alert`, then press enter to open the alert file in gedit.

![](https://miro.medium.com/max/630/1*6-OXbqGOHpEK78Iy4Wg5eg.png)

Click anywhere inside the alert file, then use the keyboard shortcut to select all, ctrl + a . The text editor should fill up blue, meaning that all the text is selected.

![](https://miro.medium.com/max/630/1*4WkU2PG1LmF1Gx1crXBRvw.png)

Press the Deleted button on the keyboard, everything will be gone.

![](https://miro.medium.com/max/630/1*AW5E0uz24xR92bMiUFrl3g.png)

Save (ctrl + s) and X out of the text editor window, and your back in the terminal.

![](https://miro.medium.com/max/630/1*HLEEBQMbBV3dO3gdcTLSJA.png)

### Deactivate/comment on the old rule.

Open the rule file with the command,  `sudo gedit local.rules`.

![](https://miro.medium.com/max/630/1*L1s3_awfP71a23g6yPsPWg.png)

To Deactivate/comment out the rule, just put a # symbol at the beginning of the line.

![](https://miro.medium.com/max/630/1*rfEJPTv1ik-X6xlhwcj17w.png)

### Write a rule to detect successful FTP logins in the given pcap.

Let’s write the rules to catch successful FTP login attempts. I am not going to lie, I checked the hint right away on this one as I was sure it was going to have a number I didn’t know about, and it did.

![](https://miro.medium.com/max/341/1*_pwnE4KXOJHs7q6F7NnrZg.png)

So our rule is going to be just like the last one we created, so let’s highlight, copy (ctrl + c), and paste (ctrl + v) under the last rule we created.

![](https://miro.medium.com/max/630/1*Vz7jDlI4go7O55ZMW4KNAw.png)

Time for rule surgery, first remove the # in the front, next change the msg: from Failed to Successful. Then content: from 530 User to 230 User, and sid from 100003 to 100004. So let’s stitch it together,  `alert tcp any 21 <> any any (msg:"Detected Successful FTP Login"; content:"230 User"; sid:100004; rev:1;)`. Once you have it all fixed, time to save.

![](https://miro.medium.com/max/630/1*3peA8MaRjPj8j47XZ3lEEg.png)

Save (ctrl + s) and X out of the text editor window, and your back in the terminal.

![](https://miro.medium.com/max/630/1*HLEEBQMbBV3dO3gdcTLSJA.png)

### What is the number of detected packets?

Time to run our rule against the ftp pcap that THM gave us. Just like in the previous task, the command is the same except the file at the end. The command is  `sudo snort -c local.rules -A full -l . -r ftp-png-gif.pcap`, after typing this in, press enter and let Snort do it’s work.

![](https://miro.medium.com/max/630/1*rXuWFNB3TBK2Gl41uRA_fQ.png)

When Snort is done running, we can use the  `ls`command to view the contents of the current directory. As we can see, we have our alert and log file now.

![](https://miro.medium.com/max/442/1*SHr6yjEW_qBRWkLhiBzqFA.png)

Let’s take a look at the log file with the command,  `sudo snort -r snort.log.1671738489`, and press enter for snort to read and output it to the terminal.

![](https://miro.medium.com/max/630/1*JigBFfTh2GJXUQXeDXOaqw.png)

When snort is done outputting the log file, you will see Total, if you look to the right in the Total row you will see a number. This number is the answer to the question. Type this answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/456/1*0WB8BFXAlNjjWC0tVFpK1A.png)

**Answer: 1**

### **Clear the previous log and alarm files.**

Let’s remove the log file first, to do this we can use the command  `sudo rm snort.log.1671738489`, then press enter. If it is ready for you to add another command, then you entered it correctly.

![](https://miro.medium.com/max/621/1*gfjXK_4O5-NZVQS1jRRMJQ.png)

For the alarm file, we can use  `gedit`. The command will be  `sudo gedit alert`, then press enter to open the alert file in gedit.

![](https://miro.medium.com/max/630/1*6-OXbqGOHpEK78Iy4Wg5eg.png)

Click anywhere inside the alert file, then use the keyboard shortcut to select all, ctrl + a . The text editor should fill up blue, meaning that all the text is selected.

![](https://miro.medium.com/max/630/1*4WkU2PG1LmF1Gx1crXBRvw.png)

Press the Deleted button on the keyboard, everything will be gone.

![](https://miro.medium.com/max/630/1*AW5E0uz24xR92bMiUFrl3g.png)

Save (ctrl + s) and X out of the text editor window, and your back in the terminal.

![](https://miro.medium.com/max/630/1*HLEEBQMbBV3dO3gdcTLSJA.png)

### Deactivate/comment on the old rule.

Open the rule file with the command,  `sudo gedit local.rules`.

![](https://miro.medium.com/max/630/1*ISOimqXVazhT1wV5zfGwQg.png)

To Deactivate/comment out the rule, just put a # symbol at the beginning of the line.

![](https://miro.medium.com/max/630/1*dMlOKBSdWjT3KTY6fqOnuA.png)

## Write a rule to detect failed FTP login attempts with a valid username but a bad password or no password.

Let’s write the rule to detect the failed FTP login attemps but with bad or no passwords. I have found a  [wiki](https://en.wikipedia.org/wiki/List_of_FTP_server_return_codes)  that has the server codes that we can use to help us. Click the link to be taken to the  [wiki](https://en.wikipedia.org/wiki/List_of_FTP_server_return_codes), once there use the browser find function ctrl + f, and type password, you will have two responses.

![](https://miro.medium.com/max/283/1*nZ5rujtTm7eBWFbhaCnaGQ.png)

Look at the first result, I think we might have a winner.

![](https://miro.medium.com/max/630/1*34IFkPpHAdKB8TW69pSX_A.png)

So back in the text editor, like before it’s time for surgery. Highlight copy (ctrl + c) the previous rule and paste (ctrl + v) under said rule.

![](https://miro.medium.com/max/630/1*oUqeNupUeBnsCIBodd7KSQ.png)

First remove the # in the front, next change the msg: from Successful to FTP Failed Login-Bad or No Password. Then content: from 230 User to 331 Password, and sid from 100004 to 100005. So let’s stitch it together,  `alert tcp any 21 <> any any (msg:"FTP Failed Login-Bad or No Password"; content:"331 Password"; sid:100005; rev:1;)`. Once you have it all fixed, time to save.

![](https://miro.medium.com/max/630/1*lxG2oONrStE1BLRHbtwnGw.png)

Save (ctrl + s) and X out of the text editor window, and your back in the terminal.

![](https://miro.medium.com/max/630/1*HLEEBQMbBV3dO3gdcTLSJA.png)

### What is the number of detected packets?

Time to run our rule against the ftp pcap that THM gave us. Just like in the previous task, the command is the same except the file at the end. The command is  `sudo snort -c local.rules -A full -l . -r ftp-png-gif.pcap`, after typing this in, press enter and let Snort do it’s work.

![](https://miro.medium.com/max/630/1*FFZfGBbCyj2UqZXCQXiE7A.png)

When Snort is done running, we can use the  `ls`command to view the contents of the current directory. As we can see, we have our alert and log file now.

![](https://miro.medium.com/max/427/1*QvhJYjyoOR176mRILXPWXQ.png)

Let’s take a look at the log file with the command,  `sudo snort -r snort.log.1671739842`, and press enter for snort to read and output it to the terminal.

![](https://miro.medium.com/max/630/1*YyIUbsPrVLeOGUa02FFiRQ.png)

When snort is done outputting the log file, you will see Total, if you look to the right in the Total row you will see a number. This number is the answer to the question. Type this answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/444/1*9gWTVdWFy2jeacdbCBMmUQ.png)

**Answer: 42**

### **Clear the previous log and alarm files.**

Let’s remove the log file first, to do this we can use the command  `sudo rm snort.log.1671739842`, then press enter. If it is ready for you to add another command, then you entered it correctly.

![](https://miro.medium.com/max/600/1*eficGjJAwfdKj1EQ06niwg.png)

For the alarm file, we can use  `gedit`. The command will be  `sudo gedit alert`, then press enter to open the alert file in gedit.

![](https://miro.medium.com/max/630/1*6-OXbqGOHpEK78Iy4Wg5eg.png)

Click anywhere inside the alert file, then use the keyboard shortcut to select all, ctrl + a . The text editor should fill up blue, meaning that all the text is selected.

![](https://miro.medium.com/max/630/1*4WkU2PG1LmF1Gx1crXBRvw.png)

Press the Deleted button on the keyboard, everything will be gone.

![](https://miro.medium.com/max/630/1*AW5E0uz24xR92bMiUFrl3g.png)

Save (ctrl + s) and X out of the text editor window, and your back in the terminal.

![](https://miro.medium.com/max/630/1*HLEEBQMbBV3dO3gdcTLSJA.png)

### Deactivate/comment on the old rule.

Open the rule file with the command,  `sudo gedit local.rules`.

![](https://miro.medium.com/max/630/1*z9HgI_dSNZhuktUenWITQw.png)

To Deactivate/comment out the rule, just put a # symbol at the beginning of the line.

![](https://miro.medium.com/max/630/1*86LL1fiO4v0x0dmohs0Uag.png)

### Write a rule to detect failed FTP login attempts with “Administrator” username but a bad password or no password.

So this time we don’t need to change much just add to what we have there. We will change up the msg to reflex what what we are looking for, add fast_pattern, and add another content section with “Administrator”. So it should look like this,  `alert tcp any 21 <> any any (msg:"FTP Failed Admin Login-Bad or No Password"; content:"331 Password"; fast_pattern; content:"Administrator"; sid:100006; rev:1;)`.

![](https://miro.medium.com/max/630/1*Ng3E4UzDGTx3qTuGct4tTg.png)

Save (ctrl + s) and X out of the text editor window, and your back in the terminal.

![](https://miro.medium.com/max/630/1*HLEEBQMbBV3dO3gdcTLSJA.png)

### What is the number of detected packets?

Time to run our rule against the ftp pcap that THM gave us. Just like in the previous task, the command is the same except the file at the end. The command is  `sudo snort -c local.rules -A full -l . -r ftp-png-gif.pcap`, after typing this in, press enter and let Snort do it’s work.

![](https://miro.medium.com/max/630/1*FFZfGBbCyj2UqZXCQXiE7A.png)

When Snort is done running, we can use the  `ls`command to view the contents of the current directory. As we can see, we have our alert and log file now.

![](https://miro.medium.com/max/425/1*NglnGkUpOZuu_JSn5VB3KQ.png)

Let’s take a look at the log file with the command,  `sudo snort -r snort.log.1671740806`, and press enter for snort to read and output it to the terminal.

![](https://miro.medium.com/max/630/1*f_qkh6nooJ62-03WlGhUlA.png)

When snort is done outputting the log file, you will see Total, if you look to the right in the Total row you will see a number. This number is the answer to the question. Type this answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/444/1*9gWTVdWFy2jeacdbCBMmUQ.png)

**Answer: 7**

**You have finished these tasks, and can now move onto  [Task 4 Writing IDS Rules (PNG) & Task 5 Writing IDS Rules (Torrent Metafile).](https://haircutfish.com/posts/Snort-Challenge-Basics-Task4-Writing-IDS-Rules-PNG-and-Task5-Writing-IDS-Rules-Torrent/)**