---
layout: post
category : 
tagline: "A log of the time an HR careers-job application tracking software vendor emailed me my own password."
tags : []
---
<style>img{border: 1px solid black}.floatr{float:right;}</style>

### Yet Another Account ###
 
<a href="https://albertahealthservices.ats.hrsmart.com/cgi-bin/a/editprofile.cgi"><img src="http://i.imgur.com/eGlDUBq.png" class="floatr" /></a>

We've all been forced to create an account at some web application. If you're lucky, the service has identity integration with the popular providers - Facebook, Twitter, Google, Microsoft, and they're only storing authentication tokens from the 3rd party.

I created an account on the [Alberta Health Services (AHS) careers or job board website](https://albertahealthservices.ats.hrsmart.com/cgi-bin/a/editprofile.cgi). I stumbled a few times with my entries into required fields not being correct or to their validator's liking, but finally succeeded with a nice long complex LastPass-generated password. This is an HR careers website; it seems like the perfect candidate for  [LinkedIn integration](http://developer.linkedin.com/documents/authentication).  The form asked for a complicated mashup of account credentials, personal demographic data, and HR job related information.


### Careful Choosing Your SASS Vendor ###

The Alberta Health Services careers site is run or provided by [HRSmart](https://www.hrsmart.com/). It's obviously a good choice by AHS not to run their own careers/recruiting/job board: outsource that to a company who's competent and is focused on providing the right features. No need to re-invent the wheel. 

I came away with the conclusion that this software has problems. The problems aren't insurmountable, but are large enough to provide roadblocks to users. 

Ask your vendor: Does your software fit my workflow, or do we as the customer need to fit (and adjust) into yours?


### They Emailed Me My Username And Password ###

<img src="http://i.imgur.com/mSKPOeC.png" alt="Are you kidding me?" title="Are you kidding me?"   />

There are at least 4 things wrong with passwords being emailed:

1. **You know my password** - you shouldn't know it. You should only know a hash of it. **Stop storing your user's/customer's passwords in your database tables.** I don't care if it was encrypted or stored in plaintext. There's no reason to. Your database tables are now full of all your customers' users' [PII](https://en.wikipedia.org/wiki/Personally_identifiable_information), and alongside sit their email address and password. A future security breach will end up with all these details leaked for the public to see. Your users will be [pwned](http://haveibeenpwned.com). 
1. **Normal people re-use passwords**: same passwords all over the web with the same unique identifier - their email address. When your data is leaked, your poor security practice is contributing to the damage that each of your users' customers' will feel. With those leaked customer credentials in hand, crackers are likely to find success in accessing other unrelated services.    
1. **You transmitted the password in the clear** - SMTP isn't encrypted, and the contents of email are available to anyone listening along the path from your server to my email inbox. 
1. **I didn't ask for this** information. Don't send it.

**Ironically, AHS or HRSmart has included this gem in their fine-print**:

![](http://i.imgur.com/Lv1MCh3.png)

The counter-argument might be something like: 

>"our #1 customer support issue is forgotten passwords, so we're pre-emptively solving that problem by emailing the user their password in case they forget. It's also convenient for non-technical users."

Stop. That's solving *your* problem as a software vendor, and probably with limited success. It also creates the problem of **leaked credentials**. Have you considered [making a password reset feature on the login page](http://www.troyhunt.com/2012/05/everything-you-ever-wanted-to-know.html) that does all that for you? 

  Things this form did correctly:

- did not ask me to provide *n* ridiculous security questions and answers for account recovery.
- showed me which fields were required with visual cues. 
- [used SSL](http://i.imgur.com/pMvFgOf.png). Actually, wait a minute, who cares if the form used SSL? The app emails the credentials in plaintext via SMTP, thereby wasting all the effort and investment on the web.

**Solution:** For identity, use another authentication service that your user trusts. 


### Feedback and Response ###

I tweeted a few times [[1]](https://twitter.com/Philoushka/status/462434155670691840) [[2]](https://twitter.com/Philoushka/status/462436248632557568) [[3]](https://twitter.com/Philoushka/status/462438911063490560) about this poor security practice, but haven't heard from either of the entities. I've [emailed HRSmart](http://i.imgur.com/rbqXHix.png) about it, but haven't heard back.

I'll post more here if anyone does respond.


### This Form Is Poorly Designed & Asks For Too Much Info Up Front ###

This is a critique of the form that the software vendor HRSmart provides their customers, who in turn present to their users. 

My goal as a visitor when visiting your site is to see what's there for me, and to take action - apply. Your goal as an application is to let me do that as easily as possible.

The ['create account' form](https://albertahealthservices.ats.hrsmart.com/cgi-bin/a/editprofile.cgi) really gets in the way. It asks for non-vital information at a vital time, and it asks for LOT of it. 

<img src="http://i.imgur.com/rsA9rhx.png" class="floatr" />

- Field titles are emphasized with red, which is a nice feature. It lets me know what I'm forced to enter. The problem is that the fields **aren't de-emphasized** (i.e. turn to black) when you've entered a valid value. So what happens? I submit the form and am punished/shown a myriad of ways that I have screwed up. Gosh, if only I had known what you wanted.
  
- Referral Source as **required** info- why does this matter at this stage? Let a recruiter ask this information in person. This info is nice for the HR department, but isn't required for the user to get their applications in. You've just forced the user through 2 dropdown boxes. Really, you want to know how well your HR recruitment efforts are doing first before actually getting the application? This information is given far too much prominence: its placement first up overtly tells me you care more about your HR recruitment events than you do about my name.

- Email Address - you JUST had me provide that as my username in step 1. **Why are you making me repeat myself?**
- City, Province, Country - you can auto-detect this information. This information is non-vital at this time. I don't expect to be sent a letter by mail or a knock on the door. Only when we engage in a contract would this information be needed.

**Non-vital **information at a vital time. Collect it later. I know that I'm in the ballpark when I apply for jobs; it's not in my best interest to apply for jobs that I'm not qualified or interested in. None of this data below is important in capturing the application. These are all candidate/profile data, and not application data. Requiring them here and now is an untimely roadblock:

- Street Address 
- Postal Code  
- Areas of expertise
- Job type
- date available
- level of education  
- previously employed
- authorization to work in Canada

I'd expect the counter-argument for this to be:

>"if we don't require people to enter this info, they'll never give it to us. We would up with incomplete data and have to chase applicants down for data. That's why we bought this software: it makes people enter their data." 

I can see how that happens if you don't guide your users appropriately. Forcing them to enter all this information up-front isn't the way to achieve your goal of complete HR applicant profiles.

### Don't Roadblock Your Users. Guide Them. ###

The goal: users want to apply for jobs. Everything else is secondary. Take away all the friction and waste in the process and have the user apply for the job.
There are secondary goals for the HR team: profile information, contact information, etc.
 
Consider this set of (simplified) workflow steps:

1. Create an account with a popular external identity provider. Make it dead simple for users to create their accounts. **Extra bonus**: you get to read the data that the user has provided you: demographic data that you're asking them to repeat into your form.

  ![](http://i.imgur.com/xe1QQIM.png)

2. Apply for job.

3. Fill in the secondary details later. You may nor may not have the policy to actually hold back the application unless the profile is complete. I'm not an HR pro, and yes I can imagine the flood of incomplete profiles. If an application doesn't fill in their profile and gives a half-hearted effort into the application, that gives you a hint, as an HR pro, to the quality of the applicant.

  ![](http://i.imgur.com/7CoRhhZ.png)

