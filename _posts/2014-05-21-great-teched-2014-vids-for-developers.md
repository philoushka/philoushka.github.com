---
layout: post
category : 
tagline: "My roundup of the best or most interesting videos from TechEd 2014 as a web and ASP.NET developer."
tags : []
---
<style>
  .vidCategory {padding-top: 40px;}
   h3 {padding-top:10px;}
</style>
<script src="http://ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js"></script>
<script type="text/javascript">

    $(function () {
        
        var vids = [
        { id: "DEV-B385", title: "Intro: The Future of .NET on the Server" ,category:"aspnet"},
        { id: "FDN05", title: "Hanselman Speed Run - Apps Spanning Devices & Services" ,category:"aspnet"},
        { id: "FDN04", title: "Modern App Lifecycle Management" ,category:"vs"},
        { id: "DEV-B413", title: "Modern Web & Visual Studio", category: "vs" },
        { id: "DEV-B411", title: "Deep Dive on ASP.NET vNext" ,category:"aspnet"},
        { id: "DEV-B416", title: "SignalR: Building Real-Time Applications" ,category:"aspnet"},
        { id: "DEV-B418", title: "Performance Optimization" ,category:"aspnet"},
        { id: "DEV-B310", title: "Getting Started With TypeScript" ,category:"typescript"},
        { id: "DEV-B339", title: "Large Scale TypeScript Apps", category: "typescript" },
        { id: "DEV-B211", title: "Getting Started With VS Online", category: "vs" },
        { id: "DCIM-B386", title: "Mark Russinovich & Mark Minasi on Cloud Computing" ,category:"cloud"},
        { id: "DEV-B352", title: "Debugging Tips and Tricks in Visual Studio 2013", category: "vs" },
        { id: "DEV-B321", title: "Visual Studio Power User: Tips and Tricks", category: "vs" },
        { id: "DEV-B412", title: "Deep Dive: Dependency Injection. Decoupled And Testable Code", category: "lang" },
        { id: "DEV-B336", title: "The Future of Visual Basic and C#" ,category:"lang"},
        { id: "DEV-B362", title: "Async Best Practices for C# and Visual Basic" ,category:"lang"},
        { id: "DBI-B489", title: "SQL Server Query Plan Analysis" ,category:"sql"}
        ];

        $.each(vids, function (index, vid) {
            var ch9Embed = "<iframe src='http://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/" + vid.id + "/player?h=540&w=960' style='height:540px;width:960px;' allowFullScreen frameBorder='0' scrolling='no'></iframe>";
            var vidItemHtml = "<h3>" + vid.title + "</h3>" + ch9Embed  ;
            $("#"+vid.category+"List").append(vidItemHtml);
        });
    });
</script>
TechEd North America 2014 in Houston was reportedly had a bit more focus on dev topics than IT and infrastructure; well at least in its keynotes.

These are my recommended web devs from TechEd 2014. This seems like a ridiculously long list. 
    
<div id="aspnetList" class="vidCategory"></div>
<div id="langList" class="vidCategory"></div>
<div id="vsList" class="vidCategory"></div>
<div id="cloudList" class="vidCategory"></div>
<div id="typescriptList" class="vidCategory"></div>
<div id="sqlList" class="vidCategory"></div>
    
