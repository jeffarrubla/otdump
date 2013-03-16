**TUESDAY, JANUARY 22, 2013**

Re-doable tasks 
=================

A friend came back to me having finished some work whose goal was to map all the OD skills, as available through the public od api to the SO tags as available through the so api. The work had a non-trivial crowdsourcing component - since the two lists have been developed independently with different naming conventions and different approaches in deciding what should be a tag and what shouldn't. The friend used both mturk workers as well as "trusted" od hires to perform the necessary QA as well as logistics management of the whole task.

The outcome seemed really interesting and could be used in many ways. Still my obvious first question was to what extent was the process repeatable - can we be rerunning thing once every year? quarter?
I also was interested in figuring out whether the reverse map can be similarly obtained: from so to od.
The answer to both was a non-convincing so and so..

I felt a bit let down.

I think an interesting requirement of an HS task is that you can pour a comparable amount of money , press the re-do button again and get back the effects of the task done again. Of course given that several of the inputs may be selected from the environment - the result may or may not be different.

![Alt text](images/redo.jpg)

Note that we can do (and redo )* something like -

HS TASK :
look at this code and find me any bugs, fix them and send me the pull request.

Or

HS TASK :
Go and calculate how much is the activity in quora  the last 6 months using the following methodology ( following pages , counting posters etc..)

Or

HS TASK :
Go and od hire 3 folks following this particular vetting process.

A: What is interesting is that when you start re-using scripts of the past then you are forced to make them more modular and parameterizable:

**B : I see, you mean change quora for example in the task above with stackoverflow?**

A : Not exactly because the instructions for collecting the quora data are quora specific. But the rest is not, so you could actually refactor the HS code so as to redo that job all you need to do is provide instruction for capturing xx  from a site...

**B : I see, for example in the hiring example the parameter would not be just a change in the skill list but possibly a refactoring of the vetting process.**

A : Yes, actually you may find that the whole task is really a different task but it simple shares a single flow that you refactor as a library

**B : I wonder how these libraries/flows tasks are shared and found. And what makes them reusable by others not only by self.**

A : It seems that best practices for writing such flows/tasks maybe rather different than normal HS tasks . For example - there should be no personal data of any sort in such a sharable task, while there probably are lots of them in a normal HS task - given its requirement that is complete/includes all context.  This doesn't seem right...


**B : I have told you that we should not be thinking about modularizing / parameterizing / templatizing HS until after we have written a minimal amount of HS code. We always get tangled this way...**

_Posted at 2:55 PM_