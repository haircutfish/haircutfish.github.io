---
layout: "post"
title: "TryHackMe MISP — Task 4 Feeds & Taxonomies, Task 5 Scenario Event, & Task 6 Conclusion"
categories: MISP
tags: TryHackMe, MISP, SOC Level One Path
---



_If you haven’t done task 1, 2, & 3 yet, here is the link to my write-up it:_ [_Task 1 Room Overview, Task 2 MISP Introduction: Features & Terminologies, & Task 3 Using the System._](https://haircutfish.com/posts/MISP-Task1-Room-Overview-Task2-MISP-Introduction-Features-and-Terminologies-Task3-Using-The-System/)

## Getting to the MISP Dashboard

Head back to Task 3, at the top will be a green button labeled Start Machine. Click it.

![](https://miro.medium.com/max/385/1*SRFf4imrT1P1RSrjv0A_kg.png)

On your local machine, open the OpenVPN program. Once the program loads, click on the toggle button to connect to your TryHackMe OpenVPN profile.

![](https://miro.medium.com/max/451/1*LxxTKSfngcQKbuOwDKKUHg.png)

![](https://miro.medium.com/max/449/1*pshseLURU1IjxxOyAZ0big.png)

Head back to task 3, once the VM is done booting up and ready to go, in the top paragraph of the Task will be a link to click on. When you click on this link, it will open a new tab to the MISP log in page. Click this link.

![](https://miro.medium.com/max/630/1*NJQsAzM6L6nBpVzduNc5qw.png)

Now you will need a Username and Password, which you can copy (ctrl + c) and paste (ctrl + v) into the boxes on the MISP login page.

![](https://miro.medium.com/max/630/1*AWrop-eX1TzwRlVVtk2V1A.png)

Once you have paste the Username and Password into the login page fields, click the login button.

![](https://miro.medium.com/max/576/1*Vbo3P2zssMLN50ya1RTlCQ.png)

You are now in the MISP Dashboard and are ready to go!!!!

![](https://miro.medium.com/max/630/1*mswhhE2MNl7tIJ-2j4KEZg.png)

## Task 4 Feeds & Taxonomies

### Feeds

Feeds are resources that contain indicators that can be imported into MISP and provide attributed information about security events. These feeds provide analysts and organisations with continuously updated information on threats and adversaries and aid in their proactive defence against attacks.

MISP Feeds provide a way to:

-   Exchange threat information.
-   Preview events along with associated attributes and objects.
-   Select and import events to your instance.
-   Correlate attributes identified between events and feeds.

Feeds are enabled and managed by the  **Site Admin**  for the analysts to obtain information on events and indicators.

![](https://miro.medium.com/max/630/0*IyojZGSlXNyQjssS.gif)

### Taxonomies

A taxonomy is a means of classifying information based on standard features or attributes. On MISP, taxonomies are used to categorise events, indicators and threat actors based on tags that identify them.

![](https://miro.medium.com/max/630/0*o8L4Lgu7WTQ8VxOU.png)

Analysts can use taxonomies to:

-   Set events for further processing by external tools such as  [VirusTotal](https://virustotal.com/).
-   Ensure events are classified appropriately before the Organisation Admin publishes them.
-   Enrich intrusion detection systems’ export values with tags that fit specific deployments.

Taxonomies are expressed in machine tags, which comprise three vital parts:

-   **Namespace:**  Defines the tag’s property to be used.
-   **Predicate:**  Specifies the property attached to the data.
-   **Value:**  Numerical or text details to map the property.

(Source: MISP)

Taxonomies are listed under the  _Event Actions_  tab. The site admin can enable relevant taxonomies.

![](https://miro.medium.com/max/630/0*U8FOkAy-RqvdBY3Y.gif)

### Tagging

Information from feeds and taxonomies, tags can be placed on events and attributes to identify them based on the indicators or threats identified correctly. Tagging allows for effective sharing of threat information between users, communities and other organisations using MISP to identify various threats.

In our CobaltStrike event example, we can add tags by clicking on the buttons in the  **Tags**  section and searching from the available options appropriate to the case. The buttons represent  _global_  tags and  _local_  tags, respectively. It is also important to note that you can add your unique tags to your MISP instance as an analyst or organisation that would allow you to ingest, navigate through and share information quickly within the organisation.

![](https://miro.medium.com/max/630/0*5IPJNviH5li34-1I.gif)

### Tagging Best Practices

Tagging at Event level vs Attribute Level

Tags can be added to an event and attributes. Tags are also inheritable when set. It is recommended to set tags on the entire event and only include tags on attributes when they are an exception from what the event indicates. This will provide a more fine-grained analysis.

The minimal subset of Tags

The following tags can be considered a must-have to provide a well-defined event for distribution:

-   [**Traffic Light Protocol:**](https://www.first.org/tlp/)  Provides a colour schema to guide how intelligence can be shared.
-   **Confidence:**  Provides an indication as to whether or not the data being shared is of high quality and has been vetted so that it can be trusted to be good for immediate usage.
-   **Origin:**  Describes the source of information and whether it was from automation or manual investigation.
-   **Permissible Actions Protocol:**  An advanced classification that indicates how the data can be used to search for compromises within the organisation.

## Task 5 Scenario Event

[CIRCL](https://www.circl.lu/)  (Computer Incident Respons Center Luxembourg) published an event associated with PupyRAT infection. Your organisation is on alert for remote access trojans and malware in the wild, and you have been tasked to investigate this event and correlate the details with your SIEM. Use what you have learned from the room to identify the event and complete this task.

## Answer the questions below

### What event ID has been assigned to the PupyRAT event?

On the Event list page is a filter bar, on the right side above the Event list. Type in the field PupyRat, and click Filter.

![](https://miro.medium.com/max/362/1*Kv88rx_RvahbwO1_atLa_Q.png)

When the page loads, the answer will be the first column at the top labeled Event ID. Once you find it, highlight copy (ctrl + c) and paste (ctrl + v) or type, the answer in the TryHackMe answer field.

![](https://miro.medium.com/max/630/1*Za6xsZ8H1TQ_OmJp8nVPgQ.png)

**Answer: 1146**

### The event is associated with the adversary gaining ______ into organisations.

From the way that the question is worded, it looks like we are looking for a type of access into an organization. Go back to the PupyRAT MISP page again, this time we are going to look at the tags. When we look at the tags, we see several that say about a type of access. Once you figure it out, highlight copy (ctrl + c) and paste (ctrl + v) or type, the answer in the TryHackMe answer field.

![](https://miro.medium.com/max/630/1*GkyuS5D4b_X8xqsyNxAHZw.png)

**Answer: Remote Access**

### What IP address has been mapped as the PupyRAT C2 Server

For this we can’t find it in the tag’s at the top, so we need to look into the information below. So let’s narrow down those search results by using the find (ctrl + f) feature of the browser. First type in C2, we get five results, look through them.

![](https://miro.medium.com/max/454/1*-v5PejtQHIeNLaQG2CqE9w.png)

Nothing good, let’s think about what C2 stands for, command and control server. So let’s just try command, we get one result, looking at it, it is the result we are looking for.

![](https://miro.medium.com/max/435/1*1flK38WYYOI7RvZ7ruj3PQ.png)

Look to the left in this row, you will see an IP address, this is the IP address associated with the PupyRat C2 server and thus the answer to the question. Highlight copy (ctrl + c) and paste (ctrl + v) or type, the answer in the TryHackMe answer field.

![](https://miro.medium.com/max/630/1*TvJQRyC3fJBXqYw5OTcbiA.png)

**Answer: 89.107.62.39**

### From the Intrusion Set Galaxy, what attack group is known to use this form of attack?

Go back to the PupyRAT MISP page again, and again we can find the answer in the tag section. If you look at the first tag it mentions galaxy and intrusion set, so if you look at the end of it you will find the answer. Once you find it, highlight copy (ctrl + c) and paste (ctrl + v) or type, the answer in the TryHackMe answer field.

![](https://miro.medium.com/max/630/1*9Adkni8IJUI6cmZmIQNfEA.png)

**Answer: Magic Hound**

### There is a taxonomy tag set with a Certainty level of 50. Which one is it?

Go back to the PupyRAT MISP page for the final time, and also look at the tags for the final time. Look for the blue tag on the bottom line, it will say certainty = “50”, the first word or acronym is the answer to this question. Once you find it, highlight copy (ctrl + c) and paste (ctrl + v) or type, the answer in the TryHackMe answer field.

![](https://miro.medium.com/max/630/1*wz-Mz6mhxK56e6Xyon8cog.png)

**Answer: OSINT**

### Task 6 Conclusion

### Recap

Hopefully, you learned a lot about MISP and its use in sharing malware and threat information in this room. This tool is useful in the real world regarding incident reporting. You should be able to use the knowledge gained to effectively document, report and share incident information.

### Additional Resources

There is plenty of information and capabilities that were not covered in this room. This leaves plenty of room for research and learning more about MISP. To guide you towards that, look at the following attached links and feel free to come back to the room to practice.

-   [MISP Book](https://www.circl.lu/doc/misp/)
-   [MISP GitHub](https://github.com/MISP/)
-   [CIRCL MISP Training Module 1](https://www.youtube.com/watch?v=aM7czPsQyaI)
-   [CIRCL MISP Training Module 2](https://www.youtube.com/watch?v=Jqp8CVHtNVk)

We wish to give credit to  [CIRCL](https://www.circl.lu/services/misp-malware-information-sharing-platform/)  for providing guidelines that supported this room.

🎉🎉🎉CONGRATS!!!! You completed the MISP room!!!🎉🎉🎉