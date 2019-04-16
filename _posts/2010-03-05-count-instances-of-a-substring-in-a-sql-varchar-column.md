---
layout: post
category : sql
tagline: "How many particular HL7 segments were in a given column."
tags : [sql,sql-server]
---

###The Problem###

Recently I needed to count how many particular HL7 segments were in a given column. Rather, I wanted to find those with 2+. I needed a solution to find how many occurrences of a substring were in a target column to be searched.
I was about to post a question on StackOverflow on this, but found the answer myself bit a bit of help from a few SQL related questions that I found while searching ([How to count instances of a character in a SQL column](http://How-to-count-instances-of-character-in-sql-column/1860478#1860478)). Funny how SO's 'search' functionality doesn't show the questions related, but when you're composing the question's title, it does a MUCH better job. 

Here's the question I would have posted:

*************************
Consider a varchar column or varchar variable holding a value like this:
   
    ABC123|foo|bar|ABC123|987|ABC123|123|DEF|456|ABC|    

The goal is to count the number of times `ABC123|` appears in that given string/column.

How would you write the algorithm in T-SQL for SQL 2005 and/or 2008?
*************************

I would suggest that mostly you'd want to take this sort of task to a higher level language, rather than do it at the database level. Sometimes you have no choice, and a customer is asking for this kind of information in a short timeframe.
 
### The Solution  ### 

* define the substring you want to find. 
* find the length of the original string 
* `REPLACE` that string with a blank 
* subtract the length of the replaced string from the length of the original 
* the remainder is the number of characters that were removed 
* the number of substrings found is found by dividing by the length of the substring 

<!-- foo -->
    DECLARE @Subj varchar(6000), 
            @Find varchar(10), 
            @NumInstances int 
    
    SELECT @Find = 'OBX|' --this is the string we want to count the occurrences of 

    , @Subj = 'MSH|^~\&|LAB|TEST|TEST||20100302132036||ORU^R01|987654321|T|2.3 PID|1||Z000000167||TESTLAST^TESTFIRST^TESTMIDDLE||19100101|M|||^^^^|||||||ABC123 PID|1||0000000135|9028520613|KGH^ECPAT^^^^||19561203|F|^^^^^||99 TESTING STREET^^TEST^CA^90210||555-333-4444|||M|NV|ABC123|ZYX987| PV1|1|P|EM^^^.|||||||||||||||ER||HP|||||||||||||||||||.||PRE| ORC|SC|0203:U00006R300.0000|||CM||||201003021319|TEST^TESTER^DR^HELLO^^^||TESTING^TEST^DR^WORLD^^^| OBR|1|0203:U00006R300.0000|0203:U00006R|Some Test^L300.0000^00024940^24356-8^Some Test Name^|||201003021319||| ||||201003021319|| TEST^TESTER^DR^HELLO^^^||||||201003021320||LAB|F||| TEST^TESTER^DR^HELLO^^^| OBX|1|ST|L300.0200^Clarity^000z4940^32167-9^Clarity|1|Clear||Clear|N|||F|||201003021320| OBX|2|ST|L300.0700^Colour^000z4940^5778-6^Colour|1|Yellow||Yellow|N|||F|||201003021320| OBX|3|NM|L300.1300^XGravity^000z4940^5811-5^XGravity|1|1.006||1-10|N|||F|||201003021320| OBX|4|NM|L300.1400^pH^000z4940^5803-2^pH|1|5.0||5.0-9.0|N|||F|||201003021320| OBX|5|ST|L300.1500^Protein^000z4940^5804-0^Protein|1|Negative|g/L|N|N|||F|||201003021320| '
    
    SELECT @NumInstances = (LEN(@Subj) - LEN(REPLACE(@Subj,@Find,'')))/LEN(@Find);     
    SELECT @NumInstances AS NumInstancesFound;
  
It'd take a tiny bit of modification to convert the logic to perform the REPLACE/LEN statement on a column, rather than a table.

    SELECT myColumn 
    FROM   myTable
    WHERE ((LEN(myColumn) - LEN(REPLACE(myColumn,@mySubstring,'')))
           / LEN(@mySubstring)) > 1 ;--where we want to find 2 or more occurrences

###Any better ways?###

Having solved the problem in a fairly string-manipulative way, I wondered if there were any other ways to achieve this in the database layer. The other possibilities:

* **Write a CLR stored procedure**. Here you could use your .NET Framework features to *easily* bust this out with a simple one-liner: `String.Split()` and `Array.Length()`. Better? Perhaps for maintainability or the abstraction of the logic. It's a bit heavy for my tastes. 
* **Set-based**. Given that's what SQL is actually for, you could perform some gymnastics on the column/variable, but the amount of code would be much more than the REPLACE/LEN solution above. 
