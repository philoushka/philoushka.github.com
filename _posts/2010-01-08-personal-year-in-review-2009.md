---
layout: post
category : 
tagline: "2009 was a great year for me professionally. I've focused on continually learning new things and pat"
tags : []
---

2009 was a great year for me professionally. I've focused on continually learning new things and patterns in software development. There was a fair amount of professional growth, learning, and the realization that **there is so much more to learn**. 
One benefit of taking a new job/position is that it helps you realize how much you don't know. I've taken on a few new skills/technologies, sharpened a few existing skills, and challenged myself to re-evaluate some beliefs or patterns I've held for a while. One exciting event was a presentation to the [British Columbia Health CIO Council](http://healthnet.hnet.bc.ca/hciocouncil.html ). The topic was our adoption of the Enterprise Master Patient Index project as part of the Electronic Health Record initiative. 

###Tech Learnings ###
 
####ASP.NET MVC####

![dino.png](img/dino.png) My opinion of [ASP.NET MVC](http://www.asp.net/mvc/whatisaspmvc/) went from **'terrible idea'** in 2007 to **'awesome'** today. [At first I just did not get ASP.NET MVC](http://stackoverflow.com/questions/390693/does-anyone-beside-me-just-not-get-asp-net-mvc); I thought it was classic ASP all over again, and I totally balked. I was looking for asp:GridViews and trying to output server controls. Then I got it. What really nailed it for me was Dino Esposito's talk at DevConnections in Fall 2008 where he made clear the distinction of ASP.NET (the HTTP runtime) and WebForms (the abstraction of state and page lifecycle). I'll frequently use [Hanselman's Motorcycle vs Car analogy](http://www.hanselman.com/blog/DevConnectionsTheASPNETMVCFramework.aspx). 
Not to knock on WebForms, because it's provided a lot of benefit to me, my projects,  and my customers for years. WebForms provides so much abstraction with its incredible productivity gains, but feels a bit dirty when it comes to control-over-HTML. 

![](img/aspnetmvcbook.png)I dove into ASP.NET MVC, and the NerdDinner sample app was a huge help in many respects. I followed up by purchasing the [Hanselman/Haack/Guthrie/Conery MVC book](http://www.amazon.com/Professional-ASP-NET-MVC-Wrox-Programmer/dp/0470384611), which is a **great resource**. 
I was lucky enough to develop and implement 3 MVC apps, and have 2 personal projects using ASP.NET MVC. I am excited to use ASP.NET MVC for projects where I care about markup and testability. [More from Dino on ASP.NET MVC](http://dotnetslackers.com/articles/aspnet/AnArchitecturalViewOfTheASPNETMVCFramework.aspx ). 
     
####LINQ####

![linq](img/linq.png) A major tool to discover and learn more about in 2009. Upcoming investment in the dead-tree edition of LINQ In Action http://www.manning.com/marguerie/. I am finding it fun to have a list of objects and write a LINQ query. It makes coding that much easier! I started with the 'query' syntax, but much rather prefer the 'dot notation' syntax. [The 'query' syntax for joins, however is much easier to read and write](http://stackoverflow.com/questions/1511833/linq-dot-notation-equivalent-for-join).  
####jQuery####
No question JavaScript has been a help in my web projects, but a pain to work with in the browser at development-time. Most of my logic has been server-side, but I know I can do better to give the user a better experience in using my apps. jQuery has been fun to start learning, and it's satisfying to be able to use a few lines of code with terse syntax to have your form elements behave as you want. The usability of the jQuery libraries is stunning. Truly this is a *'for-developers, by-developers*' library, like they've anticipated your needs. I have yet to have a need and not have jQuery have a solution. I am looking forward to more jQuery in 2010.    
####Systems Integration &amp; Health Care Messaging####
A major learning for me was around integrating different existing systems. I had **gotten used to creating greenfield** solutions or solutions where both/all ends were totally under my control. I had smaller integration subprojects where, for example, I was taking waterslide orders from an Excel document, and creating new records in my app. In that case, my solution was the consumer of that data. 
In my recent integration projects, the source and end consumer is a downstream system that I don't have control of. Actually my project is the broker/intermediaries between the source and destination. Further complicating things, there are 3 systems within this intermediary, each on different technology stacks. So the learning for me was to be the middle-man, and to work with constraints on both side of that data transfer.    <br>
####Unit Testing####
In my projects previous, I'd **tried** to create unit testing projects to help keep my code meet its requirements, and to keep code changes from deviating away from those requirements. Only recently have I begun to **rely** on unit tests to ensure my changes don't break. 

[![osherove_cover150.jpg](img/osherove_cover150.jpg)](http://www.manning.com/osherove/)With VS 2005, I was using NUnit to test my business logic in .dll assemblies. At the time I had lots of code in code-behind, and of course, that's difficult to put under test. Fast forward to today with Visual Studio's Test Project, I've abandoned NUnit. After writing a (large ? 70+ tests) set of unit tests for this particular set of web service logic have I finally proved to myself the value of unit tests. The payoff moments came when my implementations had to change (LINQifying some algorithm), and when new requirements/feature were added. From here on out, any important logic will be under test. **I feel a book purchase upcoming**:  [The Art of Unit Testing by Roy Osherove](http://www.manning.com/osherove/)

####Large Scale Applications####
I've had the pleasure of taking on two large scale health care applications this year. One had its technical requirements well laid out (mostly), and the other was a collaborative effort with my counterparts 500km away. Some lessons learned around large projects:  

* large numbers/skills/discipline/remoteness of team members make for interesting and different challenges on each of those attributes
* scalability will come back to bite you if you haven't prepared!

####Project Successes####

**Deployment** I was lucky enough to have been a part of a successful software project this year. I developed and deployed a large scale enterprise app that brokers 6000+ messages per day. The important attribute is that humans are directly **waiting** for these messages to cross &amp; acknowledge back to them. It would be nice to be able to be able to publish a high level systems diagram here instead. In this case, success is measured in **user acceptance**, **on-time delivery**, and **stability**.   

**Managing Changes** - A few times I've gotten the call/email or attended a meeting where a *breaking change* was discussed/agreed on. Not to get into a performance review here, but I found myself reacting quickly to those changes, and have breathed a sigh of relief when my implementation handled those changes well. Is it luck?  

###Looking Toward 2010 ###
![2010_inukshuk.jpg](img/2010_inukshuk.jpg) My answer to New Years resolutions is: why wait until the turn of the year to set goals for self-improvement? What were you doing throughout the year?! In any case, my list of professional goals this year are: 

* **Learn A New Language!** I have been listening to the endless talk of Ruby and Python. I fully value the concept of 'knowing more than one and many languages', both in software and in life. So this year, I'll be taking on (one of) Ruby, Python or F#. The great thing about these languages is that they're dynamically typed. F# is a first-class .NET language, but it's not clear whether IronRuby and IronPython will be first class languages in Visual Studio 2010. I am looking forward to F# in that it's a functional programming language. I will be learning WHEN to use a functional language, and I will be posting my findings. My first intro is [Luca Bolognese's PDC 2008 video presentation: "An Introduction to Microsoft F#"](http://channel9.msdn.com/pdc2008/TL11/).  'let' doesn't mean assign a value to a variable, but bind a value to a symbol! 

* **Deploy More Personal Projects!** There's nothing worse for a developer with ideas than to NOT convert on them. Smaller designs, shorter iterations, deploy more. Cost isn't an issue, really! 

* **Find A Good Webhost**. I think I've already done this with [SoftSys. Their .NET 3.5 hosting packages](http://www.softsyshosting.com/Win08Hosting.aspx) include SQL Server, which is my #1 requirement for hosting. Goodbye DiscountASP! 

* **Move This Blog to [SubText](http://www.subtextproject.com/)** I feel that BlogEngine.NET was an upgrade over DasBlog. Both aren't being actively developed and maintained. After having used SubText for my internal blog, I feel comfortable enough with SubText and *its continued development*! It requires SQL Server 2005 / Express. 

* **Do These Things Better**: Document changes. Make more graphs.

###How Are You Improving ?###
What professional challenges and successes did you have? How are you striving to be better in what you do? Are you 'sharpening the saw' in regards to your professional skills?