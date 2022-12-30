---
layout: "post"
title: "TryHackMe Snort Challenge — The Basics — Task 8 Using External Rules (Log4j) & Task 9 Conclusion"
categories: Snort-Challenge-TheBasics
tags: TryHackMe, Snort, SOC Level One Path
---



_If you haven’t done task 7 yet, here is the link to my write-up of it: [Task 7 Using External Rules (MS17–010).](https://haircutfish.com/posts/Snort-Challenge-Basics-Task7-Using-External-Rules-ms17-010/)_

## Opening the VM

Click the green Start Machine button in the top of Task 1.

![](https://miro.medium.com/max/567/0*yF1yOoRx8PmkiKRd.png)

The screen will split in half, with the VM on the right and the Tasks on the left. If the screen didn’t split in half go to the next step, if it did split in half skip the next step.

![](https://miro.medium.com/max/567/0*hUQfIHovUa5T4_nf.png)

Scroll to the top of the page, you will see a blue bottom labeled Show Split View, click this button to split the page in half.

![](https://miro.medium.com/max/567/0*mLZDKrTJMFqF0mAm.png)

Now that we have our screen split and we have our VM, we need a terminal to work in. At the top left of the VM is a terminal icon, it is hard to see, click this icon to open a terminal window.

![](https://miro.medium.com/max/308/0*EpyfDGApKmRvfTQJ.png)

Once you have your terminal window, you are good to go with the tasks ahead.

## Task 8 Using External Rules (Log4j)

Let’s use external rules to fight against the latest threats!

## Answer the questions below

### **Navigate to the task folder.**

First, let’s navigate to the correct folder, use the following command  `cd Desktop/Exercise-Files/TASK-8\ \(Log4j\)/`. Then using the command  `ls`  to see the contents of the directory. You are now ready to proceed.

![](https://miro.medium.com/max/528/1*EeJoPdHOOeFXsq1DBMqrRg.png)

### Use the given pcap file.

### Use the given rule file (**local.rules**) to investigate the log4j exploitation.

So TryHackMe already has a rule ready for us to use and wants us to use it. So using the local.rules file, we can use the command  `sudo snort -c local.rules -A full -l . -r log4j.pcap`, and press enter to run it.

![](https://miro.medium.com/max/630/1*2c4OL-11t_hUB8fUZlZ2zw.png)

### What is the number of detected packets?

When the Snort is done, look in the Action Stats section, this is the last section of the scan. Look in for Alerts, the number to the right is the answer to the question, Once you find it, type this answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/630/1*GPLqTdZDQ69JcTG895Tp1A.png)

**Answer: 26**

### Investigate the log/alarm files.

Using the command  `cat alert`, will output the alerts onto the screen. From there I can see that all the alerts have the same thing in common, they start with FOX-SRT.

![](https://miro.medium.com/max/630/1*_hcNIGmK8ANqNUNBwKytdA.png)

### How many rules were triggered?.

Using the same command as above with some added help from grep we can cut the output down a bit. The command is now  `cat alert | grep "FOX-SRT"`. Counting these up, I only count 3 rules in total that were triggered, but this isn’t the answer. So looking over the output again, I found that the numbers on the left side of FOX-SRT are all the same except the last two digits. These last two digits coincide with the rule that was triggered, which could make this the sid numbers.

![](https://miro.medium.com/max/630/1*iAFd27ZSJlk5_o33tLIASg.png)

Knowing this now we can use the command  `cat alert | grep "210037"`, and count the first instance of each number. After you have counted it up, type the answer in the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/630/1*rkFpFiMzEkXvseBp0-D5tg.png)

**Answer: 4**

### Investigate the log/alarm files.

You should already have what you need in the terminal.

### What are the first six digits of the triggered rule sids?

Back in the terminal, the answer is the six digits that we searched with grep. Type these digits into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/630/1*wEym_o-bFicoP4NODaWyNA.png)

**Answer:** 210037

### **Clear the previous log and alarm files.**

Run the command  `ls`  so we know what the names of the files

![](https://miro.medium.com/max/556/1*4izH0jeCeg7TDzbaV-w8AQ.png)

Let’s remove the log file first, to do this we can use the command  `sudo rm snort.log.1672321771`, then press enter. If it is ready for you to add another command, then you entered it correctly.

![](https://miro.medium.com/max/630/1*w2qag2Ds0NAc8wbshMnzDA.png)

For the alarm file, we can use  `gedit`. The command will be  `sudo gedit alert`, then press enter to open the alert file in gedit.

![](https://miro.medium.com/max/630/1*jWa9KrAi5noOp3KYE_Vt2g.png)

Click anywhere inside the alert file, then use the keyboard shortcut to select all, ctrl + a . The text editor should fill up blue, meaning that all the text is selected.

![](https://miro.medium.com/max/630/1*xSQDV8UqNwOSmp0J6I-70Q.png)

Press the Deleted button on the keyboard, everything will be gone.

![](https://miro.medium.com/max/630/1*PO2cyAoX0L8MgKsrGzX-pA.png)

Save (ctrl + s) and X out of the text editor window, and your back in the terminal.

![](https://miro.medium.com/max/630/1*jEV2WXsZThgmjIyz5AUXLw.png)

### Use  **local-1.rules**  empty file to write a new rule to detect packet payloads  **between 770 and 855 bytes**.

To refresh our minds, we can look back on Task 9 of the Snort room, if we scroll down to the  **Non-Payload Detection Rule Options.** Look in the table for Dsize, it will show you how to use it with an example.

![](https://miro.medium.com/max/630/1*0iS1FnVNAJiQiFtAtiSbBg.png)

Now that we know how to detect payload data sizes, let’s open up the text editor and create our rule, with the command  `sudo gedit local-1.rules`.

![](https://miro.medium.com/max/630/1*GdyjsVfpNoEynjfyg3uJ3Q.png)

So when writing this rule, we start by making it an  `alert`  so we will be notified if/when it happens. Next is the protocol, I went with  `tcp`  as it seems to be the protocol of choice for the most part. Then, since we don’t have an IP address or port on either side, we make both on the source and destination sides  `any`. Next is the msg: section, this is where we make it descriptive to what we could see, so we know from a glance what why the alert was triggered. The next section is the dsize: section, here we want to specifiy  `770<>855`, since this is what TryHackMe told us to detect. Finally the last two sections are the sid: and the rev:, the sid: section should be  `100001`  and the rev: should be  `1`. Altogether, the command is  `alert tcp any any <> any any (msg:"Log4j detected-Byte size"; dsize:770<>855; sid:100001; rev:1;)`. After you have that typed into the rule file, it’s time to save.

![](https://miro.medium.com/max/630/1*ovqwC9nJqbwXc37afEFqEQ.png)

Save (ctrl + s) and X out of the text editor window, and your back in the terminal.

![](https://miro.medium.com/max/630/1*jEV2WXsZThgmjIyz5AUXLw.png)

### What is the number of detected packets?

Time to run our rule through snort with the command  `sudo snort -c local-1.rules -A full -l . -r log4j.pcap`. Press enter to run Snort, unfortunately we have an error!!! So we have to go about this another way.

![](https://miro.medium.com/max/630/1*8d6ea9dZDoYhutgiH5hVyg.png)

When the Snort is done, look in the Action Stats section, this is the last section of the scan. Look in for Alerts, the number to the right is the answer to the question, Once you find it, type this answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/630/1*MD73bXkGiZEPd-O5j85BgQ.png)

**Answer: 41**

### Investigate the log/alarm files.

Using Snort and grep we are going to use the command  `sudo snort -r snort.log1672329139 -X` , this will display in the output all the content of the packet down to the hex values.

![](https://miro.medium.com/max/630/1*9tIjms1WZe8P_II5riA22w.png)

### What  is the name of the used encoding algorithm?

Start to scroll up through the outputs, looking for anything that would indicate what the encoding algorithm could be. Lucky we don’t have to go far up, packet number 40 has our answer in it. Look at the text on the right, look for the word Command/, the answer is after this. Once you find it type the answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/630/1*tu6Mf82UpmFAOq_ZmqY7Cw.png)

**Answer: Base64**

### Investigate the log/alarm files.

You should already have what you need in the terminal.

### What  is the IP ID of the corresponding packet?

Look at the top of Packet 40, the third line down about halfway in. You will see ID:, the numbers after this are the answer. Once you find it type the answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/630/1*-4-UMX6RHc8ld3e6SxVrCA.png)

**Answer: 62808**

### Investigate the log/alarm files.

You should already have what you need in the terminal.

### Decode the encoded command.

Go back and highlight the encoded section, you will have the hex value highlighted as well.

![](https://miro.medium.com/max/630/1*RaElXoMw9tjW4VGXBabNvw.png)

Right-click on the highlighted part, then in the drop-down menu click Copy. Now look to the left side of the VM for a little gray tab, click on it.

![](https://miro.medium.com/max/622/1*X6jhZzynhlgDqOX4h4Ffvg.png)

Click the clipboard icon in the middle of the panel.

![](https://miro.medium.com/max/99/1*DTrYyfqU7Mboqqgl5ADNMw.png)

Now the Clipboard function of the VM is open, and code we copied from the terminal is already in here. We just need to remove the hex value parts of it and combine the base64 portion.

![](https://miro.medium.com/max/463/1*zx-o5JislFZrnsCGk2srWQ.png)

After you have taken all the hex values, spaces, and new lines out. You are left with the base64 code, we are almost ready to decode this. First, highlight the base64 code, this time we can use the keyboard shortcut to copy, ctrl + c . Time to head over to  [CyberChef](https://cyberchef.org/).

![](https://miro.medium.com/max/463/1*xQjJPOSgm1o_25mklHD1_w.png)

### What is the attacker’s command?

Once at  [CyberChef](https://cyberchef.org/)  (use the link I provided), on the left side of the screen is Operations. Drag and drop From Base64 to the Recipe column in the middle of the page.

![](https://miro.medium.com/max/630/1*Vwo3i5J96M_L05QHOIbERg.png)

Now move over to the Input section on the right of the webpage, and paste (ctrl + v) the base64 code into it. In the Output section will be the decoded command, and the answer to the question. Type the answer in the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/630/1*SgOWWidJ6tizVgOnb6IcJg.png)

**Not the Answer: I am not putting the answer in here, as medium doesn’t like it and crashes every time I put it in here.**

### What is the CVSS v2 score of the Log4j vulnerability?

We won’t need the VM for this answer, but we will need a trusty friend by the name of Google. Head over to Google and search CVSS v2 score log4j vulnerability.

![](https://miro.medium.com/max/630/1*F-Y4RZfwsqdGNf8iBgODhg.png)

So we can see that the NIST site comes up again, like in the previous task. Click on and let’s check it out.

![](https://miro.medium.com/max/630/1*YNDO7Z6vXqH8vC-Vwaa1EQ.png)

When the page loads we and kinda of see what we are looking for so scroll down a little bit.

![](https://miro.medium.com/max/630/1*TPmCTNsG3zomOi22answow.png)

Now that it’s in better view we can see that it is on version 3.x but we want version 2. So click the white box labeled CVSS Version 2.0.

![](https://miro.medium.com/max/630/1*yC44ar63P_Z1CPbJdBskaA.png)

The number will change, and will be the answer you are looking for. Type the answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/630/1*hdlejJ-cuNx2UJN1ltPfXw.png)

**Answer: 9.3**

## Task 9 Conclusion

Congratulations! Are you brave enough to stop a live attack in the  [Snort2 Challenge 2](https://tryhackme.com/room/snortchallenges2)  room?

**🎉🎉🎉CONGRATS!!! You have finished the TryHackMe Snort Challenge — The Basics room!!!🎉🎉🎉**