---
layout: post
category : 
tagline: "Perhaps you've got a collection of objects that you want ordered/sorted. I recently did. Perhaps you"
tags : []
---

Perhaps you've got a collection of objects that you want ordered/sorted. I recently did. Perhaps you want them displayed in a non-deterministic manner or sorted randomly each time you write to an HTML view or otherwise consume that collection.  

###`Randomize()`###
So imagine we're working with a `List` of Customers.

![data](img/data_thumb.png)

Problem being, we don't really have anything non-deterministic to work with. We could do this in SQL Server:

      SELECT *,
	        (sin(Cust.ID * rand())) AS R
	   FROM Cust
	   ORDER BY R;
  
  
This though, puts your presentation logic in your data tier. Maybe you don't care, maybe it's not a big price to pay. I wanted to take it up to the presentation tier and do this sorting right before binding or writing these objects to the page.
Taking the [lead from Bruno Silva](http://brunosilva.net/list-random-order-in-net-using-linq/534/), I immediately realized this was the seed of the algorithm that I was looking for. Here's my modification of Bruno's algorithm:
  
    var r = new Random();
    myCusts.OrderBy(x=>(r.Next())); 
	 //bind this, or use in a foreach
  
The call to `r.Next()` is obviously the key. Each object as it is evaluated in the `OrderBy()` will get a new random number associated with it. Celebrate good times! 
###Turn It Into an Extension Method###
I haven't written much here about how much I love extension methods in the .NET CLR 3.0. I can't count the number of times that I've created a static 'utility' method that did something like this:

* take in an object of some kind. 
* modify it. 
* return it back to the caller. 
* caller reassigns the return back into the object that it calls. 

Rather than the above, I've created an extension method that I'll be able to call whenever for any collection that implements `IEnumerable<t>`. It's trivial then to write the extension method for `IQueryable`.
  
[![ExtensionMethod](img/ExtensionMethod_thumb.png)](http://www.extensionmethod.net) I've [submitted my `Randomize()` extension method](http://extensionmethod.net/Details.aspx?ID=236) over at [ExtensionMethod.net](http://www.ExtensionMethod.net). What a great site, by the way, kudos to those guys for taking user submissions and helping grow the use of this feature in .NET.

  
    public static IEnumerable<t> Randomize<t>(this IEnumerable<t> target)      
	 {       
	     var r = new Random();
        return target.OrderBy(x=>(r.Next()));
    }   