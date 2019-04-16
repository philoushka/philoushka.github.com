---
layout: post
category : visual-studio
tagline: "Run the current unit test"
tags : [visual-studio,unit-testing]
---

When hammering away at a unit test, I often found myself wanting to test the current unit test and its associated code. I of course wanted to use the debugger, break points, inspect values, use the Watch tool, etc.
###The First Iteration ###

* Put the cursor in the test method. 
* Go to Visual Studio IDE's menu  
* Click Tools - Run - Tests in Current Context 
* Debug as per normal 

![ide](img/ide5.png)

###Uh, Do It Smarter###
Then I remembered that you could put the shortcuts in the right click context menu. Ah ha!

![rightclick](img/rightclick_3.png)

You can see where this is going if you paid attention to the first iteration, as well as the title of this blog post. Taking your hands off the keyboard to move to the mouse adds so much more wasted time in development. File this under "what were you thinking?".

###Smartest###
Now it's all keyboard goodness:

* Cursor in the test method 
* use a cute mnemonic in your head when you're typing in this combo. Re Test
* **Ctrl-R, Ctrl-T**
    
What is YOUR favorite Visual Studio keyboard shortcut?
