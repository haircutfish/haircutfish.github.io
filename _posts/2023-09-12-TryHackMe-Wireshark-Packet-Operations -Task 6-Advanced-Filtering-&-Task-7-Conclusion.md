---
layout: "post"
title: "TryHackMe Wireshark: Packet Operations — Task 6 Advanced Filtering & Task 7 Conclusion"
categories: Wireshark
tags: TryHackMe, Wireshark, SOC Level One Path
---


_If you haven’t done tasks 3, 4, and 5 yet, here is the link to my write-up of them:_ [_Task 3 Statistics-Protocol Details, Task 4 Packet Filtering-Principles, & Task 5 Packet Filtering-Protocol Filters_](https://haircutfish.com/posts/Wireshark-Packet-Operations-Task-3-Statistics-Protocol-Details-Task-4-Packet-Filtering-Principles-&-Task-5-Packet-Filtering-Protocol-Filters/)

## Getting the VM Started

Starting at Task 1, you will see the green _Start Machine_ button. Click this button to get the VM Started.

![](https://cdn-images-1.medium.com/max/640/0*7acxkEjuiY-ALWD-.png)

Scroll to the top where the banner is. On the right side of the page, you will see the blue _Show Split view_. Click this blue button.

![](https://cdn-images-1.medium.com/max/640/0*aLYeGIGR8pW0Jf2q.png)

The page will split, now just wait till the VM loads.

![](https://cdn-images-1.medium.com/max/640/0*c35IqeAeJm248FsJ.png)

Once the VM loads, click the _View in Full Screen_ icon in the bottom left of the VM.

![](https://cdn-images-1.medium.com/max/640/0*LzsFbqtu81Rtzvbe.png)

A new browser tab should open with the VM in it.

![](https://cdn-images-1.medium.com/max/640/0*-HhTub30aqM4HmCG.png)

Right-click on _Exercise.pcapng_, then on the drop-down menu click the _Open With Wireshark_.

![](https://cdn-images-1.medium.com/max/640/0*19aZrRwxv-dd-Tpy.png)

While Wireshark loads, head back to the THM Task Tab. At the bottom of the VM you will see a minus ( — ), this represents _Exit Split View_. Click the — to allow the THM task to incapsilate the entire window. This won’t close out of your VM instance, it will just be on the other tab.

![](https://cdn-images-1.medium.com/max/640/0*yTBSf5jE1zWyh-Zd.png)

Now head back to the broswer tab that the VM instance is in. Wireshark should be open and ready to use.

![](https://cdn-images-1.medium.com/max/640/0*D7h6IhqtfDdX2A_i.png)

----------

## Task 6 Advanced Filtering

So far, you have learned the basics of packet filtering operations. Now it is time to focus on specific packet details for the event of interest. Besides the operators and expressions covered in the previous room, Wireshark has advanced operators and functions. These advanced filtering options help the analyst conduct an in-depth analysis of an event of interest.

### **Filter: “contains”**

![](https://cdn-images-1.medium.com/max/640/1*GuTIkLyTZOeNGIZfUD88Hg.png)

![](https://cdn-images-1.medium.com/max/640/0*VOANQ-JSm242fvxW.png)

### **Filter: “matches”**

![](https://cdn-images-1.medium.com/max/640/1*cx6tj2F9u9t7i6wj_lRgXw.png)

![](https://cdn-images-1.medium.com/max/640/0*qAUMaqGUi1dE3bzw.png)

### **Filter: “in”**

![](https://cdn-images-1.medium.com/max/640/1*Ojt_WhSRgQqko1Ltf0ykdg.png)

![](https://cdn-images-1.medium.com/max/640/0*OJyUHVikG5it3uZY.png)

### **Filter: “upper”**

![](https://cdn-images-1.medium.com/max/640/1*ulDwhgBFonVnUmE4Wfzt4A.png)

![](https://cdn-images-1.medium.com/max/640/0*ut-3NOvPgZH4p0Yr.png)

### **Filter: “lower”**

![](https://cdn-images-1.medium.com/max/640/1*gBQmT6s4KzmsiX6Q1OsMhQ.png)

![](https://cdn-images-1.medium.com/max/640/0*04VVdQaEO7tq0lot.png)

### **Filter: “string”**

![](https://cdn-images-1.medium.com/max/640/1*4w9Oz9m4lbfM6QTxI6hRhg.png)

![](https://cdn-images-1.medium.com/max/640/0*BGN0QqRAQGqLeOSs.png)

### **Bookmarks and Filtering Buttons**

We’ve covered different types of filtering options, operators and functions. It is time to create filters and save them as bookmarks and buttons for later usage. As mentioned in the previous task, the filter toolbar has a filter bookmark section to save user-created filters, which helps analysts re-use favourite/complex filters with a couple of clicks. Similar to bookmarks, you can create filter buttons ready to apply with a single click.

Creating and using bookmarks.

![](https://cdn-images-1.medium.com/max/640/0*5XxudukhaPNp_yHB.png)

Creating and using display filter buttons.

![](https://cdn-images-1.medium.com/max/640/0*oHhobz8IjGom9tfS.png)

### **Profiles**

Wireshark is a multifunctional tool that helps analysts to accomplish in-depth packet analysis. As we covered during the room, multiple preferences need to be configured to analyse a specific event of interest. It is cumbersome to re-change the configuration for each investigation case, which requires a different set of colouring rules and filtering buttons. This is where Wireshark profiles come into play. You can create multiple profiles for different investigation cases and use them accordingly. You can use the **“Edit → Configuration Profiles”** menu or the **“lower right bottom of the status bar → Profile”** section to create, modify and change the profile configuration.

![](https://cdn-images-1.medium.com/max/640/0*UyIJHjGCdYYTEEvV.png)

## Answer the questions below

### Find all Microsoft IIS servers. What is the number of packets that did not originate from “port 80”?

To start this one I needed a quick refresher on how to do _is not_, in the Wireshark filters. To do this go to the Menu bar at the top of the Wireshark and click _Analyze_. From the drop-down menu, click _Display filters…_

![](https://cdn-images-1.medium.com/max/640/1*Xl8c9pCB_LCdBzN1jU1ViQ.png)

The window will pop-up for _Display Filters_. Looking through the differnt examples we can find 3 examples of how to add an _is not_ type expression to the filter. We also find one that is not so good, but will work. Knowing how to craft our filter now, click the _OK_ button in the bottom right of the window to close it.

![](https://cdn-images-1.medium.com/max/640/1*Qt_sQe1XJKRkelNPloufzA.png)

Click on the mint green _Filter Bar,_ time to craft our filter! From the question, we know we are looking for a _Microsoft IIS Server_. Reading back over the _Contains_ filter section, we should know how to craft the first part of this filter. Since it is a server we are looking for, we want to use the syntax `http.server`. Followed by what this section should _contain_, `contains "Microsoft"`. Great we have the first part of our filter, time to build the second. If we remember from the _Display Filters_ window, to filter if something _is not_ in a packet we use `!(_place command here_)`. So filtering out any that use port 80 the syntax would be `!(tcp.port == 80)`. The full filter will be `http.server contains "Microsoft" and !(tcp.port == 80)`, then press enter to use this filter on the pcapng.

![](https://cdn-images-1.medium.com/max/640/1*eNu2ssXjtAQzfB_yUQhq0Q.png)

Look at the bottom right of the Wireshark window. You are looking for the word _Displayed:_. The numbers to the right of _Displayed_, is the answer. Type the answer in the THM answer field, and then click submit.

![](https://cdn-images-1.medium.com/max/640/1*aRYJynWjc781oBpLVbUPdA.png)

**Answer: 21**

### Find all Microsoft IIS servers. What is the number of packets that have “version 7.5”?

We need to first find out where the version number is displayed. To do this look in the Packet Detail section. If you look at _Server_, you will see _Microsoft — IIS_. After which you will see a number, this is the version of Microsoft IIS. Now we know where the version number is, let’s go make a filter.

![](https://cdn-images-1.medium.com/max/640/1*9sBCHsPY52Ou3qqDOBgK1A.png)

Click on the mint green _Filter Bar,_ time to craft our filter! Since we are still looking for the _Microsoft-IIS_ server, we can keep the first part of the filter. Additionally, since the we know that the version number is on the same line as type of server (_Microsoft-IIS)._ We can craft the filter to reflect that. So the filter should be `http.server contains “Microsoft” and http.server contains “7.5”`. Now press enter to use this filter on the pcapng.

![](https://cdn-images-1.medium.com/max/640/1*mzJIzRA4EZdDQdzkjGZwHg.png)

Look at the bottom right of the Wireshark window. You are looking for the word _Displayed:_. The numbers to the right of _Displayed_, is the answer. Type the answer in the THM answer field, and then click submit.

![](https://cdn-images-1.medium.com/max/640/1*GNT5CfDJPbap30Vc_1ClLQ.png)

**Answer: 71**

### What is the total number of packets that use ports 3333, 4444 or 9999?

Click on the mint green _Filter Bar,_ time to craft our filter! Since we are looking for ports, we want to start off the filter with `tcp.port`. Along with `in` since we are looking for a range of port numbers. Finally finishing off with the port numbers that need to be in `{}` (curly brackets) to signify the ports, `{3333 4444 9999}`. Side note, these ports are used since attackers commonly use these ports in metasploitable and other reverse shells. So the finally filter should be `tcp.port in {3333 4444 9999}`. Now press enter to use this filter on the pcapng.

![](https://cdn-images-1.medium.com/max/640/1*6zrCh4pgIiF4G7Cy2uiPlA.png)

Look at the bottom right of the Wireshark window. You are looking for the word _Displayed:_. The numbers to the right of _Displayed_, is the answer. Type the answer in the THM answer field, and then click submit.

![](https://cdn-images-1.medium.com/max/640/1*1V7Wc3eZUoGDs9uQD7MVYw.png)

**Answer: 2235**

### What is the number of packets with “even TTL numbers”?

Click on the mint green _Filter Bar,_ time to craft our filter! Going back to Task 5 we had to search for packets that had a TTL of < 10. To find the TTL we use `ip.ttl` . Now we need to convert this input to a string, so that it can match to our regex (regular expression) later on. We do this by placing our `ip.ttl` inside of the `string()` function, so it looks like `string(ip.ttl)`. The quilifier we need is `matches` , to indicate that the TTL will match to our regex. Finally, to match it to an even number we use the regex `"[02468]$"` . This regex is showing the number at the end (`$`), must match an even (`[02468]`). All together the filter should look like `string(ip.ttl) matches "[02468]$"` . Now press enter to use this filter on the pcapng.

![](https://cdn-images-1.medium.com/max/640/1*8GRAz-9QR641-b_3iJIjnw.png)

Look at the bottom right of the Wireshark window. You are looking for the word _Displayed:_. The numbers to the right of _Displayed_, is the answer. Type the answer in the THM answer field, and then click submit.

![](https://cdn-images-1.medium.com/max/640/1*-79KK6y2tOFCioyLEHohVg.png)

**Answer: 77289**

### Change the profile to “Checksum Control”. What is the number of “Bad TCP Checksum” packets?

This time instead of creating the filter, right off the bat. We need to first change the profile. To do this go to the menu bar at the top of the window. Click on the _Edit_ option, then from the drop-down menu click _Configuration Profiles…_

![](https://cdn-images-1.medium.com/max/640/1*q-2awpjbXq3aV_6FEngzBg.png)

The Configuration profile window will pop-up, look for the _Checksum Control._ Once you find it, click on it then click on the _OK_ button in the bottom right of the window.

![](https://cdn-images-1.medium.com/max/640/1*0h-4ES4kX7zPOUi2iXe5jg.png)

Click on the mint green _Filter Bar,_ time to craft our filter! I started by typing in `tcp.checksum`, and Wireshark gave me a drop down of possible filters I may want to use. Since the question wants us to find the _Bad Checksum_, I felt that the filter `tcp.checksum_bad.expert`, was the correct filter. After selecting it, I press enter to use this filter on the pcapng.

![](https://cdn-images-1.medium.com/max/640/1*n0wykSiPZBEX4OgsJd-rVg.png)

This turned out to be the correct filter we were looking for. Look at the bottom right of the Wireshark window. You are looking for the word _Displayed:_. The numbers to the right of _Displayed_, is the answer. Type the answer in the THM answer field, and then click submit.

![](https://cdn-images-1.medium.com/max/640/1*KZrGI0C0Gbyi2MApETBlfQ.png)

**Answer: 34185**

### Use the existing filtering button to filter the traffic. What is the number of displayed packets?

For this question, THM already has the filter created for us. You need to look at the end of the mint green filter bar. You should see _gif/jpeg with http-200_, click on this to apply the filter then search using it.

![](https://cdn-images-1.medium.com/max/640/1*oSnzdqoAIYNoPOXB1sP7Vw.png)

Look at the bottom right of the Wireshark window. You are looking for the word _Displayed:_. The numbers to the right of _Displayed_, is the answer. Type the answer in the THM answer field, and then click submit.

![](https://cdn-images-1.medium.com/max/640/1*_qH_DRJY2lG666F6nbW5Aw.png)

**Answer: 261**

----------

## Task 7 Conclusion

**Congratulations!**

You just finished the “Wireshark: Packet Operations” room. In this room, we covered Wireshark statistics, filters, operators and functions.

Want to learn more? We invite you to complete the **Wireshark: Traffic Analysis** room to improve your Wireshark skills by investigating suspicious traffic activities.

----------

### 🎉🎉🎉Congrats!!! You completed the TryHackMe Wireshark Packet Operations Room, Awesome Job!!!🎉🎉🎉