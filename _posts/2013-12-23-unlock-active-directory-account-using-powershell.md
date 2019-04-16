---
layout: post
category : 
tagline: "If you have an AD account that is locked, you can unlock it with a one-liner using PowerShell."
tags : []
---

Active Directory (AD) accounts can become locked; usually this is due to multiple failed attempts at authentication. If you need to unlock an AD user account, use PowerShell. The `Unlock-ACAccount` commandlet will help achieve this. 

    Get-ADUser myAccountName | Unlock-ADAccount


![unlocking a user's active directory account using cmdlet Unlocc-ADAccount](img/unlock-ad-account-powershell.png)

###Before And After###
<table><tr><td>**Account in Locked State**
<img src="img/unlock-ad-account-locked.png" />
</td><td>**Now Unlocked**
<img src="img/unlock-ad-account-now-unlocked.png" />
</td></tr></table>
