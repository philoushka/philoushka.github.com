---
layout: post
category : aspnet
tagline: "Here's a class that'll make your life easier when you want to deal with saving information in cookie"
tags : [aspnet,cookies]
---

Here's a class that'll make your life easier when you want to deal with saving information in cookies on your user's browser. Everyone needs a wrapper class for all those external data-stores - session, cookies, file system, web.config and app.config, registry, log files, etc. Here's a class usable in ASP.NET Web Forms and ASP.NET MVC.

###Wrapper Class###

Drop this into your web project, and refer to its static properties to get to your cookies. Any and all simple datatypes can be used, and heck, even serialized versions of your POCO objects can be saved/retrieved here. Image if you wanted to save those shopping cart items, a collection of user prefs, or whatever, you could simply override the `.ToString()` method in your custom class.

###Just Make Properties###

The key pattern here is that you *create new properties* for each piece of data that you want to save/retrieve. This solves the problem of:

* having to remember strings all over your project. 
* ensuring no duplicates exist imagine if multiple developers created a defect by using the same string indexer for their cookie, and ended up stomping each other's value? 
* typos in cookie names. 

Instead, the cookie retrieval is done through named properties. This solution solves all those potential problems. Here's a peek at one of these properties.

    public static string UserFullName
    {
        get { return GetCookieVal(CookieItem.UserFullName); }
        set { UpdateCookieVal(CookieItem.UserFullName, value, 365); }
    }

###Enums Help###

With the aforementioned 'remembering strings' problem, the pattern that this class uses relies internally on an enum to handle the naming of the value in the cookie. The enum will boil down to an integer, but really we don't care what the key's is actually stored as in the cookie. We really only care to access/read/save the values constantly and easily from our calling code.

###Download###

You can see that I pre-loaded it with some silly properties. Be sure to change the `ApplicationName` const at the top.

<script src="https://gist.github.com/philoushka/73cbddcd737ab993efbc.js"></script>

Special thanks to Special-K!
