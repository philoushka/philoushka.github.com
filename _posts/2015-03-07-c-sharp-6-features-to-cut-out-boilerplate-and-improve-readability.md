---
layout: post
category : C#
tagline: "Combining 3 new features of C# 6 to makes a configuration class easier to read and maintain."
tags : [C#]
---

If you have a class in your .NET application that reads configuration values from `app.Config` or `web.Config`, you can take advantage of three new C# 6 features.

- the `nameof` expression - this produces a string literal of the name of a property or parameter.
- `using static` clause - this helps us be more DRY and not have to repeat `ConfigurationManager` each time we call out to the config file.
- Expression bodied properties - saving the boiler place of the [full syntax ceremony](http://i.imgur.com/lPWVNPm.png) of a `get` accessor and `return` statement. Repeat this multiple times, and it's a significant boost in readability.

### Put It Together

Here's my class refactored to use all 3 new features. It's smaller, less error prone, and easier to read. Adding a new property to this class is a simple copy, paste, and replace. Even handier still would be to create a snippet; you'd need to replace only 1 token in the snippet.
 
    using static System.Configuration.ConfigurationManager;
    ...
    
    public static string SomePassword => AppSettings[nameof(SomePassword)];
    
    public static string ApiKey => AppSettings[nameof(ApiKey)];
    
    public static string SomeDb => ConnectionStrings[nameof(SomeDb)].ConnectionString;
    
    
**Assumption**
  
This assumes that the name of your property `SomePassword` is the **exact same** as the key within your `appSettings` element.

    <add key="SomePassword" value="someValue" />
  
More at [New Features in C# 6](http://blogs.msdn.com/b/csharpfaq/archive/2014/11/20/new-features-in-c-6.aspx)   
       
<iframe src="//channel9.msdn.com/Events/Visual-Studio/Connect-event-2014/116/player?format=html5" width="960" height="540" allowFullScreen frameBorder="0"></iframe>
