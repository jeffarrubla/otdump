**FRIDAY, FEBRUARY 22, 2013**

Work notes - loginator - smaller steps 
=================

Ok.
It seems that what I thought as the next step, ie, a system that simply allows signup/login is a bit too big of a jump, given the level of my ignorance. So I will create a sequence of helloworlds to move more incrementally.

![Alt text](images/steps.jpg)

A system that uses passport-local seems to need:
  - a db to save the information,
  - a session to remember that you are logged in,
  - cookies to allow for the session to be identified, and possibly
  - some basic routing since we have at least two urls /login and / .
Thats a lot.
So here are the steps that I would follow (found by mentally unraveling the dependencies of each of of the steps above)

- **helloword-cookies** (cookieparser?).
I would first add to my hello world the cookie functionality possibly keeping track something like the value that I entered in a form asking for a userid and my name (First, Last). After my first entry, the page should be able to display who I am and still allow me to  add a new identity
by re-filling the form.

- **helloworld-db** (mongdbhq?).
Then I would add a db to allow saving that information  (first, last) in the db keyed by my userid, save only the userid as a cookie. In the case the form would display who I am, allow me to switch identities to someone else by picking a new userid that exists already in the db, or add a new identity all together

- **helloworld-routes** (express)
I would break the single page site into multiple pages /index.html being the form that displays who
is currently logged in and gives links to logout, login-as-someone-else, register

- **helloworld-session** (?).
Then probably the next thing would be to see how I could use db backed sessions and session identifiers as the cookie in that case. In that case when I create the session I can store in there the name that I fetched from the db, and rely on that for subsequent fetches.

- **helloworld-authentication** (passport, passport-local)


_Posted at 11:27 PM_