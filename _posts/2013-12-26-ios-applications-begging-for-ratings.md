---
layout: post
category : 
tagline: "iOS apps are asking users with a modal dialog box to rate the app on the App Store. This is annoying, it interrupts the user, and makes the app look bad. These nag screens are a symptom of an underlying problem with Apple's App Store."
tags : []
---
	
**I like supporting software developers; I am one.** The software industry today has this downward trend on software pricing; Apple's App Store has made software incredibly less expensive that in the PC era. The App Store is *the* central place to get software for your iOS device. This gives the App Store a lot of power and responsibility.

To support developers and apps, I launch the App Store and give ratings in the App Store for the best apps that make me happy by giving me a great experience. I've rated my favorites: Alien Blue, Downcast, Tweetbot, and a handful of kids' games. I do it because I'm feeling mildly benevolent or throwing the developer a bone.

![](https://pbs.twimg.com/media/BcXX17gCcAEH0yK.png)
iOS applications (both on iPad and iPhone) are in the habit of asking users to rate their app. I don't have any numbers on how many apps are doing this, but it feels like this is a growing trend.

###Why Are Apps Begging For Ratings?###

As far as I can determine, developers are doing this because:

* ratings are a (supposed) way to attract new customers.
* ratings help others determine the quality level an app is at.
* the developers are lazy or aren't thinking about the user experience (UX).
* their design isn't mature enough to put rating command where it needs to be.
* the app is not, or doesn't appear to be, a top-tier application. They're fakin' it until they're makin' it.

This feels like the digital equivalent of an open hat of a street beggar. It's SEO-like scuzzy.

You don't see this in any top-tier developer; not a rating beg screen in any apps by Google, Microsoft, Chillingo, Rovio, etc. 

There's a ripple effect to this as well. As more developers put the modal nag screen up, they'll eventually get users who'll comply, and rate the app. That's a win for the developer. Another review theoretically helps with the app's positioning in the App Store; Apple doesn't publicly detail its ranking algorithms. If you're a competitor who isn't using the modal nag dialog, you may lose ground to the other apps who are using the nag dialog. As that developer, you're inclined to follow the lead of the first app, and implement the nag dialog. Unfortunately, it's a race to the bottom of your collective users' experiences.

##App Developers, Avoid This Crappy UX##

<img src="http://i.imgur.com/LuL36Cn.png" title="begging for 5 star ratings in the Apple App Store" style="float:right" />

 There are a few notes about this dialog:
 
1. The implication that my rating will help. It won't help. It would be a drop of signal in the lake of noise that is Apple's App Store search experience. This is problem #1: the App Store has a monopoly on iOS app ratings. The App Store also has a lot of friction in itself. 
2. The suggestion to rate this app with the highest rating (5 stars) is very presumptuous. It's obviously trying to help get the app the best rating it can get with the least amount of thinking on the user's part; I get it. It's just slimy.
3. Both the Dismiss and the Remind Me Later buttons do the exact same thing - bug you later.   The Dismiss button, you'd tend to believe, would close this dialog box forever. It doesn't. It will reappear on the next version of the app - the next time it's updated in the App Store.
4. This dialog appeared as soon as we hit the title screen after the app loaded.
 

###Your Dialog Is Interrupting Your User/Customer###
Dialog boxes should really be avoided. They should die, actually. They're a relic of a less civilized age. More [discussion on the appropriateness of dialog boxes](http://ux.stackexchange.com/questions/4318/should-dialogs-be-avoided-in-modern-applications) in today's UX. When I'm interrupted, I feel frustrated.

This interruption came while I was sitting playing Doodlecast, a finger painting game, with a toddler. Imagine you are a developer of an app for children: is it providing a great UX to modally pop up to a child?

###This Is A Paid App###
This app, [Sago Mini's Doodlecast](https://itunes.apple.com/ca/app/sago-mini-doodlecast/id469487373?mt=8), is **only available to paying customers** - it's $2.99. Let's be clear - I've already paid you money, and you've interrupted me to "help" you out further? That's rubbing your customer the wrong way. 

###Rating Your App Isn't My Job###
I'm a consumer. I care little about how well your app appears in search results to other users. I found your app somewhere on the internet, likely by word of mouth on Reddit or Twitter.

As a user, I don't benefit by rating the app. The title says "Help make ThisApp even better". The implication here is that a better rating will gain the developer more money, and they'd subsequently reinvest those earnings into a new version/feature and more apps in the future. If I were to actually do that, it doesn't give me any immediate benefit. Meh.

**My only concern is to use the app.** Whether the app is for productivity, enjoyment, communications, or learning, I have only ventured into this app to do that one thing. Rating your app isn't one of those things. Your modal nag dialog is getting in the way of using the app.

###Reviewing Is Friction When It's Not On My Schedule###
When you actually choose to go out of your way to review an app in the App Store, it isn't always a great experience. Half the time I choose to review an app using this type of prompt, the App Store opens, but the **App Store displays only a blank screen; the review form doesn't even load**, or I need to reauthenticate with the App Store with my Apple ID. The end result is I have to do **more** work. Now I need to come up with an intelligent sentence about how the app performs, or how I approve of the app.

##Make It Better##
The task of making your app findable in the App Store is Apple's job. The task of marketing your app to potential customers is **your** job as a developer. There are all kinds of avenues to getting the word out to potential users and customers. The App Store shouldn't be the one and only place to concentrate your efforts. Here's how I'd want an app to deal with ratings:

1. Provide a <a href="http://i.imgur.com/gJGSEJK.png">link or button to the App Store review site somewhere in your settings pages</a>. I'd be happy to see that option there without it being modal'd in my face.
2. If you must make me aware of your ratings need, create a drop banner visible for 5 seconds asking. Don't make it modal. Just make it seen by the user and move on.
3. Anytime the app registers a click on that review link/button, it should remember it forever and never ask me to review again.
4. The App Store needs to improve. Apple has let this issue stagnate, and they have the power to fix the underlying problem that's causing the symptoms above. Apple should:
    1. allow users to modify their ratings after their problem/beef is solved.
    2. allow developers to respond to ratings. So often you see a rating that says "Doesn't work on the beta of the new iOS. 1 star until you fix this" or "It doesn't have feature X, so I hate this app, 1 star". These people are harmful to the Store and the app with these comments and ratings. If developers had a chance to respond to each entry, they'd be able to clear the air.
    3. Make it a policy that apps *not* show modal nag/beg dialogs to their users and ask for 5 star ratings.