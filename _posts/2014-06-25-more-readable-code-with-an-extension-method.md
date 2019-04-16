---
layout: post
category : 
tagline: "Fewer complicated condition checks. Useful if you have lots of OR checks on the same item in a condition."
tags : []
---

*This is a bit of a **well duh** type of code blog post.*

I recently built an extension method providing readability and allowing for fewer lines of code to determine if an item is in a list. It was specifically to solve a DRY problem, and helps get rid of a lot of repeated `||` syntax ceremony in C#.

I've always liked JavaScript's arrays and particularly its `.IndexOf()` method. It helps avoid looping through a list to determine if a given item is in that list.
    
    var someColour = GetCustomerColourChoice(); //returns "red"
    var colours = ["blue","green","red","black"];
    if(colours.indexOf(someColour)>=1){
       console.log("Yep, it's in there"); 
    }  

A nice simplification would be:

    var colourIsInList = IsInList(someColour, colours);
    function IsInList(item, list){  
        return (list.indexOf(item)>-1);
    }

jQuery goes a step further and provides a nicer bit of syntax.

    var colourIndex = $.inArray(someColour, colours);
    //or more to the point:
    var colourIsInList = ($.inArray(someColour, colours) >-1);

This function returns the index of a value in an array. It returns -1 if the array doesn't contain the value. You then need to convert that to a bool value on whether that int is greater than -1.


###Over To C# ###

I see this kinds of this verbose code mostly in pre-LINQ code bases.  

    public enum Colours {Blue, Green, Red, Orange, Black}
    
    if (customer.ChosenColour == Colours.Blue || 
        customer.ChosenColour == Colours.Green ||
        customer.ChosenColour == Colours.Black) //ugh. pain.
    {
        discount = .5;
    }
This conditional check could be refactored in a few ways, first of all should be a method like `ColorIsDiscounted()`. I see stuff like this in the legacy apps I'm maintaining lately [and ugh](http://www.reactiongifs.com/r/sad.gif).

I usually refactor this kind of code to use a LINQ extension method like:

    if (new[]{Colours.Blue, Colours.Green}.Contains(customer.ChosenColour)
    {
        discount = .5;
    } 
This is still kind of awkward, right? We're putting the list first, and asking whether the subject item is in that list.

To be even more descriptive and show intent/business meaning:

    var discountedColours = new[]{Colours.Blue, Colours.Green}; 
    if (discountedColours.Contains(customer.ChosenColour)
    {
        discount = .5;
    }

This isn't enough for me though. Let's make it more readable with an extension method on the enum?

###Extension Method `In()`

Here's an extension method that allows for a more readable line of code. Here are the list values inline and hardcoded: 

    if (colour.In(PaintColour.Orange, PaintColour.Green))
    {
        discount = .2;
    }

Here's using the extension method with a variable. This works well when you're pulling from a config file, or from some other function. 

    var discountedColours = new[]{Colours.Blue, Colours.Green}; 
    if (colour.In(discountColours))
    {
        discount = .2;
    }

    public static class ColourExtensions
    {
        public static bool In(this PaintColour thisColour, params PaintColour[] colours)
        {
            return colours.Contains(thisColour);
        }
    }

###Extend To All Types

If you want to use this for any type (value type, class, or enum), you can define the extension method for `object`.

    public static class ObjectExtensions
    {
        public static bool In(this object item, params object[] list)
        {
            return list.Contains(item);
        }        
    }