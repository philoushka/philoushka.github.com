---
layout: post
category : 
tagline: "How to upgrade your Mirth Connect to Version 3."
tags : []
---

I recently migrated a Mirth Connect 1.8.2 system (from 2009!) to a more recent Mirth Connect 3.0.3. You **cannot** perform a straight forward and easy system backup and restore into 3.0. Here's how to upgrade Mirth Connect to v 3.0.3.

Our goals is to have your integration solution running on the most modern version possible, and with the minimum amount of downtime possible. 

###1. Get Your Files
Start by downloading the:

- [![](http://i.imgur.com/dQE54bu.png)latest Java runtime](https://www.java.com/en/download/index.jsp).
- [![](http://www.mirthcorp.com/wp-content/themes/atahualpa344/images/favicon/custom/mirth_16.ico) version of Mirth Connect](http://www.mirthcorp.com/community/downloads) you'll be using.

###2. Export From Mirth
Export all items from your current Mirth instance. Export the:

- all channels
- code templates
- global scripts
- entire system config
 
This will create a set of XML files on disk. Go commit them to source control.  

![](img/mirth-upgrade-exported-files.png)

###3. Save Your Mirth Connect Server Settings
Open Mirth Server, and copy out the settings you're currently using. I'm using SQL Server for Mirth's database, so I need to be sure to remember the login that's being used to access the current Mirth database.

![](img/mirth-upgrade-current-settings.png)

###4. Create A New Mirth Database
If you're using Derby, you can skip this step. If you're using an RDBMS for your Mirth database, this is required. This step is SQL Server specific.

1. Create a new database on the server that you'll be using. The only config I change is to set the [recovery model to simple](http://msdn.microsoft.com/en-us/library/ms189275.aspx) and the [auto-grow options to something sane](https://www.simple-talk.com/sql/database-administration/sql-server-database-growth-and-autogrowth-settings/).

![](img/mirth-upgrade-new-db.png)

2. If the login doesn't exist yet, create one. Give permissions to the SQL Server login by mapping it to a new user in the new database. You must give it role membership in `db_owner`.
 
![](img/mirth-upgrade-new-user-mapping.png)   

3. Using SSMS, log in to the database server using the SQL login to ensure that things are working as they should be. This is helpful to troubleshoot before proceeding.

###5. Stop Mirth Services & Uninstall Mirth
Stop Mirth's services on the machine and uninstall your current version of Mirth.

![](img/mirth-upgrade-stop-service.png)
![](img/mirth-upgrade-uninstall-old.png)

###6. Uninstall Any Old Java
Now's a good time to install a more modern version of Java. Uninstall your current version and install a new version. In general, the latest Mirth Connect works well with the latest Java. 

![](img/mirth-upgrade-uninstall-java.png)

###7. Install Java
It'll be branded as Oracle Java, and will proudly proclaim that it [runs on 3 billion devices](http://skeptics.stackexchange.com/q/9870/15369). Hooray!

###8. Install Mirth

![](img/mirth-upgrade-install-mirth-v3.png)

###9. Set Configuration in Mirth Server Manager

1. Open the Mirth Server Manager

![](img/mirth-upgrade-server-mgr.png)
2. Paste the details from Step 3

![](img/mirth-upgrade-server-mgr-connection.png)
3. **Restart the Mirth service.**

![](img/mirth-upgrade-server-mgr-restart.png)

###6. Import Old Scripts and Code Templates
Launch the Administrator Console and login with admin/admin. Mirth will force you to set a new password for the admin account.

Open the Edit Scripts, and find your backup from the old version of Mirth.

![](img/mirth-upgrade-import-scripts.png)


Open the Edit Code Templates, and find your backup from the old version of Mirth.

![](img/mirth-upgrade-import-code-templates.png)

###7. Import Channels
One by one, you must import each channel XML file that you've previously exported. 

1. Import Channel, and browse for a channel XML file.

![](img/mirth-upgrade-import-channel-browse.png)

2. You'll be asked to convert the channel to the v3 format, which you should accept.

![](img/mirth-upgrade-import-channel-convert.png)

3. Save the channel.

![](img/mirth-upgrade-import-channel-save.png)
When you've completed all channels, redeploy the system.

![](img/mirth-upgrade-import-channel-redeploy.png)

###8. Modify Any Code
There were a few lines of JavaScript that needed changing in my solution.
If an error presents in the dashboard log, and you don't immediately know where the offending line of code is, you cna find it in a text search in your full backup XML file.

**1. [Error In The Form For Connector TCP Sender](img/mirth-upgrade-import-channel-err-tcp-sender.png)**

 There was a value of `0` in a config item, and Mirth forced me to set it to a non-zero value.

![](img/mirth-upgrade-import-channel-err-tcp-sender-missing-value.png)

**2. Using `messageObject.getRawData()`**
`ERROR (com.mirth.connect.server.userutil.MessageObject:260): The messageObject.getRawData() method is deprecated and will soon be removed. Please use connectorMessage.getRawData() instead.`
 
I use this method to get the full HL7 message as a string. Convert any instances of `messageObject.getRawData()` to:

   `var hl7 = connectorMessage.getRawData();` 
     
**3. Using `ResponseFactory.getResponse`**
`ERROR (com.mirth.connect.server.userutil.ResponseFactory:129): The getResponse(message) method is deprecated and will soon be removed. The UNKNOWN status has also been removed; this method will return a response with the SENT status instead.`**
I use this in a channel postprocessor to create a new item in the response map to use in the custom responses. Convert any instance of  

`ResponseFactory.getSuccessResponse("")` or ` ResponseFactory.getResponse("")`
to
`ResponseFactory.getSentResponse("")`


**4. Checking `responseMap` status**
If you're using `responseMap`, and checking for successful send of a message, you will need to check for the response status of `SENT` (as in item 3 above) instead of `SUCCESS` as previous. Change

`responseMap.get('Write Message To Database').getStatus().toString() == "SUCCESS"`
to
`responseMap.get('Write Message To Database').getStatus().toString() == "SENT"`


###9. Backup Mirth

Now that you've got Mirth working in a new state, it's a perfect time to make a backup.

Export all items from your current Mirth instance. Export the:

- all channels
- code templates
- global scripts
- [entire system config](img/mirth-upgrade-backup-config.png)
 
This will create a set of XML files on disk. **Go commit them to source control.**  

 