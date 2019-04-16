---
layout: post
category : virtualization
tagline: "Considering desktop VM applications"
tags : [virtualization]
---

As developers, we usually have these things (file most of these under 'duh!'):

* **well powered desktop machines**. OK, mostly desktop. Maybe you've got a big honkin' laptop-with-great-specs-but-called-a-desktop-replacement. 
* a need to **deploy/test/mess about in another machine**. You don't want the cruft of your development machine to get in the way of the operation of your target environment. 
* the **desire to test out a new tool**: a beta/RC OS, a new beta of Visual Studio, a new server product (SVN), a community technology preview (CTP), or some other package that you just don't want to push to your current Dev server. Hands up if you even have a 'Dev' server other than your machine? 

In the last 4 years, I've usually run into something dev-related that I really wanted to get my hands dirty with. Yes, the [shiny-object developer syndrome](http://www.codinghorror.com/blog/archives/000916.html). The old way was to install that piece on your Dev machine. Months would go by, and you'd (theoretically) dirty up your registry, and contribute to the eventual slowdown of your Windows install. The logical solution at that point would be to format and repave your Dev machine. Looking forward, and a bit contrary to the point I was just making, I don't get the sense that Windows 7 will succumb to the bloat and eventual slowdown. That said, it doesn't invalidate the need &amp; convenience of virtualization.

###Free Options###
Enter the full on assault of free options for virtualizing operating environments. We really have an embarrassment of riches. Perhaps I am late to the party, but the *freeness* of the VM solutions is jolting:

