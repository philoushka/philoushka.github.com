---
layout: post
category : 
tagline: "A new project has me writing up the same old Country/State/Province reference tables. My feeling is "
tags : []
---

A new project has me writing up the same old Country/State/Province reference tables. My feeling is that these static (fairly static) entities should be normalized and referenced by foreign key. I had asked a StackOverflow question on whether other developers had this prebuilt set of [country/state/province create scripts](stackoverflow.com/questions/994539/sql-script-to-create-country-state-tables) in their toolbelt.
This is a code garage sale! Never again worry about creating and loading country and province/state data.

###Create The Schema###
Create your Country and State tables with this [CREATE SQL script](http://devtxt.com/blog/downloads/sql/CreateCountryAndState.sql.txt). As always, name the State table whatever you like (ProvState, tblState, whathaveyou).  Some folks don't like table names to be the same as reserved keywords. 

![country_state_erd](img/country_state_erd_thumb.png)

###Populating ###
Here is a collection of insert scripts to get the data populated quickly for you.

* [Canada_Provinces.sql](http://devtxt.com/blog/downloads/sql/Canada_Provinces.sql.txt)  
* [USA_States.sql](http://devtxt.com/blog/downloads/sql/USA_States.sql.txt) 
* [Mexico_States.sql](http://devtxt.com/blog/downloads/sql/Mexico_States.sql.txt)
    

###Have Fun###
Some developers go further down the normalization path by creating a City table, but I usually pass on that. As always, that decision is largely dependant on the problem domain or task at hand. 
Yippee for me - that'll be fun trying to reconcile data when someone [enters their city location incorrectly](http://www.epodunk.com/top10/misspelled/index.html) as "St. Paul" / "Tuscon" / "Pittsburg" instead of Saint Paul / Tucson / Pittsburgh.
If you would like to contribute an insert script or two for a country that you would like to see here, just tweet at me with your script!