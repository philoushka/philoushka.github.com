---
layout: post
category : sql-server
tagline: "Use this script to move all your objects to a new schema in your SQL Server database."
tags : [sql-server,sql,tsql]
---

If you have all your objects in `dbo` (or any other schema), use this script to move them to a new schema.

<script src="https://gist.github.com/philoushka/b4a02e0a2c34e0e0c37d.js"></script>

Your objects will now be contained in the new schema.

Notes:

- this will catch `fn_diagramobjects` and `dbo.sysdiagrams` if you have the diagramming objects installed in that database.
- if the SQL statements within those stored procs specify the schema `dbo`, then they'll be broken. You'll need to go edit and recompile.
- if there are any views that explicitly specify the schema `dbo` for any tables or functions, those views will be broken. You'll then need to go alter those views.
