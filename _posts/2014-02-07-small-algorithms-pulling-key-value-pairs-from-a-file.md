---
layout: post
category : 
tagline: "I recently had the chance to create a small algorithm to extract key-value pairs from a flat file."
tags : []
---

Someone asked me recently to help find a quick solution to this problem:

>Given a file full of these strings, find a way to extract all the key value pairs. Here's a line:

    Foo="abc" Bar="Jan 1 2010 09:33" Baz="" Qux=" "

Challenges:
* some values are empty or spaces.

###Boneheaded Approach###
[First kick was a `for` loop](http://dotnetfiddle.net/L9Svn1). It was painful. The algorithm was basically:

* try create a separation between kvp elements. Replace all `" ` with `"|`. We just made like `Foo="|abc"`. Fix/replace that `="|` with `="` 
* split on chars `"` and `=`. Careful to not kill a value with only whitespace.
* That left a List of strings in pattern
    * Key
    * Value
    * a whitespace
    repeat above

Iterate that List. 
* Save the key to a temp. variable. 
* Delete the 0th list item
* Get next top item. If key isn't empty, make a new key-value pair using the key and the val on the top of the list.
* Delete the 0th list item
* Delete the 0th list item which is a whitespace
* Continue above until the list is empty. 

###A Far More Readable Approach###
Use LINQ. Here's the [DotNetFiddle](http://dotnetfiddle.net/BoHx2d). If DotNetFiddle ever goes down, I've [saved it in a text file](http://devtxt.com/blogfiles/files/key-value-pairs-linq.txt).

The less elegant bit again is the separation of a full kvp element on Line 19.

Instead of a `Pair` class you could really use a `Dictionary<string,string>`.

<iframe width="100%" height="640" src="http://dotnetfiddle.net/Widget/BoHx2d" frameborder="0"></iframe>

