---
layout: post
category : C#
tagline: "I need to determine whether a list/array of integers was sequential."
tags : [C#,linq]
---

###Checking Whether A List of Numbers Is In Sequence Using C# and LINQ###

I had a situation where I needed to detect *server-side* whether the user has input numbers that would fall into a continuous sequence, starting at 1. The grid had a textbox named `Sequence`. The user could put anything in there, and not necessarily numeric. I need to determine whether my list/array of integers was sequential.

![](http://i.imgur.com/aSGwpwX.png)

###LINQ to the rescue, yet again.###

My searches didn't find any code on StackOverflow or other explicitly fitting my scenario, but I did [find an answer using `Enumerable.SequenceEqual()`](http://stackoverflow.com/a/713364/23199). So basically the .NET Framework has this functionality built-in. 

    List<string> sequences = myGrid
                             .Rows
                             .Cast<GridViewRow>()
                             .Select(r => (r.FindControl("Sequence") as TextBox).Text.Trim())
                             .ToList();  
    try
    {       
        int[] userSequence = sequences.Select(x => int.Parse(x))
                                      .OrderBy(x => x).ToArray();                
        bool isInSequence = userSequence.SequenceEqual(Enumerable.Range(1, userSequence.Count()));
    }
    catch(Exception){return false;}

The 2nd shortcut here is the `Enumerable.Range()`. It basically produces an ordered integer array from 1 to *n* to compare against the user's input. 
![](http://i.imgur.com/FGfNA1X.png)

###Readability & Maintainability####

This one line using [`Enumerable.SequenceEqual()`](http://msdn.microsoft.com/en-us/library/bb348567.aspx) saved a bunch of procedural code like this:

    for (int i = 0; i < userSequence.Count(); i++)
    {
        if (i > 0 && (userSequence[i] - 1 != userSequence[i - 1]))
        {
            isInSequence = false;
        }
    }
    isInSequence = true; 

Is the LINQ line more readable that the procedural iteration? Perhaps not. 

I'll argue though that I'd rather produce fewer lines of code, and would rather trust the framework doing the comparison work for me.

Nitpick to the .NET Framework team: I wish that method was named `AreSequencesEqual()` to be more intuitive that it's returning a bool. I could always write my own extension method to wrap this functionality.
