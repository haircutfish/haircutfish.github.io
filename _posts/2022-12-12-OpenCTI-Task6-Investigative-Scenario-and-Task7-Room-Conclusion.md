---
layout: "post"
title: "TryHackMe OpenCTI — Task 6 Investigative Scenario & Task 7 Room Conclusion"
categories: OpenCTI
tags: TryHackMe, OpenCTI, SOC Level One Path
---

_If you haven’t done task 1 thru 5 yet, here is the link to my write-up it: Task1 thru Task 5_

### Getting to the OpenCTI Dashboard

Let’s get to the OpenCTI Dashboard, to do this first we need to click the green Start Machine button at the top of the Task 4, to get the VM up and running.

![](https://miro.medium.com/max/228/0*-cugG7KKFFFUCMGy.png)

Then go to the top of the Webpage and click the blue Start AttackBox icon, the screen will split and take about a minute and a half for the VM to load.

![](https://miro.medium.com/max/311/0*7PMfKgewueTVcdKH.png)

At the bottom of the VM is two arrows pointing in the oppiosite directions, this is the full screen icon. Click on it.

![](https://miro.medium.com/max/229/0*u6bhd1nIvjTCo0el.png)

A new tab will open with the VM in it, while it loads go back to the TryHackMe tab. Go back to the bar at the bottom of the VM and click the — button to exit splitscreen.

![](https://miro.medium.com/max/229/0*ph_RTwgom254ijXe.png)

There is a terminal on the screen, if you have read through this, press enter to close it.

![](https://miro.medium.com/max/567/0*AY97n0zaStveR9QG.png)

On the right side of the VM is a quick panel, at the top of this panel is Firefox. Click on the firefox icon.

![](https://miro.medium.com/max/87/0*kgmn4dl9aANHbzVS.png)

While Firefox loads, go back to the TryHackMe Task. In the first paragraph you will see a link that will take you to the OpenCTI login page. Highlight and copy (ctrl + c) the link.

![](https://miro.medium.com/max/270/0*dDsLUjShieykmHcF.png)

Go back to the VM tab, click on the URL bar. Paste (ctrl + v) the OpenCTI address into the bar and press enter.

![](https://miro.medium.com/max/552/0*UbJU6GkfYMwvVHH6.png)

The site will load the login page for OpenCTI. The login credentials are back on the TryHackMe Task, you can either highlight copy (ctrl + c) and paste (ctrl + v) or type, the credentials into the login page. Then click the blue Sign In button.

![](https://miro.medium.com/max/270/0*XLDKtgSbmW8mItMk.png)

![](https://miro.medium.com/max/336/0*jjkVu65gcVxiDao2.png)

You will have a small pop-up to save you password into firefox, just click Don’t Save.

![](https://miro.medium.com/max/350/0*mw3cMEHRmq5USvXS.png)

You are now in the OpenCTI dashboard and ready to proceed!!!

## Task 6 Investigative Scenario

As a SOC analyst, you have been tasked with investigations on malware and APT groups rampaging through the world. Your assignment is to look into the  **CaddyWiper**  malware and  **APT37**  group. Gather information from OpenCTI to answer the following questions.

## Answer the questions below

### What is the earliest date recorded related to CaddyWiper? Format: YYYY/MM/DD

So we know from above that CaddyWiper is Malware, and we learned from Task 4 that on the OpenCTI Dashboard we can find Malware under the Arsenal tab.

![](https://miro.medium.com/max/630/1*HTEVnf0MSMlINLT0deTTJw.png)

Going over to the OpenCTI Dashboard in the VM, we see the different tabs on the left side of the screen. Go to Arsenal, and click on it.

![](https://miro.medium.com/max/162/1*hhxlZwLEtdZyEEh5gYBo2A.png)

The Malware tab is already selected, after you have clicked on the Arsenal tab. So at the top, will be a search bar, type Caddywiper into the search bar and press enter.

![](https://miro.medium.com/max/630/1*HQ7ixDidIYs7ltIPfY3mjA.png)

You will have one result, click on the result.

![](https://miro.medium.com/max/590/1*yA0Fr1j19o-ed0z5HGTT8A.png)

You will now be at the Overview page of the CaddyWiper Malware, scroll down till you reach the Latest reports about this entity.

![](https://miro.medium.com/max/630/1*Mp6UmrbEHQEI0q6_wQh8GA.png)

Once you are down on the Latest Reports about this entity panel, the bottom entry is the one we are looking for. You can see part of the date on it. Click this entry.

![](https://miro.medium.com/max/496/1*1fFUQdrV8to37NuIlVj7aA.png)

On this page you will see two panels, the one you are looking for is the Entity details panels. Inside this panel, look at the Description, you will find the earliest date here. Once you find it, type it into the TryHackMe answer field and click submit.

![](https://miro.medium.com/max/630/1*ev8r15_9RdlCfkyXDr1FJg.png)

**Answer: 2022/03/15**

### Which Attack technique is used by the malware for execution?

Go back to the top panel, and click on the Knowledge Tab.

![](https://miro.medium.com/max/630/1*jcQebd6W105SUsElP5yD-Q.png)

When the Knowledge panel loads, a new panel will load on the right side of the screen. On this panel, click the Attack patterns.

![](https://miro.medium.com/max/186/1*B4hzg1pWnKxLx2kyZkWoUQ.png)

The question ask for the Attack technique during the execution phase, so scroll over to till you see the Execution column.

![](https://miro.medium.com/max/630/1*wp6vuPYozHYo2fYQPBFc_w.png)

Once you reach the Execution column, you will see one of the technique boxes is red, this indicate that it is used in the Caddywiper malware. So the answer is what is written in the red box. Once you find it, type it into the TryHackMe answer field and click submit.

![](https://miro.medium.com/max/138/1*ktxHfSnlu3DdvjwZZvTofw.png)

**Answer: Native API**

### How many malware relations are linked to this Attack technique?

Going back to the Execution technique section, click on answer to the previous question.

![](https://miro.medium.com/max/138/1*fWEdaixpMeHzhli4GiCj0Q.png)

When the page loads for this execution technique, click the Knowledge tab at the top of the page.

![](https://miro.medium.com/max/630/1*9rWX0_rp_5i1lPGSON2OcA.png)

On the Knowledge page, you will find the answer. You will see three panels at the top of the center of the page, under them is two panels, looking at these two panels look at the one on the right. It is labeled Distribution of Relations, and one of the categories is Malware. Inside that box is a number, that number is the answer to the question. Once you find it, type it into the TryHackMe answer field and click submit.

![](https://miro.medium.com/max/630/1*L9XB9INPNcdg-khGvvvg0A.png)

**Answer: 113**

### Which 3 tools were used by the Attack Technique in 2016? (Ans: Tool1, Tool2, Tool3)

Staying in the Knowledge tab of this technique, look to the right and you will see a panel with different tabs, one of the tabs is labeled Tools. Click on it.

![](https://miro.medium.com/max/184/1*3zzjqYZJyqCmXWMbOk1CLg.png)

Awesome, we have the tools, but we have both 2019 and 2016 mixed in. So to help organize it better, click on the Start time, this will Put the 2019 at the top and the three from 2016 at the bottom.

![](https://miro.medium.com/max/630/1*lqTjoxAlKnZ8uzhpnFzOcg.png)

Better organized, now we can type them into the TryHackMe answer field. Start from the top of the list and work your way down with a comma and space in between. Then click submit.

![](https://miro.medium.com/max/630/1*lKYOfMH3fQGklRNjqlHXIw.png)

**Answer: ShimRatReporter, Empire, Bloodhound**

### What country is APT37 associated with?

So we learned we can find where APT group’s are back in Task 4, so let’s put that knowledge to us.

![](https://miro.medium.com/max/630/1*91J8yRQ2-cApZoIHLsH7lQ.png)

Going back to OpenCTI, look to the panel on the left side of the screen. This time, click on the Threats tab.

![](https://miro.medium.com/max/164/1*3LBPyWjm676LRIKEJRnhuQ.png)

After you have clicked on the Threats tab, look to the top of the screen, you should see an Intrusion Sets tab, click on it.

![](https://miro.medium.com/max/362/1*hZpup0jBQE-wtHkWOppR2w.png)

We are ready to search for the APT37 group, so at the top of the center panel is a search bar. Click in it and type APT37, and press enter to search it.

![](https://miro.medium.com/max/630/1*xwwea6BZGFV5_GyU5ajA2A.png)

You will have two results, click on the first one labeled APT37.

![](https://miro.medium.com/max/630/1*HIomLShLmnk0BVExfWaIoA.png)

When the page loads, you will have two panels. Look to the panel on the right labeled Details, the answer can be found under the description within the first sentence. Once you find it, type it into the TryHackMe answer field and click submit.

![](https://miro.medium.com/max/630/1*tyTpG16HpwdbP8kbTX4gvA.png)

**Answer: North Korean**

### Which Attack techniques are used by the group for initial access? (Ans: Technique1, Technique2)

The question doesn’t say it, but it is looking for the technique ID, after learning this it made it a little easier to find the answer.

Staying on the APT37, look to the top of the page and click on the Knowledge tab.

![](https://miro.medium.com/max/630/1*mZmSh08ephd7vx4ZpeMQVg.png)

In the knowledge tab, you will see two large panels. Under these panels on the left are two tabs, click on the Global Kill Chain tab.

![](https://miro.medium.com/max/630/1*daNwj1todisaanDPuuM8ug.png)

Scroll down till you reach the Initial Access, once you reach this section you will see the answer. TryHackMe has the order start at the bottom then the top, so type the answers into the answer field that way then click submit.

![](https://miro.medium.com/max/630/1*iw5Wk0bRUC4NKycogjPwKA.png)

**Answer: T1189, T1566**

## Task 7 Room Conclusion

Fantastic work on going through and completing the OpenCTI room.

In this room, we looked at the use of the OpenCTI platform when it comes to processing threat intel and assisting analysts in investigating incidents. Check out the documentation linked within the room to get more information about OpenCTI and the different tools and frameworks used.

🎉🎉🎉CONGRATS!!! You completed the OpenCTI room!!!🎉🎉🎉