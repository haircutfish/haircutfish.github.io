---
layout: "post"
title: "TryHackMe Room — Summit"
categories: Cyber Defence Frameworks
tags: TryHackMe, SOC Level One Path, SOC, Cyber Defence Frameworks
---

----------
This is a subscribers only room on TryHackMe. It was created by [TryHackMe](https://tryhackme.com/p/tryhackme). Here it the link to said room, [TryHackMe Room — Summit](https://tryhackme.com/r/room/summit).

Can you chase a simulated adversary up the Pyramid of Pain until they finally back down?


![](https://cdn-images-1.medium.com/max/720/0*MVlunZCB-pUZ4tx4.png)

## Task 1 Challenge

### Objective

After participating in one too many incident response activities, PicoSecure has decided to conduct a threat simulation and detection engineering engagement to bolster its malware detection capabilities. You have been assigned to work with an external penetration tester in an iterative purple-team scenario. The tester will be attempting to execute malware samples on a simulated internal user workstation. At the same time, you will need to configure PicoSecure’s security tools to detect and prevent the malware from executing.

Following the **Pyramid of Pain’s** ascending priority of indicators, your objective is to increase the simulated adversaries’ cost of operations and chase them away for good. Each level of the pyramid allows you to detect and prevent various indicators of attack.

### Room Prerequisites

Completing the preceding rooms in the [Cyber Defence Frameworks module](https://tryhackme.com/module/cyber-defence-frameworks) will be beneficial before venturing into this challenge. Specifically, the following:

-   [The Pyramid of Pain](https://tryhackme.com/room/pyramidofpainax)
-   [MITRE](https://tryhackme.com/room/mitre)

### Connection Details

Please click **Start Machine** to deploy the application, and navigate to [https://LAB_WEB_URL.p.thmlabs.com](https://lab_web_url.p.thmlabs.com/) once the URL has been populated.

Start by clicking on the green _Start Machine_ box in the top right of the Task 1 section.

![](https://cdn-images-1.medium.com/max/720/1*AMx1Pns_0O367TJiZod6Dg.png)

Once the URL is available, give it a click. You should be greated with the following below

![](https://cdn-images-1.medium.com/max/720/1*WOqKmqcS_aAtkdbDGigRWQ.png)

**Note:** It may take a few minutes to deploy the machine entirely. If you receive a “Bad Gateway” response, wait a few minutes and refresh the page.

----------

## Answer the questions below

### What is the first flag you receive after successfully detecting **sample1.exe**?

From the VM URL page, first read through the email from Sphinx. Afterwards we have a sample to check out. Click on the _sample1.exe_ box at the bottom of the email to move over to the Malware Sandbox tool.

![](https://cdn-images-1.medium.com/max/720/1*bbYFoawfTdNDHV5wZOAsrA.png)

We can analysis the sample by clicking the bluish/gray box labeled _Submit for Analysis_.

![](https://cdn-images-1.medium.com/max/720/1*qcESuTFpDl9oLxndm5aOnQ.png)

After the analysis has completed, we will have the General Info for sample1.exe. Remebering from the [Pyramid of Pain](https://tryhackme.com/r/room/pyramidofpainax), Hashes are Trival and can easily be change. But we can use them here to detect sample1.exe. So copy the SHA256 hash, then click on the hamburger in the top left of the screen. From the drop-down menu, click on _Manage Hashes_.

![](https://cdn-images-1.medium.com/max/720/1*_d8I0qicM35zKhlcgAnMSQ.png)

In Manage Hashes, we can add the SHA256 hash that was detected. To do this, click on the circle to the left of SHA256 which will make it blue and have it selected. Then paste the hash value in the box below it. Finally, click the bluish/gray _Submit Hash_ button.

![](https://cdn-images-1.medium.com/max/720/1*sbzCxgYpB5Agtn6KlZGYoA.png)

If done correctly, you will see _The hash value was added to the blocklist!_ After which you will see _Nice work! You prevented_ `_sample1.exe_` _from executing by detecting its unique hash value. Check your inbox for the next steps._ Click on the _inbox_ link from the statement above the Hash Blocklist.

![](https://cdn-images-1.medium.com/max/720/1*foPSS8KxXPnGspHIxx1jYg.png)

An email update has appeared in the Mail section. Read through it as it gives great information. At the end of the email you will find the flag and the answer to the question. Copy and paste it into the THM answer field, then click _Submit_.

![](https://cdn-images-1.medium.com/max/720/1*8YcuDYwEz39ePZT54WHBAA.png)

_ANSWER: THM{f3cbf08151a11a6a331db9c6cf5f4fe4}_

  

### What is the second flag you receive after successfully detecting **sample2.exe**?

Reading through the new email, Sphinx has recompiled the malware and was able to run it again. They gave us the sample to analyze again, so click on the sample at the bottom of the email to hop over to the Malware analysis screen.

![](https://cdn-images-1.medium.com/max/720/1*hZRWWEiPjQ7U-c3bUvbgSw.png)

We are now at the Malware Sandbox screen. Before we can analyze, we need to change the sample to _sample2.exe_. This can be done by clicking the down caret on the _File:_ drop-down box. In the drop-down select choose _sample2.exe_. Finally click the bluish/gray _Submit for Analysis_ button

![](https://cdn-images-1.medium.com/max/720/1*K6mLo_DDopDseYue766ENg.png)

After the analysis of the file has completed, we can review the findings. If you scroll down to the bottom we can see this time we have some new findings in the way of Network Activity. As per the next stage up on the pyramid we want to look at the IP address. As we can see the IP address _154.35.10.113_ goes to a very suspicious URL. Highlight and copy the IP address, then we need to head to the firewall to block it.

![](https://cdn-images-1.medium.com/max/720/1*za2aJtRNIhUG4WzTqvDLQw.png)

So get to the Firewall Manager, click on the hamburger in the top left of the window. In the drop-down you will see _Firewall Manager_, click on it.

![](https://cdn-images-1.medium.com/max/720/1*sdzQlyP8YTLUrn_I5_fZAA.png)

Next you will need to click on the _Create Firewall Rule_ button.

![](https://cdn-images-1.medium.com/max/720/1*yx_x8Joq4txL4pJ-ZAmsuw.png)

New options will propagate indicating to _Create Firewall Rule_. For the _Type_ we want to choose _Egress_ as that mean leaving (I think of it as E as in Escape). Next up is _Source IP_, for it to work on all systems of the company, you will want to type _Any_. What this means is that it will cover any system reaching out to the destination IP. Which brings us to the next section, _Destination IP_. This is where you will paste the IP address from the Malware Analysis page. Lastly the _Action_ section, you will want to keep it as _Deny_. This is so that any system reaching out to _154.35.10.113_ will be deny and not allow to connect. Now click on the _Save Rule_ button.

![](https://cdn-images-1.medium.com/max/720/1*xRhidi3odWxJxbHr0knRNA.png)

After clicking _Save Rule_, it will be indicated that _sample2.exe_ was blocked. Additionally, it will let us know we have a new email. Click on the _inbox_ link to head over and read it.

![](https://cdn-images-1.medium.com/max/720/1*Em3PMrk2zJhelcZXEa05ag.png)

Again, the flag can be found towards the bottom of the email. Copy and paste it into the THM answer field, then click _Submit_.

![](https://cdn-images-1.medium.com/max/720/1*7gMdojkR1_knbpfnICNmaw.png)

_ANSWER: THM{2ff48a3421a938b388418be273f4806d}_

  

### What is the third flag you receive after successfully detecting

As before, read through the email as it gives great insight. Once you have finished click on _sample3.exe_ at the bottom to move over to the Malware Sandbox page.

![](https://cdn-images-1.medium.com/max/720/1*0GbVMOdOOJN0YQ4aIfGtow.png)

On the Malware Sandbox page, click the down caret. This will drop-down all the samples we have access to. Click on _sample3.exe_, then click on the _Submit for Analysis_ button.

![](https://cdn-images-1.medium.com/max/720/1*iHI8y0hYF4n8IBQ1kpjQwQ.png)

When the analaysis has completed, we can read the _Behaviour Analysis_. This section gives you an idea of what the Malware is doing. After you have done this, it’s time to scroll down and look at the artifacts.

![](https://cdn-images-1.medium.com/max/720/1*ImHOLox2A13CsRqZhYDpOA.png)

Scrolling down we can see we have some more information this time. As we can see, there is a suspicious looking domain appearing in our results. Highlight the suspicious domain from the _Domain_ section at the bottom. Now lets head over to the DNS Filter page.

![](https://cdn-images-1.medium.com/max/720/1*L1lm_JuB02P-HrxPK3GSfQ.png)

Click on the hamburger in the top left of the window. In the drop-down you will see _DNS Filter_, click on it.

![](https://cdn-images-1.medium.com/max/720/1*WMXqkdPCb3-c1Lgrga4wUg.png)

Once on the _DNS Rule Manager_ page, click on the _Create DNS Rule_.

![](https://cdn-images-1.medium.com/max/720/1*A0sGDPlwkJHU7I7z4ckaAQ.png)

Starting at the top, we need to name the rule. This can be however you want to name it. I chose _Stop Malware download,_ which goes back to what we saw in the _Behavior Analysis_ section. Next up is the _Category_ section, we can leave this as _Malware_. Following that section is _Domain Name_, which we can paste in the domain from the analysis page. The last section is _Action_, which can be left to _Deny_. Our rule basically means that any traffic going to or coming from _emudyn.bresonicz.info_ will be denied. The last step is to click the _Save Rule_ button.

![](https://cdn-images-1.medium.com/max/720/1*_DYv3-xAnLwlmfMQMmzCdA.png)

After clicking _Save Rule_, it will be indicated that _sample3.exe_ was blocked. Additionally, it will let us know we have a new email. Click on the _inbox_ link to head over and read it.

![](https://cdn-images-1.medium.com/max/720/1*OrPYhgVM7YAtABJo4RpbDg.png)

The flag can be found towards the bottom of the email. Copy and paste it into the THM answer field, then click _Submit_.

![](https://cdn-images-1.medium.com/max/720/1*EYiLjTWRDqQhRwaxG61tHQ.png)

_ANSWER: THM{4eca9e2f61a19ecd5df34c788e7dce16}_

  

### What is the fourth flag you receive after successfully detecting **sample4.exe**?

Read through the email again. Once you have finished click on _sample4.exe_ at the bottom to move over to the Malware Sandbox page.

![](https://cdn-images-1.medium.com/max/720/1*2ar7nw6PPqJvHDDwYZxLJA.png)

On the Malware Sandbox page, click the down caret. This will drop-down all the samples we have access to. Click on _sample4.exe_, then click on the _Submit for Analysis_ button.

![](https://cdn-images-1.medium.com/max/720/1*sKhJ6u1SslSoxZ3SJARa0Q.png)

After the analysis has completed, we can take a look at the _Behaviour Analysis_ section. In it we can see the Malwave _Disables Windows Defender Real-time monitoring_. With this knowledge, let’s scroll down to see how Sphinx accomplished this.

![](https://cdn-images-1.medium.com/max/720/1*bqm6XKLKvl9v_jWAgOmeug.png)

We have a new section called _Registry Activity_, in this section we can see registry modifications that were made during the malware execution. Since we saw in the _Behavior Analysis_ that Windows Defender was disabled. Its safe to say that out of the three registry events that top one is the one we are looking for. Highlight and copy all the infomation from registry event and paste it notepad for the time being. Now lets head over to _Sigma Rule Builder_ to create a Sigma rule that detects when this registry value has changed to 1.

![](https://cdn-images-1.medium.com/max/720/1*I4hoj7b_uPmSu_nSvfZqBA.png)

Click on the hamburger in the top left of the window. In the drop-down you will see _Sigma Rule Builder_, click on it.

![](https://cdn-images-1.medium.com/max/720/1*JGFtGR0tKiGJvN6scZuU2Q.png)

On the _Sigma Rule Builder_ we need to click on the _Create Sigma Rule_ button to open the options to create the Sigma rule.

![](https://cdn-images-1.medium.com/max/720/1*qzDesGloBoGH6Rx-UhWusg.png)

We are given four options to start step 1 of creating our Sigma Rule. Read through the options, a registry change doesn’t apply to _Web Server Logs_, _VPN Logs_, or _Application Logs_. Meaning that _Sysmon Event Logs_ are our best option at this point. Click on _Sysmon Event Logs_.

![](https://cdn-images-1.medium.com/max/720/1*0ezQalXhWdiN5EQ7uPs2ag.png)

We are given another four choices. Looking them over the obvious choice is _Registry Modifications_, as we know that the Malware made a registry value change. Click on _Registry Modifications_.

![](https://cdn-images-1.medium.com/max/720/1*XHhu8-AG5LB4nKVWqNcTdQ.png)

Using the information we copied and pasted into our notepad, we will use it to fill out the final step of our _Sigma Rule Creation_. Starting with the _Registry Key_, paste _HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Defender\Real-Time Protection_ into this input field. Next up is the _Resgistry Name_, which we will use _DisableRealtimeMonitoring_. The _Value_ that the registry entry was changed to was _1_. Lastly, we need to map it to a MITRE ATT&CK ID. Looking over the list we can see _Defense Evasion (TA0005)_. Since the Malware disables Windows Defender, it’s safe to say it is trying to evade our defenses. Lastly, we need to click on _Validate Rule_. Which will create the Sigma rule and Validate that it detects the Malware.

![](https://cdn-images-1.medium.com/max/720/1*fdluL4qXSVErB-LLydil_w.png)

After clicking _Validate Rule,_ you will see a quick pop up at the top of the window (so fast I didn’t get a chance to screenshot it) indicating that the rule did detect the Malware. Additionally, a sound that you have a new message will play as well. Let’s head to our Mailbox to see what Sphinx has to say. Again, click the hamburger in the top left of the window. Then click on _Mail(1)_.

![](https://cdn-images-1.medium.com/max/720/1*TsjyUC18-KnZ8ras60JEpw.png)

The flag can be found towards the bottom of the new email. Copy and paste it into the THM answer field, then click _Submit_.

![](https://cdn-images-1.medium.com/max/720/1*RcWsHewqjcBx8Hq-hdTbkg.png)

_ANSWER: THM{c956f455fc076aea829799c0876ee399}_

  

### What is the fifth flag you receive after successfully detecting **sample5.exe**?

Read through the email. Once you have finished click on _outgoing_connections.log_ at the bottom of the email.

![](https://cdn-images-1.medium.com/max/720/1*ub79mDrr2i-i06gD-djtZQ.png)

You will be able to view the attachment on the right side of the window. Looking over the _outgoing_connections.log_ file, lets find some patterns. Starting with the Destination Column the IP address 51.102.10.19 appear a lot. Looking at the Date and Time column in correlation to IP address that appears, it seems to occur every _30 mins_. Next shifting over to the Port column, we can see that the connection always occurs over _port 443_. Lastly, looking at _Size_ column, the _Packet Size_ always sticks to _97 bytes_. We should have all the information we need to create a Sigma rule to detect this type of traffic, let’s head over and create it.

![](https://cdn-images-1.medium.com/max/720/1*Wz8Coy55WL086A2yEadiGw.png)

Click on the hamburger in the top left of the window. In the drop-down you will see _Sigma Rule Builder_, click on it.

![](https://cdn-images-1.medium.com/max/720/1*JGFtGR0tKiGJvN6scZuU2Q.png)

On the _Sigma Rule Builder_ we need to click on the _Create Sigma Rule_ button to open the options to create the Sigma rule.

![](https://cdn-images-1.medium.com/max/720/1*qzDesGloBoGH6Rx-UhWusg.png)

Starting with _Step 1_, we are working with a log file. So the best option at hand is _Sysmon Event Logs_. So click on _Sysmon Event Logs_.

![](https://cdn-images-1.medium.com/max/720/1*riQb6DcLDBaUWOXqN8vPFg.png)

Next up is _Step 2._ We know that the _outgoing_connections.log_ file deals with

![](https://cdn-images-1.medium.com/max/720/1*zjTl09MaZgxQdXROQMgv7w.png)

Lastly, we need to click on _Validate Rule_. Which will create the Sigma rule and Validate that it detects the Malware.

![](https://cdn-images-1.medium.com/max/720/1*P4_p6d3shdSkNIWZJ0C0Fw.png)

After clicking _Validate Rule,_ you will see a quick pop up at the top of the window (so fast I didn’t get a chance to screenshot it) indicating that the rule did detect the Malware. Additionally, a sound that you have a new message will play as well. Let’s head to our Mailbox to see what Sphinx has to say. Again, click the hamburger in the top left of the window. Then click on _Mail(1)_.

![](https://cdn-images-1.medium.com/max/720/1*TsjyUC18-KnZ8ras60JEpw.png)

The flag can be found towards the bottom of the new email. Copy and paste it into the THM answer field, then click _Submit_.

![](https://cdn-images-1.medium.com/max/720/1*cLYxIis44xh7iKYNeD4bDA.png)

_ANSWER: THM{46b21c4410e47dc5729ceadef0fc722e}_

  

### What is the final flag you receive from Sphinx?

Read through the email. Once you have finished click on _commands.log_ at the bottom of the email.

![](https://cdn-images-1.medium.com/max/720/1*cwXnUi5QOoRZrHzcpXieJw.png)

You should be able to view the attachment on the right side of the screen now. Parsing through the log, we can see that Sphinx has their malware sending information to `%temp%\exfiltr8.log`  file. This should give us enough information to create a Sigma rule. Let’s head over and make one.

![](https://cdn-images-1.medium.com/max/720/1*4CO5ZLDoQB8X7vAaCLvdxg.png)

Click on the hamburger in the top left of the window. In the drop-down you will see _Sigma Rule Builder_, click on it.

![](https://cdn-images-1.medium.com/max/720/1*JGFtGR0tKiGJvN6scZuU2Q.png)

On the _Sigma Rule Builder_ we need to click on the _Create Sigma Rule_ button to open the options to create the Sigma rule.

![](https://cdn-images-1.medium.com/max/720/1*qzDesGloBoGH6Rx-UhWusg.png)

Looking through the chooses again, _Sysmon_ _Event Logs_ appears to be the best choice. As it encompasses _detailed information about command line activity_. Click on _Sysmon Event Logs_.

![](https://cdn-images-1.medium.com/max/720/1*UHI0Tfy9-mRThLEwGvOiuQ.png)

Looking at the _commands.log_ file, we know that Sphinx’s malware is creating a file in the _%temp%_ directory, then adding information to it for exfiltration. With this knowledge, we are going to click on _File Creation and Modification_ to choose it.

![](https://cdn-images-1.medium.com/max/720/1*sgD6NjpRuPg044FRunlV5g.png)

Now before the rule can be created, we need to add the information we gained from the _connection.log_ file. Starting with the file path is where the file is located, this would be `%temp%` . Next up is the filename, which is `exfiltr8.log` . Lastly, we have choose the correct ATT&CK ID what matches what the Sphinx is trying to do. In this case, they are trying to _Exfiltrate_ data  meaning _Exfiltration (TA0010)_ is what we want to choose. Finally, click on the _Validate Rule_ button.

![](https://cdn-images-1.medium.com/max/720/1*RhgUSPiGBc17KcbLkW7k6Q.png)

After clicking _Validate Rule,_ you will see a quick pop up at the top of the window (again, so fast I didn’t get a chance to screenshot it) indicating that the rule did detect the Malware. Additionally, a sound that you have a new message will play as well. Let’s head to our Mailbox to see what Sphinx has to say. Again, click the hamburger in the top left of the window. Then click on _Mail(1)_.

![](https://cdn-images-1.medium.com/max/720/1*TsjyUC18-KnZ8ras60JEpw.png)

Once you are back at your Inbox, you will see the new email. The final flag can be found at the bottom of the email. Copy and paste it into the THM answer field, then click _Submit_.

![](https://cdn-images-1.medium.com/max/720/1*NdFxHkrWDCJOqhsBm4h_TQ.png)

_ANSWER: THM{c8951b2ad24bbcbac60c16cf2c83d92c}_

  

----------

## 🎉🎉🎉 Congrats!!!! You just completed the Summit Room!!!🎉🎉🎉