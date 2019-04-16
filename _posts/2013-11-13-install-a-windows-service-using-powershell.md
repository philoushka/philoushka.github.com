---
layout: post
category : 
tagline: "Visual Studio 2012 removed support for Windows Service installer projects. Good riddance. Make your life easier by using PowerShell than that ridiculously complicated installer."
tags : []
---
Visual Studio 2012 removed support for Windows Service installer projects (vdproj) as [described by Buck Hodges in this MSDN blog post](http://blogs.msdn.com/b/buckh/archive/2011/03/17/visual-studio-setup-projects-vdproj-will-not-ship-with-future-versions-of-vs.aspx). My usage of this project type was for installing Windows Services. The experience wasn't satisfying, but rather complicated and ponderous.
 
Make your life easier by using PowerShell. If you're holding onto Visual Studio 2010 because of an installer project for a Windows service, you might consider using PowerShell.

This script will:

* initalize a few strings to be used later during installation
* convert your plaintext password to a secure string
* create a security credential for the Windows service to be run under
* check whether the service exists. if so, stop the service, and delete it.
* install the service
* optionally start the service

If you experience an error when running this script like `The specified service has been marked for deletion`, I've found that closing any instances of `services.msc` has solved that issue.

**[Download It](http://devtxt.com/files/install-service-example.ps1.txt)**
    
    $serviceName = "My Service Name"
    $exePath = "C:\Program Files\foo\bar.exe"
    $username = "someUser"
    $password = convertto-securestring -String "somePassword" -AsPlainText -Force  
    $cred = new-object -typename System.Management.Automation.PSCredential -argumentlist $username, $password
    
    $existingService = Get-WmiObject -Class Win32_Service -Filter "Name='$serviceName'"
    
    if ($existingService) 
    {
      "'$serviceName' exists already. Stopping."
      Stop-Service $serviceName
      "Waiting 3 seconds to allow existing service to stop."
      Start-Sleep -s 3
        
      $existingService.Delete()
      "Waiting 5 seconds to allow service to be uninstalled."
      Start-Sleep -s 5  
    }
    
    "Installing the service."
    New-Service -BinaryPathName $exePath -Name $serviceName -Credential $cred -DisplayName $serviceName -StartupType Automatic 
    "Installed the service."
    $ShouldStartService = Read-Host "Would you like the '$serviceName ' service started? Y or N"
    if($ShouldStartService -eq "Y")
    {
        "Starting the service."
        Start-Service $serviceName
    }
    "Completed."
