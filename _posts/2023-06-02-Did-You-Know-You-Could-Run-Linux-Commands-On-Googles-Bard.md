---
layout: "post"
title: "Did You Know You Could Run Linux Commands On Google’s Bard"
categories: Tips & Advice
tags: Tips, Bard, Linux Commands
---

![](https://miro.medium.com/v2/resize:fit:700/0*hv6laESIDVMOjnnj.png)

Before I can go into how I discovered this, I want to lay out how I got there. The other day I was messing around on my Kali VM, trying to create a bash script to pull IPs from log files. Kept getting errors and frustrated, so I turned to Google’s Bard asking question how it would do the same thing and comparing my code to it. Now jumping between VM and Bard, I forgot to jump back into my VM, and ran the command  `ls`. To which Bard gave the the contents of it’s current directory. I thought I just discovered something. So I tried to traverse the file system on Bard to see what else I could discover. Which lead me to putting a bug bounty into Google, since I looked online and couldn’t find anything on being able to do this. Well I got the email back from Google stating that it is not a security vulnerability, and is intented. So I wanted to share my discovery with you, this is basically how I went about doing it!!!

So let us test some commands on Google Bard!!!! Starting out simply, let’s run  `ls`  and see what Bard give’s us:

![](https://miro.medium.com/v2/resize:fit:700/0*Jkism8uh5wkpFB7Y.png)

You can see from the screen shot above that it will list its current directories contents.

Can we change directorires? Let us trying with the  `cd /`, then  `ls -la`  to see the contents of we are:

![](https://miro.medium.com/v2/resize:fit:700/1*lRc9IBSJzP5Pa88Zg9p49Q.png)

Now  `ls -la`:

![](https://miro.medium.com/v2/resize:fit:700/1*yJPHbrD_4GM6wnZgOKbmGA.png)

As you can see we are now in the root directory. Can we move into any of those files? Let’s try  `cd sbin`:

![](https://miro.medium.com/v2/resize:fit:700/1*2TjOLbyMQN3MNiYAs09a4w.png)

Ok we are in, let’s see what we can see with  `ls -la`:

![](https://miro.medium.com/v2/resize:fit:535/1*0po4O5bXuDZn7Oa8cYzP7w.png)

We can see the contents of the /`sbin`, and since we ran  `ls` with the  `-la`  parameter. We see who owns the files, mostly root. But let’s see if we can change that. Type in Bard  `chown bard:bard cp`

![](https://miro.medium.com/v2/resize:fit:700/1*MwYRS4mcmf7CP7d01H50GQ.png)

Checking out if it works:

![](https://miro.medium.com/v2/resize:fit:652/1*GC75R8PuaLDTAaIw-eY2lQ.png)

Bard kind of went nuts and changed a bunch of different file owners.

With this little write-up on running Linux commands in bard, go out and test Bard to see what it is capable of. Explore your enviroment, Expand your knowledge, and finally Be Awesome!!!