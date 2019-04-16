---
layout: post
category : 
tagline: "Starting to contribute to GitHub projects, from a newbie's perspective. Lessons learned early."
tags : []
---

GitHub's bootbamp and intros mention [getting social](https://help.github.com/articles/be-social). That's cool, I guess. I interpret it loosely as 'coding alongside strangers whom you have never met'. Perhaps the team members are active on Twitter, and you're vaguely familiar with them, or you've seen them speak at conferences, and perhaps you've had zero interaction. 

I'm coming from the point of view of a typical dayjob LOB/enterprise developer in an office setting. I'm used to interacting on a team locally in the same physical space where small short discussions happen spontaneously and planned. Rarely have I contributed source code with multiple developers remotely. 

I found myself thinking/worrying about a few things while coding on a forked repo recently.

**Refactoring** - how far and deep should I refactor? Do all developers appreciate smaller, tighter and more methods? How will your variable renaming and method refactoring be received by the repo owner in your pull request?  

I've settled on the idea that perhaps if a refactoring didn't break functionality, and you're confident that your refactoring made the code readable, and the project owner doesn't accept the pull request because there was too much change, then perhaps this project isn't for you - and that's OK. Next step: move on, find another project (there isn't a shortage of projects that could use your efforts!) where the repo owner would be more . Reflect a little, perhaps write a blog post about your experience and the positive things you learned. Realize then that your efforts were good, and the mismatch is likely not your fault, but an indication about future interactions. 

**Am I pushing too many changes at once?** - it's super easy to make a whole bunch of changes and package them all into one commit. The problem comes when your commit message doesn't cover all the changes that you made. I know I am prone to making changes to suit my mental model, and have stopped midway to ask whether it's needed here. Refactoring is great, but go back to your issues list. Make an issue and discuss with other contributors. Pull out 2 or 3 examples and ask if this kind of refactor is welcome. The answers that the other contributors have will be helpful in whether those changes should be made. If and when you do make them, put them in their own commit for review, and don't tie in with another issue/fix that you're solving.

**Code style/Layout** - when we're discussing source code, there are trivial things that surface - things like like **curly brace style**(same line or new line), **tabs v. spaces**, naming conventions, etc. When your editor converts one to the other, your subsequent commits and pull request will show that as a change. That adds a small mental hurdle for the repo owner when reviewing your pull request. Perhaps the owner had some guidance in their readme around the conventions; if not, ask via an issue. Agree on a style, or agree to not care, and configure your editor to suit. I can see how that might get to be a pain when you're contributing to multiple projects, and switching around constantly.

**Someone will be reading this** - *I need to make this code bulletproof. I had better make this code clean and tight. I'm going to be judged on the quality of my code here.* I am getting the sense that this feeling is natural, and probably more in your head than reality. Also it's a good opportunity to remind yourself not to judge people based on their code. It's tough, but realize that everybody's learning... always.
 
**Eeek. Is my code too basic? Am I contributing code that's too unnecessarily complicated?** Should I be `async`'ing here? Dang, which pattern would fit best here? I've renamed a variable to be more descriptive. Hrrrmmmm. Why was it short in the first place? 

Don't worry about that stuff. It's not a contest, but rather about leveling-up the code base and making the project better. If you need to stop and think about it, go make an issue and discuss with other contributors. Commit your code in a basic format, and you can discuss and return later to add/refactor to include that async hotness. Make an issue specifying that it's a to-do item. This might be more of a self-confidence or getting to know the other devs on the team, and getting to a place where you feel comfortable around them.

#### tl;dr
Create an issue on the repo page to ask questions and talk about issues before you embark on a change that you're unsure of. The more you discuss, the more the whole team learns.

Remember - projects are open-sourced, and on GitHub for a reason - devs want to collaborate and improve the project. 

Read the readme.