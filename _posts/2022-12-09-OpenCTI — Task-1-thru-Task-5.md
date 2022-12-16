---
layout: "post"
title: "TryHackMe OpenCTI — Task 1 thru Task 5"
---


# TryHackMe OpenCTI — Task 1 thru Task 5

Provide an understanding of the OpenCTI Project

# Task 1 Room Overview

This room will cover the concepts and usage of OpenCTI, an open-source threat intelligence platform. The room will help you understand and answer the following questions:

-   What is OpenCTI and how is it used?
-   How would I navigate through the platform?
-   What functionalities will be important during a security threat analysis?

Prior to going through this room, we recommend checking out these rooms as prerequisites:

-   [MITRE ATT&CK Framework](https://tryhackme.com/room/mitre)
-   [TheHive](https://tryhackme.com/room/thehiveproject)
-   [MISP](https://tryhackme.com/room/misp)
-   [Threat Intelligence Tools](http://tryhackme.com/room/threatinteltools)

![](https://miro.medium.com/max/788/0*jJYrN_PJeHO-dkDp.png)

# Task 2 Introduction to OpenCTI

Cyber Threat Intelligence is typically a managerial mystery to handle, with organisations battling with how to input, digest, analyse and present threat data in a way that will make sense. From the rooms that have been linked on the overview, it is clear that there are numerous platforms that have been developed to tackle the juggernaut that is Threat Intelligence.

# OpenCTI

[OpenCTI](https://www.opencti.io/)  is another open-sourced platform designed to provide organisations with the means to manage CTI through the storage, analysis, visualisation and presentation of threat campaigns, malware and IOCs.

# Objective

Developed by the collaboration of the  [French National cybersecurity agency (ANSSI)](https://www.ssi.gouv.fr/), the platform’s main objective is to create a comprehensive tool that allows users to capitalise on technical and non-technical information while developing relationships between each piece of information and its primary source. The platform can use the  [MITRE ATT&CK framework](https://tryhackme.com/room/mitre)  to structure the data. Additionally, it can be integrated with other threat intel tools such as MISP and TheHive. Rooms to these tools have been linked in the overview.

![](https://miro.medium.com/max/788/0*USa8ifSW8yepovbA.png)

# Task 3 OpenCTI Data Model

## OpenCTI Data Model

OpenCTI uses a variety of knowledge schemas in structuring data, the main one being the Structured Threat Information Expression ([STIX2](https://oasis-open.github.io/cti-documentation/stix/intro)) standards. STIX is a serialised and standardised language format used in threat intelligence exchange. It allows for the data to be implemented as entities and relationships, effectively tracing the origin of the provided information.

This data model is supported by how the platform’s architecture has been laid out. The image below gives an architectural structure for your know-how.

![](https://miro.medium.com/max/788/0*H_xtsQ85B5XUiLyl.png)

Source:  [OpenCTI Public Knowledge Base](https://luatix.notion.site/OpenCTI-Public-Knowledge-Base-d411e5e477734c59887dad3649f20518)

The highlight services include:

-   **GraphQL API:**  The API connects clients to the database and the messaging system.
-   **Write workers:**  Python processes utilised to write queries asynchronously from the RabbitMQ messaging system.
-   **Connectors:** Another set of python processes used to ingest, enrich or export data on the platform. These connectors provide the application with a robust network of integrated systems and frameworks to create threat intelligence relations and allow users to improve their defence tactics.

According to OpenCTI, connectors fall under the following classes:

![](https://miro.medium.com/max/788/1*sGPK75EWIA5_D_o5gfplJQ.png)

Refer to the  [connectors](https://github.com/OpenCTI-Platform/connectors)  and  [data model](https://luatix.notion.site/Data-model-4427344d93a74fe194d5a52ce4a41a8d)  documentation for more details on configuring connectors and the data schema.

# Task 4 OpenCTI Dashboard 1

Follow along with the task by launching the attached machine and using the credentials provided; log in to the OpenCTI Dashboard via the AttackBox on  `[http://MACHINE_IP:8080/](http://machine_ip:8080/)`. Give the machine 5 minutes to start up and it is advisable to use the AttackBox on fullscreen.

Username:  **info@tryhack.io**

Password:  **TryHackMe1234**

## Getting OpenCTI Started

So before we go further let’s get to the OpenCTI Dashboard, to do this first we need to click the green Start Machine button at the top of the task, to get the VM up and running.

![](https://miro.medium.com/max/316/1*vcFTmUxX4kPoThvH359JXQ.png)

Then go to the top of the Webpage and click the blue Start AttackBox icon, the screen will split and take about a minute and a half for the VM to load.

![](https://miro.medium.com/max/432/1*9ldix9Aa9f_3hhVcTEhU1w.png)

At the bottom of the VM is two arrows pointing in the oppiosite directions, this is the full screen icon. Click on it.

![](https://miro.medium.com/max/318/1*LXrW6HRdyFYbSQECKWjSRw.png)

A new tab will open with the VM in it, while it loads go back to the TryHackMe tab. Go back to the bar at the bottom of the VM and click the — button to exit splitscreen.

![](https://miro.medium.com/max/318/1*HyTroEkHHedMSwBi1N-k2A.png)

There is a terminal on the screen, if you have read through this, press enter to close it.

![](https://miro.medium.com/max/788/1*YuakmP8Om-Ayl2zpc4S4CA.png)

On the right side of the VM is a quick panel, at the top of this panel is Firefox. Click on the firefox icon.

![](https://miro.medium.com/max/122/1*mNs00GbHY8U672AbZM-KwA.png)

While Firefox loads, go back to the TryHackMe Task. In the first paragraph you will see a link that will take you to the OpenCTI login page. Highlight and copy (ctrl + c) the link.

![](https://miro.medium.com/max/375/1*XabYxHRqLhW2C5SMV7-QFg.png)

Go back to the VM tab, click on the URL bar. Paste (ctrl + v) the OpenCTI address into the bar and press enter.

![](https://miro.medium.com/max/766/1*WvmNZ0s3ZuWbgQDlQ201GA.png)

The site will load the login page for OpenCTI. The login credentials are back on the TryHackMe Task, you can either highlight copy (ctrl + c) and paste (ctrl + v) or type, the credentials into the login page. Then click the blue Sign In button.

![](https://miro.medium.com/max/375/1*Eoy7VD36ZLM7Rg39qnsqRQ.png)

![](https://miro.medium.com/max/467/1*m040KSleWlKeTRKXl453fQ.png)

You will have a small pop-up to save you password into firefox, just click Don’t Save.

![](https://miro.medium.com/max/486/1*Gq538jQzPuL0gFsvUg8x7Q.png)

You are now in the OpenCTI dashboard and ready to proceed!!!

![](https://miro.medium.com/max/788/1*FvObFzEqhsn3hc_UrsVSMQ.png)

## OpenCTI Dashboard

Once connected to the platform, the opening dashboard showcases various visual widgets summarising the threat data ingested into OpenCTI. Widgets on the dashboard showcase the current state of entities ingested on the platform via the total number of entities, relationships, reports and observables ingested, and changes to these properties noted within 24 hours.

See Image.

![](https://miro.medium.com/max/788/0*JYS27FRhpO7HsM54.gif)

## Activities & Knowledge

The OpenCTI categorises and presents entities under the  **Activities and Knowledge**  groups on the left-side panel. The activities section covers security incidents ingested onto the platform in the form of reports. It makes it easy for analysts to investigate these incidents. In contrast, the Knowledge section provides linked data related to the tools adversaries use, targeted victims and the type of threat actors and campaigns used.

## Analysis

The Analysis tab contains the input entities in reports analysed and associated external references. Reports are central to OpenCTI as knowledge on threats and events are extracted and processed. They allow for easier identification of the source of information by analysts. Additionally, analysts can add their investigation notes and other external resources for knowledge enrichment. As displayed below, we can look at the  **Triton**  Software report published by MITRE ATT&CK and observe or add to the details provided.

See Image.

![](https://miro.medium.com/max/788/0*zzQWWEs-CeeD_h1w.gif)

## Events

Security analysts investigate and hunt for events involving suspicious and malicious activities across their organisational network. Within the Events tab, analysts can record their findings and enrich their threat intel by creating associations for their incidents.

See Image.

![](https://miro.medium.com/max/788/0*ytm0sKJqSfVm3zvB.gif)

## Observations

Technical elements, detection rules and artefacts identified during a cyber attack are listed under this tab: one or several identifiable makeup indicators. These elements assist analysts in mapping out threat events during a hunt and perform correlations between what they observe in their environments against the intel feeds.

See Image.

![](https://miro.medium.com/max/788/0*__4vm07z135WBNT3.gif)

## Threats

All information classified as threatening to an organisation or information would be classified under threats. These will include:

-   **Threat Actors:**  An individual or group of attackers seeking to propagate malicious actions against a target.
-   **Intrusion Sets:**  An array of TTPs, tools, malware and infrastructure used by a threat actor against targets who share some attributes. APTs and threat groups are listed under this category on the platform due to their known pattern of actions.
-   **Campaigns:**  Series of attacks taking place within a given period and against specific victims initiated by advanced persistent threat actors who employ various TTPs. Campaigns usually have specified objectives and are orchestrated by threat actors from a nation state, crime syndicate or other disreputable organisation.

See Image.

![](https://miro.medium.com/max/788/0*D-1noJaxYVCimuzv.png)

## Arsenal

This tab lists all items related to an attack and any legitimate tools identified from the entities.

-   **Malware:**  Known and active malware and trojan are listed with details of their identification and mapping based on the knowledge ingested into the platform. In our example, we analyse the  **4H RAT**  malware and we can extract information and associations made about the malware.
-   **Attack Patterns:**  Adversaries implement and use different TTPs to target, compromise, and achieve their objectives. Here, we can look at the details of the  **Command-Line Interface and make decisions based on the relationships established on the platform and navigate through an investigation associated with the technique.**
-   **Courses of Action:**  MITRE maps out concepts and technologies that can be used to prevent an attack technique from being employed successfully. These are represented as Courses of Action (CoA) against the TTPs.
-   **Tools:**  Lists all legitimate tools and services developed for network maintenance, monitoring and management. Adversaries may also use these tools to achieve their objectives. For example, for the Command-Line Interface attack pattern, it is possible to narrow down that  **CMD**  would be used as an execution tool. As an analyst, one can investigate reports and instances associated with the use of the tool.
-   **Vulnerabilities:**  Known software bugs, system weaknesses and exposures are listed to provide enrichment for what attackers may use to exploit and gain access to systems. The Common Vulnerabilities and Exposures (CVE) list maintained by MITRE is used and imported via a connector.

See Image.

![](https://miro.medium.com/max/788/0*UytTOTnyWVUFJSpg.gif)

## Entities

This tab categorises all entities based on operational sectors, countries, organisations and individuals. This information allows for knowledge enrichment on attacks, organisations or intrusion sets.

See Image.

![](https://miro.medium.com/max/788/0*HsS2okaXb2fguxOD.gif)

## Answer the questions below

### What is the name of the group that uses the  **4H RAT**  malware?

So we learned from the Arsenal section above that we can find out about Malware on the Arsenal tab. So head over to the OpenCTI dashboard.

![](https://miro.medium.com/max/788/1*4tR7oEGNQpWUdbuq8XtBSw.png)

Once on the OpenCTI dashboard, look to the panel on the left. You will see Arsenal in grey close to the bottom, click on it. This will open the Malware section in the main part of the window on the right.

![](https://miro.medium.com/max/190/1*qnTl4rR__3N4FCkkxkkqbQ.png)

You could use the search bar to look for the 4H RAT malware but, because it is in alphebetical order you can find it right at the top. Click on the 4H RAT box.

![](https://miro.medium.com/max/788/1*go0BWgyYALjzSj5pPhmDUw.png)

You will see two panels in the middle of the screen, the panel on the right is the Details panel and the one you want to focus on. If you read the description you will find the answer. Once you find it, highlight copy (ctrl + c) and paste (ctrl + v) or type, the answer into the TryHackMe answer field and click submit.

![](https://miro.medium.com/max/788/1*a8QYwtn4BY2cu-9tGEqsDQ.png)

**Answer: Putter Panda**

### What kill-chain execution phase is linked with the  **Command-Line Interface**  Attack Pattern?

Go back to the panel on the left, click on Arsenal again.

![](https://miro.medium.com/max/190/1*qnTl4rR__3N4FCkkxkkqbQ.png)

Above the center panels you will see this tab panel, click on Attack patterns.

![](https://miro.medium.com/max/741/1*h4AcO4JUpJSqmwko1TiSWQ.png)

At the top of the Attack pattern panel is a search bar, type Command-Line Interface, into the search bar and press enter to search it.

![](https://miro.medium.com/max/758/1*fQ6OrB1jXyQYgsC_r_mC7w.png)

Your top result will be what you are looking for, click on it.

![](https://miro.medium.com/max/788/1*AzWTflUFlX7MuXU_dFeVBw.png)

Again you will have two panels in the middle of the screen, and again we will be focusing on the Details panel. This time though, on the right side of the panel you should see Kill Chain Phase, right underneath it is the answer. Once you find it, highlight copy (ctrl + c) and paste (ctrl + v) or type, the answer into the TryHackMe answer field and click submit.

![](https://miro.medium.com/max/788/1*zj4slqml7zrPg4WctNDJ2w.png)

**Answer: execution-ics**

### Within the Activities category, which tab would house the  **Indicators**?

This answer can be found above, in these section it mentions that under this tab can be found one or several indicators. Once you find it, highlight copy (ctrl + c) and paste (ctrl + v) or type, the answer into the TryHackMe answer field and click submit.

![](https://miro.medium.com/max/788/1*V8rAp7GstqFbqzoguAVUyQ.png)

On OpenCTI this is where you can find it.

![](https://miro.medium.com/max/774/1*myF0-ro2AY0FZv3QqVZ3OA.png)

**Answer: Observations**

# Task 5 OpenCTI Dashboard 2

## General Tabs Navigation

The day-to-day usage of OpenCTI would involve navigating through different entities within the platform to understand and utilise the information for any threat analysis. We will be looking at the  **Cobalt Strike**  malware entity for our walkthrough, mainly found under the Arsenal tab we’ve covered previously. When you select an intelligence entity, the details are presented to the user through:

-   **Overview Tab:**  Provides the general information about an entity being analysed and investigated. In our case, the dashboard will present you with the entity ID, confidence level, description, relations created based on threats, intrusion sets and attack patterns, reports mentioning the entity and any external references.

See Image.

![](https://miro.medium.com/max/788/0*R_ML85dH_KUx6rE0.png)

-   **Knowledge Tab:**  Presents linked information associated with the entity selected. This tab will include the reports associated, indicators, relations and attack pattern timeline of the entity. Additionally, an analyst can view fine-tuned details from the tabs on the right-hand pane, where information about the threats, attack vectors, events and observables used within the entity are presented.

See Image.

![](https://miro.medium.com/max/788/0*fh7w91eXhhHDbN8d.gif)

-   **Analysis Tab**: Provides the reports where the identified entry has been seen. The analysis provides usable information about a threat and guides investigation tasks.

See Image.

![](https://miro.medium.com/max/788/0*S8AR-qSN0-W3Xmdu.png)

-   **Indicators Tab**: Provides information on IOC identified for all the threats and entities.
-   **Data Tab:**  Contains the files uploaded or generated for export that are related to the entity. These assist in communicating information about threats being investigated in either technical or non-technical formats.
-   **History Tab:**  Changes made to the element, attributes, and relations are tracked by the platform worker and this tab will outline the changes.

## Answer the questions below

### What Intrusion sets are associated with the Cobalt Strike malware with a Good confidence level? (Intrusion1, Intrusion2)

Once on the OpenCTI dashboard, look to the panel on the left. You will see Arsenal in grey close to the bottom, click on it. This will open the Malware section in the main part of the window on the right.

![](https://miro.medium.com/max/190/1*qnTl4rR__3N4FCkkxkkqbQ.png)

Using the search bar type Cobalt Strike into it and press enter.

![](https://miro.medium.com/max/737/1*0uIbX9fFZW70u9lAGZcX8w.png)

Your first result will be Cobalt Strike, click on it.

![](https://miro.medium.com/max/788/1*Jiv1OOpr9uwEG3QL0Ef1qw.png)

From here we are going to click on the Knowledge tab at the top panel.

![](https://miro.medium.com/max/788/1*pVMi5BxhAhjKFYfRFtvfWg.png)

When the Knowledge panel loads in the middle of the screen you will see another panel on the right-side of the page now. Go to that new panel and click on the diamond icon that says Intrusion sets.

![](https://miro.medium.com/max/233/1*rcv47Lty5ioRR7prPbOf1g.png)

When the Intrusion sets panel loads, the first entry gives us the first half of the answer. Now just scroll down till you see the next Intrusion set with a confidencence score of Good, when you find it that is the second half of the answer. Once you find it, type the answer into the TryHackMe answer field and click submit.

![](https://miro.medium.com/max/788/1*DvCQO8k0oot3uwSqM8CFkw.png)

**Answer: CopyKittens, FIN7**

### Who is the author of the entity?

Go back to the top panel and click on the Overview tab.

![](https://miro.medium.com/max/788/1*wvSyoK_FJyCFIAjOwa4asQ.png)

This time instead of looking at the Details panel on the right, we are going to look at the Basic Information panel on the left. Above the Distribution of Opinions is the Author. Once you find it, type the answer into the TryHackMe answer field and click submit.

![](https://miro.medium.com/max/788/1*9-2A_GDquoBzBVwxoaxnbg.png)

**Answer: The MITRE Corporation**
