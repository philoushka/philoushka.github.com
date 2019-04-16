---
layout: post
category : 
tagline: "Find the StackOverflow questions best suited for you to get the Unsung Hero badge. Recently I'"
tags : []
---

[Find the StackOverflow questions best suited for you to get the Unsung Hero badge](http://odata.stackexchange.com/stackoverflow/s/456/)

Recently I've been reading/hearing lots regarding the StackOverflow badge 'Unsung Hero'. Its formal description is:

>Zero score accepted answers: more than 10 and 25% of total[![zero_thumb.png](img/zero_thumb.png)](img/zero.png)
  
So this means, in my estimation:

* the earlier in your answering you can get this, the better, or less # accepted answers required. Those with large numbers of accepted answers may be in for a long ride.
* you'll need to find a way to answer people's questions, and avoid an upvote for your answer.

###The Badge###
I'm not sure how useful this badge is for StackOverflow. I like being awarded SO badges, who doesn't?

![unsung.png](img/unsung.png)

How does this happen – answers accepted without upvotes? Does that mean it's a technically correct answer, but smells bad enough that it's not worthy of an upvote? Perhaps the answer was rude? I don't get it.

The [desirable behaviour](http://blog.stackoverflow.com/2010/07/improvements-to-badge-system/) – answering lots of questions for newbies.

###How Unsung Are You?###
You can see what your progress is on the Unsung Hero badge by using this "[How Unsung Am I](http://odata.stackexchange.com/stackoverflow/s/345/how-unsung-am-i)" query on the [StackOverflow Odata site](http://odata.stackexchange.com/stackoverflow/queries). You'll simply need your StackOverflow UserID. Easy to find – just look at the URL when you hit your profile page.

[http://odata.stackexchange.com/stackoverflow/s/345/how-unsung-am-i](http://odata.stackexchange.com/stackoverflow/s/345/how-unsung-am-i)

###The Solution to Getting Unsung Hero###
Take this query for a spin. I've written this query to determine the question that you're best suited to answer in order to help gain this Unsung Hero badge. The query finds unanswered questions:

* written by people with low reputation (<15). their reputation is such that they can't upvote your answer, but can only accept it. 
* users who recently re-visited stackoverflow 
* tagged with tags that you actively ask and answer in. your top 25 tags. 
* with a small number of answers already given. the fewer the answers = better chance for you to give a great answer.

[http://odata.stackexchange.com/stackoverflow/s/456/unsung-hero-hunter](###http://odata.stackexchange.com/stackoverflow/s/456/unsung-hero-hunter###)

Enjoy! Remember – the Odata StackOverflow is working with the [most recent StackOverflow data dump](http://blog.stackoverflow.com/category/cc-wiki-dump/) – it could be up to 30 days old.
