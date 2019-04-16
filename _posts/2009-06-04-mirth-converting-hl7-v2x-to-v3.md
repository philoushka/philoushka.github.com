---
layout: post
category : 
tagline: "The Goal: Have your HL7 v3 converted by Mirth to a specified HL7 v2 message.   The Prerequisites    "
tags : []
---



**The Goal:** Have your HL7 v3 converted by Mirth to a specified HL7 v2 message. 
###The Prerequisites###

* Using Mirth 1.8+. This may work with previous versions, but this solution hasn't been tested on anything but 1.8. 
* You know what your HL7 XML looks like. You have a sample message available. 
* You know what you want the HL7 v2 to look like. 
* You may be expecting repeating segments to be converted. That's OK, it will be covered here. 

###Let's Do It###

-1. Login to your Mirth Administrator, create a new channel. 
        
 * Give your channel a name 
 * Ensure the incoming datatype is set to HL7 v3 
 * All the other defaults are OK 
 * Save 
        
 [![1](img/1_thumb.png)](img/1_2.png)
 
 -2. Switch to the Source tab.
        
 * Ensure your Listener port is something unique. 
 * All the other defaults are OK 
        
  [![1b](img/1b_thumb.png)](img/1b_2.png)
 
 -3. Switch to the Destinations tab. 
        
 * Give the first Destination a good name 
 * Change the connector type to anything 
 * Save         

 [![3](img/3_thumb.png)](img/3_2.png)
 
 -4. Switch to the "Edit Transformer" menu option 
        
* Click "Add New Step" 
* Change the Type to "JavaScript". This walkthrough will take the JavaScript route as more code/mapping can be fit into one window. The other mappers may fit your style better! 
* Give it an appropriate name, hit Enter 
        

[![4](img/4_thumb.png)](img/4_2.png)

[![4b](img/4b_thumb.png)](img/4b_2.png)

-5. On the top right pane, click the Message Templates tab. 
       
* This is where your XML HL7 v3 template will go. If you don't have a template, you can make one up for your experimental/development purposes! 
* Find your XML HL7 v3 template, and paste it here. 
        
[![5](img/5_thumb.png)](img/5_2.png)
[![5b](img/5b_thumb.png)](img/5b_2.png)

-6. On the bottom right pane, find the Outbound Message Template. It will likely default to HL7 v3.0. 
        
* Ensure the data type dropdown shows HL7 v2.x. 
* Find your HL7 v2 template, and paste it here. Keep any default values that you have, but go through and prefix them with something unique to remind yourself to ensure that value is mapped from the HL7 v3 message. That'll help identify any mapping that has been missed. 
       
[![6](img/6_thumb.png)](img/6_2.png)
[![6b](img/6b_thumb.png)](img/6b_2.png)

-7. Click Message Trees 
        
* You'll see a tree representation of both your messages. 
        
[![7](img/7_thumb.png)](img/7_2.png)
        
-8.     Now it's time to match up the elements that you want to go from the v3 to the v2. Draggy-droppy time! Repeat this for EACH data field that you want moved from the v3 to the v2. 

* Drill down into the Outbound Message Template. Find the v2 element that you want filled. (e.g. Patient Last Name at PID 5.1) 
* Pick the Green dot icon. Drag it over and drop onto to the JavaScript window. 
* You'll now have something like this in the JavaScript code window:              

    `tmp['PID']['PID.5']['PID.5.1']`

* Type the equals sign at the end of this line. We're going to assign this value to something after the next step. Now you'll have this: 

    `tmp['PID']['PID.5']['PID.5.1'] =`
                
* Go back to the Inbound Message Template Tree. Drill down into where the Patient Last Name is at. 
* Drag and drop that Green dot icon over to the JavaScript window. Drop it off after the equals sign. 
* You should now have something like this code in your JavaScript window:              

    `tmp['PID']['PID.5']['PID.5.1']=msg['controlActProcess']['subject']['target']['identifiedPerson']['name']['family'].toString()`

* Congrats, you've just mapped one property from v3 to v2. 
* Repeat the above step as necessary for all the fields that you need transformed from v3 to v2. 
* You code any steps by hand in JavaScript now that you have the basic syntax down. I'd suggest creating new Transformer steps for each v2 segment. It will help you find/fix problems that you find for a particular segment if/when they appear. It follows the idea of modularity. 
          
[![8](img/8_thumb.png)](img/8_2.png)
[![8b](img/8b_thumb.png)](img/8b_2.png)

-9. Use this sample channel for the full solution.
        
-10. Deploy your channel and use the Send Message command.
        
* Copy/paste a V3 message with all the values filled in. 
* Click Send. 
* In the "Encoded Message" tab of the Destination Connector, you'll see your output HL7 v2. 
