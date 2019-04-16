---
layout: post
category : asp-net-mvc
tagline: "I've recently had the need in 2 projects where the user needs to upload files to the web application"
tags : [asp-net-mvc,uploading,jQuery]
---

I've recently had the need in 2 projects where the user needs to upload files to the web application. Previous methods in the .NET 1.1 and 2.0 timeframes made this painful. 

###Use jQuery Uploadify To Upload Files to Your Web App ###

This article will focus on the jQuery plugin [Uploadify](http://www.uploadify.com/).  It provides: 
  <table border="0" cellspacing="0" cellpadding="2" width="559">
    <tbody>
      <tr>
        <td valign="top" width="248">Benefits to the Developer</td>
        <td valign="top" width="309">Benefits to the User</td>
      </tr>
      <tr>
        <td valign="top" width="248">        
- event based development <BR>
- easy to use jQuery <BR>
- No typical file type=input 
        
        </td>
        <td valign="top" width="309">
        
- Instant and realtime feedback on how the upload is performing<BR> 
- No typical file type=input controls 
        </td>
      </tr>
    </tbody>
  </table>

The Uploadify projet site doesn't have samples for ASP.NET MVC, however. For those developing an ASP.NET MVC solution, you might be wondering how to weave in Uploadify to your Views and Controllers. There aren't too many tricks here, but it's a working solution that hopefully you can modify to your needs. 
In this solution, I've leveraged Uploadify with ASP.NET MVC.  I added in a few other features in this example, but here are the basic steps:
 
* The user clicks on the  `<input type="file">`. The Uploadify nicely styles the boring old file input control into a Flash object.
* The user chooses 1 or more files to upload
* Each file has its own upload progress bar. The jQuery fade effect is a nice touch.     
* The `'script'` attribute on the Uploadify element is important. It's the controller method that will be receiving the call. Note that instead of hard-coding the URL, we let the MVC View engine determine the route. `<%=Url.Action( "UploadPhoto","Photo")%>`    
* The script hits the Controller method. This is a POST operation.
* The Controller saves the uploaded image to disk.  (This logic should live OUTSIDE the controller in a class whose sole job is this.)
* It creates a thumbnail image, and saves that to disk.    
* The Controller returns a JSON object with the 2 pieces of data that the View needs: thumbnail and fullsize image URLs.     
* The `onComplete()` method on the Uploadify object receives the JSON object. It writes out the returned thumbnail in an `<img>` tag, and its wrapped with a link to the larger image. 

###Breaking Down the Uploadify element. ###

    $(document).ready(function () { 
        $('#fileInput').uploadify({      
           //the Flash object that sits overtop the <input type='file'> 
           'uploader': '<%=ResolveUrl("~/Scripts/Uploadify/uploadify.swf")%>',  
           'cancelImg': '<%=ResolveUrl("~/Scripts/Uploadify/cancel.png")%>',   //path to your cancel image. 
           'script': '<%=Url.Action( "UploadPhoto","Photo")%>', //don't hardcode your URL here if possible     
           //'folder': '/Uploads', //you don't really need this here; the Controller will determine where to save the upload       
           'multi': true,   //Allow the user to select many items at one time.       
           'auto': true,    //start the upload of the file(s) right away, instead of waiting for the form submission.     
           'fileExt': '*.jpg;*.png;*.gif;*.bmp;*.jpeg;',      //whitelist of file extensions.    
           'buttonText': 'Include A Picture',                 //the text you wish to show on the 'Upload' button       
           'displayData': 'speed',       
           onComplete: function (event, queueID, fileObj, response, data) 
           { 
                eval("var resp=" + response); //this is critical. You must eval the response into another object. A defect likely. To do with JSON and Uploadify together. 
                //show the thumbnails as links to the larger pictures for the user.       
                $("#uploadedImgs").append("[![" + resp.Thumb + "](img/" + resp.Thumb + ")](" + resp.NewFile + ")"); 
           }, 
           'onError': function (e, q, f, o) {
               alert("We had a problem: " + o.info); 
           } 
       }); 
    });


###Controller ###

    public class PhotoController : Controller     
    {      
        [AcceptVerbs(HttpVerbs.Post)]      
        public JsonResult UploadPhoto(HttpPostedFileBase image_upload)      
        {      
            try      
            {                  
                if ((image_upload == null) &amp;&amp; (Request.Files.Count > 0))      
                {      
                    image_upload = Request.Files[0];      
                } 

                string tempPath = Server.UrlDecode(SaveLocation);     
                string urlpath = tempPath; 

                tempPath = EnsurePathIsWellFormedForServer(tempPath); 

                string savepath = Server.MapPath(tempPath);     
                string filename = image_upload.FileName;            

                EnsurePathExistsOnDisk(savepath);     
                filename = EnsureFileNameIsUnique(filename, savepath); 

                string fileFullPath = System.IO.Path.Combine(savepath, filename);     
                image_upload.SaveAs(fileFullPath); 

                FileInfo f = new FileInfo(fileFullPath);     
                string thumbpic = string.Empty; 

                using (Image newPic = SmallJob.Helpers.Thumbnail.CreateThumbnail(Image.FromFile(fileFullPath), 25))      
                {      
                    ImageFormat iff = DetermineImageFormat(f.Extension.ToLower());      
                    newPic.Save(f.FullName.Replace(f.Extension, "-Thumb" + f.Extension), iff);      
                    thumbpic = f.Name.Replace(f.Extension, "-Thumb" + f.Extension);                   
                }      
                //return back the various details that the View wants. The URL to the Thumb and the original pic.      
                return Json(new { NewFile = urlpath + "/" + filename , Thumb = urlpath + "/" + thumbpic});      
            }      
            catch (Exception ex)      
            {      
                string errText = "Error: " + ex.Message;      
                return Json(new { Err = ex.Message });      
            }      
        } 

        public static Image CreateThumbnail(System.Drawing.Image fullSizeImage, decimal percentage)     
        {      
            if (percentage < 0)="" percentage="percentage" *="" 100;="" ensure="" the="" user="" passed="" in="" a="" full="" value="" greater="" than="" one.="" percentage="percentage" 100;="" now="" kick="" it="" down="" to="" the="" percentage.="" int="" thumbwidth="Convert.ToInt32((decimal)fullSizeImage.Width" *="" percentage);="" int="" thumbheight="Convert.ToInt32((decimal)fullSizeImage.Height" *="" percentage);="" return="" fullsizeimage.getthumbnailimage(thumbwidth,="" thumbheight,="" null,="" intptr.zero);="" }="" private="" static="" imageformat="" determineimageformat(string="" fileextension)="" {="" imageformat="" iff="null;" switch="" (fileextension)="" {="" case="" ".png":="" iff="ImageFormat.Png;" break;="" case="" ".jpeg":="" iff="ImageFormat.Jpeg;" break;="" case="" ".jpg":="" iff="ImageFormat.Jpeg;" break;="" case="" ".bmp":="" iff="ImageFormat.Bmp;" break;="" case="" ".gif":="" iff="ImageFormat.Gif;" break;="" default:="" break;="" }="" return="" iff;="" }="" private="" static="" string="" ensurepathiswellformedforserver(string="" temppath)="" {="" if="" (!temppath.startswith("~"))="" temppath="~" +="" temppath;="" if="" (!temppath.endswith("/"))="" temppath="" +="/" ;="" return="" temppath;="" }="" private="" void="" ensurepathexistsondisk(string="" savepath)="" {="" if="" (!directory.exists(savepath))="" directory.createdirectory(savepath);="" }="" private="" string="" ensurefilenameisunique(string="" filename,="" string="" savepath)="" {="" string="" tempname="filename;" int="" newfilenameindex="1;" system.io.fileinfo="" f="new" fileinfo(filename);="" string="" filenameonly="f.Name.Replace(f.Extension," string.empty);="" while="" (system.io.file.exists(savepath="" +="" "/"="" +="" filename))="" {="" filename="string.Format(" {0}-{1}{2}","="" filenameonly,="" newfilenameindex,="" f.extension);="" newfilenameindex++;="" }="" return="" filename;="" }="" private="" string="" savelocation="" {="" get="" {="" string="" uploaddir="/Uploads" ;="" if="" (!string.isnullorempty(configurationmanager.appsettings["customeruploadsdirectory"]))="" {="" uploaddir="ConfigurationManager.AppSettings[" customeruploadsdirectory"].tostring();"="" }="" return="" uploaddir;="" }="" }="" }="" ###view="" ###=""><script src="http://ajax.microsoft.com/ajax/jquery/jquery-1.4.2.min.js" type="text/javascript"></script>  
    <link href="<%=ResolveUrl("~/Scripts/Uploadify/uploadify.css")%>" rel="stylesheet" type="text/css">
    <script src="<%=ResolveUrl("~/Scripts/Uploadify/jquery.uploadify.v2.1.0.min.js")%>" type="text/javascript"></script>       
    <script src="<%=ResolveUrl("~/Scripts/Uploadify/swfobject.js")%>" type="text/javascript"></script>
    <script type="text/javascript"> 
        $(document).ready(function () { 
            $('#fileInput').uploadify({     
                'uploader': '<%=ResolveUrl("~/Scripts/Uploadify/uploadify.swf")%>',      
                'cancelImg': '<%=ResolveUrl("~/Scripts/Uploadify/cancel.png")%>',      
                'script': '<%=Url.Action( "UploadPhoto","Photo")%>', //don't hardcode your URL here if possible       
                'multi': true,      
                'auto': true,     
                'fileExt': '*.jpg;*.png;*.gif;*.bmp;*.jpeg;',    
                'buttonText': 'Include A Picture',      
                'displayData': 'speed',          
                 onComplete: function (event, queueID, fileObj, response, data) { 
                     eval("var resp=" + response);
                     $("#uploadedImgs").append("<a href='" + resp.NewFile + "'><img border='0' id='' src='" + resp.Thumb + "'/></a>");   
                 },       
                'onError': function (e, q, f, o) {      
                       alert("We had a problem: " + o.info);     
                } 
             });          
         });        
    </script> 
 
####Any Pictures to Include?####

    Include pictures here.     
    <input id="fileInput" name="fileInput" type="file">    
    <div id="uploadedImgs"></div>
