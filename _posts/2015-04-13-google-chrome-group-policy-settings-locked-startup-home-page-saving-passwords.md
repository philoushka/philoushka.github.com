---
layout: post
category : google-chrome
tagline: "You might find your Windows machine's Chrome settings set and locked by Windows Group Policy."
tags : [google-chrome,group-policy,powershell,registry,windows]
---

![](http://i.imgur.com/oUSrnwC.png)

### Chrome in the Enterprise

For  those on the enterprise slow train, it's nice to see that Chrome is being allowed and/or blessed by the IT Overlords. Some even allow Chrome to update itself! Amazing!

The issue is that the IT management types want to lock settings for everyone. In typical enterprise fashion, it's what works for them, and not so much for the user. [Mooooove!](http://i.imgur.com/L5iCone.jpg)

### That's Our Policy 

This post is not a lament about Group Policy settings, but rather that those settings are chosen and **locked** without override by the user.

#### Pages

There are a handul of Group Policies for Chrome settings:

- *startup pages*: which URLs should load on browser startup.
- *home button*: whether the home button appears to the left of the address bar.
- *bookmark bar*: whether the bookmark bar can be hidden from underneath the address bar.

<!-- break -->
![](http://i.imgur.com/U2ngOt5.png)

Additionally, the Group Policy setting can set and lock the URL that the Home button will load.

![](http://i.imgur.com/7a6d8ny.png)

#### Passwords

A Group Policy setting can force Chrome to offer the user to save the credentials in Chrome's credential store.

![](http://i.imgur.com/JynVU24.jpg)

Locking this Chrome setting is annoying. <em>I already have a <a href="https://www.lastpass.com">password manager</a></em> that manages this functionality for me. For those who don't use a password manager, this is setting/suggestion is benefical. 

The result is a constant nag everytime you authenticate with a new site.

![](http://i.imgur.com/8mi9A7H.png)

I cannot find a reason that an IT admin would choose to *lock* this functionality to always offer to save passwords. It seems to be a reasonable suggestion as a default setting, but it's the locking of that choice, thereby creating a nag screen that is the problem.