* [Microsoft Virtual PC](http://www.microsoft.com/windows/virtual-pc/support/virtual-pc-2007.aspx)
    
* [Sun VirtualBox](http://www.virtualbox.org/)
    
* [VMWare Server](www.vmware.com/products/server)
    
* [VMWare ESXi](www.vmware.com/products/esxi)
    

###My Fave Virtualization Platforms###
Doubtless you know the benefits of running VMs. Lower TCO in terms of number of physical metal boxes, lower cost of electricity to power and cool, etc. For me, it's the ability to RDP into a new machine on the 'network' and install/configure/test whatever I am working on. The ability to mount ISOs for OS and app installation is just another kick ass speed benefit. Even better are the instances where you can download a pre-configured VM. Check out [ALMWorks' turnkey Bugzilla](http://almworks.com/vbs/overview.html) and [Subversion virtual machines](http://www.bing.com/search?q=free+subversion+virtual+machine).

####[Sun VirtualBox](http://www.virtualbox.org/)####

[![sun_virtualBox](img/sun_virtualBox_thumb.jpg)](http://devtxt.com/blog/blogimg/VirtualizationTheDevelopersDesktopMachin_DDA9/sun_virtualBox.jpg) Great product here. Easy creation of virtual hard drive disks, mount ISOs, and a nice looking application overall. Its config files are all XML, and messing around with file locations is easy. The one thing about VirtualBox is that it doesn't run VMs out of a single window, but rather opens a new window in your (in Windows anyway) taskbar. This is different from VMWare, likely due, in part, to VMware being headless.
My big want out of VirtualBox is the ability to run headless. It's the one big feature that would allow me to adopt it as my one and only VM product on the Developer's machine. Sun releases this product for Windows, Mac and Linux hosts, and I think they've done a great job. The release frequency is stunning! Keep up the good work, Sun! **8/10**

####[VMWare Server](www.vmware.com/products/server)####

[![vmware-server](img/vmwareserver_thumb.png)](http://devtxt.com/blog/blogimg/VirtualizationTheDevelopersDesktopMachin_DDA9/vmwareserver.png) I first got into VMWare Server as I was encouraged to run Windows 2003 on the job. Previously I had only used the Microsoft Virtual PC products, which were decent. The killer bit that won me over on VMWare Server was that it is HEADLESS. The machines can startup and shutdown in parallel with your host OS. Excellent feature for those who would expect those services to be up 100% of the time that your dev machine is (Dev or Test SQL Server, Active Directory services, build machine, etc). This is basically gives you the Ron Popeil method of running additional machines: set it, and forget it (curse you, 90's infomercials).
The kicker for me today is that VMWare does NOT make Windows 7 64-bit signed drivers. Absolute killer for me during the Release Candidate of Windows 7, and still today at Win 7's release. Reading the forums and related searches, it appears there were hacks for Vista 64, but the important part here is that Microsoft REQUIRES signed drivers for 64 bit systems today, starting with windows 7. *VMWare, please*! Get those signed drivers out! 
There's one thing about the latest releases of VMWare Server that gets me. The 1.x versions all had built in console on the host where you defined/configured/started/stopped your VMs. It was a nice presentation with console UI elements coming in an .exe. The 2.x releases have moved to a web-based console. I much preferred the 1.x presentation.
I'm still using in on the job with Win7 32-bit, and it works well! **9/10**

####[Microsoft Virtual PC](http://www.microsoft.com/windows/virtual-pc/download.aspx)####

[![virtual_pc](img/virtual_pc_thumb.jpg)](http://devtxt.com/blog/blogimg/VirtualizationTheDevelopersDesktopMachin_DDA9/virtual_pc.jpg) This was my first foray into VM'ing. I think XP was the modern OS at the time, and it was a great introduction to testing out changes or running other apps that I didn't want on my machine. The kicker again here was that the system was not headless. Today, you'll run [Virtual PC 2007 on XP or Vista hosts](http://www.microsoft.com/windows/virtual-pc/support/virtual-pc-2007.aspx), while Win7 has the 'year' moniker dropped.
The biggest one was a Toshiba voicemail/PBX management app that ONLY ran on XP machines that were NOT on a domain. What a pile of disappointment. The phone technician who installed the system had to be called out every time the company wanted to adjust the phone system (change a number, a name/label on the phone's display, or any options on the phone system overall). It turns out he simply was running this web app on IIS on his laptop. He just needed to tweak the IP address in the app to match the customer's phone system. One day I asked him how to DIY, and he suggested to run this web app on my machine. It was a perfect candidate for virtualization. Thanks MS Virtual PC 2004! **7/10**
  
####[VMWare Server ESXi](www.vmware.com/products/esxi)####

[![vmware-esxi](img/vmwareesxi_thumb.png)](http://devtxt.com/blog/blogimg/VirtualizationTheDevelopersDesktopMachin_DDA9/vmwareesxi.png) This is a free hypervisor product. Really it's the entry-level product within the hypervisor line. It allows you to deploy multiple VMs on a machine and incur just a small performance penalty for the host OS. The licensing cost is zero. It runs a Linux kernel, and its [footprint is ~32MB](http://en.wikipedia.org/wiki/VMware_ESXi#VMware_ESXi)! Hmmm... could you install that to a USB thumbdrive? So the real benefit here is that you don't have to worry about the license for your host, nor the overhead of the host.
My next project will be to take my 4 virtual machines and deploy them to a machine running ESXi. How cool is it that VMWare makes it free? Your only limitation at this point is the amount of RAM and disk space (hardly a limitation today at 7 cents per GB on a SATA drive). The product is a downloadable ISO. You boot into its setup app, and from then on, you use the console application to communicate with it. 

<iframe width="640" height="360" src="https://www.youtube.com/embed/yZeeanyy-8k?feature=player_detailpage" frameborder="0" allowfullscreen></iframe>

####Also-Ran####
The new hotness is Virtual XP with Windows 7. It's not really a multi-machine solution, and as a developer, it doesn't do much for me. I am surprised that they are doing the '[Remote App](http://en.wikipedia.org/wiki/RemoteApp#RemoteApp)' thing in Windows 7, and definitely applaud Microsoft for it! XP, however... 2003 called, and it wants its... oh, nevermind!
