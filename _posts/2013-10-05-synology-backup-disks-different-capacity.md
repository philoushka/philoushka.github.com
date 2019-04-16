---
layout: post
category : 
tagline: "If you're running a Synology NAS and aren't using RAID, you can still protect your data."
tags : []
---

This may be interesting to you if you have a Synology NAS with 2 drive bays and:

* have disks with different capacities
* they're not running in SHR mode, but in Basic mode or otherwise without data protection
* you want to give your data some added protection
* you might have an external USB drive

Basically as above, the Synology is operating on the single drive. The problem is that **the data isn't being duplicated or backed up regularly**.

Consider backing up to either a smaller internal disk or an external USB disk. All you'll need is a second disk with enough storage for the itmes you want to back up. In my examples below, the disks are:

* Bay 1 with 2 TB (the primary copy of the data)
* Bay 2 with 750 GB   

###Create A Backup Task To Your 2nd Smaller Disk###

* Install your 2nd disk in Bay 2.
* If this 2nd disk is smaller than your 1st disk, then you must create a Basic volume.

![](img/synology-create-shared-on-2nd-disk.png)

* Create a new backup task

![](img/synology-create-backup-task.png)

![](img/synology-backup-destination.png)

![](img/synology-backup-folders.png)

* kick off a backup

![](img/synology-backup-now.png)

You now have a copy of those shared folders on Disk 2
 

###Create Backup Task To Your USB External Disk###

Follow the same process above, but simply choose the **usbshare1** destination directory.

![](img/synology-backup-to-usb.png)


###Now Get It Offsite###

Following the steps above, you should now have 2 backups: one to 2nd hard disk, and one to external USB disk.

Now take that USB disk somewhere safe and off-site, and bring it back periodically. [Make yourself a reminder](https://ifttt.com/recipes/121684).

![](img/synology-backup-to-2nd-disk.png)
