---
layout: "post"
title: "KC7 Module: A Scandal in Valdoria: Section 1 KQL 101"
categories: KC7
tags: KC7, KQL, Scandal in Valdoria, KQL 101
---

----------

Here is the link to the Module: [A Scandal in Valdoria 🌟](https://kc7cyber.com/challenges/132)

### Breakdown

The module is broken up into four different sections: KQL 101, Welcome to Valdoria!, Plenty of Phish, and A Scandal. In the write-up we will be focusing on the first section, KQL 101. As you work you way through the questions each should build onto each other. Example being, you may discover an IP address in one question that leads you to investigate it for several other questions. Additionally, KC7 also provides an [amazing resource](https://kc7cyber.com/guide/132) for this room, which I just linked.

### Run on your own

While you can use the KC7 ADX (Azure Data Explorer) provided. You are able to run them yourself using your own ADX. The way to do this is to click the _Query Data (ADX)_ at the top of the ADX panes.

![](https://cdn-images-1.medium.com/max/720/1*DsBrVTpKnltrwcFayj9Fyg.png)

From here you will need to either use your Microsoft account or create a new Microsoft account. Once you get logged in you will be brought to your own ADX. You will have a pop-up asking if you trust the KC7 data that is trying to be added to your ADX. Click _Trust_, and the _kc7001.eastus_ data will be added to your ADX.

![](https://cdn-images-1.medium.com/max/720/1*1bu8Vz1dQKODy7XsImw0Iw.png)

We need to expand and select the correct data, so we can be able to investigate. First click on the carat to the left of _kc7001.eastus_, which will drop down the different data correlating to each module. Then scroll down till you see _ValdyTimes_.

![](https://cdn-images-1.medium.com/max/720/1*Y-0dPsWgEhzmC50lt0NveQ.png)

Once you see _ValdyTimes_, click on it to load the data. Additionally, you can click on the carat, which will drop down the different tables we will be able to use during this module.

![](https://cdn-images-1.medium.com/max/720/1*uuNtKxT6EQps7D7MVEZzTw.png)

### The Reason why

The purpose of these modules is to help you learn how to investigate. They do this by laying the ground work and fundamentals needed to understand why you are looking. Join me as I go through the room. But please note, I may not share all the questions in this write up, only the ones pretendant to the investigation. I will be including the answers to the questions as well. But please know, while the answers may change, the way that you get them should remain the same. Now, let’s get started!!!

### Section 1: KQL 101

#### Learning about Valdoria and the Scandal

> Welcome to Valdoria!
>
> On the eve of the election, Nene Leaks, the esteemed editor of The Valdorian Times, awoke to a nightmare. The Valdorian Times, the beacon of truth for the city, published a scandalous article accusing Luffy of corruption and misconduct. The article, a vile concoction of lies, was not what she had approved.
>
> The article alleged that Luffy, hailed for his environmental activism and social reforms, was secretly involved in a land deal scandal, exploiting his position to benefit a shadowy network of real estate moguls. Furthermore, it accused Luffy of accepting substantial bribes to push environmentally damaging policies, a stark contradiction to his public persona.
>
> However, the article, a vile concoction of lies, was not what had been approved by the newspaper’s editor 😵.
>
> The Valdorian Times has hired you as a cyber incident responder to help investigate the incident and get to the bottom of how the falsified article was published.

### Familiarize yourself

Before starting any investigation, you should be familiar with the information at hand. You need to know what you do and don’t have access to. In our case, the tables that are present in the picture below, we are able to use. As explained above in the _Run on your own_ section, we can easily see the tables in our ADX.

![](https://cdn-images-1.medium.com/max/720/1*vOwhp47vjzWWZGMmHAqL7Q.png)

Knowing these tables will help us to better understand where we need to go to get the information during our investigation. I would also suggest that as you gather new information, that you keep it stored somewhere. For me I am using Notion to write/type this down, and created a Database to store the information gathered. Here it what we know so far:

**Nene Leaks**

-   Editor at the Valdorian Times
-   Claims she didn’t approve of the article written about Luffy Monk, that was printed on January 20, 2024

  

**Luffy Monk**

-   Mayoral candidate
-   Environmental Advocate

  

**Erik Stevens**

-   Current Mayor
-   Platform aligns more with business and rapid expansion

### How many employees work at the Valdorian Times?

Heading over to our _Query Pane_, we know that the table we want to start looking at is _Employees._ From there we can use the _count_ function to give us the number of records in the _Employees_ table. In the Query Pane, type:
```
Employees  
| count
```
Then click the blue _Run_ button in the top left of the query pane (I am show this one, but won’t be from here on out).

![](https://cdn-images-1.medium.com/max/720/1*pGqz41USYP4PMMRRcZsgcQ.png)

In the _Results Pane_ at the bottom, only one column will appear. In the Count Column will be the answer. Type it into the _Answer box_ and click _Submit_.

![](https://cdn-images-1.medium.com/max/720/1*91iCUnVoCu_Op2oCdYDZkw.png)

_ANSWER: 100_

----------

### What is the Editorial Director’s name?

Again, sticking with the _Employees_ table. We know from the question, that the _role_ of the person is _Editorial Director_. With this information, we can craft the query where we are looking at the _Employees_ table. Then from that table we only want to see which Employee’s have the role of _Editorial Director_. If they do, it will show us the result’s in the _Results Pane_. Our query should look like the following:
```
Employees  
| where role == "Editorial Director"
```
Once typed into the _Query Pane_, press the blue _Run_ button in the top left. There will be only one result in the _Result Pane_. On said result, look for the _name_ column. The Employee’s name will be listed under here. We can either type the name into the _Answer Box_ or _right-click_ and choose _copy_, then _paste_ the answer into the _Answer Box_. Then click _Submit_.

![](https://cdn-images-1.medium.com/max/720/1*XpVvl__tkZ_mx9SzGuzNVg.png)

_ANSWER: Nene Leaks_

----------

### How many emails did Nene Leaks receive?

From our previous query we can also get Nene’s email address (nene_leaks@valdoriantimes(.)news). We can use this information to search the _Email_ table. To start our query, we first need to declare the table, which again is _Email_. Then we press enter to start a new line, and a pipe ( | ) should automatically get placed on the new line. If it doesn’t then type a pipe ( | ) before you start typing. From here we need to pull only Nene Leaks emails that she received. This can be done by using _where_, which will filter a table using a filter given. In our case that filter is _recipient_. We then know what Nene Leaks email address is, so our next qualifier is _contains_. Finally, we add Nene Leaks email address between double quotes ( “ ). Lastly, we need to start a new line, and again making sure the pipe ( | ) is in place. Then use the function _count_ to count the number of results. Altogther the query should look like the following:
```
Email  
| where recipient contains "nene_leaks@valdoriantimes.news"  
| count
```
Run the query in ADX, and look at the _Results Pane_ for the results. Since we used the _count_ function, there will only be one column, under which is the answer to the question. Type the answer into the _Answer Box_ then click _Submit_.

![](https://cdn-images-1.medium.com/max/720/1*LYUPYHXR4cce2JOZivyWJQ.png)

_ANSWER: 18_

----------

### How many distinct senders were seen in the email logs from the domain name “[weprinturstuff.com](http://weprinturstuff.com)”?

In our ADX we can expand the _Email_ table by clicking on the carat. This will then show the different columns of information we have access to. Amoungst them is the _Senders_ column. With this information we can now build a query to answer our question.

![](https://cdn-images-1.medium.com/max/720/1*93DOuED1kP0eW-HLMiP4gA.png)

We will be sticking with the _Email_ table. Using the similar query we used in our previous attempt, we only need to change a couple things. In this case instead of _recipients_ we will change it to _sender,_ and instead of _“nene_leaks@valdoriantimes.news”_ it will be _“_[_weprinturstuff.com_](http://weprinturstuff.com)_”_. Finally we will leave the last line the same, that being _count_. Your query should look like the one below.
```
Email  
| where sender contains "weprinturstuff.com"  
| count
```
Click the _Run_ button to search using our query. When it is finished running, you will see one column in the _Results pane_. Under that column will be the answer, type it into the _Answer Box_ and click _Submit_.

![](https://cdn-images-1.medium.com/max/720/1*_mi_cqfF8U3LSm_NhyPm_A.png)

ANSWER: 100

----------

### How many distinct websites did “Lois Lane” visit?

First we need to gather some information on _Lois Lane_. To do this we need to query up information from the _Employees_ table. The query will start with the table name, that being _Employees_. We have her name, so we can build out the query with _where name == “Lois Lane”._ The final query should look like it does in the code block below.
```
Employees  
| where name == "Lois Lane"
```
Click the blue _Run_ button. Once it has completed, we will have information regarding Lois Lane. This includes her _IP Address_. I have placed this and some of her information on the _Information Gathered_ database I created in Notion. Time to create our query to find the number of unique (distinct) websites that Lois Lane visited.

![](https://cdn-images-1.medium.com/max/720/1*4fTNu8ot7oF5Jg9nbT3HmA.png)

Looking at the different tables we have access, the one that works best for this situation is the _OutboundNetworkEvents_.

![](https://cdn-images-1.medium.com/max/720/1*vq3Ka1VvgTUU2NDXftjvJg.png)

Starting our query out with _OutboundNetworkEvents_. We we need to only show results that pertain to Lois Lanes _IP Address_. To do this we use _where src_ip == “10.10.0.22”_. Next line down we want to only see the unique (distinct) _URL_s. Finally, the last line will be _count_. If we type the query out correctly it should look like the following in the code block:
```
OutboundNetworkEvents  
| where src_ip == "10.10.0.22"  
| distinct url  
| count
```
Click the _Run_ button to search using our query. When it is finished running, you will see one column in the _Results pane_. Under that column will be the answer, type it into the _Answer Box_ and click _Submit_.

![](https://cdn-images-1.medium.com/max/720/1*a8aWlncQXBnPlhLkMqz37g.png)

_ANSWER: 62_

----------

### How many distinct domains in the PassiveDns records contain the word “hire”?

The question contains key information that will aid us in figuring out the proper query to use. Here is the keywords to focus in on: _distinct_, _domains_, _PassiveDns_, and _“hire”_. Looking at the usable tables, we can see that _PassiveDns_ is one of the tables. Meaning that we know how we will start our query, using the _PassiveDns_ table.

![](https://cdn-images-1.medium.com/max/720/1*YExmEblny-bsdN4_L8D3qA.png)

Next up we need to pull the domains. From the question we are looking for domain names that contain the word _“hire”_. So from previous queries, we should know how to pull this type of information. Using the following line: _where domain contains “hire”_. This will pull **all** the domains that contain hire, even multiple instances of them. On the next line we will take care of that using the _distinct_ function. Finally, on the last line we will use the _count_ function to count the number of unique domains. The final query should look like it does below:
```
PassiveDns  
| where domain contains "hire"  
| distinct domain  
| count
```
Click the _Run_ button to search using our query. When it is finished running, you will see one column in the _Results pane_. Under that column will be the answer, type it into the _Answer Box_ and click _Submit_.

![](https://cdn-images-1.medium.com/max/720/1*stQ4ou3lU8ddc1qiQdG0kA.png)

_ANSWER: 6_

----------

### What IPs did the domain “[jobhire.org](http://jobhire.org)” resolve to (enter any one of them)?

We will stick with the _PassiveDns_ table again for this question. From there we will are looking for the domain _“_[_jobhire.org_](http://jobhire.org)_”_. We can use the same type of query line as we have done before: _where domain == “_[_jobhire.org_](http://jobhire.org)_”_. With that we our query should look like the following:
```
PassiveDns  
| where domain == "jobhire.org"
```
Click the _Run_ button to search using our query. When it is finished running, we will see two columns. One for IP and the other for the domain. Click on the _IP Address_ and copy ( _ctrl c_ ) and paste ( _ctrl v_ ) the _IP Address_ in the _Answer Box._ Then click _Submit_

![](https://cdn-images-1.medium.com/max/720/1*r6Ru5JZ7n9cDZQOgy2q5iw.png)

_ANSWER 191.7.248.112_

----------

### How many distinct websites did employees with the first name “Mary” Visit?

For this question, we first need to find out how many people named Mary work for the Valdorian Times and get their IP addresses. Then take those IP addresses and search them against outbound connections. Finally, only showing one instance of website connected to and then counting those instances. With all that understood, let’s build our query. All the above can be done in one query!! To do this we will create a variable that will encapsulate the results from the first part of query and use it in our second. Enough talking about it let’s do it!!

To set a variable we will use _let_ followed by what we want to name our variable and the equals ( = ) symbol. I named my variable _marys_ips._ Additionally you can’t have spaces in the name of the variable, which is why I added the underscore ( _ ). Next up, we want to pull from the _Employees_ table. In the next line we will use the _where_ function and _name_ column, but this time using the _startswith_ function as well. This will take a string that we specify, and look at the _name_ column to see if it starts with that. To end this variable, we only want to show one instance of each unique IP address. This can be done using _distinct ip_addr._ Finally end the line with a semi-colon ( ; ), which will tell the query that everything to that point will be in the variable we started with.

Time for the next part of our query. The next line will be directly under the previous one, no extra spaces needed. We will be using the _OutboundNetworkEvents_ table for this part of the query. The next line down, we will use the _where_ function and _src_ip_ column. Followed by the _in_ operator and our variable within parathesis. This will take the IP addresses from the first query and only give us results pertaining to these IP addresses. Onto the next line, we will want to only have a single instance of an website visited. To show this we use the _distinct_ function with the _url_ column. Lastly, we want to count how many unique instances there were. Again, we will use the _count_ function. After all is said and done, our query should look like it does below:
```
let marys_ips =   
Employees  
| where name startswith "Mary"  
| distinct ip_addr;  
OutboundNetworkEvents  
| where src_ip in (marys_ips)  
| distinct url  
| count
```
Click the _Run_ button to search using our query. When it is finished running, you will see one column in the _Results pane_. Under that column will be the answer, type it into the _Answer Box_ and click _Submit_.

![](https://cdn-images-1.medium.com/max/720/1*0XlazWEcWt3VztCanz9iBA.png)

_ANSWER: 58_

----------

### How many authentication attempts did we see to the accounts of employees with the first name Mary?

This question seems quite similar to our previous question. The difference here though is that we are looking for _Authentication attempts_, which give us a clue for one of the tables we need to use. To be able to authenticate to a service you are going to need a piece of information, in this case it would be the usernames for the different Mary’s at Valdorian times. Let’s us get to building our query!!

The query is going to be very similar to our previous query we ran, so let’s start at the top and work our way down. Like before we are going to create a variable, I changed the variable’s name to _marys_usernames_. Ending the line with an equal ( = ). The next line will be the _Employees_ table, followed by line underneath: _where name startswith “Mary”_. Onto the next line down we make another change, instead of the ip_addr from the previous command. We will be using _distinct username_, indicating that we want the employees username. Finally ending the variable with a semi-colon ( ; ).

As I mention at the beginning of this question, we are checking for the _Authentication attempts_. Which looking at the available tables, one is named _AuthenticationEvents_. This is the table we will want to check. The next line down will have another change to it, this time being: _where username in (marys_usernames)_. Which means that we are pulling out each instance that a Mary attempted to authenticate. Lastly, we want to count these instances, which is done by using the _count_ function. When all is typed out, it should look like it does below:
```
let marys_usernames =   
Employees  
| where name startswith "Mary"  
| distinct username;  
AuthenticationEvents  
| where username in (marys_usernames)  
| count
```
Click the _Run_ button to search using our query. When it is finished running, you will see one column in the _Results pane_. Under that column will be the answer, type it into the _Answer Box_ and click _Submit_.

![](https://cdn-images-1.medium.com/max/720/1*dFgnHV7hvqrIixG5Chvz5Q.png)

_ANSWER 70_

----------

### Learning Points

This section is a great primer to get you started in the world of KQL. By this point you should know how to do the following:

-   Basic KQL query structure and syntax
-   Using the ‘where’ clause to filter results
-   Employing the ‘contains’ operator for partial string matches
-   Utilizing the ‘distinct’ function to eliminate duplicates
-   Applying the ‘count’ function to tally results
-   Creating and using variables with the ‘let’ statement
-   Chaining multiple operations in a single query
-   Querying across different tables (e.g., PassiveDns, Employees, OutboundNetworkEvents)
-   Using the ‘startswith’ function for string comparisons
-   Implementing the ‘in’ operator to check for multiple values

All the above skills are going to be vital to understanding and creating better KQL queries for log analysis in the future.

### Congrats!

Congratulations, you have completed the first section of the A Scandal in Valdoria module from KC7. Don’t stop now, there are still three more sections to complete!