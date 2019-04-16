---
layout: post
category : powershell
tagline: "I frequently need to run SSMS as a different domain user. Here's how to create a shortcut to run an application under different Active Directory credentials."
tags : [powershell,windows]
---

<style>img{border:solid 1px black;}</style>

Sometimes I need to connect to SQL Server using Active Directory credentials using my admin account. The reason for this is that some SQL Server deployments are configured to allow developers access via admin accounts only, a practice I definitely agree with (make it harder to screw things up).

I use my dev machine with my regular (non-admin) AD account. Usually I would open SSMS with the Run As command on the shortcut. I found it turned into real *first-world dev problem * that took too many clicks to run SQL Server Management Studio (SSMS) under the credentials of another AD account.  

<img src="http://i.imgur.com/YQcjMmn.png" style="float:right" />
Here's how I was doing it:
 
1. Right click SSMS
1. Shift-right click SSMS
1. Choose Run As Different User
1. Type the username
1. Type the password
1. Mutter <a href="http://i.giflike.com/TqPgN2U.gif">"There's got to be a better way"</a>

<div style="clear:both;"></div>

### Creating A Shortcut With Run As Different User

This cuts the number of clicks/steps down from 5 to 1. This will create a shortcut that will run the application under the account you specify. This will work for any executable. 

1. Create a new shortcut anywhere.
2. [`runas /user:myDomain\myAdminAccount "C:\windows\notepad.exe"`](http://i.imgur.com/YqYZoyn.png)
3. Give it a good name.

Now when you execute the shortcut, you're prompted for the password of the account you specified.

![](http://i.imgur.com/eakeicq.png)

### Creating A Custom Icon For Your Shortcut

1. Find or make a decent png/jpg. Make it square. 
2. Convert it to an .ico - use [www.converticon.com](http://www.converticon.com)
3. [Include all the sizes.](http://i.imgur.com/3MAxw58.png)
4. Save As will then download a new .ico file
5. [Right-click -> Properties on the shortcut and Change Icon to this new icon set](http://i.imgur.com/mxdTuMZ.png).
6. Drag it to your Windows taskbar

![](http://i.imgur.com/SVsimnO.png)
