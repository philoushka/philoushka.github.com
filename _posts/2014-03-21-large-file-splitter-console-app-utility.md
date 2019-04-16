---
layout: post
category : 
tagline: "Someone asked me to split a large file. I wrote a small utility and published it to GitHub."
tags : []
---

<a href="https://github.com/philoushka/LargeFileSplitter"><img src="http://i.imgur.com/dl0lyrx.png" style="float:right"/></a>
###Utility App For Splitting Large Files###
A coworker recently asked for a data dump of a table. I put a 350MB .csv file on a shared directory, and for some reason Excel 2007 choked on the file. Hmm, that's weird. So I wrote a utility to split the large file into smaller files. 


####[Download The App At GitHub](https://github.com/philoushka/LargeFileSplitter/blob/master/CompiledBinary/LargeFileSplitter.exe)![](http://i.imgur.com/1eAJLou.png)####


The concept is that sometimes you might have a large file like a web server log, a large csv from some app, or dumped from [SSMS](https://en.wikipedia.org/wiki/SQL_Server_Management_Studio). If you actually need to open and view the files (i.e. in Excel), then you might want to have a set of smaller files. 

Otherwise, if you're searching for a needle in that haystack, you're best off to use a tool like [Notepad++](http://notepad-plus-plus.org/download) or [Sublime Text](http://www.sublimetext.com/2) and their ['find in files'](http://i.imgur.com/Ib3dcD8.png) capabilities.  

It's a simple console app that will take or ask you for 2 args:

1. The file you want to split and create multiples from.
2. The number of new files to create. 

Can you run this app from Windows Explorer or via the command line and optionally send arguments to the app.

###How Does It Work?###

The app basically does this:

* gets, cleans, and verifies the args from the user.
* loads the contents of the original file. 
* opens the source file and finds the number of <a href="#lines">lines</a>.
* calculates the number of lines to write per split file
* writes each chunk of the source to the new files

![](http://i.imgur.com/9iqlMtu.png)
<a name="lines"></a>
###Line-Based###
I took the approach of reading files by their lines, rather than their bytes. I took this approach because the files are assumed to be structured as rows/lines, and it's easier to understand from the user's point of view.
The user likely can answer better the question *"how many files would you like?"*, rather than *"how many MB each file would you like?"*.

The app attempts to read all lines from the source file into memory. It calculates the number of lines per file using

    linesPerFile = RoundUp(sourceLines / numFiles)

For relatively large files, in my tests during development, the app will internally encounter an `OutOfMemoryException` when it attempts to read all lines of a 900 MB+ file. In that case, the app will catch and retry by lazy loading the lines while processing.

The files are created by looping from `1` to `n`. Take `x` lines from the source file, and write to a new file.

<img src="http://i.imgur.com/HcW52TM.png" style="border:1px solid black" />

###Small Utility. Who Cares?###

Nobody. It's more of an effort to [prevent being the ghost who codes](http://www.troyhunt.com/2013/02/the-ghost-who-codes-how-anonymity-is.html). The compiled binary and its source code are available at my [LargeFileSplitter GitHub repository](https://github.com/philoushka/LargeFileSplitter).
