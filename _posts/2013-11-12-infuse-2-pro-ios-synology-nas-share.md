---
layout: post
category : 
tagline: "You might have difficulty connecting your iPad or iPhone using Infuse 2 Pro to Synology NAS Shares. Come here."
tags : []
---

[Infuse 2](https://itunes.apple.com/app/id577130046) is a great video player app from [FireCore](http://firecore.com/) for iPad and iPhone. It supports playback of video loaded on your device, but additionally the Pro version allows users to stream files from network shares, typically from a PC or a NAS. With the Pro 2.0, however, there's a small wrinkle that some Synology NAS users might find. 

###Problem Connecting To Any and All Shares###

It was curious that **none** of my Synology's shares were shown in the Available Shares section. 

Futher confusing, I attempted to connect to a share, and was presented with an error message in the Infuse app: `An error occurred; the operation could not be completed`.
![](img/infuse-synology-connection-details.png)

![](img/infuse-synology-connection-error.png)

###File Share Protocol###

The problem was that my shares were being served **using AFP only**. SMB was NOT being used. [James on the Firecore support forums confirms that AFP is NOT supported by Infuse 2](http://forum.firecore.com/topic/11329?page=1#comment-66179). **You must use SMB, and not AFP.**

###Enable Windows File Service On The Synology###

Even though Infuse 2 can connect to [AFP shares](https://en.wikipedia.org/wiki/Apple_Filing_Protocol) on OSX, but not to AFP shares on the Synology.
You must enable SMB or "Windows File Service" on the Synology to allow Infuse 2 to connect to its shares.  
![](img/infuse-synology-share-windows-file-service.png)