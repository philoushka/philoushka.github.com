---
layout: post
category : sql
tagline: "Your IDE/editor already makes it readable."
tags : [sql,software-development,habits]
---

One day I caught myself doing what I've always done - capitalizing SQL keywords as I'm writing code: `SELECT`, `FROM`, `WHERE`, `COLLATE`, `ALTER`, `INDEX`, etc. I noticed that it felt a bit awkward because I kept correcting my own typos, and acknowledged to myself that there is more friction than required - capitalizing these keywords does nothing for me at development-time, but obviously is there for the readability benefit for future devs.

Why is it engrained in me as a SQL writer that I should uppercase SQL keywords in DML and DDL statements?

Neither ANSI SQL nor any modern RDBMS requires DML or DDL statements to have keywords in caps.

For as long as I've been a developer, I've seen:

- my various teams' *Official Documented Recommended Best Practice Coding Standards.doc* has included a section stating thou shalt uppercase your SQL keywords because that's how it's always been done. The justification is some variation of uppercase being **easier to read**.
- [samples](https://msdn.microsoft.com/en-us/library/ms187731.aspx), [documentation](http://dev.mysql.com/doc/refman/5.6/en/delete.html), [examples](http://docs.oracle.com/cd/B10501_01/server.920/a96540/statements_103a.htm#2066379) from all the vendors using uppercase.
- developers follow suit. [Questions and answers online](http://stackoverflow.com/questions/292026/is-there-a-good-reason-to-use-upper-case-for-sql-keywords) largely follow this practice.

### It's Not *More* Readable ###

Having [SQL keywords](https://en.wikipedia.org/wiki/SQL#Queries) uppercased doesn't automatically make it more readable. It's more distinguishable, but at some mental cost of being shouted at.

![](http://i.imgur.com/zTk975X.png)

Keyword colorization does far more for readability than uppercase does. Your editor probably already does this for you.

**SQL in a designer**

If your SQL is written in a database IDE of some kind, or where your SQL code is contained in a stored procedure in your RDBMS, or otherwise standalone from your web application, the chances are high that you're using an editor or IDE that provides keyword styling/colorization.  

Atom, Notepad++, Sublime Text, Visual Studio Code, Eclipse, SQL Server Management Studio, Toad, pgAdmin, phpMyAdmin, and [0xDBE](https://www.jetbrains.com/dbe/) all provide keyword styling.

**Hardcoded SQL**

If SQL DML and DDL statements are native/hardcoded/inline strings in an application language, then there are readability problems that uppercase SQL keywords can solve: layout, testing/debugging, code brittleness, separation of concerns, etc.

### Why Are Samples & Documentation Capitalized Anyway? ###

It's not a coding style choice with rationale, but a technical documentation style choice.

Vendor *documentation* has its own style guide. Keywords are capitalized as a rule, and bold and italic denote other characteristics of the demonstrated syntax. 

I suspect that developers see the technical documentation styles and copy+pasted (cargo-culted) those styles into their code. The practice snowballed into dev culture and has become the seemingly default coding style. 

<a href="https://technet.microsoft.com/en-us/library/ms177563(v=sql.90).aspx" ><img src="http://i.imgur.com/i24BuVu.png" style="border:1px solid black;" /></a>

### Intertia ###

Choosing to do (continue) write SQL with uppercase keywords is obviously a style choice for each team, but ask yourself *why* you've chosen that.

Answers like *because that's how we've always done it* or *that's how they do it online* aren't reasons to continue this practice.

The tools are already in place to provide readability. Habitual uppercasing only provides friction.
