---
layout: post
category : 
tagline: "There isn't a clear path leading developers away from Windows Services "
tags : []
---

Currently I use local Windows Services to check or poll for items to process on a set schedule. Typically this includes picking up items that are queued or in a status in some kind of a workflow like:

- check for emails to send
- give me the top *n* waiting orders to be processed
- check for waiting emails in an email account
- check for waiting files in a directory
- call a web service (or any URL) to kick off some work

<img alt="Windows Services" src="http://i.imgur.com/N7BYdJy.png" style="float:right" />

### Why Windows Services?

I've **chosen Windows Services** in the past because:

- they've been stable and durable for me
- auto-startup on machine startup
- easy to write business logic with C#

I'm ready to **ditch Windows Services** because: 

- friction to install and deploy (scripting with PowerShell alleviates this)
- redeploy tasks include a bunch of yak shaving (stopping a remote machine's service, redeploy new build, restart remote service.)  
- initial development is more difficult than other apps
- I've been spoiled by using Azure Scheduler.

### No Obvious Replacement 

The problem is that there's no easy webby replacement for Windows Services. There's no pit of success that .NET devs are starting to expect. Seeing the incredible pace and volume of awesomeness from .NET vNext and continuous features in Azure is starting to raise my expectations.

### Ideal Replacements

<img alt="schedule" src="http://i.imgur.com/Ig94OJ3m.png" style="float:right;" />

1. WebAPI enhancements to allow service methods within to be scheduled. Imagine a way to configure or write your WebAPI methods to be called automatically themselves.

2. On-premises [Azure Scheduler](http://azure.microsoft.com/en-us/documentation/services/scheduler/) that can [call an HTTP endpoint](http://i.imgur.com/XY52bZJ.png) on a [schedule of your choosing](http://i.imgur.com/Ig94OJ3.png). You put your tasks in a web service that's callable via HTTP. It's another web app that you can scale as much as you need, and the scheduled calls occurs in the Scheduler.

3. On-premises [Azure Web Jobs](http://azure.microsoft.com/en-us/documentation/articles/web-sites-create-web-jobs/) that can run PowerShell, JavaScript, etc.

4. [**Hangfire**](http://hangfire.io/) - An "easy way to perform fire-and-forget, delayed and recurring tasks inside ASP.NET applications. No Windows Service required". Looks easy to integrate, and comes with a dashboard.

5. Write your own. Why bother though? - Hangfire is already miles ahead.
<div style="clear:all"/></div>

### Hangfire - Scheduling and Monitoring
Looks like a great choice. Open source, on [NuGet](https://www.nuget.org/packages/HangFire), comes with a dashboard. I'm impressed. 

![hangfire](http://i.imgur.com/rYgNNIY.png)

### Alternatives I'm Not Crazy About

- Windows Task Scheduler - this ties the job to a machine. Not as portable as I'd like. I like that you can set all attributes via PowerShell, but a web interface feels more natural. 
 
- SQL Server Agent jobs - doesn't fit the bill in most scenarios, especially if you want to write complex logic, and perform tasks outside of your RDBMS. SQL Mail? - um, no.

### I Dunno 

I'm still stuck. I can't see a clear winner on how to schedule repeated calls to an on-prem web service.