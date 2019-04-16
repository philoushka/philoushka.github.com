---
layout: post
category : c#
tagline: "On two recent projects, I've had the need to write out the properties of multiple custom entities."
tags : [c#,reflection]
---

On two recent projects, I've had the need to write out the properties of multiple custom entities. The example here will be around the venerable `Customer class. Let's pretend that a requirement would be to send an email each time a customer makes an order to a support rep in your company. Yes, we'll be logging the order to the database, but the value-add here is that the recipient of the email will receive a link to the order, plus all the details of the customer and order included in the email.
So we need to take an object, iterate through its properties and their values, and put into a string for the body of an email. 
The first thought might be: "just loop through each property and write it to the email body". That's fine, but as soon as you add a property in the future, you need to remember to change the emailing code. That's not helpful for the developer needing to maintain this application. Let's look at the [Reflection namespace in the .NET framework](http://msdn.microsoft.com/en-us/library/system.reflection.aspx). 

###Reflection in .NET###
Reflection lets you programmatically find out information about types in your assemblies at runtime. Using classes in the `System.Reflection` namespace, you can learn details of a class's methods &amp; properties. In the topic at hand, we're interested in the names, values, and datatypes of properties. You could possibly use reflection to get info at runtime about a method's parameters. 

###Override Customer.ToString()###
The `Customer` class needs its own `ToString()` method overridden. Here's the class: 
  
    using System.Reflection; 
    using System.Text;
    
    public class Customer
    {
        public string Name{ get; set; } 
        public string Email { get; set; }
        public string Address { get; set; } 
        public string City { get; set; } 
        public string State { get; set; } 
        public DateTime JoinDate { get; set; }
        public override string ToString() 
        {
            StringBuilder personString = new StringBuilder(); 
            foreach (PropertyInfo pi in this.GetType().GetProperties()) {        
                personString.AppendLine(string.Format("{0}: {1}", pi.Name, pi.GetValue(this,null))); 
            } 
            return personString.ToString(); 
        }
    }

###Use It!###

    Customer cust = new Customer{ Name = "Mike", Email = "some@dot.com", HomeAddress = "1 Some Street",State = "ZZ"};
    string customerOuput = cust.ToString(); //now put this in your email body!
    Console.WriteLine(customerOutput);
    
    /* Console will show:     
            Name: Mike
            Email: some@dot.com      
            HomeAddress: 1 Some Street      
            City:       
            State: ZZ      
            JoinDate:       
    */  

###Consider###

* collections aren't handled well. 
* complex datatypes aren't either.
* consider customizing your implementation to include special formatting for `DateTime`s.
* what happens when you want the output to have a well-formatted output for a property like `HomeAddress`. We'd probably want it to show as "Home Address".
* consider handling `null` values better than writing `"null"`.

###Wrap Up###
I know this will save developers time in two ways:
 
* Not having to iterate manually through X properties to build your string for email. That'll scale depending on the number of properties and your adeptness at Ctrl-C, Ctrl-V. 
* When you add a new simple property, you will NOT have to adjust anything for it to show in the `.ToString()` method.
 
I'm always interested to see how devs are using `System.Reflection`. 
