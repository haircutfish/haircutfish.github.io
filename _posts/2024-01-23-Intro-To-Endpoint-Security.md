---
layout: "post"
title: "TryHackMe Intro to Endpoint Security Room"
categories: Intro Endpoint Security
tags: TryHackMe, Endpoint Security, SOC Level One Path
---


  

![](https://cdn-images-1.medium.com/max/640/0*eB_wyxjnkaHooJvX.png)

Learn about fundamentals, methodology, and tooling for endpoint security monitoring.

## Task 1 Room Introduction

In this room, we will introduce the fundamentals of endpoint security monitoring, essential tools, and high-level methodology. This room gives an overview of determining a malicious activity from an endpoint and mapping its related events.

To start with, we will tackle the following topics to build a stepping stone on how to deal with Endpoint Security Monitoring.

-   Endpoint Security Fundamentals
-   Endpoint Logging and Monitoring
-   Endpoint Log Analysis

At the end of this room, we will have a threat simulation wherein you need to investigate and remediate the infected machines. This activity may require you first to understand the fundamentals of endpoint security monitoring to complete it.

Now, let’s deep-dive into the basics of Endpoint Security!

----------

## Task 2 Endpoint Security Fundamentals

### **Core Windows Processes**

Before we deal with learning how to deep-dive into endpoint logs, we need first to learn the fundamentals of how the Windows Operating System works. Without prior knowledge, differentiating an outlier from a haystack of events could be problematic.

To learn more about Core Windows Processes, a built-in Windows tool named Task Manager may aid us in understanding the underlying processes inside a Windows machine.

Task Manager is a built-in GUI-based Windows utility that allows users to see what is running on the Windows system. It also provides information on resource usage, such as how much each process utilizes CPU and memory. When a program is not responding, the Task Manager is used to terminate the process.

![](https://cdn-images-1.medium.com/max/640/0*4TRLlD5kcITZ9xFi.png)

A Task Manager provides some of the Core Windows Processes running in the background. Below is a summary of running processes that are considered normal behaviour.

Note: **“>”** symbol represents a parent-child relationship. `System (Parent) > smss.exe (Child)`

-   System
-   System > smss.exe
-   csrss.exe
-   wininit.exe
-   wininit.exe > services.exe
-   wininit.exe > services.exe > svchost.exe
-   lsass.exe
-   winlogon.exe
-   explorer.exe

In addition, the processes with no depiction of a parent-child relationship should not have a Parent Process under normal circumstances, except for the System process, which should only have **System Idle Process (0)** as its parent process.

You may refer to the [Core Windows Processes Room](https://tryhackme.com/room/btwindowsinternals) to learn more about this topic.

#### Sysinternals

With the prior knowledge of Core Windows Processes, we can now proceed to discuss the available toolset for analyzing running artifacts in the backend of a Windows machine.

The Sysinternals tools are a compilation of over 70+ Windows-based tools. Each of the tools falls into one of the following categories:

-   File and Disk Utilities
-   Networking Utilities
-   Process Utilities
-   Security Utilities
-   System Information
-   Miscellaneous

We will introduce two of the most used Sysinternals tools for endpoint investigation for this task.

-   **TCPView** — Networking Utility tool.
-   **Process Explorer** — Process Utility tool.

#### TCPView

**“TCPView** is a Windows program that will show you detailed listings of all TCP and UDP endpoints on your system, including the local and remote addresses and state of TCP connections. On Windows Server 2008, Vista, and XP, TCPView also reports the name of the process that owns the endpoint. TCPView provides a more informative and conveniently presented subset of the Netstat program that ships with Windows. The TCPView download includes Tcpvcon, a command-line version with the same functionality.” (**official definition**)

![](https://cdn-images-1.medium.com/max/640/0*wX0ysEio1KcU7ROc.png)

As shown above, every connection initiated by a process is listed by the tool, which may aid in correlating the network events executed concurrently.

### Process Explorer

“The **Process Explorer** display consists of two sub-windows. The top window always shows a list of the currently active processes, including the names of their owning accounts, whereas the information displayed in the bottom window depends on the mode that Process Explorer is in: if it is in handle mode, you’ll see the handles that the process selected in the top window has opened; if Process Explorer is in DLL mode you’ll see the DLLs and memory-mapped files that the process has loaded.” (**official definition**)

![](https://cdn-images-1.medium.com/max/640/0*8XficNzW9R-TaTWh.png)

Process Explorer enables you to inspect the details of a running process, such as:

-   Associated services
-   Invoked network traffic
-   Handles such as files or directories opened
-   DLLs and memory-mapped files loaded

To learn more about Sysinternals, you may refer to the [Sysinternals Room](https://tryhackme.com/room/btsysinternalssg).

## Answer the questions below

Since the answers can be found above, I won’t share the actual answer below. Just where you can find them.
### What is the normal parent process of services.exe?

The answer can be found under the _TaskManager_ section above. Look for _Note:_, under which you will see different process names. Look for _services.exe_, once you find it look at the process name to the left. This is the Parent Process and thus the answer to the question. Once you find it, type the answer into the TryHackMe answer field and click _Submit_.

![](https://cdn-images-1.medium.com/max/640/1*UNwYZVc1eMh56nZcK742dw.png)

  

### What is the name of the network utility tool introduced in this task?

This answer first appears in the _Sysinternals_ section. But then the section afterwards is all about this tool. Once you find it, type the answer into the TryHackMe answer field and click _Submit_.

![](https://cdn-images-1.medium.com/max/640/1*sEd3mLoLlGu8GgwSqSvb_g.png)

  

----------

## Task 3 Endpoint Logging and Monitoring

From the previous task, we have learned basic knowledge about the Windows Operating system in terms of baseline processes and essential tools to analyze events and artefacts running on the machine. However, this only limits us from observing real-time events. With this, we will introduce the importance of endpoint logging, which enables us to audit significant events across different endpoints, collect and aggregate them for searching capabilities, and better automate the detection of anomalies.

### Windows Event Logs

The Windows Event Logs are not text files that can be viewed using a text editor. However, the raw data can be translated into XML using the Windows API. The events in these log files are stored in a proprietary binary format with a .evt or .evtx extension. The log files with the .evtx file extension typically reside in `C:\Windows\System32\winevt\Logs`.

There are three main ways of accessing these event logs within a Windows system:

1.  **Event Viewer** (GUI-based application)
2.  **Wevtutil.exe** (command-line tool)
3.  **Get-WinEvent** (PowerShell cmdlet)

An example image of logs viewed using the **Event Viewer** tool is shown below.

![](https://cdn-images-1.medium.com/max/640/0*UehGiq1OzVxFHMbN.png)

You may refer to the [Windows Event Logs Room](https://tryhackme.com/room/windowseventlogs) to learn more about Windows Event Logs.

### Sysmon

Sysmon, a tool used to monitor and log events on Windows, is commonly used by enterprises as part of their monitoring and logging solutions. As part of the Windows Sysinternals package, Sysmon is similar to Windows Event Logs with further detail and granular control.

Sysmon gathers detailed and high-quality logs as well as event tracing that assists in identifying anomalies in your environment. It is commonly used with a security information and event management (SIEM) system or other log parsing solutions that aggregate, filter, and visualize events.

Lastly, Sysmon includes 27 types of Event IDs, all of which can be used within the required configuration file to specify how the events should be handled and analyzed. An excellent example of a configuration file auditing different Event IDs created by SwiftOnSecurity is linked [here](https://github.com/SwiftOnSecurity/sysmon-config).

The image below shows a sample set of Sysmon logs viewed using an **Event Viewer**.

![](https://cdn-images-1.medium.com/max/640/0*vqjbbFYhArjuzaaG.png)

To learn more about Sysmon, you may refer to the [Sysmon Room](https://tryhackme.com/room/sysmon).

### OSQuery

Osquery is an open-source tool created by Facebook. With Osquery, Security Analysts, Incident Responders, and Threat Hunters can query an endpoint (or multiple endpoints) using SQL syntax. Osquery can be installed on various platforms: Windows, Linux, macOS, and FreeBSD.

To interact with the Osquery interactive console/shell, open CMD (or PowerShell) and run `osqueryi`. You'll know that you've successfully entered into the interactive shell by the new command prompt.

  ```
								cmd.exe 
								
C:\Users\Administrator\> osqueryi  
Using a virtual database. Need help, type 'help'  
osquery>
```
A sample use case for using OSQuery is to list important process information by its process name.

 ``` 
								 osqueryi 
							 
osquery> select pid,name,path from processes where name='lsass.exe';  
+-----+-----------+-------------------------------+  
| pid | name      | path                          |  
+-----+-----------+-------------------------------+  
| 748 | lsass.exe | C:\Windows\System32\lsass.exe |  
+-----+-----------+-------------------------------+  
osquery>
```
Osquery only allows you to query events inside the machine. But with Kolide Fleet, you can query multiple endpoints from the Kolide Fleet UI instead of using Osquery locally to query an endpoint. A sample of Kolide Fleet in action below shows a result of a query listing the machines with the `lsass` process running.

![](https://cdn-images-1.medium.com/max/640/0*tP6lTP-lh2k_oZzP.png)

To learn more about OSQuery, you may refer to the [OSQuery Room](https://tryhackme.com/room/osqueryf8).

### Wazuh

Wazuh is an open-source, freely available, and extensive EDR solution, which Security Engineers can deploy in all scales of environments.

Wazuh operates on a management and agent model where a dedicated manager device is responsible for managing agents installed on the devices you’d like to monitor.

As mentioned, Wazuh is an EDR; let’s briefly run through what an EDR is. Endpoint detection and response (EDR) are tools and applications that monitor devices for an activity that could indicate a threat or security breach. These tools and applications have features that include:

-   Auditing a device for common vulnerabilities
-   Proactively monitoring a device for suspicious activity such as unauthorized logins, brute-force attacks, or privilege escalations.
-   Visualizing complex data and events into neat and trendy graphs
-   Recording a device’s normal operating behaviour to help with detecting anomalies

A sample view of how Wazuh works is shown below.

![](https://cdn-images-1.medium.com/max/640/0*cW0Jh6wzBcFmzrI7.gif)

To experience Wazuh in action, you may refer to the [Wazuh Room](https://tryhackme.com/room/wazuhct).

## Answer the questions below

Since the answers can be found above, I won’t share the actual answer below. Just where you can find them.

### Where do the Windows Event logs (.evtx files) typically reside?

The answer can be found in the _Windows Event Logs_ section. You will find an absolute path that ends with _\Logs_. Once you find the path, copy and paste it in the TryHackMe answer field, then click _Submit_.

![](https://cdn-images-1.medium.com/max/640/1*HlXKdJ9QETmIinTuyYYVIg.png)

  

### Provide the command used to enter OSQuery CLI.

Looking under the _OSQuery_ section, you will see a sentence that explains the command needed to start _OSQuery_ on the commandline. Once you find the command, copy and paste it into the TryHackMe answer field, then click _Submit_.

![](https://cdn-images-1.medium.com/max/640/1*JM6aSAZZUcFbYQC4KZXccA.png)

  

  

### What does EDR mean? Provide the answer in lowercase.

Looking at the _Wazuh_ section, you will see the acronymn _EDR_ several times. Look for _(EDR)_, when you find it the answer it to the left. Copy and paste the answer into the TryHackMe answer field, then click _Submit_.

![](https://cdn-images-1.medium.com/max/640/1*VbbD_i6i6NERkWZx3o9HxA.png)

  

----------

## Task 4 Endpoint Log Analysis

### Event Correlation

Event correlation identifies significant relationships from multiple log sources such as application logs, endpoint logs, and network logs.

Event correlation deals with identifying significant artefacts co-existing from different log sources and connecting each related artefact. For example, a network connection log may exist in various log sources such as Sysmon logs (Event ID 3: Network Connection) and Firewall Logs. The Firewall log may provide the source and destination IP, source and destination port, protocol, and the action taken. In contrast, Sysmon logs may give the process that invoked the network connection and the user running the process.

With this information, we can connect the dots of each artefact from the two data sources:

-   Source and Destination IP
-   Source and Destination Port
-   Action Taken
-   Protocol
-   Process name
-   User Account
-   Machine Name

Event correlation can build the puzzle pieces to complete the exact scenario from an investigation.

### Baselining

Baselining is the process of knowing what is expected to be normal. In terms of endpoint security monitoring, it requires a vast amount of data-gathering to establish the standard behaviour of user activities, network traffic across infrastructure, and processes running on all machines owned by the organization. Using the baseline as a reference, we can quickly determine the outliers that could threaten the organization.

Below is a sample list of baseline and unusual activities to show the importance of knowing what to expect in your network.

![](https://cdn-images-1.medium.com/max/640/1*L1YU8bj7i9xlZ2605JJG0g.png)

### Investigation Activity

We have tackled the foundations of endpoint security monitoring from previous tasks. Now, we will wear our Blue Team Hat and apply the concepts we discussed by investigating a suspicious activity detected on a workstation owned by one of your colleagues.

## Answer the questions below

### Click on the green View Site button in this task to open the Static Site Lab and start investigating the threat by following the provided instructions.

This is explained well enough above, here is a screenshot to help.

![](https://cdn-images-1.medium.com/max/640/1*Mkdwvrs-ilTJ2zrbUxehFw.png)

  

### Provide the flag for the simulated investigation activity.

The screen should be split in half now. We can start the investigation by clicking the _Start Investigation_ button that is in the _Warning!_ window.

![](https://cdn-images-1.medium.com/max/640/1*o4A_9rzXGIYFaJ-Ew4slxg.png)

We are now presented with a running Process List. But we first need to know what they system is suppose to run before we can identify the abnormal running process. To do this click on the _Baseline Document_ link.

![](https://cdn-images-1.medium.com/max/640/1*mWapg-yVYqY4qUyIoOnrpQ.png)

A window will pop up showing the normal processes that run on the system. Using this list, we can compare to see if any other processes are running on this system. When your done, click the _X_ in the top right corner of the window.

![](https://cdn-images-1.medium.com/max/640/1*hz_P-qdovPkCzt6Fgv1X_A.png)

Looking over the list of current running processes, we can see _beacon.exe_ wasn’t on the list from our _Baseline Processes_. This looks to be the _abnormal Process_, so click on the _beacon.exe_ process.

![](https://cdn-images-1.medium.com/max/640/1*E1kZ93ykPIqEOmulm_fSsA.png)

We are now presented with two new windows. The one on the left is showing our _Notes_ related to our investigation. The window on the right is the next step to our investigation. We have to identify the _Malicious Network Traffic_. We can see two processes named _svchost.exe_ running which look to be typical/normal network traffic. The final one is from the _beacon.exe_ process we named as being Malicious earlier. Now we have some more information about it. We can see the _Destination IP address_ and _Destination Port_. The _Destination Port_ being _4444_ is very suspicious, I believe we have found the _Malicious Network Traffic,_ click on _beacon.exe_ to select it for the investigation.

![](https://cdn-images-1.medium.com/max/640/1*4DcFE21fWrq75_Og4RmwKw.png)

We can now see that the _Malicious IP Address_ has been added to the _Notes_ window. Our next step is to see if any other systems on the Network have made connections with the _Malicious IP Address_. This can be done by copying and pasting the _Malicious IP Address_ into the _Search_ field of the new window on the right side of the desktop. Press Enter or click the _Magnifing Glass_ icon to search for the _Malicious IP Address_.

![](https://cdn-images-1.medium.com/max/640/1*aBhBwTwjwjs23WBYU6J1ow.png)

Four other systems were found to have connected with the _Malicious IP Address._ The next step we need to do is _Remediate_ the issue on said machines. To do this there is a button for each that says _Remediate_, click on each of these button.

![](https://cdn-images-1.medium.com/max/640/1*sODWHWz0hpMueVUa85fYbQ.png)

Once you have remediated the issue from the system. You have completed the task and investigation. We are now greated with the message that the _flag.txt_ file is now avaible on the desktop. Click anywhere on the desktop to remove the message.

![](https://cdn-images-1.medium.com/max/640/1*hBMAC8cGlT0w3p0skDZqGA.png)

Now we can click on _flag.txt_, to open the file and get the flag.

![](https://cdn-images-1.medium.com/max/640/1*zO0UNUrkiq8DPrU_q6xrOQ.png)

A window will pop up on the desktop, revealing the flag. Copy and paste the flag into the TryHackMe answer field, then click _Submit_.

![](https://cdn-images-1.medium.com/max/640/1*CsJ_c6XTPjVppPexIJr1lg.png)

**Answer: THM{3ndp01nt_s3cur1ty!}**

----------

## Task 5 Conclusion

Congratulations! You have completed the investigation task.

In the simulated threat investigation activity, we have learned the following:

-   Having a baseline document aids you in differentiating malicious events from benign ones.
-   Event correlation provides a deeper understanding of the concurrent events triggered by the malicious activity.
-   Taking note of each significant artefact is crucial in the investigation.
-   Other potentially affected assets should be inspected and remediated using the collected malicious artefacts.

In conclusion, we covered the basic concepts of Endpoint Security Monitoring:

-   **Endpoint Security Fundamentals** tackled Core Windows Processes and Sysinternals.
-   **Endpoint Logging and Monitoring** introduced logging functionalities such as Windows Event Logging and Sysmon and monitoring/investigation tools such as OSQuery and Wazuh.
-   **Endpoint Log Analysis** highlighted the importance of having a methodology such as baselining and event correlation.

You are now ready to deep-dive into the Endpoint Security Monitoring Module. To continue this path, you may refer to the list of rooms mentioned in the previous tasks:

-   [Core Windows Processes](https://tryhackme.com/room/btwindowsinternals)
-   [Sysinternals](https://tryhackme.com/room/btsysinternalssg)
-   [Windows Event Logs](https://tryhackme.com/room/windowseventlogs)
-   [Sysmon](https://tryhackme.com/room/sysmon)
-   [OSQuery](https://tryhackme.com/room/osqueryf8)
-   [Wazuh](https://tryhackme.com/room/wazuhct)

## 🎉🎉🎉Congrats!!! You completed the TryHackMe Intro to Endpoint Security Room, Awesome Job!!!🎉🎉🎉