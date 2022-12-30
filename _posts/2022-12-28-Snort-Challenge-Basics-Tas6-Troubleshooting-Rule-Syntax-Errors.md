---
layout: "post"
title: "TryHackMe Snort Challenge — The Basics — Task 6 Troubleshooting Rule Syntax Errors"
categories: Snort-Challenge-TheBasics
tags: TryHackMe, Snort, SOC Level One Path
---


_If you haven’t done task 4 & 5 yet, here is the link to my write-up of it:_ [_Task 4 Writing IDS Rules (PNG) & Task 5 Writing IDS Rules (Torrent Metafile)._](https://haircutfish.com/posts/Snort-Challenge-Basics-Task4-Writing-IDS-Rules-PNG-and-Task5-Writing-IDS-Rules-Torrent/)

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

## Task 6 Troubleshooting Rule Syntax Errors

Let’s troubleshoot rule syntax errors!

First, let’s navigate to the correct folder, use the following command  `cd Desktop/Exercise-Files/TASK-6\ \(Troubleshooting\)/`. Then using the command  `ls`  to see the contents of the directory. You are now ready to proceed.

![](https://miro.medium.com/max/630/1*ehVm_UBMxRNyuKX3wSCp3g.png)

## Answer the questions below

### **In this section, you need to fix the syntax errors in the given rule files.**

You can test each ruleset with the following command structure;

`sudo snort -c local-X.rules -r mx-1.pcap -A console`

### Fix the syntax error in  **local-1.rules**  file and make it work smoothly.

Open the local-1.rules in the text editor with  `sudo gedit local-1.rules`.

![](https://miro.medium.com/max/630/1*lCFxyEMJIVSt7LhbkPfM1g.png)

At first glance, the last any doesn’t have a space between it and the parenthesis. So we need to add one in there, once we do, it is time to save.

![](https://miro.medium.com/max/585/1*C-DiPtvpoP0ee5Rpqn1rxg.png)

![](https://miro.medium.com/max/590/1*Zg2vN_mcMuRzQKeNVCW7Bw.png)

Save (ctrl + s) and X out of the text editor window, and you're back in the terminal.

![](https://miro.medium.com/max/630/1*c0gQ7Bk-ygswgspY_B4RHA.png)

### What is the number of the detected packets?

Now let’s run the fixed syntaxed rule against the pcap file and see what we get in return. So type the command  `sudo snort -c local-1.rules -r mx-1.pcap -A console`  into the terminal, then press enter to run it.

![](https://miro.medium.com/max/630/1*xuM7mjPIc87-JKSWhETalA.png)

When the Snort is done, look in the Action Stats section, this is the last section of the scan. Look in for Alerts, the number to the right is the answer to the question, Once you find it, type this answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/630/1*IQ_a2l2zaP5tTgW1FbkIJg.png)

**Answer: 16**

### Fix the syntax error in  **local-2.rules**  file and make it work smoothly.

Open the local-2.rules in the text editor with  `sudo gedit local-2.rules`.

![](https://miro.medium.com/max/630/1*P6i8ka8oUgbwBvx3thY3jw.png)

Looking at this rule, I see two problems with it. The first one is before the directional arrow, the rule is missing an any. The second is a space gap between msg: and “Troubleshooting 2”. So make the changes, and you're ready to save.

![](https://miro.medium.com/max/587/1*XEpEwKUqAxkNz-Q6TpFgVg.png)

![](https://miro.medium.com/max/590/1*AuhpS39fO6o195zlCL_d8A.png)

Save (ctrl + s) and X out of the text editor window, and you're back in the terminal.

![](https://miro.medium.com/max/630/1*c0gQ7Bk-ygswgspY_B4RHA.png)

### What is the number of the detected packets?

Now let’s run the fixed syntaxed rule against the pcap file and see what we get in return. So type the command  `sudo snort -c local-2.rules -r mx-1.pcap -A console`  into the terminal, then press enter to run it.

![](https://miro.medium.com/max/630/1*oZiBwmDvRzXcRuUYxbG6vA.png)

When the Snort is done, look in the Action Stats section, this is the last section of the scan. Look in for Alerts, the number to the right is the answer to the question, Once you find it, type this answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/630/1*75N96tf528XKJNYgrXsnBg.png)

**Answer: 68**

### Fix the syntax error in  **local-3.rules**  file and make it work smoothly.

Open the local-3.rules in the text editor with  `sudo gedit local-3.rules`.

![](https://miro.medium.com/max/630/1*QyTIg-hVPrFbSvc2M-_P6A.png)

This time we have two rules to look at. I see that we once again that we have a space gap in the msg: field. Also, the sid: field is not incremented, so we need to change these but removing the space between message and incrementing the sid: by one in the second rule.

![](https://miro.medium.com/max/630/1*0D5u0z6UvpGwey4K_YML9w.png)

![](https://miro.medium.com/max/630/1*bBcjOxOCrJsy66G3Oa8AKw.png)

Save (ctrl + s) and X out of the text editor window, and your back in the terminal.

![](https://miro.medium.com/max/630/1*c0gQ7Bk-ygswgspY_B4RHA.png)

### What is the number of the detected packets?

Now let’s run the fixed syntaxed rule against the pcap file and see what we get in return. So type the command  `sudo snort -c local-3.rules -r mx-1.pcap -A console`  into the terminal, then press enter to run it.

![](https://miro.medium.com/max/630/1*vRsf-LJnx3j0tWp0DKYPnA.png)

When the Snort is done, look in the Action Stats section, this is the last section of the scan. Look in for Alerts, the number to the right is the answer to the question, Once you find it, type this answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/615/1*1Ci7Uc2fiw72ZFb2AuK5vw.png)

**Answer: 87**

### Fix the syntax error in  **local-4.rules**  file and make it work smoothly.

Open the local-4.rules in the text editor with  `sudo gedit local-4.rules`.

![](https://miro.medium.com/max/630/1*tR1Wqr2FyUAwNgXpdOy4vQ.png)

These rules look similar to the rules of the previous question. But after closer inspection, I see two issues. The first is, once again, the space gap in the msg: field (I don’t think it really matters but for me, I think it looks better for proper syntax), and the second is a colon instead of a semicolon to denote a new field after the msg: field. So let's make these changes.

![](https://miro.medium.com/max/630/1*rVXvXZs-K8jB0m4kSTn1pw.png)

![](https://miro.medium.com/max/630/1*Y4QK1xZuHYHiLVzrIZlCRQ.png)

Save (ctrl + s) and X out of the text editor window, and you're back in the terminal.

![](https://miro.medium.com/max/630/1*c0gQ7Bk-ygswgspY_B4RHA.png)

### What is the number of the detected packets?

Now let’s run the fixed syntaxed rule against the pcap file and see what we get in return. So type the command  `sudo snort -c local-4.rules -r mx-1.pcap -A console`  into the terminal, then press enter to run it.

![](https://miro.medium.com/max/630/1*WPN_b4tvnJZkl2Wudwx09w.png)

When the Snort is done, look in the Action Stats section, this is the last section of the scan. Look in for Alerts, the number to the right is the answer to the question, Once you find it, type this answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/630/1*rpEmqhbwC9n21IPRQKP7RA.png)

**Answer: 90**

### Fix the syntax error in  **local-5.rules**  file and make it work smoothly.

Open the local-5.rules in the text editor with  `sudo gedit local-5.rules`.

![](https://miro.medium.com/max/630/1*YGWJ1CjVGifc1HZbpTp4Hg.png)

Ohh boy, we have three rules to look at this time. After looking it over, I found 4 different syntax errors. The first bad syntax is the directional arrows, you can’t have the arrows point in that direction, so you have to change it to point to the right. This indicates ICMP coming from source to destination. The second being, as it has always been, the space gap in the msg: field. The second being in the third rule, if you look at the sid field they put a semicolon where a colon should be. The final being on the last rule, they put a colon where a semicolon should be between the msg and sid field to denote the new field. Make the changes, and when you're done, you are ready to save.

![](https://miro.medium.com/max/630/1*ujXx8rpIOdXyfyb08yXW_w.png)

![](https://miro.medium.com/max/630/1*RJ8HPDTmaDbNuCLGJErSWA.png)

Save (ctrl + s) and X out of the text editor window, and you’re back in the terminal.

![](https://miro.medium.com/max/630/1*c0gQ7Bk-ygswgspY_B4RHA.png)

### What is the number of the detected packets?

Now let’s run the fixed syntaxed rule against the pcap file and see what we get in return. So type the command  `sudo snort -c local-5.rules -r mx-1.pcap -A console`  into the terminal, then press enter to run it.

![](https://miro.medium.com/max/630/1*arOZhBUaBQTQ2eF4qgTqSg.png)

When the Snort is done, look in the Action Stats section, this is the last section of the scan. Look in for Alerts, the number to the right is the answer to the question, Once you find it, type this answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/630/1*rYmgWG5cAOqC-22m-AambA.png)

**Answer: 155**

### Fix the logical error in  **local-6.rules**  file and make it work smoothly to create alerts.

Open the local-6.rules in the text editor with  `sudo gedit local-6.rules`.

![](https://miro.medium.com/max/630/1*wVvNK178NEACTvvxyrDGmQ.png)

This time we have only one rule to look at, but within that rule we have three syntax errors. The first being, once again the space in the msg: field. The next syntax error is, the content field, the hex within reads out to lowercase. So we want to add a nocase field next to the content field so it will search for get despite case. Then finally the space gap in the sid field much like the gap in the msg field. Make all the changes, and get it ready to save.

![](https://miro.medium.com/max/630/1*6ws6eKYl33enJwWX1zmJyA.png)

![](https://miro.medium.com/max/630/1*f2dCBOw2LAuTHBi9aISAmQ.png)

Save (ctrl + s) and X out of the text editor window, and you’re back in the terminal.

![](https://miro.medium.com/max/630/1*c0gQ7Bk-ygswgspY_B4RHA.png)

### What is the number of the detected packets?

Now let’s run the fixed syntaxed rule against the pcap file and see what we get in return. So type the command  `sudo snort -c local-6.rules -r mx-1.pcap -A console`  into the terminal, then press enter to run it.

![](https://miro.medium.com/max/630/1*OGM52eLVPsIy8RtwE_mVlQ.png)

When the Snort is done, look in the Action Stats section, this is the last section of the scan. Look in for Alerts, the number to the right is the answer to the question, Once you find it, type this answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/630/1*Xlia2vOsbc5qKRbVs29B9Q.png)

**Answer: 2**

### Fix the logical error in  **local-7.rules**  file and make it work smoothly to create alerts.

Open the local-7.rules in the text editor with  `sudo gedit local-7.rules`.

![](https://miro.medium.com/max/630/1*tarDGHfz2T-PrwH5c_sSJA.png)

As we can see, we have a couple of issues here, the rule is missing the msg: field and has a space added in the sid: field. Before we can add a message we need to know what the message is going to be, to do this let's head to the website  [CyberChef](https://cyberchef.org/). Using the link, head to  [CyberChef](https://cyberchef.org/), once on the page, go to the left side of the page. Drag and drop From Hex into the Recipe section.

![](https://miro.medium.com/max/630/1*cvgO9DCFeu65srLIR2DULA.png)

Then on the right side of the page is an Input field, type the Hex value into the Input field. Below it, the Output field will populate with the converted text.

![](https://miro.medium.com/max/630/1*cw6EHEz72pRb6Bjzg1c4yw.png)

So seeing this we are looking for HTML files, so we can make the msg: field “HTML file found”. We can then just remove the space that was added in the sid: field. Then we should be ready to save.

![](https://miro.medium.com/max/611/1*IR0OgRgYM_wHYZpQ7hquDA.png)

![](https://miro.medium.com/max/630/1*WLw8KlvaYcbSaSmKpR_HNg.png)

Save (ctrl + s) and X out of the text editor window, and you’re back in the terminal.

![](https://miro.medium.com/max/630/1*c0gQ7Bk-ygswgspY_B4RHA.png)

### What is the name of the required option:

The answer for this is, the section that we had to go do research on in CyberChef. Once you figure it out, type this answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/630/1*UwXVtVls2YGMhXOQ_oygzQ.png)

**Answer: msg**

I decided to run the rule we fixed against the pcap file, since we did the work. So type the command  `sudo snort -c local-7.rules -r mx-1.pcap -A console`  into the terminal, then press enter to run it.

![](https://miro.medium.com/max/630/1*_re8-jVFckkw4LSi4C_HWA.png)

Our file caught a total of 9 html files. Pretty cool.

![](https://miro.medium.com/max/630/1*6El9WvtqWAOXA90A-LEtww.png)

 **You have finished these tasks, and can now move onto [Task 7 Using External Rules (MS17–010).](https://haircutfish.com/posts/Snort-Challenge-Basics-Task7-Using-External-Rules-ms17-010/)**