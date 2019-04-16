---
layout: post
category : google-chrome
tagline: "Use these work-arounds to fix/override Chrome locked settings."
tags : [google-chrome,group-policy,powershell,registry,windows]
---

Previously I wrote about how [Windows Group Policies related to Google Chrome](http://www.devtxt.com/blog/google-chrome-group-policy-settings-locked-startup-home-page-saving-passwords) that can set and lock down settings that you might want to change: password saving in Chrome, home button URL, and start-up URLs.

Here's how to configure Chrome the way you want. These examples use PowerShell to ensure the process is repeatable. If you know your way around the Windows Registry, you'll find your way easily.

If you make any changes to the Registry, you [MUST close Chrome](http://i.imgur.com/jLubl8N.png) (and Hangouts if applicable).


### Password Saving

One Group Policy setting enables the Chrome Password Manager. Every time you successfully log into a site, [Chrome will prompt you to save that password](http://i.imgur.com/8mi9A7H.png). If you're already using a password manager, this is redundant, potentially less secure, and annoying.

    $regKey = "HKCU:\SOFTWARE\Policies\Google\Chrome"
    Set-ItemProperty -Path $regKey -Name PasswordManagerEnabled -Value 0

![stop Chrome force asking to save passwords](http://i.imgur.com/c7MATEC.png)


### Start Pages/URLs

The URLs for Chrome to launch on startup are stored in the Windows Registry at:

    HKCU:\SOFTWARE\Policies\Google\Chrome\RestoreOnStartupURLs 

![forced Chrome start up URLs](http://i.imgur.com/xHlj5zs.png)

Use this PowerShell script to reset those:

    $regKey = "HKCU:\SOFTWARE\Policies\Google\Chrome\RestoreOnStartupURLs"
    $startUrls = 
    "https://tweetdeck.twitter.com",
    "https://trello.com",
    "https://github.com"
    
    $urlNumber=1
    foreach ($url in $startUrls) {
        Set-ItemProperty -Path $regKey -Name $urlNumber -Value $url
        $urlNumber++
    }
 
If there are 1 or 2 start-up URLs, you can replace them. Obviously if there are more forced URLs than you want to set with your own, you'll need to script them to be deleted.

![fixed Chrome startup URLs](http://i.imgur.com/1yLregj.png)

### Home Button

If you use the Chrome home button, you might want to customize it.

    $regKey = "HKCU:\SOFTWARE\Policies\Google\Chrome"
    Set-ItemProperty -Path $regKey -Name HomepageLocation -Value "http://www.example.com"


If you want your home button to simply open an empty new tab: use  value `1` or `0`: (the `HomepageLocation` will be ignored)
 
    Set-ItemProperty -Path $regKey -Name HomepageIsNewTabPage -Value 0 -Type DWord 

![fixed Chrome home button location](http://i.imgur.com/0DxhvHF.png)

### Restart Chrome.exe

You need to restart Chrome. Maybe even quit Hangouts as well, if you have that installed.

### All Together Now

Put all the above in a script, and run on login. There aren't any guarantees through that an Group Policy won't update these values while you're logged on. In that case, run it as a scheduled task at some time interval (perhaps every hour or so).

<script src="https://gist.github.com/philoushka/6c7f4402cc4b50b494e1.js"></script>
