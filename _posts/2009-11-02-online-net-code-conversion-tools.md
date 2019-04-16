---
layout: post
category : 
tagline: "I recently had the privilege of working on a contract where the main goal of the project was to port"
tags : []
---

I recently had the privilege of working on a contract where the main goal of the project was to port/convert the web project and associated assemblies (business and data layers) from one .NET language to another. The other tasks were around fixing a handful of defects, and adding a few bits of functionality. The project was hard-capped at a set quoted number of hours, so there was little room for error. 

The solution consisted of three .NET 3.5 projects:

*  **ASP.NET web project** - this project had roughly 10 pages and a handful of helper classes in the App_Code directory. This project had VB as its language.
*  **Business Layer Assembly** - 6 classes brokering access to the data layer. Very much pass-through code with not a lot of business logic in between the web layer and data layer. There were moderate amounts of looping and updating of the business object properties.
*  **Data Layer Assembly** - the DL included the matching DL classes for each of the 6 classes above. The most challenging (code for the converter here was the LINQ To SQL code.

###Sizing Up the Task###
The largest part of the project for me was the conversion task. All told, the conversion/translation involved:

* 12 .cs files 
* ~55 methods
* ~500 lines of code

I had previously figured the smartest way to spend my time was *not rewriting code by hand*. If there's anything a developer should be good at, it's evaluating and choosing to use the right tool for the job. That's a major part of your job as a developer!

###Enter the Telerik Batch Converter Tool###
A quick [search](http://www.bing.com/search?q=convert+vb+to+c%23) brought me to a few options: online-in-the-browser-cut-and-paste style, or full file upload.
I first noticed that [Telerik had a batch converter tool](http://converter.telerik.com/batch.aspx). This allows the user to upload a handful of source code files, and the converter will do its magic on the server. This was right up my alley, as it meant that I didn't have to laboriously *open* each code file, *copy*, *paste*, and *make* a new source code file.

[![Telerik Batch Code Converter Upload](img/TelerikBatchCodeConverter_3.png)]("http://converter.telerik.com/batch.aspx)

The initial load of the page shows the user 3 input boxes where you can browse to the location of your code file. Obviously for those ASP.NET web projects needing conversion, you don't need to upload your `.aspx` files, but rather your code-behind files. This particular project was using code-behind files, rather than inline `<script>` tags.

**Aside**: It's amazing to me that some developers are using `<script>` tags to hold their code which belongs in a code behind  `Page.aspx.cs or `.vb file. Obviously it's a style or configuration issue, but to me it just feels wrong. I like the separation of .NET code and HTML markup. Perhaps it's just a side effect of trawling the web for source code, and people are choosing to format their `.aspx to include code within, instead of posting separate files. 
Back to the task. The process is easy:

* Browse one-by-one for the files you need converted. Make sure to remember to pickup your LINQ To SQL's `.designer.vb or `.cs class. That's the file where your SQL Server tables are mapped to POCO [Plain Old CLR Objects ;) ]
* Upload, Convert and Download a .zip containing the artifacts of the conversion. Included are all the converted files, and a Report.txt file.

![Telerik Batch Code Converter Done](img/TelerikBatchCodeConverter_done.png)

###Results &amp; Conversion Report###

The real answer you're looking for is right here: **the results of the conversion with the Telerik tool, for me, were 100%**; absolutely no problems in compiling a new project with these new files added to it. I can't believe it was so easy. Here's the report that Telerik included in the .zip (irrelevant or repetitive bits snipped):
    
>Conversion Error Report (Created [datetime])   
>
>Every time a possible conversion problem is located, the file name, problem severity , and problem description are recorded. There are three levels of severity: 
>
>  Warning    = code will convert and will likely work, but conversion may need manual improvement       >
>    Minor    = code will convert, but it will likely need manual correction to work        >
>    Major    = code will not convert. It must be modified before used with converter 
>
>There are also general issues to remember when converting web sites:       
>
>   - Events connected with the Handles syntax in VB will not work in C#. Events must be connected in code or in the control markup.        >
>   
>Report Details:
>
>================================================     
>
>1: TEST.designer.cs    Minor    Your region may not convert from C# to VB if quotes have not been used to name the region. Make sure region name is surrounded in quotes before using code.
>
>2: TEST.designer.cs    Minor    Your region may not convert from C# to VB if quotes have not been used to name the region. Make sure region name is surrounded in quotes before using code. 
>
>End Report (11 total matches)
  

###Easy &amp; Accurate Results###

I can't believe it was so easy to convert the code. It really meant that I could spend more time ADDING VALUE to the project by way of **adding features** and **fixing defects** than by the drudgery of converting source between languages. The price to pay for the Telerik online batch tool was the included comments at the bottom of each source file. That's an easy price to pay! Can I say now a BIG THANK YOU to Telerik, NRefactory &amp; SharpDevelop, and [Todd Anglin @ Telerik](http://blogs.telerik.com/toddanglin/posts.aspx?page=1) for making this tool free and available for the world at large!

![](img/TelerikBatchCodeConverter_Comments_thumb.png)

###Stitching your Converted Files Back Into a Project &amp; Solution###

The tricky work is to then take the output of the converter and create a new project. For each of the assembly projects, I:

* copied all the reusable non-.NET files from the old solutions - *.xml, *.config, etc.
* made new .vbproj projects in Visual Studio
* for the web project, Add Existing Files -> Select all your converted files.

For those converting a web project, just create a new Web Project. For each of your pages, modify your .aspx  to have its Page directive to have the appropriate configurations:
  
    <%@ Page Language="VB" MasterPageFile="~/SomeMaster.master" CodeFile="SomeFile.aspx.vb"

Then do the same Add Existing Files routine for all your converted .aspx.vb or .cs files.

###Quick Online .NET VB and C# Converters###
In some cases, you'll find snippets online (yes, the bathroom wall of code) where you actually like the snippet, but rather want it in the language of your choice. I recently searched for and used both these tools when needing to convert a large snippet of VB to C#.

[DeveloperFusion's online code conversion tool](http://www.developerfusion.com/tools/convert/vb-to-csharp/)