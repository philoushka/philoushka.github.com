---
layout: post
category : ui
tagline: "Message box alerts are a UI fail usually containing poor info."
tags : [ui]
---

###Quick Rant On Message Boxes###

Message Boxes are so full of fail. Here's one from an application that thousands of people use.  

![](http://i.imgur.com/ZC6Oaxf.png)


####1. Using A Message Box####
This is a desktop application. My biggest annoyance with this is that the application interrupts what the user. It forces the user to navigate to its only button - the stylish `Close` button. So it rewards me with the required action of basically making no choices. My acknowledgment of the problem actually means nothing.
  
**Fix:** implement and promote a *status bar* where information is presented. Flash up new information. Keep history. Fade away.
 

####2. Mixed or Confusing Message####
The message mixes 2 different issues and doesn't clarify which is the real issue. ***Access Denied*** and ***Can't get IP address for server*** are different problems with different solutions. 
So which is it? Is it both?

**Fix:** give the user only useful and **correct** information in the headline. Option for more.
 

####3. Lack Of Useful Info####
OK, so the app is trying to hit a server. What can I do about it? Why is that important to the task I was doing?

**Fix:** Tell the user what they need to know in terms they can understand.

 
####4. Is This User The Right Person To Notify?####
No. The user in this case is a clinical user, like a nurse or registration clerk, who only needs to get their job done. They don't know jack about servers on the back end. This is the wrong message for this user.

**Fix:** send this message to the administrative or technical types who can actually act on the problem. Send an email or SMS to that group. Log it.

###Give The Right Message To The Right User###
I want to improve in this aspect myself, so here's my new list for creating messaging to user(s) when an exception occurs:

1. Can I tell whether the current user should be reasonably expected to know that this could happen?
1. Can the user actually do something about it?
1. Is there an admin group that I can alert?
1. Do I need the user to make a choice between Action A or B?
1. Can I retry silently *n* times while the user waits a bit?
1. Don't force-interrupt the user.
1. Tell the user in a status area:
 * Something is a blocking them from doing that thing they wanted.
 * The root cause is blocking them from (saving the info/sending the notification/calculating the average/making the change).
 * We retried *n* times. 
 * It's (not) a problem they can solve.
 * It will (not) block them from Task X.  
 * Someone has been alerted at *datetimestamp*.
 * You should retry when (admins let you know/etc.). 
1. Update the status area when we can detect that the problem has been solved. 

###Bonus Alert###

![](http://i.imgur.com/H2A34hi.png)
