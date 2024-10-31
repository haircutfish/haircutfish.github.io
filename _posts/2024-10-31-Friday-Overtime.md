---
layout: "post"
title: "TryHackMe Room — Friday Overtime"
categories: CTI
tags: TryHackMe, SOC Level One Path, SOC, CTI, Cyber Threat Intelligence
---

----------

This is a subscribers only room on TryHackMe. It was created by [TryHackMe](https://tryhackme.com/p/tryhackme) . Here it the link to said room, [TryHackMe Room — Friday Overtime.](https://tryhackme.com/r/room/fridayovertime)

Step into the shoes of a Cyber Threat Intelligence Analyst and put your investigation skills to the test.

![](https://cdn-images-1.medium.com/max/720/0*4x-yh9WzCOr9R2Xg.png)

## Task 1 Challenge Scenario

### Disclaimer

**_Please note: The artefacts used in this scenario were retrieved from a real-world cyber-attack. Hence, it is advised that interaction with the artefacts be done only inside the attached VM, as it is an isolated environment._**

Hello Busy Weekend. . .

It’s a Friday evening at PandaProbe Intelligence when a notification appears on your CTI platform. While most are already looking forward to the weekend, you realise you must pull overtime because SwiftSpend Finance has opened a new ticket, raising concerns about potential malware threats. The finance company, known for its meticulous security measures, stumbled upon something suspicious and wanted immediate expert analysis.

As the only remaining CTI Analyst on shift at PandaProbe Intelligence, you quickly took charge of the situation, realising the gravity of a potential breach at a financial institution. The ticket contained multiple file attachments, presumed to be malware samples.

With a deep breath, a focused mind, and the longing desire to go home, you began the process of:

1.  Downloading the malware samples provided in the ticket, ensuring they were contained in a secure environment.
2.  Running the samples through preliminary automated malware analysis tools to get a quick overview.
3.  Deep diving into a manual analysis, understanding the malware’s behaviour, and identifying its communication patterns.
4.  Correlating findings with global threat intelligence databases to identify known signatures or behaviours.
5.  Compiling a comprehensive report with mitigation and recovery steps, ensuring SwiftSpend Finance could swiftly address potential threats.

Connecting to the machine

Start the virtual machine in split-screen view by clicking the green **Start Machine** button on the upper right section of this task.

![](https://cdn-images-1.medium.com/max/720/1*IuX2xLlPJa90ezk4ygKN7g.png)

If the VM is not visible, use the blue **Show Split View** button at the top-right of the page.

![](https://cdn-images-1.medium.com/max/720/1*uFEmfIlIOZxwd4fM6WlBbA.png)

Additionally, you can open the DocIntel platform using the credentials below.

![](https://cdn-images-1.medium.com/max/720/0*4G7hyrjPq-4kuP77.png)

**Username:** ericatracy

**Password:** Intel321!

**IP:** MACHINE_IP

![](https://cdn-images-1.medium.com/max/720/1*ToICvPw7Jx5p-kvBhojbAA.png)

**Note:** While the web browser (i.e., Chromium) will immediately start after boot up, it may show tabs that have “Connection Refused” displayed. This is because the DocIntel platform takes a few more minutes to finish starting up after the VM has completely booted up. The ticket details can be found by logging in to the DocIntel platform. **OSINT, a web browser, and a text editor outside the VM will also help.**

----------

## Answer the questions below

### Who shared the malware samples?

Once you get logged into the DocIntel platform, you are greeted with the _Latest documents from your subscriptions_. Start reading down through the email/documents. You should be able to easily find the name of the person that sent the email/document. If you are still having trouble, make your way to the end of the email and you will find it there. Copy and paste or type the answer into the THM answer field. Then click _Submit_.

![](https://cdn-images-1.medium.com/max/720/1*IOuFLAbR3tMCVW_8J5b-zQ.png)

_ANSWER:_ O_liver Bennett_

  

### What is the SHA1 hash of the file “pRsm.dll” inside samples.zip?

There is a link at the top of the email/doc along with a link in the _Latest Documents_ on the right side of the window. It is labeled _Urgent: Malicious Malware Artefacts Detected_, click on it.

![](https://cdn-images-1.medium.com/max/720/1*iJGfuqFFPb7GM1yXlgbZJw.png)

We are now brought to the details page. From here we can see at the bottom right of the page is the _sample.zip_ file. Click on it to download the file.

![](https://cdn-images-1.medium.com/max/720/1*bPU2lC9ZO--AP-LK0HU7Aw.png)

Scroll down to the _Immediate Actions Taken_ section. About half way down down this section, you will see the following: _The password to the attached archive is_ _Panda321!_ . This is the password you will need to unzip the malware sample. Let’s open the terminal and get the file unzipped.

![](https://cdn-images-1.medium.com/max/720/1*eE4xLKaU1SE6E2tRysU9Fg.png)

At the bottom of the screen is the icon for the terminal. Click on this icon to open the terminal.

![](https://cdn-images-1.medium.com/max/720/1*cOONaDQFFr686csR3er2Kw.png)

The terminal window will open. The file will be located in the Downloads folder. Navigate there using the command `cd Downloads`, pressing enter to run. Then using `ls` to confirm that the file is here.

![](https://cdn-images-1.medium.com/max/720/1*BLbKYvn9BMeRRYuutERVeA.png)

Using the command `unzip samples.zip`, will begin the unzipping process. But we first need to use the password we got from the _Immediate action taken_ section. Which is _Panda321!_ . Once you type this password in and press enter, the file will be unzipped in the current directory.

![](https://cdn-images-1.medium.com/max/720/1*bi1uY-3UeTgNE-9z_QschQ.png)

We can use `ls` again to view the newly unzipped files. We can see the _pRsm.dll_ file amongst the files present. That file is what we need to get the SHA1 hash for.

![](https://cdn-images-1.medium.com/max/720/1*JVh9YXfjODam_b2LbOkN9w.png)

To get the SHA1 hash for the file, we will use the command `sha1sum pRsm.dll`. Pressing enter will run the command and output the SHA1 hash. Highlight and copy (ctrl Shift C) and paste the hash into the THM answer field. Then click _Submit_.

![](https://cdn-images-1.medium.com/max/720/1*2g9YqFio4EhjJ7olPiwelQ.png)

_ANSWER: 9d1ecbbe8637fed0d89fca1af35ea821277ad2e8_

  

### Which malware framework utilizes these DLLs as add-on modules?

To find the answer to this question, we need to head to our best friend Google (or your search engine of choice). I started by searching the name of our artifact along with _malware framework_. So the search was _prsm.dll malware framework_. The first result I had was from ESET about _Evasive Panda APT Group_. In the details sections we can see our artifact, let’s start with this result, click on it to be taken to the page.

_Here is the page just in case it is not easily found:_ [_https://www.welivesecurity.com/2023/04/26/evasive-panda-apt-group-malware-updates-popular-chinese-software/_](https://www.welivesecurity.com/2023/04/26/evasive-panda-apt-group-malware-updates-popular-chinese-software/)

![](https://cdn-images-1.medium.com/max/720/1*I7Dx11UUkh-6dCw8IyIc_Q.png)

The webpage will open, and we will first need to scroll down to the start of the article. Once we see the _Key points of the report_, read through them. The final point will discuss about a Malware that has plugin modules. Once you find it type the answer into the THM answer field, and then click _Submit._

![](https://cdn-images-1.medium.com/max/720/1*s1PSfk7z0EDw-dipVTrg2Q.png)

_ANSWER: MgBot_

  

### Which MITRE ATT&CK Technique is linked to using pRsm.dll in this malware framework?

Heading back to the article, let’s see if it has any information relating it to MITRE ATT&CK. To do this we can use the find feature (_ctrl f_ ), which will open a search bar in your browser. Type in _prsm.dll_ into the search bar. It looks like we will have 3 results, press the right arrow to cycle through them.

![](https://cdn-images-1.medium.com/max/720/1*VVUbsZhpsvoslDlquErNpw.png)

When we reach the third result, we reached pay dirt. You will see a MITRE ATT&CK Technique number to the left of the finding. Copy and paste or type the number into the THM answer field. Then click _Submit_.

![](https://cdn-images-1.medium.com/max/720/1*pAjo29WPWWcBVRY-laSZZQ.png)

_ANSWER: T1123_

  

### What is the CyberChef defanged URL of the malicious download location first seen on 2020–11–02?

Looking through the question, I decided to dissect the question to see if anything stands out in the article. Starting with the word _download_ in the find feature of the browser. We have 11 results.  
_note: for some reason it wouldn’t detect the date when searching for it, which is why I didn’t go this route in the explaination._

![](https://cdn-images-1.medium.com/max/720/1*5L6UawLKu0fGfSxHW2vXJw.png)

The first result doesn’t show us much. But if you scroll down a bit you will see a URL. To the right of which you can see the first time it was seen was 2020–11–02. So this is the URL we need, highlight and copy the URL. Now let’s head over to [CyberChef](https://gchq.github.io/CyberChef/).

![](https://cdn-images-1.medium.com/max/720/1*UiHpUZEBp1xAAdjnpxQ6nA.png)

Start by typing _Defang_ in the search bar under _Operations_. Next drag _Defang URL_ into the _Recipe_ section. Moving over to the _Input_ section, paste the URL into this section. The newly defanged URL will appear in the _Output_ section. Highlight, copy, and paste the URL over into the THM answer field. Then click _Submit_.

![](https://cdn-images-1.medium.com/max/720/1*Io29AYaQDqrHkw8zAfWvsQ.png)

_ANSWER: hxxp[://]update[.]browser[.]qq[.]com/qmbs/QQ/QQUrlMgr_QQ88_4296[.]exe_

  

### What is the CyberChef defanged IP address of the C&C server first detected on 2020–09–14 using these modules?

This time let’s start by searching the date in the find field. Type out _2020–09–14_. Only one result is found.

![](https://cdn-images-1.medium.com/max/720/1*ORONSZOSv1GslhoL4ceKLA.png)

As we can see from the results, it gives us the IP address associated with the C&C server. Copy the IP address, then let’s head back to CyberChef.

![](https://cdn-images-1.medium.com/max/720/1*vTY7SwL2b7ENNxunc8-PZw.png)

First we need to replace the _Defang URL_ recipe with the _Defang IP Addresses_ recipe. To do this drag the _Defang URL_ over to the operations column, and drag _Defang IP Addresses_ to the _Recipe_ section.

![](https://cdn-images-1.medium.com/max/720/1*a6nm9KrPv4hVRTuohvrTkA.png)

At first the Output won’t change. We need to do some editing of the IP address. Specifically, removing the brackets around the last period ( . ). Once this is done the Output will change and be defanged. Then highlight, copy, and paste the answer into the THM answer field. Then click _Submit_.

![](https://cdn-images-1.medium.com/max/720/1*h9Ub6lzyY9GjOW2-3UhXCQ.png)

_ANSWER: 122[.]10[.]90[.]12_

  

### What is the SHA1 hash of the spyagent family spyware hosted on the same IP targeting Android devices on November 16, 2022?

To find the answer to this question, we need to do some digging. Let’s start at [VirusTotal](https://www.virustotal.com/gui/home/search). Once at VirusTotal, using the search feature, paste the fanged IP address into the search bar and press enter.

![](https://cdn-images-1.medium.com/max/720/1*h0zPKzNI18zGTdR8c4MJVg.png)

We are brought to the _Detections_ page. Since we are looking for the SpyAgent spyware that is _related_ to this IP address. The next logical step is to head over to _Relations_. Click on the _Relations_ tab.

![](https://cdn-images-1.medium.com/max/720/1*JHD0Ij3rp-YsdMRt7OEjww.png)

Now that we are in the _Relations_ tab, we can look at some of the different types of relations associated with this IP address. The one that stands out is the _Android_ type under _Communicating Files_. Let’s check it out by clicking on the _Name_.

![](https://cdn-images-1.medium.com/max/720/1*TA_ETSjiUAuG702JPA3Bkw.png)

We will now be brought to the new _Detection_ page for_  
951F41930489A8BFE963FCED5D8DFD79_. To find the SHA1 hash, or any details about the malware, you need to click on the _Details_ section.

![](https://cdn-images-1.medium.com/max/720/1*hJtj50sNHdvh8hW8mCYqkg.png)

In the _Basic Properties_ section, the second hash is the SHA1 hash. Highlight, copy, and paste the hash into the THM answer field. Then click _Submit_.

![](https://cdn-images-1.medium.com/max/720/1*eguJ7P1iaRQGpiPgWJqHlw.png)

_ANSWER: 1c1fe906e822012f6235fcc53f601d006d15d7be_

  

----------

## 🎉🎉🎉 Congrats!!!! You just completed the Friday Overtime Room!!!🎉🎉🎉