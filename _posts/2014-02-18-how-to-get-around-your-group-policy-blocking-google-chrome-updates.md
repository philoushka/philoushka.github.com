---
layout: post
category : 
tagline: "I had a lab scenario where Group Policy from Active Directory blocked Google Chrome from updating itself. Here's how I fixed that."
tags : []
---
<style>img {border: 1px solid black;}</style>

Corporate IT departments love locking down workstations. It's their job. One great tool is Active Directory Group Policy. IMO, forcing users to stick to one version of a browser is a) lame and b) dangerous. 
<img src="http://i.imgur.com/Zh105m7l.png" style="float:right"/>

**Rant**

Preventing web browser updates is dangerous because these policies are actively preventing security updates from being distributed to the client. Their belief is probably that there's an application that somehow needs something non-Internet Explorer, but it (wrongly) needs to be locked to the version that the vendor shipped it with. There's all kinds of *you're doing it wrong* in this scenario.

> Update failed (error: 7) An error occurred while checking for updates: Google Chrome or Google Chrome Frame cannot be updated due to inconsistent Google Update Group Policy settings. Use the Group Policy Editor to set the update policy override for the Google Chrome Binaries application and try again; see http://goo.gl/uJ9gV for details.


###Workaround The Policy###
If your workstation has a Group Policy blocking Google Chrome updates, **and you have administrative privileges**, you can reconfigure your machine to get updates.  

###1. Install This Group Policy Template###

Google makes available a [Group Policy Administrative Template for Google Chrome updating](https://support.google.com/installer/answer/146164?hl=en#Obtaining_the_Administrative_Tem). Download it here, too - [GoogleUpdate.adm](files/GoogleUpdate.adm) 
<img src="http://i.imgur.com/F1ygUOs.png" style="float:right"/>
**Install it:**

* run `gpedit.msc`
* open **Computer Configuration / Administrative Templates**. Right click, and select `Add/Remove Templates`.
* Add the GoogleUpdate.adm template.
 
Navigate down to `Classic Administrative Templates/Google/Google Update`.

**Modify These Policies**

* Preferences/Auto-update check period override -> Enabled
* Applications/Update Policy Override Default -> Enabled -> [Always Allow Updates](http://i.imgur.com/Jo8iXlK.png)
* Applications/Google Chrome/Allow Installation -> Enabled 
* Applications/Google Chrome/Update Policy Override -> Enabled -> Always Allow Updates
* Applications/Google Chrome Binaries/Allow Installation -> Enabled 
* Applications/Google Chrome Binaries/Update Policy Override -> Enabled -> Always Allow Updates

<div style="clear:all;" />
###2. Tweak The Registry###

Your Group Policy may have left a few items in the Registry that need removing.

Inspect and use this Registry editor file - [GoogleChromeUpdateEnable.reg](files/GoogleChromeUpdateEnable.reg) - to delete those 2 values. 
       
    [HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Google\Update]
    "Update{8A69D345-D564-463C-AFF1-A69D9E530F96}"=-
    "Update{8BA986DA-5100-405E-AA35-86F34A02ACBF}"=-


As per Google's [Update fails due to inconsistent Google Update Group Policy settings](https://support.google.com/a/answer/1385049), you should verify that your configuration is updated correctly:

>Start > Run > regedit
>Find and open `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Google\Update\`
>Verify that the following **new** group policy setting is present:
>Update{4DC8B4CA-1BDA-483E-B5FA-D3C12E15B62D}
>**Delete** these values in `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Google\Update` :

> `Update{8A69D345-D564-463C-AFF1-A69D9E530F96}`
> `Update{8BA986DA-5100-405E-AA35-86F34A02ACBF}`

###Policy Sidestepped###

Simply relaunch the [Chrome About page](chrome://chrome/) and it will automatically start the check. You won't need to restart Windows or log off.

![Chrome Update Success](http://i.imgur.com/rXbVrJc.png)
