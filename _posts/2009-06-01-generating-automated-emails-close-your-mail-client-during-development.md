---
layout: post
category : 
tagline: "So your application needs to send emails to stakeholders-customers-admins-managers. You know the kind"
tags : []
---

Yep, this StackOverflow question keeps on giving! [Hidden features of ASP.NET](http://stackoverflow.com/questions/54929/hidden-features-of-asp-net)

So your application needs to send emails to stakeholders/customers/admins/managers. You know the kind of emails:

* password reminders,
* account balances, 
* reminders &amp; status updates 
* confirmations of all sorts 

Typically my development routine consisted of something like this:
  
 1. Write a template email. String constants with placeholders, etc. Dear [FirstName] [LastName],
 1. Read all appropriate details from a data-store. You know, the things specific to the recipient of the email. Replace [FirstName] [LastName] with real names, or a link specific to their account to reset their password, etc.
 1. Write the email sending business logic. `System.Net.Mail` and all the goodness within. Attachments, BCC, SMTP, all those good things provided by that namespace. (Thank you Microsoft, for helping us move on from CDONTS.) 
 1. Put in your own email address to receive the unit tests and integration tests. 
 1. Brace for the email flood into your mail client. 
 1. Context switch between the mail client and development IDE. More back and forth for you! 
  

###New Tool in the Toolbox – Already Built into the .NET Framework!###

While testing, you can have emails sent to a directory instead of being sent to SMTP server. Simply put this in your web.config:
  
    <system.net>
       <mailsettings> 
          <smtp deliverymethod="SpecifiedPickupDirectory"> 
            <specifiedpickupdirectory pickupdirectorylocation="c:\SomeEmailDirectory\"></specifiedpickupdirectory> 
          </smtp> 
        </mailsettings>
    </system.net> 
  
  
###So What?###

  So how much time does it really save you? It's negligible, really, when your mail server is on the LAN. If you are working with an SMTP server that is unreliable, slow, or keeping accounting on mail count/charging for bandwidth, the seconds per sent email can add up.
  No matter about SMTP servers... good, bad or ugly. You could [monitor a directory with the .NET `FileSystemWatcher`](http://articles.techrepublic.com/5100-10878_11-6165137.html) to watch for newly dropped email files, and then open them automatically! 
  Imagine, your unit or integration tests create a new email to be sent, and another dev tool (using `FileSystemWatcher`) can automatically `ShellExecute` it for you. That saves you the time of switching to the directory, double clicking the newly created email, and then getting on with the work of checking for correctness.
