---
layout: "post"
title: "KC7 Module: A Scandal in Valdoria: Section 2 Welcome to Valdoria!"
categories: KC7
tags: KC7, KQL, Scandal in Valdoria, KQL 101
---

----------

Here is the link to the Module: [A Scandal in Valdoria 🌟](https://kc7cyber.com/challenges/132)

## Before you start

Before continuing with this write-up. If you haven’t already completed or checked out the write-up on [Section 1 KQL 101](https://haircutfish.com/posts/A-Scandal-in-Valdoria-Section-1-KQL-101/). Please go back and do so. As these modules work best if you start at the beginning and work your way through. They help you to fully understand how to properly investigate and lay the ground work to be able to know what you are looking for. Also, as you go through each question, they can build off each other. Meaning an answer you get from one question, could be information you will use in another questions query. As in my prior write-up, I may not share all the questions in this write up, only the ones pretendant to the investigation. I will be including the answers to the questions though. But please know, while the answers may change, the way that you get them should remain the same.

## Take notes

As you proceed through the modules, it is imperative that you take notes of key information that you find. It is far easier to go through and grab the information you have saved, then to have to re-run queries to get it again. Additionally, in an investigation, it helps you to have that information on hand to be able to piece together what is happening. For me I am taking my notes in Notion, using a database to keep the key pieces of information accessible. But that may not be the way you do it, and that is ok. Take the notes the way that best suits you and your thinking.

## Section 2: Welcome to Valdoria!

**Now we’re starting with the investigation!**

> As a first step, you reach out to the Editorial Director `Nene Leaks` to ask for more information:

![](https://cdn-images-1.medium.com/max/720/1*GSH3XYtH6t4BnkPo-ngVgQ.jpeg)

## **What is the Newspaper Printer’s name?**

Reading through the above text message, you should easily be able to find the name of the Newspaper Printer. Once you do you can type it into the _Answer Box_, and click _Submit_.

For my notes, I ran the following query:
```
Employees  
| where name == "Clark Kent"
```
This query looks in the _Employees_ table under the _name_ column for the name _Clark Kent_. In the results I gathered the username, IP address, and email for my notes. In case I will be coming back to Clark or need his information in future queries.

----------

> Next, you talk with `Clark Kent`. He seems very distressed about the whole situation. 😓 He tells you he simply printed the article that was emailed to him, as he always does.
>
> He tells you he thinks the Editorial Intern was the one who sent him the final draft of the article.

## **What is the Editorial Intern’s name?**

We need to begin our query in the _Employees_ table. Then on the next line down, we will use the _where_ operator along with the _role_ column. Finishing up the line with double equals ( == ) and _“Editorial Intern”_. This query will search in the _Employee_ table, under the _role_ column for any instances of _“Editorial Intern”_. If it’s found, it will place the results in the _Results Pane._ Below is what our query should look like:
```
Employees  
| where role == "Editorial Intern"
```
Press the blue _Run_ button in the top left of the ADX. In the _Result Pane_, one entry will be found. Click on the name and copy the information by pressing _ctrl c_. Then paste ( _ctrl v )_ the information into the _Answer Box_ and press _Submit_.

![](https://cdn-images-1.medium.com/max/720/1*AWmzmE0FxxeAtfi6oP0lRw.png)

_ANSWER: Ronnnie McLovin_

----------

## **When was the Editorial Intern hired at The Valdorian Times?**

Heading back to the _Result Pane_, we can see that there is a _hire_date_ column. Under which is the date that Ronnie was hired. Click on the timestamp and copy the information by pressing _ctrl c_. Then paste ( _ctrl v )_ the information into the _Answer Box_ and press _Submit_.

![](https://cdn-images-1.medium.com/max/720/1*8d8Wd5o2GVE6bGUTia-pdA.png)

_ANSWER: 2024–01–02T08:00:00Z_

----------

> You contact `Ronnie McLovin` to ask more about the article. At this point, you haven't ruled out the possibility of an [insider threat](https://www.ibm.com/topics/insider-threats) 🕵️, so it's important that you get multiple perspectives of the situation from multiple individuals.
>
> `Ronnie` tells you she was in charge of the OpEd piece about the mayoral candidates, and she was supposed to send the final draft to `Clark Kent` for printing the night before publication. However, she overslept 😴, and never actually sent the article.
>
> You go back to `Clark Kent` with this information, but he is certain that the final draft came in an email from `Ronnie McLovin`. He says he received the email on `January 31, 2024`.

## **How many total emails has Clark Kent received?**

We are given a lot of really great information above. But what we need to focus on for this question, is how many emails Clark Kent received. We will start with the _Email_ table. On the next line, we will use the operator _where_ and the column we are filtering for is _recipient_. From there if you took notes and have Clark Kent’s email address, we will use a double equal ( == ) and Clark’s email address. Last line will be the _count_ operator, make our query look like it does below:
```
Email  
| where recipient == "clark_kent@valdoriantimes.news"  
| count
```
Once it is typed into the _Query Pane_, press the blue _Run_ button. The results will be found in the _Result Pane_ under the one and only column. Type the answer into the _Answer Box_, and click _Submit_.

![](https://cdn-images-1.medium.com/max/720/1*lZ2ygltNExDGrf5rtA-CEw.png)

_ANSWER: 21_

----------

> Review the emails sent to `Clark Kent` for the one sent on **January 31, 2024** containing the final edits for the election OpEd.

## **What was the subject line of this email?**

We are going to use most of the previous query with some tweaking. The first two lines will remain the same, that being the _Email_ table and then _where recipient_ lines. Then we will remove the _count_ operator. We will need to now search for the time in question. We can do this by using the _where_ operator, but this time using the _timestamp_ column. Next using the _between_ operator, we will be looking at a time range since we know that it was received on _January 31, 2024._ The syntax needs to be like the following `datetime(YYYY-MM-DDTHH:MM:SSZ)` , the _T_ and _Z_ do not change. That syntax will be between parenthesis ( ), with two periods in the middle. On paper it sounds confusing, so it’s best just to show : `where timestamp between (datetime(2024–01–31T00:00:00Z) .. datetime(2024–02–01T00:00:00Z))` . The finished query should look like the following:
```
Email  
| where recipient == "clark_kent@valdoriantimes.news"  
| where timestamp between (datetime(2024-01-31T00:00:00Z) .. datetime(2024-02-01T00:00:00Z))
```
Once it is typed into the _Query Pane_, press the blue _Run_ button. The results will be found in the _Result Pane_, you will first need to scroll to the right. When you see the _subject_ column, click on the result then copy ( _ctrl c_ ) and then paste ( _ctrl v_ ) the answer into the _Answer Box._ Then click _Submit_.

![](https://cdn-images-1.medium.com/max/720/1*GXztruz0D7sKHjCX0281tw.png)

_ANSWURGENT: Final OpEd Draft Edits (Please publish the following article in tomorrow’s paper))_

----------

> Who sent this email containing the final edits for the OpEd piece?

## **Enter the sender’s email address.**

Head back to the _Results Pane_, and scroll back to the left until you see the _sender_ column. When you see the _sender_ column, click on the result then copy ( _ctrl c_ ) and then paste ( _ctrl v_ ) the answer into the _Answer Box._ Then click _Submit_.

![](https://cdn-images-1.medium.com/max/720/1*MBskn4TmDXYI08bb37wy1g.png)

_ANSWER: ronnie_mclovin@valdoriantimes.news_

----------

## **What was the name of the .docx file that was sent in this email?**

Heading back to our _Result_s again, this time we will click on the carat located on the left side of the result. This will drop down all the information to easily be seen. The last result is the link to a sharepoint, the end of the link indicates the file that was sent. Highlight and copy ( _ctrl c_ ) and paste ( _ctrl v_ ) the name of the file in the _Answer Box_, then click _Submit._

![](https://cdn-images-1.medium.com/max/720/1*WcgYqjeRkG3Ut0ZDf_sN2Q.png)

_ANSWER:_ OpEdFinal_to_print.docx

----------

> So, it looks like Ronnie did send the email. When you go back and talk to Ronnie, she is adamant that she never sent the draft. She thinks maybe someone else used her account to send it.
>
> She doesn’t recall getting any unusual emails or any other weird activity on her computer.

The question asks if we should investigate this further. The answer is of course YES!! If someone claims that they didn’t send an email, but you have proof that it came from their email. More investigation needs to be done to see if their email may have gotten compromised.

----------

## Information gathered thus far

After texting Nene Leaks, she told us to reach out to Clark Kent the Newspaper Printer. From a discussion with Clark, he only printed the article that was emailed to him. We dug into the logs to find out that the Editorial Intern is Ronnie McLovin. Investigating the email logs revealed that an email was sent from Ronnie to Clark on January 31st. Said email contained a file named OpEdFinal_to_print.docx. Talking with Ronnie, she admits that she never sent that email. Which means that her account may have been compromised. To which we will now look into this possibility.

![](https://cdn-images-1.medium.com/max/720/1*XdPHdIouCZ_zCF3YXjwp0Q.png)

## Done already?!

With that you have completed the second section of the scandal in Valdoria. In this section we learned the following:

-   Reinforcing the basics of KQL
-   Understanding the beginning methodology to investigating and incident
-   Taking notes of key information (As long as you took notes)

### Let’s continue this amazing journey into Section 3: Plenty of Phish.