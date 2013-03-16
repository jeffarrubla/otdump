**SUNDAY, MARCH 3, 2013**

worknotes - helloworld with db 
=================

Ok,
Looking back at my [smaller steps plan](../02/work-notes-loginator-smaller-steps.md) blog post:

[1] helloword-cookies (cookieparser?).  DONE
[2] helloworld-db (mongdbhq?).  NOT
[3] helloworld-routes (express) ALSO DONE
[4] helloworld-session (?). NOT
[5] helloworld-authentication (passport, passport-local) NOT

It seems that the primary change from the original plan was the earlier introduction of express to allow writing the hello world following dglittle's code-style: ie make the index.htmk be just js functions that use apis to figure out the state and create appropriate displays. The server side APIs involve routing which brings the need for express.

So the next step would be to add the db layer.
In this simple next step we would
- on register
+ use the db to enforce username uniqueness
+ store the userinfo in the db
+ set the username in the cookie
+ return the complete userinfo
- on logout
+ reset the username cookie
- add a login screen that allows the user to switch to a prior user context.
+ checks for username existance and if found sets the username to the cookie
- add a change user info screen that is prefilled with the userinfo and allows one to change
the user to change first or last

```
    * Here is the github repo : https://github.com/ogt/helloworld-node-db
    * Here is the heroku app : http://helloworld-node-db.herokuapp.com (20+ sec delay at first fetch)
    * Here is the blog post about this : [http://otdump.blogspot.com/2013/03/worknotes-helloworld-with-db.html](../03/worknotes-helloworld-with-db)
```

I will use mongolab as the db.
Ok it seems that
```> heroku addons:add mongolab```
(which is equivalent to heroku addons:add mongolab:starter) ie free plan for mongolab)
is doing all the right things. It registers the add-on - and it seems to be somehow associated with the specific app. I am actually not sure what exactly that means.
I hope it means that I can get a free starter plan with every one app (as opposed to just one for my account). I hope it doesn't mean that I can't access the mongodb from two separate apps if I wanted by sharing the URI.  Even though there was a UI to add the mongo lab addon, the ability to do all that just from the command line  (with the command above) feels so ... good and powerful.
Befor I added the db code, I wanted to familiarize myself a bit with the db - I thought of using the mongo shell for that.
First attempt failed - it doesn't take heroku uris as parameter.
```> heroku config|grep mongo ```

```MONGOLAB_URI: mongodb://heroku_app1234567:some_secret_pass@ds0123456.mongolab.com:45432/heroku_app1234567```
What does the man page say?  no man page.. Googl-ing instead I find some docs, re-trying it, 
after 4 efforts and going back and forth googling for docs I am really annoyed that there is no man page.
How could it be that there is no man page? I just brew installed it. Maybe the manpath isn't right..
No, there is no mongo* in /usr/local/share/man/*/.
... 1 hr later... I have man pages.. it took quite some doing:
```
 > brew install sphinx  #that probably wasn't needed
> pip install sphinx  # building the docs requires sphinx-build
> cd /tmp
> hub clone mongodb/docs
> cd docs
> make man # fails with some docutils error  #active bug
> pip uninstall docutitls # remove current docutils
> pip install docutils==0.9.1  # last 
> make man
> cd build/master/man/man1

> man mongo.. #yeahhh

> cp * /usr/local/share/man/man1
> pip install --upgrade docutils # bring back the current version
> rm -rf /tmp/docs #cleanup
```

Luckily right after that I managed to get mongo to connect:

```
> mongo -u heroku_app1234567 -p some_secret_pass ds0123456.mongolab.com:45432/heroku_app1234567
..
```
and I got in

_Posted at 11:23 AM_