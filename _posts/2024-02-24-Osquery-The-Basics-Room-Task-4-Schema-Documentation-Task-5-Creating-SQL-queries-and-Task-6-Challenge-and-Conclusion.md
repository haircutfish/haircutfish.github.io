---
layout: "post"
title: "TryHackMe Osquery: The Basics Room — Task 4 Schema Documentation, Task 5 Creating SQL queries, and Task 6 Challenge and Conclusion"
categories: OSquery
tags: TryHackMe, OSquery, SOC Level One Path
---

_If you haven’t done tasks 1 through 3 yet, here is the link to my write-up of them: [Task 1 Introduction, Task 2 Connect with the Lab, and Task 3 Osquery: Interactive Mode](https://haircutfish.com/posts/Osquery-The-Basics-Room-Task-1-Introduction-Task-2-Connect-with-the-Lab-and-Task-3-Osquery-Interactive-Mode/)_

## Task 4 Schema Documentation

For this task, go to the schema [documentation](https://osquery.io/schema/5.5.1/) of Osquery version 5.5.1, the latest version. The schema documentation looks like the image shown below:

![](https://cdn-images-1.medium.com/max/720/0*71pxAJ5-qUrCBOy5.png)

### Breakdown

Let’s break down the important information we could find in this schema documentation:

1.  A dropdown lists various versions of Osquery. Choose the version of Osquery you wish to see schema tables for.
2.  The number of tables within the selected version of Osquery. (In the above image, 106 tables are available).
3.  The list of tables is listed in alphabetical order for the selected version of Osquery. This is the same result we get when we use the `.table` command in the interactive mode.
4.  The name of the table and a brief description.
5.  A detailed chart showing each table’s **column**, **type**, and **description**.
6.  Information to which Operating System the table applies. (In the above image, the **account_policy_data** table is available only for **macOS**)
7.  A dropdown menu to select the Operating System of choice. We can choose multiple Operating Systems, which will display the tables available for those Operating systems.

![](https://cdn-images-1.medium.com/max/720/0*zE2NY4__yhGcuoQf.png)

You have enough information to navigate this resource to retrieve any necessary information confidently.

## Answer the questions below

To be able to answer these questions. You need to click the _documentation_ link at the top of this task. This will take you to the OSquery Schema Documentation site. This is where you will find the answer for the following questions.

![](https://cdn-images-1.medium.com/max/720/1*mEsaZTvHfbPFckO1mYtl8g.png)

![](https://cdn-images-1.medium.com/max/720/1*9hc9AM8eVpgC_6uS055nUw.png)

### In Osquery version 5.5.1, how many common tables are returned, when we select both Linux and Window Operating system?

Look for _Show only Tables compatible with:_, to the right of this is a carot. Click on the blue circle carot, a drop-down will appear. In the drop-down menu, click on _Linux_ and _Windows_.

![](https://cdn-images-1.medium.com/max/720/1*WdjmOuPuG8EjXmtLQKYerA.png)

In the upper right corner of the page, under the OSquery logo. Is a blue box with the work _Tables_ to the right. The number in this box is the answer. Type it into the TryHackMe answer field, and then click the _Submit_ button.

![](https://cdn-images-1.medium.com/max/720/1*Yl_uHgJ_NeCzIdcFj4jQfg.png)

  

**Answer: 56**

  

### In Osquery version 5.5.1, how many tables for MAC OS are available?

Going back to the _Show only Tables compatible with:_ drop-down menu, click on _MacOS_ to _Check/Select_ it. Then _Uncheck/Deselect_ _Linux_ and _Windows_.

![](https://cdn-images-1.medium.com/max/720/1*cRqMbhN_GutSKZKQ82UCiw.png)

In the upper right corner of the page, under the OSquery logo. Is a blue box with the work _Tables_ to the right. The number in this box is the answer. Type it into the TryHackMe answer field, and then click the _Submit_ button.

![](https://cdn-images-1.medium.com/max/720/1*fOKQNJqsJD4S6HsoUs11Ww.png)

**Answer: 180**

  

### In the Windows Operating system, which table is used to display the installed programs?

Going back to the _Show only Tables compatible with:_ drop-down menu. Click on _Windows_ to _Check/Select_ it, and _Uncheck/Deselect_ _MacOS._

![](https://cdn-images-1.medium.com/max/720/1*-Ak4vEq4_mwL39MhK2_DsA.png)

Since we are looking for the table that displays installed programs. Let’s start by looking for the word _program_. We can do use by using the find feature in most browsers. To open this use the keyboard shortcut _ctrl + f_, you should see a search field drop down from under the address or bookmark bar. In this field type _program_. We can see that we have 6 hits, the first one highlighted is a table called _Programs_. Click on it to be taken to that tables Schema. It will let us see what this table does.

![](https://cdn-images-1.medium.com/max/720/1*dnswLtyzVDkIM_46-xD2-g.png)

Reading through the description, it states:

> Represents products as they are installed by Windows Installer

We have found the correct table! Type the name into the TryHackMe answer field, then click the _Submit_ button.

![](https://cdn-images-1.medium.com/max/720/1*yynrXiEEuKtx1XA4SAi0Qg.png)

**Answer: programs**

  

### In Windows Operating system, which column contains the registry value within the registry table?

Let’s start by typing _registry_ into the Find Field. We get 22 hits, but the first one is for a _Table_ called _registry_. Click on the _registry_ to be taken to the Schema regarding the Windows Registry.

![](https://cdn-images-1.medium.com/max/720/1*qnJuq1PUOzP44JYPD_e4-A.png)

Reading through the _DESCRIPTION_s on the _registry_ Schema Table. One is descibed as _content of registry value._ Sounds like the one we are looking for. Moving to the left till you get to the _COLUMN_ column, and look at the name. This is the answer we are looking for. Type it into the TryHackMe answer field, then click the _Submit_ button.

![](https://cdn-images-1.medium.com/max/720/1*Vikpy_UdkMuyRmAzyMrRmw.png)

**Answer: data**

  

----------

## Before we begin Task 5

_If you already have the machine up and running, and OSqueryi started in PowerShell. Skip down to Task 5_

We need to get the VM up and running. Start by clicking on the green _Start Machine Button_ at the top of Task 2.

![](https://cdn-images-1.medium.com/max/720/1*8pLDErQor61K0N8unOoFBQ.png)

Scroll to the top of the webpage. Once at the top, look for the blue box labeled _Show Split View_. When you find it, click on it.

![](https://cdn-images-1.medium.com/max/720/1*NkPh5bkLwmluXT07apTAkg.png)

The Screen will split, and you will have to wait till the machine loads. It may take a couple of minutes.

![](https://cdn-images-1.medium.com/max/720/1*PARPQ2LVb5W2UxT6OwTJSw.png)

Once the machine is fully loaded and ready. Click on the _expanding arrows_ located in the bottom left corner of the machine’s window. This will open the VM in a new Tab and give you a _Full Screen View_.

![](https://cdn-images-1.medium.com/max/720/1*sWFPTcvRlOvW_j6FByCfng.png)

![](https://cdn-images-1.medium.com/max/720/1*wExZRCMdhZmf7oi9bK-Nqw.png)

Once the new tab is loaded, go back to your TryHackMe window with the _Split View_. You can now click on the `-`(_minus symbol_) located in the bottom right split window. This will exit split view and give your TryHackMe Task window the full window use again.

![](https://cdn-images-1.medium.com/max/720/1*wxo0gQpW7AzHFfbb-ikr7Q.png)

Heading back over to the VM Tab. We need to start _PowerShell_. We can do this by clicking on the _PowerShell_ icon located on the taskbar at the bottom of the desktop.

![](https://cdn-images-1.medium.com/max/720/1*FWZIjmpCaWO-GSfUF03aLw.png)

In the _PowerShell_ window type `osqueryi`, and press enter to run the command. Give it a couple of seconds and then you are greeted with the _osquery>_ prompt. Meaning you are ready to start running OSQuery commands.

![](https://cdn-images-1.medium.com/max/720/1*NCan8JZw8OEFcvthsYek9w.png)

----------

## Task 5 Creating SQL queries

The SQL language implemented in Osquery is not an entire SQL language that you might be accustomed to, but rather it’s a superset of SQLite.

Realistically all your queries will start with a **SELECT** statement. This makes sense because, with Osquery, you are only querying information on an endpoint. You won’t be updating or deleting any information/data on the endpoint.

**The exception to the rule**: Using other SQL statements, such as **UPDATE** and **DELETE,** is possible, but only if you’re creating run-time tables (views) or using an extension if the extension supports them.

Your queries will also include a **FROM** clause and end with a **semicolon**.

### Exploring Installed Programs

If you wish to retrieve all the information about the installed programs on the endpoint, first understand the table schema either using the `.schema programs` command in the interactive mode or use the documentation [here](https://osquery.io/schema/5.5.1/#programs).

**Query:** `SELECT * FROM programs LIMIT 1;`
```
root@analyst$ osqueryi  
Using a virtual database. Need help, type '.help'  
osquery>select * from programs limit 1;  
              name = 7-Zip 21.07 (x64)  
           version = 21.07  
  install_location = C:\Program Files\7-Zip\  
    install_source =  
          language =  
         publisher = Igor Pavlov  
  uninstall_string = "C:\Program Files\7-Zip\Uninstall.exe"  
      install_date =  
identifying_number =
```
In the above example `LIMIT` was used followed by the number to limit the results to display.

**Note**: Your results will be different if you run this query in the attached VM or your local machine (if Osquery is installed). Here line mode is used to display the result.

The number of columns returned might be more than what you need. You can select specific columns rather than retrieve every column in the table.

**Query**: `SELECT name, version, install_location, install_date from programs limit 1;`
```
root@analyst$ osqueryi  
Using a virtual database. Need help, type '.help'  
osquery>select name, version, install_location, install_date from programs limit 1;  
            name = 7-Zip 21.07 (x64)  
         version = 21.07  
install_location = C:\Program Files\7-Zip\  
    install_date =
```
The above query will list the name, version, install location, and installed date of the programs on the endpoint. This will still return many results, depending on how busy the endpoint is.

### Count

To see how many programs or entries in any table are returned, we can use the **count()** function, as shown below:

**Query**: `SELECT count(*) from programs;`
```
root@analyst$ osqueryi  
Using a virtual database. Need help, type '.help'  
osquery>select count(*) from programs;  
count(*) = 160
```
### WHERE Clause

Optionally, you can use a **WHERE** clause to narrow down the list of results returned based on specified criteria. The following query will first get the user table and only display the result for the user James, as shown below:

**Query**: `SELECT * FROM users WHERE username='James';`
```
root@analyst$ osqueryi  
Using a virtual database. Need help, type '.help'  
osquery>SELECT * FROM users WHERE username='James';  
        uid = 1002  
        gid = 544  
 uid_signed = 1002  
 gid_signed = 544  
   username = James  
description =  
  directory = C:\Users\James  
      shell = C:\Windows\system32\cmd.exe  
       uuid = S-1-5-21-605937711-2036809076-574958819-1002  
       type = local
```
The equal sign is not the only filtering option in a **WHERE** clause. Below are filtering operators that can be used in a **WHERE** clause:

-   `=` [equal]
-   `<>` [not equal]
-   `>`, `>=` [greater than, greater than, or equal to]
-   `<`, `<=` [less than or less than or equal to]
-   `BETWEEN` [between a range]
-   `LIKE` [pattern wildcard searches]
-   `%` [wildcard, multiple characters]
-   `_` [wildcard, one character]

### Matching Wildcard Rules

Below is a screenshot from the Osquery [documentation](https://osquery.readthedocs.io/en/stable/deployment/file-integrity-monitoring/) showing examples of using wildcards when used in folder structures:

-   `%`: Match all files and folders for one level.
-   `%%`: Match all files and folders recursively.
-   `%abc`: Match all within-level ending in "abc".
-   `abc%`: Match all within-level starting with "abc".

### Matching Examples

-   `/Users/%/Library`: Monitor for changes to every user's Library folder, _but not the contents within_.
-   `/Users/%/Library/`: Monitor for changes to files _within_ each Library folder, but not the contents of their subdirectories.
-   `/Users/%/Library/%`: Same, changes to files within each Library folder.
-   `/Users/%/Library/%%`: Monitor changes recursively within each Library.
-   `/bin/%sh`: Monitor the `bin` directory for changes ending in `sh`.

Some tables _require_ a **WHERE** clause, such as the **file** table, to return a value. If the required **WHERE** clause is not included in the query, then you will get an error.
```
root@analyst$ osqueryi  
Using a virtual database. Need help, type '.help'  
osquery>select * from file;  
W1017 12:38:29.730041 45744 virtual_table.cpp:965] Table file was queried without a required column in the WHERE clause  
W1017 12:38:29.730041 45744 virtual_table.cpp:976] Please see the table documentation: https://osquery.io/schema/#file  
Error: constraint failed
```
### Joining Tables using JOIN Function

OSquery can also be used to join two tables based on a column that is shared by both tables. Let’s look at two tables to demonstrate this further. Below is the schema for the **user’s** table and the **processes** table.
```
root@analyst$ osqueryi  
Using a virtual database. Need help, type '.help'  
osquery>.schema users  
CREATE TABLE users(`uid` BIGINT, `gid` BIGINT, `uid_signed` BIGINT, `gid_signed` BIGINT, `username` TEXT, `description` TEXT, `directory` TEXT, `shell` TEXT, `uuid` TEXT, `type` TEXT, `is_hidden` INTEGER HIDDEN, `pid_with_namespace` INTEGER HIDDEN, PRIMARY KEY (`uid`, `username`, `uuid`, `pid_with_namespace`)) WITHOUT ROWID;  

osquery>.schema processes  
CREATE TABLE processes(`pid` BIGINT, `name` TEXT, `path` TEXT, `cmdline` TEXT, `state` TEXT, `cwd` TEXT, `root` TEXT, `uid` BIGINT, `gid` BIGINT, `euid` BIGINT, `egid` BIGINT, `suid` BIGINT, `sgid` BIGINT, `on_disk` INTEGER, `wired_size` BIGINT, `resident_size` BIGINT, `total_size` BIGINT, `user_time` BIGINT, `system_time` BIGINT, `disk_bytes_read` BIGINT, `disk_bytes_written` BIGINT, `start_time` BIGINT, `parent` BIGINT, `pgroup` BIGINT, `threads` INTEGER, `nice` INTEGER, `elevated_token` INTEGER, `secure_process` INTEGER, `protection_type` TEXT, `virtual_process` INTEGER, `elapsed_time` BIGINT, `handle_count` BIGINT, `percent_processor_time` BIGINT, `upid` BIGINT HIDDEN, `uppid` BIGINT HIDDEN, `cpu_type` INTEGER HIDDEN, `cpu_subtype` INTEGER HIDDEN, `translated` INTEGER HIDDEN, `cgroup_path` TEXT HIDDEN, `phys_footprint` BIGINT HIDDEN, PRIMARY KEY (`pid`)) WITHOUT ROWID;
```
Looking at both schemas, `uid` in `users`table is meant to identify the user record, and in the processes table, the column `uid` represents the user responsible for executing the particular process. We can join both tables using this `uid` field as shown below:

**Query1:** `select uid, pid, name, path from processes;`

**Query2:** `select uid, username, description from users;`

**Joined Query:** `select p.pid, p.name, p.path, u.username from processes p JOIN users u on u.uid=p.uid LIMIT 10;`
```
root@analyst$ osqueryi  
Using a virtual database. Need help, type '.help'  
osquery>select p.pid, p.name, p.path, u.username from processes p JOIN users u on u.uid=p.uid LIMIT 10;  
+-------+-------------------+---------------------------------------+----------+  
| pid   | name              | path                                  | username |  
+-------+-------------------+---------------------------------------+----------+  
| 7560  | sihost.exe        | C:\Windows\System32\sihost.exe        | James    |  
| 6984  | svchost.exe       | C:\Windows\System32\svchost.exe       | James    |  
| 7100  | svchost.exe       | C:\Windows\System32\svchost.exe       | James    |  
| 7144  | svchost.exe       | C:\Windows\System32\svchost.exe       | James    |  
| 8636  | ctfmon.exe        | C:\Windows\System32\ctfmon.exe        | James    |  
| 8712  | taskhostw.exe     | C:\Windows\System32\taskhostw.exe     | James    |  
| 9260  | svchost.exe       | C:\Windows\System32\svchost.exe       | James    |  
| 10168 | RuntimeBroker.exe | C:\Windows\System32\RuntimeBroker.exe | James    |  
| 10232 | RuntimeBroker.exe | C:\Windows\System32\RuntimeBroker.exe | James    |  
| 8924  | svchost.exe       | C:\Windows\System32\svchost.exe       | James    |  
+-------+-------------------+---------------------------------------+----------+
```
**Note:** Please refer to the Osquery [documentation](https://osquery.readthedocs.io/en/stable/introduction/sql/) for more information regarding SQL and creating queries specific to Osquery.

## Answer the questions below

### Using Osquery, how many programs are installed on this host?

TryHackMe gives a detailed explaination of the use of _count_ in the Count section above. Let’s use _count_ agains’t the _programs_ table. To do this we can use the command `select count(*) from programs;`. Type this into the osqueryi console and press enter to run.

![](https://cdn-images-1.medium.com/max/720/1*f8TjY6CFkHb-yGOBcNKsJA.png)

The amount of installed programs will be displayed in the output. Once you see it type the answer into the TryHackMe into the answer field. Then click the _Submit_ button.

![](https://cdn-images-1.medium.com/max/720/1*jaksjLXGYoQ2YVJ85W95Pg.png)

**Answer: 19**

  

### Using Osquery, what is the description for the user James?

Looking in the _Where_ section above, gives us a great start. Using the query `SELECT * FROM users WHERE username=’James’;` , we need to make a change. Instead of having `*` after `SELECT`, we can replace it with `description`. Since we just want to see the secription for the user James. So the query should be `SELECT description FROM users WHERE username=’James’;`. Once you have it typed into OSquery console, press _enter_ to run.

![](https://cdn-images-1.medium.com/max/720/1*fv25d0yg2sOX8WP9iXtpfQ.png)

The answer will be found in the output from our query. Once you see it, type the answer into the TryHackMe answer field. Then click the _Submit_ button.

![](https://cdn-images-1.medium.com/max/720/1*PXL0B2zzQRcCDqCX83Kppw.png)

**Answer: Creative Artist**

  

### The next couple of questions are pretty straight forward, in the fact that you run the query given to you. Then find the answer in the output.

### When we run the following search query, what is the full SID of the user with RID ‘1009’?

**Query: select path, key, name from registry where key = ‘HKEY_USERS’;**

After coping and pasting the query into the OSquery console, and running it. Looking through the output, we can see the RID (Registry ID) of 1009 at the end of the path. Moving across the rows to the right, we can see the full SID (Security Identifier). Copy and paste this value into the TryHackMe answer field, then click the _Submit_ button.

![](https://cdn-images-1.medium.com/max/720/1*YQap09rblHk30OOs7s1ukQ.png)

**Answer: S-1–5–21–1966530601–3185510712–10604624–1009**

  

### When we run the following search query, what is the Internet Explorer browser extension installed on this machine?

**Query: select * from ie_extensions;**

After coping and pasting the query into the OSquery console, and running it. Looking through the output, we can see the Name, Registry_Path, Version, and Path. Though the question is asking for the name, it really is asking for the Path. Knowing this, we can get the answer from the final column. Copy and paste this value into the TryHackMe answer field, then click the _Submit_ button.

![](https://cdn-images-1.medium.com/max/720/1*z0KS-JHCCYQ8wh6JIqDvgQ.png)

**Answer: C:\Windows\System32\ieframe.dll**

  

### After running the following query, what is the full name of the program returned?

**Query: select name,install_location from programs where name LIKE ‘%wireshark%’;**

  

![](https://cdn-images-1.medium.com/max/720/1*HOpCJ0QHNPdbpbTXlJ5nAQ.png)

**Answer: Wireshark 3.6.8 64-bit**

----------

## Task 6 Challenge and Conclusion

Now that we have explored various tables, learned how to create search queries, and ask questions from the operating system, it’s time for a challenge. Use OSquery to examine the host and answer the following questions.

## Answer the questions below

### Which table stores the evidence of process execution in Windows OS?

We need to learn more about the tables of OSquery, to do so head over to the [Schema Documentation Site](https://osquery.io/schema/5.5.1/) that was shared in Task 4. Once there, we need to narrow down the tables to only show ones related to Windows system. Do this by clicking on the _Blue Carot_ in the middle of the page. Then Click on _Windows_, to check the box and only show Tables related to Windows.

![](https://cdn-images-1.medium.com/max/720/1*bwZ0NGuLjFpm0OqWtHRxpw.png)

Since the question is asking about processes that have been executed. Let’s search for _execution_. We can do this by using the _Find_ feature. Press _ctrl + f_ to open the find search bar. Once the bar appears, type _execution_. And as we can see we have 19 results.

![](https://cdn-images-1.medium.com/max/720/1*Y9avUPWbC8kS1XCYhDYa3w.png)

Since we only have 19 results, time to parse through until we find our answer.

![](https://cdn-images-1.medium.com/max/720/1*_z1VmwtPI3-tIxoAtvmYAg.png)

As you go through you will come across _last_execution_time_. Reading the explanation of the table it states _tracks when a user executes an application._ Which seems to line up with what the question is asking. Type the name of the Table into the TryHackMe answer field, and then click _Submit_.

![](https://cdn-images-1.medium.com/max/720/1*M_QIiClRXgm3IA8NV2e4BQ.png)

**Answer: Userassist**

  

### One of the users seems to have executed a program to remove traces from the disk; what is the name of that program?

Using the table new we got from the previous question. Let’s query the results from that table. To do so we can use the SQL query style we learned in Task 3 and 5, `SELECT * FROM userassist;`. After you have the query typed into the OSquery console, press enter to run it. Now start parsing through the results. The you can find the name of the programs that were run at the end of the destination path(example: _\cmd.exe_). Now it’s time to parse through the results.

![](https://cdn-images-1.medium.com/max/720/1*qvODQ9NpFIsfsPLLzKg5zQ.png)

Going down through, one program should stick out. Once you see it, type the program name into the TryHackMe answer field. Then click the _Submit_ button.

![](https://cdn-images-1.medium.com/max/720/1*Pgi15HnvzzOiIcLXerpUgA.png)

**Answer: DiskWipe.exe**

  

### Create a search query to identify the VPN installed on this host. What is name of the software?

The question is asking about an installed program on the system. Using our knowledge from previous task, we can look at the _programs_ table. So lets craft the query. Using the same SQL style as we have previous, `select name from programs;`. Since we only need the name we can just pull the name column, which is why we used `name` instead of `*`. Then press enter to run the query. Let’s parse through the results, start to look down through to you see the VPN name.

![](https://cdn-images-1.medium.com/max/720/1*1PqSkv4R8Ldb00s1eQZ-6w.png)

While parsing through, the VPN program will stand out. Once you find it, type it into the TryHackMe answer field. The click the _Submit_ button.

![](https://cdn-images-1.medium.com/max/720/1*RLnqgkO268pW4vOLXAeimA.png)

**Answer: protonvpn**

  

### How many services are running on this host?

We learned about how to use _count_ back in Task 5. Time to craft the query, `select count(*) from services;`, which will count the number of results and output it into the OSquery query. Press enter to run the query.

![](https://cdn-images-1.medium.com/max/720/1*PU_4ZfuIZ2bLpH3DzQVRag.png)

The number of running services will be output to the console. Type the number into the TryHackMe answer field. Then click the _Submit_ button.

![](https://cdn-images-1.medium.com/max/720/1*xGYXiKBBjSfBMNhlbRHD4Q.png)

**Answer: 214**

  

### A table **autoexec** contains the list of executables that are automatically executed on the target machine. There seems to be a batch file that runs automatically. What is the name of that batch file (with the extension .bat)?

Back in Task 5 we learned about searching for a specific pattern. Using this knowledge lets craft the query: `select * from autoexec WHERE name LIKE ‘%.bat’;`. We are searching on the _autoexec_ table where the name matches the pattern of ending with _.bat_. Press enter to run the query

![](https://cdn-images-1.medium.com/max/720/1*zIYpom0MqhQWgNTN4uuJ-w.png)

The results will be output the the OSquery console. You will be able to the name of the file ending with _.bat_. Type the name into the TryHack answer field. Then click the _Submit_ button.

![](https://cdn-images-1.medium.com/max/720/1*6h_nPo76JDjnRtaQVfbKcQ.png)

**Answer: batstartup.bat**

  

### What is the full path of the batch file found in the above question? (Last in the List)

This answer can be found from the results of the previous question. Look at the last row under the _Path_ column. This path is the answer to the question. Copy and paste the answer into the TryHackMe answer field. Then click the _Submit_ button.

![](https://cdn-images-1.medium.com/max/720/1*Pwo2Bpt4rzaCdhxn0hwQaA.png)

**Answer: C:\Users\James\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\batstartup.bat**

  

----------

## 🎉🎉🎉Congrats!!! You completed the TryHackMe Osquery: The Basics Room, Awesome Job!!!🎉🎉🎉