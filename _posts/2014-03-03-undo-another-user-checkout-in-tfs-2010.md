---
layout: post
category : 
tagline: "Sometimes developers leave the dev team, or the organization. Sometimes you pave a dev machine with files checked out. Here's how to reset the checkout status for that user/workstation."
tags : []
---

    tf undo /workspace:machineName;domain\acct $/TeamProject/Path/To/Files/* /server:yourTfsServerName/TeamProjCollection

Sometimes I'd see an error returned: `TF249051: No URL can be found the corresponds to the following server name: Verify that the server name is correct`

Try including the full URL to the project collection:

    tf undo /workspace:machineName;domain\acct $/TeamProject/Path/To/Files/* /server:http://yourTfsServerName:8080/tfs/TeamProjCollection


Or maybe you'd rather nuke the user's workspace,

    tf workspace /delete machineName;domain\acct /server:http://yourTfsServerName:8080/tfs/TeamProjCollection
    