**FRIDAY, MARCH 1, 2013**

Open source library vs service 
=================

I was looking at the  [clockwork raven](http://twitter.github.com/clockworkraven/) - the open source ui layer for mturk by twitter.
In summary, if you are a company with many people that do often mturk jobs - it would be handy -
its a ruby app that provides a UI with a few templates that makes it rather easy to
submit a task batch - a csv + a form editor + a few prebuilt form templates to get started + a mode to self test the form before you push it mturk + a console for reviewing all of your active/inactive job batches.

Of course given its original use (internal twitter tool - single installation/setup many users using it) this app is not ideal for the more common user.
It has more than a half hour of configuration/installation plus it requires that you will allocate a ec2 box - it needs a mysql, a redis for resque and something (ldap server etc) for authentication.

*Q : So like everything else that looks like that I wonder: why don't the people that put all the effort to write the code don't put the minimal effort to setup the service instead?*
A : The answer is because setting up such a service adds up significantly in the long term in terms of support and cost probably more than the actual cost of polishing-up and open sourcing what the guys have already done.

*Q: But is this really true? Even using a service like heroku?*
A: Heroku would be even more expensive than EC2. web + worker + dbs..

*Q: Ok. So if someone is willing to pay this 50-100/mo and a bit of occassional IT support they can convert this open source layer into an even more useful service that can be used by many more people?*
A: Actually no. Because there is still configuration left over. That someone will still need to think about creating aws account,  figuring out the keys etc.

*Q: So I think we are getting somewhere. If someone were to bring that service up as described above but against their own aws account - then there would be no configuration left over, right?*
A: Sorry to disappoint you but you are forgetting one last thing - the user authentication. Some how the guy that hosts the service against their own aws account need to allow users to signup and probably pay-up a (micro-)balance that they can then use for this service. All that is new code that has to be written.

*Q:I think this is one more of this service that needs the above - the appstore convenience of autheticating/micropayments. Nice... *

Of course now that I think about it, something that another friend mentioned maybe also interesting:
This service can definitely leverage an abstraction layer on top of anything that has a crowd-api, meaning anything that can be translated into an mturk equivalent job/task submission.
In that case we can be adding plugins for a variety of such services - be it transcription/translation/freebies like captcha...The caller will still need to pick the target provider of the service - but the abstraction layer can take the csv+questionaire form and convert it appropriately.

Hm...the freebie case is interesting. Allowing people that setup a questionaire/evaluation to actually share it (email to friends, or social sharing) with the purpose of getting some help from their friends to get the job done is actually interesting. No money needed - you get top notch trusted quality, the platform gets instant viral-loops.... Hm, of course the problem is that people would not help that easily. They would need some sort of incentive. Badges and "Galon blood donor" bumper stickers come to mind. The whole recognition thing not public but within a social circle could be a strong incentive. And in those cases something that people can do casually (not working), ie on iphone/ipad/fbook app may be the right approach. I think I have seen this somewhere... Maybe not.

_Posted at 10:17 PM_