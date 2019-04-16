---
layout: post
category : windows
tagline: "Drop-dead easy TLS protocol, cipher, and hash configuration."
tags : [windows,ssl]
---

###IIS Crypto

This tool removes all the hassle of modifying registry settings for TLS, its ciphers, cipher order, hashes, perfect forward secrecy, etc. Set all your Windows servers to use today's recommended TLS configuration. This tools works on Windows Server 2008 and newer.

You just need to run ONE command:

    IISCryptoCli40 /best

The tool modifies all the necessary Registry keys to have the right values.

![](http://i.imgur.com/dST3RDW.png)

###Use The GUI

Simply click the <kbd>Best Practices</kbd> button. The tool selects only the settings considered modern, and removes the outdated ones. Click Apply and restart the machine. 

![](http://i.imgur.com/Gbx7wYQ.png)

The tool is developed by [Nartac Software](https://www.nartac.com/Products/IISCrypto/Download), and has been updated as the TLS landsacpe changes. The tool's code is _not_ open sourced or source-open.

###Get It

1. Via [Chocolatey](https://chocolatey.org/packages?q=nartac)

 `choco install iiscrypto-cli`
   
 or
   
 `choco install iiscrypto`
    
2. Download it from the IIS Crypto site at [Nartac Software](https://www.nartac.com/Products/IISCrypto/Download)

###Confirm at SSL Labs

Diagnose your server's new settings (after a machine restart) using [SSL Labs](https://www.ssllabs.com/ssltest/).

<a href="https://www.ssllabs.com/ssltest/analyze.html?d=github.com&s=192.30.252.130"><img src="http://i.imgur.com/4wFzajQ.png" /></a>
