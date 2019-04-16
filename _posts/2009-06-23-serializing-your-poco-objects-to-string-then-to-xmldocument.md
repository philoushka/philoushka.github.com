---
layout: post
category : 
tagline: "Today's Dreaded Exception: Data at the root level is invalid.  Found a problem recently when seriali"
tags : []
---

**Today's Dreaded Exception**: Data at the root level is invalid.
Found a problem recently when serializing a custom object.  Here's what I was working with. Warning: [this is the bathroom wall of code](http://www.codinghorror.com/blog/archives/001268.html) version. Please **do not copy/paste** this into production.
  

    public static XmlDocument SerializeToXmlDoc(Object obj)
    {
        try
        {
            XmlDocument xmlDoc = new XmlDocument();
            string xmlString = SerializeIt(obj);
            xmlDoc.LoadXml(xmlString);
            return xmlDoc;
        }
        catch (Exception e) { return null; }
    }

    public static string SerializeIt(Object obj)
    {
        try
        {
            MemoryStream memoryStream = new MemoryStream();
            XmlSerializer xs = new XmlSerializer(obj.GetType());
            XmlTextWriter xmlTextWriter = new XmlTextWriter(memoryStream, Encoding.UTF8);
            xs.Serialize(xmlTextWriter, obj);

            memoryStream = (MemoryStream)xmlTextWriter.BaseStream;

            return UTF8ByteArrayToString(memoryStream.ToArray());                
        }
        catch (Exception e) { return null; }
    }

    private static string UTF8ByteArrayToString(byte[] characters)
    {                      
        return new UTF8Encoding().GetString(characters);            
    }

The problem that was that as I passed one of my custom objects to it, I'd get this exception:    

> Data at the root level is invalid. Line 1, position 1. 

Fine, root level… got it. Let's take a peek at what's actually trying to be loaded.

###Wait, What The?###
Here's the kicker: there was a funny null/something character at the beginning of the string, and therefore, my XmlDoc couldn't successfully execute the LoadXml method. Confessional: I scraped this method from the interwebs and its bathroom wall of code. I tweaked it to suit my needs. I figured it was ready for ANY kind of POCO object. Guess not. I have hit the 10% case where it didn't work well. Well, let's fire up the Text Visualizer and figure out why that string isn't loading into an `XmlDocument` properly.
 
![Text Visualizer Visual Studio xml string](img/xmlString.png)

Hmm. That's funny. What is that?! Turning to the Immediate Window didn't give any real answers as to the value of that unknown/bad character.

![immediate window Visual Studio 2008](img/immediate.png)

Hmm. Looks blank. I then copied that value right from the Immediate Window, pasted into Notepad, it comes out as a question mark. Nice! Here's the direct paste:

    ?xmlString.Substring(0,1)
    >"?"

###Solved!###
You could go down all kinds of kludgey roads and try to replace the first character if it's not angle bracket `<`, or try and trim null chars, etc. turns out that a `Stringwriter` will do the job well in this case. No more null character leading to a failed load of the string.
(via the bathroom wall of code at [http://asp.net2.aspfaq.com/xml-serialization/simple-serialization.html](http://asp.net2.aspfaq.com/xml-serialization/simple-serialization.html))

    public static string  SerializeIt(Object obj) 
    { 
        try {             
                var xmlSer = new System.Xml.Serialization.XmlSerializer(obj.GetType());
                using (var sw = new StringWriter())
                {
                    xmlSer.Serialize(sw, obj);                 
                    return sw.GetStringBuilder().ToString();
                } 
        }      
        catch (Exception e) {  return null; }      
    } 
    

The `MemoryStream` algorithm worked well for some of my POCO objects, but not for another.
 