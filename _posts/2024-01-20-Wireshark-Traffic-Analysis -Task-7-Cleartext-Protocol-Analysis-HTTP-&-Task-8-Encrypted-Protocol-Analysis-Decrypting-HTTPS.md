---
layout: "post"
title: "TryHackMe Wireshark:Traffic Analysis — Task 7 Cleartext Protocol Analysis: HTTP & Task 8 Encrypted Protocol Analysis: Decrypting HTTPS"
categories: Wireshark
tags: TryHackMe, Wireshark, SOC Level One Path
---


_If you haven’t done tasks 5 and 6 yet, here is the link to my write-up of them: [Task 5 Tunneling Traffic: DNS and ICMP & Task 6 Cleartext Protocol Analysis: FTP](https://haircutfish.com/posts/Wireshark-Traffic-Analysis-Task-3-ARP-Poisoning-&-Man-In-The-Middle-and-Task-4-Identifying-Hosts-DHCP-NetBIOS-and-Kerberos/)_

## Getting the VM Started

Starting at Task 1, you will see the green _Start Machine_ button. Click this button to get the VM Started.

![](https://cdn-images-1.medium.com/max/600/0*_BHceNJ1VRtlLk4v.png)

Scroll to the top where the banner is. On the right side of the page, you will see the blue _Show Split view_. Click this blue button.

![](https://cdn-images-1.medium.com/max/600/0*jlhlxhqcQ6NR9wbK.png)

The page will split, now just wait till the VM loads.

![](https://cdn-images-1.medium.com/max/600/0*xUXjf8i_J27b7mq4.png)

Once the VM loads, click the _View in Full Screen_ icon in the bottom left of the VM.

![](https://cdn-images-1.medium.com/max/600/0*97XpuRfEtO3OuuJO.png)

A new browser tab should open with the VM in it.

![](https://cdn-images-1.medium.com/max/600/0*RI7TVGri4r5-xWpX.png)

Double-Click on the e_xercise-pcap_ folder to open it.

![](https://cdn-images-1.medium.com/max/600/0*L68OBAvwqGMaPoAb.png)

While folder opens, head back to the THM Task Tab. At the bottom of the VM you will see a minus ( — ), this represents _Exit Split View_. Click the — to allow the THM task to incapsilate the entire window. This won’t close out of your VM instance, it will just be on the other tab.

![](https://cdn-images-1.medium.com/max/600/0*MBV7FEHAo0KjNnZC.png)

Heading back to the browser tab that the VM is in. The folder should be open. Inside this folder will be other folders containing the files needed for the tasks ahead. The folders are named accordingly to the task they are associated with.

![](https://cdn-images-1.medium.com/max/600/0*nJ2FtDPbbBUQVVvT.png)

----------

## Task 7 Cleartext Protocol Analysis: HTTP

### **HTTP Analysis**

Hypertext Transfer Protocol (HTTP) is a cleartext-based, request-response and client-server protocol. It is the standard type of network activity to request/serve web pages, and by default, it is not blocked by any network perimeter. As a result of being unencrypted and the backbone of web traffic, HTTP is one of the must-to-know protocols in traffic analysis. Following attacks could be detected with the help of HTTP analysis:

-   Phishing pages
-   Web attacks
-   Data exfiltration
-   Command and control traffic (C2)

**HTTP analysis in a nutshell:**

![](https://cdn-images-1.medium.com/max/600/1*aUlbSIGkX5pXW6R3Z73aiA.png)

![](https://cdn-images-1.medium.com/max/600/1*gTCLT8jqLAAuxZC_nsrJCA.png)

![](https://cdn-images-1.medium.com/max/600/1*g3CRYzjZ8NlSkczeLIl2pA.png)

### **User Agent Analysis**

As the adversaries use sophisticated technics to accomplish attacks, they try to leave traces similar to natural traffic through the known and trusted protocols. For a security analyst, it is important to spot the anomaly signs on the bits and pieces of the packets. The “user-agent” field is one of the great resources for spotting anomalies in HTTP traffic. In some cases, adversaries successfully modify the user-agent data, which could look super natural. A security analyst cannot rely only on the user-agent field to spot an anomaly. Never whitelist a user agent, even if it looks natural. User agent-based anomaly/threat detection/hunting is an additional data source to check and is useful when there is an obvious anomaly. If you are unsure about a value, you can conduct a web search to validate your findings with the default and normal user-agent info ([**example site**](https://developers.whatismybrowser.com/useragents/explore/)).

**User Agent analysis in a nutshell:**

![](https://cdn-images-1.medium.com/max/600/1*f3KXWG1IifwJn302-WbrSQ.png)

![](https://cdn-images-1.medium.com/max/600/0*yYJXGW3KboDuER2U.png)

### **Log4j Analysis**

A proper investigation starts with prior research on threats and anomalies going to be hunted. Let’s review the knowns on the “Log4j” attack before launching Wireshark.

**Log4j vulnerability analysis in a nutshell:**

![](https://cdn-images-1.medium.com/max/600/1*FM_hmQAIVk2NHcVgv8SSaQ.png)

![](https://cdn-images-1.medium.com/max/600/0*G0yzFzod3b5SZ_M7.png)

Detecting suspicious activities in chunked files is easy and a great way to learn how to focus on the details. **Now use the exercise files to put your skills into practice against a single capture file and answer the questions below!**

## Answer the questions below

### **Use the “Desktop/exercise-pcaps/http/user-agent.cap” file.**

Inside the _exercise-pcaps_ folder, double-click on the _http_ folder.

![](https://cdn-images-1.medium.com/max/600/1*Xqx2-rOthGUoYQAHG6_GKA.png)

Inside the http folder you will see the _user-agent.cap_ file. Right-click on it, then choose _Open With Wireshark_ from the drop-down menu.

![](https://cdn-images-1.medium.com/max/600/1*UIu3T4otMhbps9rJD_FyBg.png)

  

### Investigate the user agents. What is the number of anomalous “user-agent” types?

To make this task a bit easier, we need to do a little prep. Inside of Wireshark, right-click on the _Column names_ that are underneath the filter bar. Once you have right-clicked on this row, a drop-down menu will appear. Click on _Column Preferences…._

![](https://cdn-images-1.medium.com/max/600/1*pLZF5FHkoA1yxnTx30TK6Q.png)

The _Wireshark Preferences_ window will pop up onto your screen. From here, there is a `+` icon under the different column’s that can be displayed. Click the `+` icon.

![](https://cdn-images-1.medium.com/max/600/1*LJA3m1lJCxk9ws11nleoWA.png)

A new row will appear in the chart. You will need to interact with both the _Title_ and _Fields_ cells of the new row. To do this, you will only need to double-click on the cell. So for the _Title_ cell, you can name it _User Agent_. Then for the _Fields_ cell, you will put in the filter needed to show the User Agent. That filter is `http.user_agent`. Once you have done this, the _Type_ cell will change from _Number_ to _Custom_. This is normal and good.

![](https://cdn-images-1.medium.com/max/600/1*-xu6z_SNVyb1ArXo3HDSKQ.png)

Click on the _OK_ button, in the bottom right of the window.

![](https://cdn-images-1.medium.com/max/600/1*FeV5pQA5Zl2Yi7ArdUW06g.png)

The _Wireshark Preferences_ window will disappear. You should see the main Wireshark window. But, looking to the right, you will see the new Column we just added to the _Packet List_ section. Click on the new _User Agent_ column to organize the _Packet List_ by _User Agent_.

![](https://cdn-images-1.medium.com/max/600/1*_HvgYvZtKlgeEbP17unAdg.png)

Looking through the different User Agents, I was still coming to a wall. So I took a look at the Hint, it shares about looking into the _Windows NT 6.4_. So I did a little Googling, and found this [Article](https://b1thunt3r.se/2015/02/windows-nt-10-what-happened-to-nt-6-4) , that explains that there is no such Windows User Agent Version. It goes from Windows NT 6.3 to Windows NT 10. So we have found our Anomolous Packets. Time to count them. Once you have counted the number of Packets that contain this User Agent. Type this number into the TryHackMe answer field, then click submit.

![](https://cdn-images-1.medium.com/max/600/1*hL1y9NU7pEnciZFUpC5wBA.png)

**Answer: 6**

  

### What is the packet number with a subtle spelling difference in the user agent field?

Hover your cursor over the divide bar to the right of the_User Agent_ column we created. Once the cursor changes to arrows pointing both ways, _Click and Hold_ then slide the column to the left to expand it. If needed, repeat this same step on the right side to expand the column some more.

![](https://cdn-images-1.medium.com/max/600/1*CS-khw22rbhBZVDhcV3-Nw.png)

Now that the column is expanded, it’s time to start parsing through the information.

![](https://cdn-images-1.medium.com/max/600/1*ySGth8NvKZPl1qQZukMLtg.png)

Once you find the spelling error, look at the first column on the left. This is the _Packet Number_. Take this number and type it into the TryHackMe answer field. Then click _Submit_.

![](https://cdn-images-1.medium.com/max/600/1*jPwiHKXkt3aOx8nBYlsP1g.png)

**Answer: 52**

  

### **Use the “Desktop/exercise-pcaps/http/http.pcapng” file.**

Going back to the http folder, right-click on the _http.pcapng_ file. From the drop-down menu, click on _Open With Wireshark_.

![](https://cdn-images-1.medium.com/max/600/1*NBV0P0aKoSlFYDzuUo3zdA.png)

  

### Locate the “Log4j” attack starting phase. What is the packet number?

Looking over the section above in regards to Log4j, it gives us some areas to start with. Since we are looking for the starting phase packet number, the table tells us that the attack starts with a _POST request_. Along with some known cleartext patterns. Let’s build a filter, head back to Wireshark.

![](https://cdn-images-1.medium.com/max/600/1*oM7Jp0GtSv3eYIaf8CelHA.png)

In the mint green filter bar let’s create our filter. We will start by encapsilating the first pramater in `()`. Our first parameter is filtering only _POST request_, to do this use `(http.request.method == “POST”)` . We then want to add `and` to let Wireshark know that the filter needs to match both parameters to get a result. Next we again are using `()` to encapsilate the parameters and function. The parameter this time is looking for the clear text patterns in the IP field. Here is how this should look `((ip contains “jndi”) or ( ip contains “Exploit”))`. We use the double `()`, with the `or` function to say that this parameter can match either one of these filters. If it does along with it being a _POST Request_, then a result will be given. The full filter will look like this: `(http.request.method == “POST”) and ((ip contains “jndi”) or ( ip contains “Exploit”))`. Once you have this typed into the filter bar, press enter to run.

![](https://cdn-images-1.medium.com/max/600/1*hq5LB-r-ziF1keht3b2olw.png)

You will be left with one result. Look at the Packet number in the first column of the Packet List Section. Type this number into the TryHackMe answer field, then click _Submit_.

![](https://cdn-images-1.medium.com/max/600/1*Biyy8huuo7EE9kikuOHJBw.png)

**Answer: 444**

  

### Locate the “Log4j” attack starting phase and decode the base64 command. What is the IP address contacted by the adversary? (Enter the address in defanged format and exclude “{}”.)

Going back to Wireshark, we can see in the hex output of the packet the _Base64_ string. We need to copy this string so we can decode it. The easiest way is to click the _drop-down carot_ for _HyperText Transfer Protocol_ found in the Packet Detail Section.

![](https://cdn-images-1.medium.com/max/600/1*H-WJ20JXlJYLBF6L8WPJQQ.png)

Once we have done that, we can see the _User-Agent_ Field. The _Base64_ value can be found in the field. Start by _right-clicking_ the _User-Agent_ field. In the drop-down menu, hover your cursor over _Copy._ A new drop down will appear. Move your cursor over to _Value_, then click on it. The User-Agent is now copied!

![](https://cdn-images-1.medium.com/max/600/1*uNURAZo2mF2CDUNr_n8obg.png)

Now head over to [CyberChef](https://gchq.github.io/CyberChef/), time to work some magic. In the _Input_ field, paste the _User-Agent String._ Under _Operations_ drag and drop _From Base64_ into the _Recipe_ field.

![](https://cdn-images-1.medium.com/max/600/1*Ckq5ImMSoh1TANq9qq0Wvg.png)

As we can see we have some extra info that we don’t need. Remove all the characters starting at the `$` and ending at `Base64/`. Then finally the `}`, at the end of the _User-Agent String_. You should be left with the _Base64 String_.

![](https://cdn-images-1.medium.com/max/600/1*uNGW3sFVWR4za85SBg8M5w.png)

You should now be able to see the IP address in the _Output_ field, with the rest of the command from the _Base64 String_. But we need it to be defanged for the answer. To do this we need to search _defang IP_ in the search field under _Operations_. After typing _defang IP_, you should see it at the top of the list/under the search field. Drag and drop it over into the _Recipe_ field.

![](https://cdn-images-1.medium.com/max/600/1*H2DAt6QRgpX25VqMd1xF6w.png)

You will now see the defanged IP in the _Output_ field. Higlight the defanged IP, then copy (ctrl+c) and paste(ctrl+v) into the TryHackMe answer field. Then click _Submit_.

![](https://cdn-images-1.medium.com/max/600/1*5c8oyBQWzPXSzMvB9zCX6w.png)

**Answer: 62[.]210[.]130[.]250**

  

----------

## Task 8 Encrypted Protocol Analysis: Decrypting HTTPS

### **Decrypting HTTPS Traffic**

When investigating web traffic, analysts often run across encrypted traffic. This is caused by using the Hypertext Transfer Protocol Secure (HTTPS) protocol for enhanced security against spoofing, sniffing and intercepting attacks. HTTPS uses TLS protocol to encrypt communications, so it is impossible to decrypt the traffic and view the transferred data without having the encryption/decryption key pairs. As this protocol provides a good level of security for transmitting sensitive data, attackers and malicious websites also use HTTPS. Therefore, a security analyst should know how to use key files to decrypt encrypted traffic and investigate the traffic activity.

The packets will appear in different colours as the HTTP traffic is encrypted. Also, protocol and info details (actual URL address and data returned from the server) will not be fully visible. The first image below shows the HTTP packets encrypted with the TLS protocol. The second and third images demonstrate filtering HTTP packets without using a key log file.

**Additional information for HTTPS :**

![](https://cdn-images-1.medium.com/max/600/1*TaE4QHIQHyNJxlua1U_dxw.png)

![](https://cdn-images-1.medium.com/max/600/0*0osmQ1c3V7bjhzLa.png)

Similar to the TCP three-way handshake process, the TLS protocol has its handshake process. The first two steps contain “Client Hello” and “Server Hello” messages. The given filters show the initial hello packets in a capture file. These filters are helpful to spot which IP addresses are involved in the TLS handshake.

-   Client Hello: `(http.request or tls.handshake.type == 1) and !(ssdp)`
-   Server Hello:`(http.request or tls.handshake.type == 2) and !(ssdp)`

![](https://cdn-images-1.medium.com/max/600/0*Sr5VIEM8-28O5jM_.png)

An encryption key log file is a text file that contains unique key pairs to decrypt the encrypted traffic session. These key pairs are automatically created (per session) when a connection is established with an SSL/TLS-enabled webpage. As these processes are all accomplished in the browser, you need to configure your system and use a suitable browser (Chrome and Firefox support this) to save these values as a key log file. To do this, you will need to set up an environment variable and create the SSLKEYLOGFILE, and the browser will dump the keys to this file as you browse the web. SSL/TLS key pairs are created per session at the connection time, so it is important to dump the keys during the traffic capture. Otherwise, it is not possible to create/generate a suitable key log file to decrypt captured traffic. You can use the “right-click” menu or **“Edit → Preferences → Protocols → TLS”** menu to add/remove key log files.

**Adding key log files with the “right-click” menu:**

![](https://cdn-images-1.medium.com/max/600/0*C6vOmCduhClapnpF.png)

**Adding key log files with the “Edit → Preferences → Protocols → TLS” menu:**

![](https://cdn-images-1.medium.com/max/600/0*bxxgNqe9HUBIemd-.png)

**Viewing the traffic with/without the key log files:**

![](https://cdn-images-1.medium.com/max/600/0*ei-8xDYj3UX4lR2j.png)

The above image shows that the traffic details are visible after using the key log file. Note that the packet details and bytes pane provides the data in different formats for investigation. Decompressed header info and HTTP2 packet details are available after decrypting the traffic. Depending on the packet details, you can also have the following data formats:

-   Frame
-   Decrypted TLS
-   Decompressed Header
-   Reassembled TCP
-   Reassembled SSL

Detecting suspicious activities in chunked files is easy and a great way to learn how to focus on the details. **Now use the exercise files to put your skills into practice against a single capture file and answer the questions below!**

## Answer the questions below

### **Use the “Desktop/exercise-pcaps/https/Exercise.pcap” file.**

Going back to the folder where the pcapng file is located. Click on the _Back_ button in the upper left of the dns-icmp folder’s window.

![](https://cdn-images-1.medium.com/max/600/1*h1tK-SGXJphUvGqDoTN16g.png)

Now being in the exercise-pcaps folder, double-click on _https_ folder to open it.

![](https://cdn-images-1.medium.com/max/600/1*pT1f7WdlhX9QASe1FQD6Kg.png)

Now being inside the ftp folder, right-click on the _Exercise.pcapng_ file. From the drop-down menu, click on _Open With Wireshark_.

![](https://cdn-images-1.medium.com/max/600/1*WLGfLt3kB2_T5w3dmJCt_w.png)

  

### What is the frame number of the “Client Hello” message sent to “accounts.google.com”?

Reading through the materials above. TryHackMe gave us a great start with a filter that will get us only the _Client Hello_.

![](https://cdn-images-1.medium.com/max/600/1*CFzEXYYRrr0l1wLZnLrP5w.png)

Copy and Paste or type the filter for _Client Hello_ into the mint green filter bar. Once entered in the filter bar press enter to run the filter.

![](https://cdn-images-1.medium.com/max/600/1*5tBHxJFBZ_oq30NCE1TwZg.png)

Now we are only left with the _Client Hello_ packets. We need to find the one that was sent to _accounts.google.com_. If we look at the hex dump of the packet. We can see the word _google_ in it. Click on _google_ in the hexdump to expand upon it in the _Packet Detail_ section.

![](https://cdn-images-1.medium.com/max/600/1*_uAxqFhSGymN7MhTQHsjKg.png)

In the _Packet Detail_ section you will see _Server Name: clientservices.googleapis.com_ highlighted. This isn’t the server we are looking for, but it will help us to locate the _accounts.google.com_. We first need to right-click on _Server Name: clientservices.googleapis.com_. This will bring up a drop-down menu. Move your cursor over the _Apply as Filter_. A new drop-down will appear, move your cursor over to _Selected_ and click on it.

![](https://cdn-images-1.medium.com/max/600/1*AsOm69AhrQra4lVFoNO0VA.png)

Looking at the mint green filter bar, we can see the new filter we ran. But as I said before, _clientservices.googleapis.com_ is not the _Name Server_ we are looking for. So let’s change that! Remove _clientservices.googleapis.com_ and replace it with _accounts.google.com_. Once you have it replaced, press enter to run the new/updated filter.

![](https://cdn-images-1.medium.com/max/600/1*-aiC1gSNgnifF1mKlrhxeQ.png)

![](https://cdn-images-1.medium.com/max/600/1*FqGyvLflsWwfuNTKqd0ChA.png)

You will be left with one packet left. Look at the _Packet Number_ from the first column. Once you see it type the answer into the TryHackMe answer field, then click submit.

![](https://cdn-images-1.medium.com/max/600/1*jGaptD88B3BNRxjQwQVlKg.png)

**Answer: 16**

  

### Decrypt the traffic with the “KeysLogFile.txt” file. What is the number of HTTP2 packets?

First let’s decrypt the traffic. To do so click _Edit_ in the top left of Wireshark. From the drop-down menu, move your cursor to the bottom where it say _Preferences_ and click on it.

![](https://cdn-images-1.medium.com/max/600/1*Rj30PVpobDB-pmvfEWmveg.png)

The Wireshark Preference window will pop-up in the middle of the screen. Find _Protocols_, click the down carot that is on the left.

![](https://cdn-images-1.medium.com/max/600/1*HoYq6J-STR6sXntPoebveA.png)

Now either scroll down till you see _TLS_ or type _TLS_ quickly to be taken to it.

![](https://cdn-images-1.medium.com/max/600/1*WWzXNxLlbVCm4jmKAZs83g.png)

Look for _(Pre)-Master-Secret log filename_, you will see a field under with a _Browse…_ button to the right. Click on this _Browse…_ button.

![](https://cdn-images-1.medium.com/max/600/1*Ghn9-DcZO-QB3hVEUus1bg.png)

A File Explorer Window will pop-up. If you remember, when we opened the PCAP file, there was another file in the folder. This file is _KeysLogFile.txt_, and the file we are looking for. So we need to navigate to this file. To do so follow the path of _Desktop > exercist-pcaps > https_. Once in the folderwe see the _KeysLogFile.txt._

![](https://cdn-images-1.medium.com/max/600/1*qBL53W7CfQfxUtdyTbKjQA.png)

![](https://cdn-images-1.medium.com/max/600/1*u7Ar1myOSdvc8qJZr0W19g.png)

To select the file, either _double-click_ on _KeysLogFile.txt_. Or click on _KeysLogFile.txt_ then click on the _Open_ button in the bottom right of the File Explorer Window.

![](https://cdn-images-1.medium.com/max/600/1*9wI_3Mt_hGSq1h3fboaohA.png)

You will be brought back to the Wireshark Preferences window. We can now see that the file along with the absolute path is in the _(Pre)-Master-Secret Log Filename_ field. Next you can click the _Ok_ button in the bottom right of the Wireshark Prefernces window.

![](https://cdn-images-1.medium.com/max/600/1*VXCUtr7VJ7sDxeUo2SxAuQ.png)

Since the question is looking for the number of packets that are _http2 protocol_. Then we need to filter for _http2_, which is quiet simple as the filter is _http2_. Type this into the mint green filter bar, then press enter to run.

![](https://cdn-images-1.medium.com/max/600/1*3bCMVBfVit76dGy-YDMBUQ.png)

Looking to the bottom right of the Wireshark window you will see the word _Displayed_. The number to the right of this is the number and _http2_ packets and thus the answer to this question. Once you found it type the answer into the TryHackMe answer field, and click the _Submit_ button.

![](https://cdn-images-1.medium.com/max/600/1*TzXla2-ZxhhqfPpoNyEdJA.png)

**Answer: 115**

  

### Go to Frame 322. What is the authority header of the HTTP2 packet? (Enter the address in defanged format.)

Keeping the filter from the previous question, let’s elaborate on it. Since we want to see _Frame 322_, we can add to our filter the following. Start with _and_ as we want the filter to match both _http2_ along with our frame number. Then we will add _frame.number == 322_, which is looking for _Frame 322_. Once we have our filter build, press enter to run it.

![](https://cdn-images-1.medium.com/max/600/1*B_QH8ZoLijrFf9PjBN849Q.png)

Looking in the _Packet Details_ section, look for _HyperText Transfer Protocol_. Once you find it click the _carot_ to the left of it to drop-down more information. You will see a new line, and thats it. But we can drop-down some more. So click the _carot_ to the left of _Stream:_ to discover more information. Now we can scroll down till we see the _Header: :authority:_ field.

![](https://cdn-images-1.medium.com/max/600/1*mzKbVeOITA657GK7g9a_AA.png)

Once we see the _Header: :authority:_ field, we can see the domain name. But the question is asking for the domain to be defanged. So we need to grab the domain. To do this _right-click_ on _Header: :authority:_ field. A drop-down menu will appear, hover your cursor over _Copy_. A new drop-down will appear. Move your cursor over to _Description_, then click on it. You now have what you need, time to head over to [CyberChef](https://gchq.github.io/CyberChef/).

![](https://cdn-images-1.medium.com/max/600/1*OKd9x6ZeHnLE7_TWrHkIgQ.png)

Once at CyberChef, type _defang_ in the input field under _Operations_. The top result will be _Defang URL_. Drag and drop _Defang URL_ into the _Recipe_ area.

![](https://cdn-images-1.medium.com/max/600/1*miJYgW7yaDInFpMkwYXEzg.png)

Now paste in the _Description/Domain_ we copied from WireShark. CyberChef should automatically defang the URL which you will see in the _Output_ field. Now Copy and Paste the defanged URL into the TryHackMe answer field, then click the _Submit_ button.

![](https://cdn-images-1.medium.com/max/600/1*OQCmfrSMdm8xj5vA3FlBbg.png)

**Answer: safebrowsing[.]googleapis[.]com**

  

### Investigate the decrypted packets and find the flag! What is the flag?

Time to use our investigation skills we have learned so far. Since we are looking at _http_ traffic, the first place I like to look is _Export Objects_. _Export Objects_ is where you can export/save files that were captured in the PCAP file. To do this first click on _File_ in the top right of the Wireshark window. On the drop-down menu, move your cursor to hover over _Export Objects_. A new drop-down will appear. On this drop-down you will see _HTTP…_, click on _HTTP…_

![](https://cdn-images-1.medium.com/max/600/1*yZC98rI4K6U44GWM70T6tw.png)

We can see two files that were captured from the HTTP Protocol. The first one has an interesting _Filename_, let’s check it out. To do this click on the first row with the interesting _Filename_. Then click the _Save_ button in the bottom right of the Wireshark Export HTTP object list.

![](https://cdn-images-1.medium.com/max/600/1*yZh8-hjX6giQ6qLVT6WumA.png)

The Wireshark Save Object As… window will popup. On the left side of this window we can see _Desktop_, click on _Desktop_. Now click the _Save_ button in the bottom right of the window.

![](https://cdn-images-1.medium.com/max/600/1*JWqAGnF71Y_-gCRDr_gBqw.png)

The file is now saved to the Desktop, so let’s head there. First _X_ out of the Wireshark Export HTTP object list window. Then _Minimize_ the Wireshark window.

![](https://cdn-images-1.medium.com/max/600/1*3u3W8H3osHehuyJtIJ6-iA.png)

We can now see the new file on the desktop. Let’s open it by double-clicking on the new file on the desktop.

![](https://cdn-images-1.medium.com/max/600/1*rCZxvyJfiqbppymcuFgbxw.png)

Once the file opens, we are greeted with some sweet ASCII art and what looks like the flag!! Highlight and copy the flag, then paste the answer in the TryHackMe answer field, and click the _Submit_ button.

![](https://cdn-images-1.medium.com/max/600/1*kaw0iBmTAYMhs9xe1rADJQ.png)

**Answer: FLAG{THM-PACKETMASTER}**

  

## You have finished these tasks and can now move on to Task 9 Bonus: Hunt Cleartext Credentials!, Task 10 Bonus: Actionable Results!, and Task 11 Conclusion.