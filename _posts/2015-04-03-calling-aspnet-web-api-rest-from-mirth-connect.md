---
layout: post
category : Mirth
tagline: "Here's how I created a REST web service for consumption by a Mirth Connect interface. Spoiler: it's easy."
tags : [Mirth,web-services]
---

I had a scenario given to/architected at me where a Mirth interface needed to call a .NET web service. The items to be sent were the name and contents of a file. In this case, Mirth isn't being used as it usually is (a health care HL7 integration engine), but used as a directory monitor. 

![](http://i.imgur.com/iRwmapV.jpg)

Mirth will pick up and process new files. In this case, it's a customer order from a scanner/fax machine, and saved as a [.tif file](https://en.wikipedia.org/wiki/Tagged_Image_File_Format). This file needs to be sent to the web application. It is my task to build the sender and web service.

The hopelessly out of date "*accepted best practice*" for web services at this customer site is *still* ASMX SOAP web services. Inertia is tough to break for some people. 

Out with the old, and hello .NET Web API. Let's build and use HTTP REST services.

### Data Flow

- Mirth detects a new file
- reads the file's contents, Base64 encodes
- sends the contents and file name to a web service. We'll POST the contents via HTTP.
- web service converts file to another format
- web service saves its work somewhere (database, file system, whatever your workflow is)
- Mirth archives/deletes the original file

### Receiver - .NET Web API Class

Instead of a SOAP ASMX web service, use a REST Web API Controller. The file can be POSTed to a method.

The file being transmitted was a .tif, but really it could be any file type. It's expecting the file contents to be incoming as Base64 encoded in the request body, along with the file name. 

Create a class to encapsulate all the data that will be required. I called mine `CustomerFile`.

Note: only *one* param is allowed in the method signature when using `FromBody` attribute on the param. This is by design in Web API.

    public class DocumentsController : ApiController
    {
      public void Post([FromBody]CustomerFile file)
      {
          byte[] incomingBytes = Convert.FromBase64String(file.FileContentsBase64);
          using (var incomingFile = new MemoryStream(incomingBytes))
          using (var tif = Bitmap.FromStream(incomingFileStream))
          using (var tifStream = new MemoryStream())
          {
              tif.Save(tifStream, ImageFormat.Tiff);
              file.PngBytes = ConvertTifToPng(tif);
              SaveIncomingFile(file);
          }
      }
    }
    public class CustomerFile
    {
        public string FileName { get; set; }
        public string FileContentsBase64 { get; set; }
    }
    
The endpoint will use the Web API defaults for route and method name: `https://localhost:6788/api/documents`. The method name is `Post`, and the route is `api/<controller name>/`. In my case it's `documents`.

### Sender - Mirth Interface

We'll use Mirth's HTTP Sender destination. Use HTTP instead of a Web Service Sender, which deals with sending SOAP messages).

I used `Raw` as the data type in the inbound and outbound templates. [Using default HL7 v2.x results in bad](http://i.imgur.com/V9rDdpm.png). Make sure **both** Source and Destination [message types are Raw](http://i.imgur.com/T8mAljT.jpg).

#### Source Transformer:

    channelMap.put("fileBase64Contents", getFileBase64());
    channelMap.put("fileName",sourceMap.get('originalFilename'));
    
    function getFileBase64()
    {
    	var fileBytes = getFileBytes();
    	return FileUtil.encode(fileBytes);
    }
    
    function getFileBytes()
    {
    	var filePath = buildFilePath(); 
    	return FileUtil.readBytes(filePath);
    }
    
    function buildFilePath()
    {
    	var filePath = sourceMap.get('fileDirectory') + "\\" + sourceMap.get('originalFilename');
    	return filePath.replace(/\\\\/g, "\\");
    }


#### Destination

We simply use those values stored in the channel variables in a JSON payload to the web service.

![](http://i.imgur.com/ExR8gxQ.jpg)

The key here is that:

- the JSON has keys that map exactly to the properties on `CustomerFile`. `FileName` and `FileContentsBase64`.
- the channel variables are put within quotes. The engine will substitute their values within the quotes.

<!--code-->

    {  
      "FileName":"${fileName}", 
      "FileContentsBase64":"${fileBase64Contents}"
    }

**Destination Properties**

- Channel Type: HTTP Sender
- URL: `http://localhost:1982/api/documents` where `documents` is the class name of your Web API controller.
- Method: `POST` - choose the right method for your scenario. I upvoted [POST vs PUT](http://stackoverflow.com/questions/630453/put-vs-post-in-rest)
- Content Type: `application/json`
- Content: your JSON with channel variables within (as above)


![](http://i.imgur.com/q63ikmc.jpg)
