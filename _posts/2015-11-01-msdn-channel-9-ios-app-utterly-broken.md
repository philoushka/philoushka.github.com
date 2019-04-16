---
layout: post
category : ios
tagline: "This app could be so useful, but is so badly broken."
tags : [ios,microsoft,channel9]
---
<style>
img{margin:5px;
   display: block;
   height: auto;
   border: 1px solid black;
   max-width: 100%;
}
</style>

###A User-Hostile App

<div style="float:right;"><img src="http://i.imgur.com/gBCnsxD.png" style="border:0;" /></div>
I used the [Channel 9 iOS app](https://itunes.apple.com/us/app/microsoft-channel-9/id994423736?mt=8) for a bit, but can't shake its poor implementation. 
It's so badly broken.

### Tap Any Menu Item to Enter The Black-Hole

It's user-hostile because 70% of its features shows you a blank/empty screen with no nav. YHou can't access these features, nor view any videos that you've downloaded. Now you have gigs of wasted space on your phone.

You're black-holed and forced to quit the app. 

You're better off uninstalling the app and [telling the Channel 9 team](https://twitter.com/ch9) why.

###Not Updated For iPhone 6 

The app isn't complied for larger display iOS devices. This results in:

- the menu bar is magnified by 2x
- the keyboard is much larger than the rest of the OS

The subtle message here is: 

- we're poor stewards of our app. We haven't cared to update this app for devices circa Sep 2014.
- hey user: your experience doesn't matter.


<img src="http://i.imgur.com/PlXtQNgm.jpg" style="margin-right:15px;" /><img src="http://i.imgur.com/wfFJ1ocm.jpg" />


###Black-Hole Blank Pages

I tapped into Featured, and get a blank screen. There was no way to go back. The user must now force quit the app.
The same blank screen + force quit scenario applies to 70% of those menu options. 

What a magnificent fail.

<img src="http://i.imgur.com/H2DNl5cm.jpg" />

###Friction: Add-to-Queue Confirmation is Unnecessary

<img src="http://i.imgur.com/UyTJC7hm.jpg" />

_**YES!** I just tapped the add to queue button. Just f$#%&* do it!_

When you add a video to your queue, you get a popup modal dialog. This is completely unnecessary. 
Modal dialogs are for situations where the choice has a large impact, or the result is difficult/expensive to undo.

If the user taps 'add to queue', then relabel the button to 'remove from queue'.

### No Look-Ahead Keyword Search

Don't make me type out my full search token. Look ahead, please.

<img src="http://i.imgur.com/GkAo1vRm.jpg" />

_I'm pretty sure you can tell what I'm searching for here._

### Friction: Force Tap Focus in Search Box 

<img src="http://i.imgur.com/m4DN0nLm.jpg" />

When you tap the magnifying glass icon to search, the search box appears, but the focus/cursor isn't given to the search box.

This forces me to tap into the box, which is friction. I *just* indicated that I wanted to search. The app should put the focus on the textbox and get me searching as fast as possible.

### Case Sensitive Search

Confusing: you get no results for `Sql` or `SQL` on a developer video site, yet lots for `sql`?
Mobile devices typically capitalize the first letter in a textbox for your convenience. 
Don't punish the user for this. The app forces friction on the user to get the search term correct.
 
<img src="http://i.imgur.com/Wa6CLfNm.jpg" style="margin-top:20px;" />
<img style="margin-top:20px;"src="http://i.imgur.com/J1iGDzom.jpg"  />

Yet when you search for all lowercase `sql`:

<img src="http://i.imgur.com/oN9E3Ham.png" style="margin-top:20px;" />
 
- *Best case:* waste the user's time in guessing how to capitalize my search token.  
- *Worst case:* make the user think you have no relevant content for `SQL`.


### Search Results WTF

When you correct your search to be all lowercase, the search results are as expected.
The search results count label isn't updated properly.

<img src="http://i.imgur.com/1JnL2Ovm.jpg" />

You cannot search within the Tags screen, regardless of that seemingly convenient-looking `Search tags` textbox.

**The textbox doesn't accept focus.**

<img src="http://i.imgur.com/FPVpIRGl.png" />

###Demo
Here's a collection of all these points.

<iframe   height="360" src="https://www.youtube.com/embed/I0gDTDJALv0" frameborder="0" allowfullscreen></iframe>

## What The App Gets Right!

Lest I look like a massive complainer, here's what I love about this app:

- it plays videos
- swipe back navigation
- native AV player
- share works perfectly
- local downloads in the quality I specify - yet this is useless because it black-holes you when you visit your downloads
- video queue
- inline show notes
