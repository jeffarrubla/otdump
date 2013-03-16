**TUESDAY, MARCH 12, 2013**

Open startups 
=================

Typically folks talk about open source - and open source is obvious in the case of software for which you deliver an executable - you are supposed to provide the source for that executable. That doesn't mean a few random source files - but instead a while set of files and a makefile that you run make on and produce the executable at least for one platform. Not all your code is in source - it may be using for example platform libraries, and even if there is not code for these libraries (e.g. you provide source code for solaris and you are using some proprietary solaris libs) - most people will consider your software opensource
 - even though you just provided a single port
 - even though the port is for a non-open source platform
 - even though your code is (dynamically) linking modules that are not open source.

![Alt text](images/clipart.png)

Why that diatribe on these 20-th century concepts.
Because when you are providing a web-service/web app/web site the question is re-opened - what does it mean to have that app to be "open source" . I remember quite a long time ago this question rage around [sourceforge](http://en.wikipedia.org/wiki/SourceForge) a decade+ old iteration on github. Sourceforge used open source elements and they themselves contributed to further improvement of these open source components but as the audience complained they didn't release openly "the glue", the rest of the facilities that would be required for someone else to do another sourceforge. The authors initially reacted that the glue is not code - its just various deployment/installation/configuration scripts (none of the language of today existed in 2000 to describes these more accurately - I do remember people calling it "glue!")  but eventually accepted the reality they were not open source and they could use open source components and they could expand with non-opensource GPL-licensed components and unlike in the case of executables they could get away with it. GPL 3.0 tried  force open-source-ness in the server side but not only it didnt get adopted but the opposite thing happened GPL fell out of favor and other less restrictive licenses become more popular in the years to come.
So what next?
I think there is a resurgence in the open-* use - to some extent driven by the success of a business model that says - if you are a free-app I give you free access if you ask for money I charge you. This type of "[fremium](http://www.forbes.com/sites/quora/2013/02/26/how-do-free-services-on-the-web-make-money/)" business model (exemplified by github, mashape etc) gives companies the opportunity to give a (costly) resource for free and boostrap their reach and still have means to make money without aggravating their original "free" users.

So I think that we will shortly need to think of "open-startups" in a mult-dimensional way.
- Open source : An open source startup is one that provides source code not just for its components but for its complete deployment system. The [crowd-funding](http://tombh.co.uk/crowdfunded-paas/) post gives an example of how heroku could enforce that : it could enable pulling from github repos (as opposed pushing only from repos in your own machine as today) and obviously for heroku to be able to pull - the github repo would have to be non-private. The combination that heroku supports only interpretive languages (as opposed to C for example) and that the complete deployment system (except the client issued heroku configs) is public would allow heroku to practically guarantee that this service can easily replicated by someone else that is willing to recreate all the third party systems (whether these are heroku addons or aws or.... anything else that is communicated via heroku config to the deployment system and acts like the "libraries" in the executable story above)
- Open data : This is a longer topic - but this blog has just crossed my 30 mins limit per post... so I will put a summary. If the service has data that is available to all users - it should provide a [non PII](http://en.wikipedia.org/wiki/Personally_identifiable_information)  version of this whole db a regular backup (like stackoverflow does). It doesn't have to make it easier to read. If it has multiple stores it doesn't have to "unify" them. It just needs to provide a regular backup that someone can restore that doesn't include data that the company is not allowed to share by the law.
In addition to that it should allow the same for each user that includes all the data that the user has access to. Again it could be multiple backups of whatever db but it should include all the data that the user has access to in the system (excluding those that are accessible to all users and included inthe previous part.
- Open finance/Open profit :
The startup uses an open system to report its income stmt and balance sheet. It should be detailed and simplified enough to allow a casual user to see
  a) how much people that work in the startup make
  b) how much third party vendors cost
  c) how much money the company makes from which source
  d) how much own money the company has in the bank (various accounts), how much owed money it has and how much  money it is owed.  (balance sheet)

How can these two (open data and open finance) be enforced?... I have some ideas - but it may not be necessary to be enforcable.

_Posted at 9:24 AM_