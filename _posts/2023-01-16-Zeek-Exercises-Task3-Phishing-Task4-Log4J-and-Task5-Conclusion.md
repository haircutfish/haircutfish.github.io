---
layout: "post"
title: "TryHackMe Zeek Exercises — Task 3 Phishing, Task 4 Log4J, & Task 5 Conclusion"
categories: Zeek-Exercises
tags: TryHackMe, Zeek, SOC Level One Path
---

_If you haven’t done task 1 & 2 yet, here is the link to my write-up of it:_ [_Task 1 Introduction & Task 2 Anomalous DNS._](https://haircutfish.com/posts/Zeek-Exercises-Task1-Introduction-Task2-Anomalous-DNS/)

## Getting the VM Started

Click the green button labeled Start Machine, at the top of Task 1.

![](https://miro.medium.com/max/630/0*5o5MfcTWGdYUbhC8.png)

The screen should split in half if it doesn’t go to the top of the page. You will see a blue button labeled Show Split View, click this button.

![](https://miro.medium.com/max/630/0*nKZpiG4j333wst19.png)

The screen should be split now, you have to wait for the VM to load. When it is finished loading it will look like it does below. You are ready to continue with the tasks ahead.

![](https://miro.medium.com/max/630/0*T__SBx7DuvMr6Di-.png)

On the VM, you will see a terminal icon in the middle of the VM screen on the right. Click on it.

![](https://miro.medium.com/max/630/0*Y0OV-OUWcA5om-E6.png)

A terminal window will pop up, time to move to the Exercise-Files directory. To do this we will use the  `cd`  command, which stands for change directory. We will use this command in combination with Tab completion. With Tab complete, you only have to press Tab after starting to type, and if it only has one entry that matches, it will auto-complete it. So let’s type out the command  `cd Desktop/Exercise-Files/`, then press enter to run the command. Follow up with the  `ls`  command to see the contents of the directory.

![](https://miro.medium.com/max/630/0*evluuG2FitdRzW43.png)

At the bottom of the VM, is a panel click the diagonal arrow icons. This will open the VM to full screen and make it easier to copy and paste.

![](https://miro.medium.com/max/475/1*dgrhjTVcdJ0EDCT17X7e4g.png)

## Task 3 Phishing

**An alert triggered:** “Phishing Attempt”.

The case was assigned to you. Inspect the PCAP and retrieve the artifacts to confirm this alert is a true positive.

## Answer the questions below

First, we need to move into the correct directory, to do this we need to use the command  `cd phishing/`, then press enter. Using  `ls`  will list out the directories contents.

![](https://miro.medium.com/max/562/1*Ffq2-F9syTEIqGW5f3lJsA.png)

Next, let’s run Zeek against the phishing pcap file. To do this we use the command  `zeek -r phishing.pcap`, and press enter. Then use  `ls`  to see the contents of the current directory.

![](https://miro.medium.com/max/528/1*v0eiRxpsy2ct-y4UxXI7sw.png)

### Investigate the logs. What is the suspicious source address? Enter your answer in  **defanged format**.

After doing some investigating myself, I came to the realization that they want to know what the infected local machine is. So I went to the dhcp.log file and looked at it with  `cat dhcp.log | less`, pressing enter to open it.

![](https://miro.medium.com/max/519/1*1g8mNsmOpn-l_7nMJWbvCg.png)

At a quick glance at the different fields, we see that one of the field names is client_addr. This seems to be the field we want to use, time to use some zeek-cut.

![](https://miro.medium.com/max/630/1*Zz46_emeHHIg4wI0d3UTeA.png)

To keep with using the command line, I asked ChatGPT what is the command line script to defang an IP address. It gave me a bin/bash script to do this, I then asked it for one that doesn’t require bin/bash. ChatGPT gave me this script  `echo "IP address" | sed -e 's/\./[.]/g'`.

![](https://miro.medium.com/max/630/1*RbVQdCMnpyCZ6m7YccjMmg.png)

So with our newly learned code from ChatGPT, and the command line kung-fu we already know let us get the answer. So the command we use is  `cat dhcp.log | zeek-cut client_addr | uniq | sed -e 's/\./[.]/g'`, and press enter to run. We take the field and run it through zeek-cut, and pipe the results through uniq. Uniq is used to remove any duplicates, then we pipe the results into sed to defang the IP address. After running the command we are left with a defanged IP address in the output of the terminal, and the answer to the question. Type the answer into the TryHackMe answer field, and click submit.

![](https://miro.medium.com/max/630/1*_d4yRlcLxvbQgL4q43s8Pg.png)

**Answer: 10[.]6[.]27[.]102**

### Investigate the  **http.log**  file. Which domain address were the malicious files downloaded from? Enter your answer in  **defanged format**.

Now let’s cat the HTTP log file and pipe it through less to see if we can figure out the name of the field we need to use.

![](https://miro.medium.com/max/630/1*-OwMfwIcCrNJIqMWCugP-g.png)

Once less opens the HTTP log file, press the right arrow key once.

![](https://miro.medium.com/max/630/1*eL7uHCuSpmRgNab108t64Q.png)

We can see the name of the field we are looking for is host, and if we remember the malicious file from task 2. We can see it here, along with the domain that it was downloaded from. Time to use some zeek-cut, so press  `q`  to exit less.

![](https://miro.medium.com/max/630/1*xuJ7H9biguhlvcfpu0NZkw.png)

With the name of the field, and some command line kung-fu let's get the answer. The command we are going to run is  `cat http.log | zeek-cut host | grep "smart-fax" | uniq | sed -e 's/\./[.]/g'`, press enter to run the command. We take the field and run it through zeek-cut, and pipe the results through grep. Using grep we pull out only the host that matches our string, we then pipe those results into uniq. With uniq we get rid of the duplicates, and we then pipe those results into sed. Finally with sed to defang the domain. After running the command we are left with a defanged domain in the output of the terminal, and the answer to the question. Type the answer into the TryHackMe answer field, and click submit.

![](https://miro.medium.com/max/630/1*cEETe7jsYGEhDKctl1cauw.png)

**Answer: smart-fax[.]com**

### Investigate the malicious document in VirusTotal. What kind of file is associated with the malicious document?

To start off, we need to run Zeek again, this time with the script hash-demo.zeek. The command we are going to run is  `zeek -C -r phishing.pcap hash-demo.zeek`, and press enter to run. After Zeek is done, us the command  `ls`  to show the contents of the current directory.

![](https://miro.medium.com/max/630/1*aIV2ShtdGuCgo2ExbEzXEQ.png)

Now let’s cat the files log file and pipe it through less to see if we can figure out the name of the field we need to use

![](https://miro.medium.com/max/630/1*OWKoTIfCs1kdAkEQE_W8Xw.png)

Once less opens the files log file, press the right arrow key once.

![](https://miro.medium.com/max/630/1*07JiXs5YK8QgSiEL4tdigw.png)

From the Zeek room, we know that we want to look at the mime_type field. We can see this by the fact that the application/msword is in this field.

![](https://miro.medium.com/max/630/1*PkwhAEkvK_n3KCAIdvMEHA.png)

Next, we need to look at the hash field, use the right arrow key to move to the right till you reached the hashes. Once there, you will see the name of the md5 hash field. Now we have all the info we need for now, press  `q`  to exit less.

![](https://miro.medium.com/max/630/1*5ZCVPoPY6EBr1dt2ZMkAOQ.png)

So to get the hash that we need we can use some command line kung-fu. The command we are using is  `cat files.log | zeek-cut mime_type md5 | grep "word"`  , then press enter to run. You will have the hash will be in the output of the terminal.

![](https://miro.medium.com/max/630/1*yqAROCrNJ3n2LWSJHmborQ.png)

Highlight the hash, right-click on the highlighted hash, then click Copy on the drop-down menu.

![](https://miro.medium.com/max/411/1*Rqe7WouyeKwI7q6Ob0CbyA.png)

Open a browser, go to the  [VirusTotal](https://www.virustotal.com/)  website (I provided the link to the site). Once the site loads, click the SEARCH tab in the middle of the screen.

![](https://miro.medium.com/max/630/1*ESRY4cRzb2PYcqCbQvRuog.png)

A search field will be in the middle of the page, using the keyboard shortcut ctrl + v to paste the hash in search field and press enter to search the hash.

![](https://miro.medium.com/max/630/1*zgsj5yx6yyvgzKrQoPPDzQ.png)

Once the DETECTION page loads, click the RELATIONS tab.

![](https://miro.medium.com/max/630/1*xttkQ0u0YZCNxGe9w3ud8A.png)

Once the RELATIONS page loads, scroll down till you see Bundled Files section.

![](https://miro.medium.com/max/630/1*WXfURGkLPk0sQDjCET4y_g.png)

Once you reach the Bundled Files section, you will see a column labeled File type. The three-letter file abbreviation is the answer, type the answer into the TryHackMe answer field, and click submit.

![](https://miro.medium.com/max/583/1*2_SqDc_fX-glNcO_BsxWHw.png)

**Answer: VBA**

### Investigate the extracted malicious  **.exe**  file. What is the given file name in Virustotal?

Head back to the terminal and leave VirusTotal open. Since we know the field to look at from the previous question, let’s use zeek-cut and grep to get hash for the exe file. The command being  `cat files.log | zeek-cut mime_type md5 | grep "exe"`, press enter to run the command.

![](https://miro.medium.com/max/630/1*_93Adl-__kmDwXzbloxjdw.png)

Highlight the hash, right-click on the highlighted hash, then click Copy on the drop-down menu.

![](https://miro.medium.com/max/422/1*Qt0qlzjs54nsiet2J0ETmg.png)

Back at VirusTotal highlight the hash at the top of the page, and press the delete key to remove it from the search field.

![](https://miro.medium.com/max/630/1*XcAWXoPhJc6sSPOx8H6x6g.png)

Use the keyboard shortcut ctrl + v to paste the new hash into the search field, then press enter to search it.

![](https://miro.medium.com/max/630/1*-vWcH9SZPS1w8crD51krGQ.png)

Once the DETECTION tab loads, you can see this is malicious. At the top is a box that has some general information about the file. Inside this box, under the hash, you will see the name of the file, and thus the answer to the question. Highlight copy (ctrl + c) and paste (ctrl + v) or type, the answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/630/1*GRbeWeBrjkEmVEXB66Eg1g.png)

**Answer: PleaseWaitWindow.exe**


### Investigate the malicious  **.exe**  file in VirusTotal. What is the contacted domain name? Enter your answer in  **defanged format**.

Go back to VirusTotal, you already have the exe file hash searched in VirusTotal so we just need to do a little looking for the answer to this question. Once back on VirusTotal, click the RELATIONS tab.

![](https://miro.medium.com/max/630/1*WX6Rjev11i75HNp7GGNCzA.png)

The first section is Contacted Domains, there is one that has a detection. You don’t need the full domain for the answer, just every after dunlop.. You can type the answer in and defange it yourself or use the command  `echo hopto.org | sed -e 's/\./[.]/g'`, and press enter to run. Highlight copy (ctrl + c) and paste (ctrl + v) from the VM or type, the answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/630/1*OAzTU6Eg4gHjFA5Xl1GOag.png)

**Answer:hopto[.]org**

### Investigate the  **http.log**  file. What is the request name of the downloaded malicious  **.exe**  file?

Head back to your terminal in the VM, use the command  `cat http.log | grep "exe"`, you will see the name of the malicious file. Type the answer into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/630/1*72WJ18j5LJiqqtYt_Fmq4A.png)

**Answer: knr.exe**

## Task 4 Log4J

**An alert triggered:** “Log4J Exploitation Attempt”.

The case was assigned to you. Inspect the PCAP and retrieve the artefacts to confirm this alert is a true positive.

## Answer the questions below

First we need to move from the phishing directory to the log4j directory. Use the command  `cd ..`, to back out of the current directory. Then using the command  `cd log4j/`, to move forward into the log4j directory. Finally, use the command  `ls`  to list the content of the current directory.

![](https://miro.medium.com/max/517/1*B645dZT2RU8I5jGk0MnDfw.png)

### Investigate the  **log4shell.pcapng file** with **detection-log4j.zeek**  script. Investigate the  **signature.log**  file. What is the number of signature hits?

Start by using the command  `zeek -C -r log4shell.pcapng detection-log4j.zeek`, press enter to run. Then use the command  `ls`to see the contents of the current directory.

![](https://miro.medium.com/max/630/1*hM3EGlv2e41yNQwAcELLRA.png)

Now let’s cat the signatures log file and pipe it through less to see if we can find the answer.

![](https://miro.medium.com/max/630/1*Ok8C-2FUkQoItNSo55TCSg.png)

Once less opens the signatures log file, press the right arrow key once.

![](https://miro.medium.com/max/630/1*DS91l9joDwKY_I3vjQy9QQ.png)

If you count the number of Signatures here in the note field you will get your answer. But I will show you the command line way of finding it. Press  `q`  to exit less.

![](https://miro.medium.com/max/630/1*iOgtivm1-DiaFqI7A_s1vA.png)

Back in the terminal, we want to use the command  `cat signatures.log | zeek-cut note | uniq -c`, press enter after you were done typing the command. After you have run the command you will have the answer in the output of the terminal, type it into the TryHackMe answer field, then click submit.

![](https://miro.medium.com/max/630/1*f_vdy3eRZ4rDXhgKO9R6nw.png)

**Answer: 3**

### Investigate the  **http.log** file. Which tool is used for scanning?

Now let’s cat the http log file and pipe it through less to see if we can find the answer.

![](https://miro.medium.com/max/630/1*pRzfCa8vtFVEyvSHspuFFg.png)

Once less opens the http log file, press the right arrow key once.

![](https://miro.medium.com/max/630/1*7vzfI8J25ZG5-HlK4b6JlQ.png)

As we look through the user_agent field we can see some interesting information, so the field we are looking for is user_agent. Time to use some zeek-cut, so press  `q`  to exit less

![](https://miro.medium.com/max/630/1*m1meI6lkscdrr2XDTp10Lw.png)

Knowing the field we want to look at let’s run zeek-cut, sort, and uniq. The command being  `cat http.log | zeek-cut user_agent | sort | uniq`, after you have finished typing out the command press enter. We use zeek-cut to “cut” that field out to look at, taking the results for zeek-cut we pipe it through sort. With sort, the results are sorted alphabetically, those results are then piped through uniq. Finally uniq will remove any dupilcates. After the command is finished running, look through the output you should be able to notice a famous network mapping program (wink wink). Once you find it, type the answer into the TryHackMe answer field, and click submit.

![](https://miro.medium.com/max/630/1*QuJ712VKjXaFMjzeHanJCg.png)

**Answer: Nmap**

### Investigate the  **http.log**  file. What is the extension of the exploit file?

Now let’s cat the http log file and pipe it through less to see if we can find the answer.

![](https://miro.medium.com/max/630/1*pRzfCa8vtFVEyvSHspuFFg.png)

Once less opens the http log file, press the right arrow key once.

![](https://miro.medium.com/max/630/1*7vzfI8J25ZG5-HlK4b6JlQ.png)

As we look through the user_agent field we can see some interesting information, so the field we are looking for is uri. Time to use some zeek-cut, so press  `q`  to exit less

![](https://miro.medium.com/max/630/1*jtT9mjEtVYBdnAK5TQFMeQ.png)

Knowing the field we want to look at let’s run zeek-cut, sort, and uniq. The command being  `cat http.log | zeek-cut uri | sort | uniq`, after you have finished typing out the command press enter. We use zeek-cut to “cut” that field out to look at, taking the results for zeek-cut we pipe it through sort. With sort, the results are sorted alphabetically, those results are then piped through uniq. Finally uniq will remove any dupilcates. After the command is finished running, look through the output you should be able to see only one file extension, this is the answer. Once you find it, type the answer into the TryHackMe answer field, and click submit.

![](https://miro.medium.com/max/630/1*CHUjbXZ_wCPwctuKCKhRzQ.png)

**Answer: .class**

### Investigate the  **log4j.log**  file. Decode the base64 commands. What is the name of the created file?

Now let’s cat the log4j log file and pipe it through less to see if we can find the answer. Once the log4j file opens in less, looking through the fields along with the field contents we can see some of the base64 we need to decode. Time to use some command line kung-fu to help slim down the results.

![](https://miro.medium.com/max/630/1*NEBgt7pQAoSNDVxtU5_xhQ.png)

Time for the command line kung-fu, the command we want to run is  `cat log4j.log | zeek-cut uri | sort -nr | uniq`, after you have done typing the command out press enter to run it. You will see three base64 codes in the output. Next we will be decoding them.

![](https://miro.medium.com/max/630/1*btXF3MEovOXEuqOyxRgDUg.png)

To decode all three the take the same steps to reach. First step is to highlight the base64 code, then right-click on it. On the drop-down menu click copy.

![](https://miro.medium.com/max/406/1*ZPhbsrZQWKS9zhT7oi4WWg.png)

Then type  `echo`  into the terminal, using the paste shortcut for linux terminal, ctrl + shift + v, paste the base64 code into the terminal. Then pipe it to  `base64 -d`, this command will take a base64 code and decode it. So the command is  `echo {base64 code} | base64 -d`, press enter to run the code.

![](https://miro.medium.com/max/630/1*IUPqoRraVRpHn0UNLo9VoQ.png)

Repeat these steps for the other two base64 codes. Now that you have them all decoded, you should see the name of the file created at the end of the first line. Touch is used to create, and with the name on the end this says that this is the name of the file. Once you have found it, type the answer into the TryHackMe answer field, and click submit.

![](https://miro.medium.com/max/630/1*92zMUCSShyIALwJa-tIV8Q.png)

**Answer: pwned**

## Task 5 Conclusion

**Congratulations!** You just finished the Zeek exercises.

If you like this content, make sure you visit the following rooms later on THM;

-   [**Snort**](https://tryhackme.com/room/snort)
-   [**Snort Challenges 1**](https://tryhackme.com/room/snortchallenges1)
-   [**Snort Challenges 2**](https://tryhackme.com/room/snortchallenges2)
-   [**Wireshark**](https://tryhackme.com/room/wireshark)
-   [**NetworkMiner**](https://tryhackme.com/room/networkminer)

Note that there are challenge rooms available for the discussed content. Use the search option to find them! Happy hacking!

🎉🎉🎉CONGRATS!!! You have completed the Zeek Exercises Room!!!🎉🎉🎉
