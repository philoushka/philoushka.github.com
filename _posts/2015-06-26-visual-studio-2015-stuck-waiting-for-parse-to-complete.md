---
layout: post
category : visual-studio
tagline: "Solved by deleting the hidden .suo file."
tags : [visual-studio]
---

Visual Studio 2015 is stuck and unresponsive on loading a solution with a message box and status.

> Loading Solution. Waiting for parse to complete... 

I wasn't sure whether it was related to a file change I had made before opening the solution. 

I solved this by deleting the `.suo` file for the project. This is a new VS 2015 path that doesn't get created in previous versions of Visual Studio.

The file is at `<solution root>\.vs\<project name>\v14\.suo`. 

    del "C:\Users\camp9\Source\Repos\myProject\.vs\myProject\v14\.suo" -force
    
![](http://i.imgur.com/aS4iN9p.png)    
