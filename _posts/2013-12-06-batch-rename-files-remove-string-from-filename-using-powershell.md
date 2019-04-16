---
layout: post
category : powershell
tagline: "SQL Server Management Studio scripts out 'StoredProcedure' in file names. Here's how to remove a substring in many files in a directory with one line of PowerShell."
tags : [powershell]
---

Use this PowerShell command to rename all the files in the directory to remove the "StoredProcedure" substring. This substring showed up for me when SQL Server Management Studio's Generate Scripts utility wrote the files out to disk. The same suffix is present when scripting out other objects - `View`, `Table`, etc.
 
![](http://i.imgur.com/wdd53HD.png)

###Remove Filename Substrings With PowerShell###
Open a command prompt, navigate to the directory your files are in, and run this one-liner to remove those substrings.

    PowerShell
    Dir *.StoredProcedure.sql | rename-item -newname { $_.name  -replace ".StoredProcedure","" }


![](http://i.imgur.com/w0vklHo.png)

Hat tip to [Steve's article on Tweaks.com](http://tweaks.com/windows/49459/batch-file-rename-with-windows-powershell/)
