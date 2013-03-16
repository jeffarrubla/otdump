**TUESDAY, FEBRUARY 12, 2013**

Global chatbox for web apps 
=================

A friend that is writing a web app, that is getting pretty heavy usage, just fixed an error that was plaguing several users. And he commented in his blog:
I wish I had a global chatbox so as I can tell to all this users why they were getting the error and that the error was fixed.

My first reaction was to tell him to try to look for a site-wide message library. But then he is writing everything in javascript - it would probably make more sense to find something like that as disqus-like plugin.
Also, a site wide message may not be the right approach - a small number of the users encountered the error.. Maybe site-wide-message libraries have mechanisms to define user subsets that the message gets broadcasted to.
Still, a broadcast popup seems to be big of an alert for something that is a notification by nature.
What he really needs is disqus-like message/inbox plugin that allows the user to interact with the system. Possibly tickets/notifications, back and forth threads can be captured/archived there.
Or it may just as well be a more realtime js plugin that offers chat - between the application (owner/it/support) and the user.
Any of the above can be one-to-one (essentially the administrator multi-casting a message in peoples inboxes/chatboxes or a group thing where people can also interact with other users in that group.

The common thread here, is that any web app would benefit from having a "systray" (think of a bottom bar like in facebook) always there whose implementation is not the responsibility of the web app but it brings things that any web app may need. These things above are all kinds of functionality that make sense for any web app. As soon as you have that you have the ability in an out-of-band way add in the "sys tray" of the user functionality that is not in your app - either you (the application owner) by controlling the app-specific part of the systray (through options available to registered web-app administrators in some systray provider web service) or the user by controlling any personalization customization options might exist in the systray provider web service.

_Posted at 9:49 AM_