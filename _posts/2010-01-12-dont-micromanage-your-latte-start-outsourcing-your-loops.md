---
layout: post
category : 
tagline: "Consider your behaviour and desires as a customer when you visit:          a) your favourite local c"
tags : []
---

Consider your behaviour and desires as a customer when you visit:   

* your [favourite local coffee shop](blenz.com) - you specify **what you'd like**, rather than how it's made. You care about the outcome, but rarely care about the process/sequences/steps that are followed as it's being constructed.
* a Subway/Quiznos shop - you care equally about the outcome and the construction. Meats, veg, bread type, order of placement of each, precise amount of mustard, pickles, etc.

![barista](img/barista_thumb.png)
 The difference here is: you aren't instructing the coffee barista on how to steam the milk, or when to start brewing the espresso. You don't remind them that their level of ground beans is getting low, or where to store the milk. You are happy to assume they know their job best, and order of operations is properly under their control. They have their efficiencies to care about, and you're happy to let them manage that. 
Consider now your desires as a programmer when your task is to find customers with a condition. Let's say we want to use this contrived example:
    
**Find the customers whose account balance owing is over $5,000. Find the youngest customer in that set.**


###The Sandwich Model of Algorithms ###

    //find all customers with the appropriate account balance      
	var owingOver5000 = new List();
	foreach (Customer c in myCustomers)
	{
	  if (c.TotalAmountOwing > 5000)
	  {
	    owingOver5000.Add(c);
	  }
	} 
	
	var youngestCust;
	DateTime youngestBirthdate=null; 
	
	foreach(Customer c in owingOver5000)
	{
	   //initialize on the first go-round; many ways to do this.
	   if (youngestBirthdate==null)
	   {
	      youngestBirthdate=c.BirthDate;
	   } 
	
	   //find the youngest by their age
	   if (c.Birthdate < youngestBirthdate) //pretend nobody has the same birthdate ;)
	   {
	      youngestCust = c;
	   }
	}
	//you now have youngestCust populated (in most cases) 

Very fine-grain operations are explicitly laid out by the developer, and execution path follows exactly what the developer wrote. Defects and all! The number of defects is up to you! 
###The Coffee Shop Model of Algorithms ###
Consider now the Coffee Shop model of this algorithm. We'll use LINQ. 
  
    var youngestCust = myCustomers
                      .Where(c=>c.TotalAmountOwing > 5000)                    
                      .OrderBy(c=>c.BirthDate)                    
                      .SingleOrDefault(); 
                      
It should be obvious by now, if it wasn't at the start: the LINQ extension methods are doing all the looping for you, and taking care of all the small bits and housekeeping. **You as the customer, don't want to care about how it's found, but rather, you declare what you want. **

###Outsource Your Loops ###
I hate to steal/reblog Eric Lippert's thought on this, but it's worth saying once more in a different way: 

**Avoid loops. They're almost becoming a code smell. Let built-in methods and functionality do the boring non-value added logic for you.**

You should be focused on YOUR business logic or end-goals (i.e. eating your sandwich and drinking your coffee), and less on syntax + language constructs. Take advantage of more declarative constructs provided in your language/framework. LINQ is a perfect example of this. 

<sub>*this post is a mashup of [Luca Bolognese's PDC 2008 F# metaphor](http://channel9.msdn.com/pdc2008/TL11) and [Eric Lippert's post on loops](http://blogs.msdn.com/ericlippert/archive/2010/01/11/continuing-to-an-outer-loop.aspx). Apologies to both!*</sub>
