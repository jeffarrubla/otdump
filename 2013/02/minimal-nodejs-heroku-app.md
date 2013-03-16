**SUNDAY, FEBRUARY 17, 2013**

Work notes - a minimal node.js heroku app 
=================

Here are the final instructions: (prerequisites brew instal node npm hub, and [minimal web server](https://github.com/ogt/helloworld-js-heroku/blob/master/web.js) )
(trying to see if embedded gists are better ... they look better but its too much work for each little piece of code....)  

```
> mkdir ~/Dropbox/Home/code/node/helloworld-js-heroku
> cd !$
> # add a minimal hello world app
> cat > index.html
<html>
<body>
hello world!!!
</body>
</html>
^D
> # add a minimal web server that needs no dependencies from
> cp ../helloworld/web.js .
> heroku login
> cat > package.json
{
  "name": "node-example",
  "version": "0.0.1",
  "dependencies": {
  },
  "engines": {
    "node": "0.8.x",
    "npm": "1.1.x"
  }
}
^D
> npm install
npm WARN package.json node-example@0.0.1 No README.md file found!
> cat > README.md
Simplest possible hello world heroku node.js app
> npm install  #note that no node_modules was added since we have no dependencies
> ls
/                    README.md             package.json
../                  index.html            web.js
> 
> cat > Procfile
web: node web.js
^D
> foreman start
12:19:11 web.1     | started with pid 35582
12:19:11 web.1     | Server running at http://127.0.0.1:8000/
...

> open http://127.0.0.1:8000/

...
12:19:30 web.1     | /index.html
12:19:30 web.1     | /favicon.ico
^C
> cat > .gitignore
.*
!/.gitignore
^D
> git init
> git add .
> git commit -m "init"
> heroku create
Creating calm-taiga-3864... done, stack is cedar
http://calm-taiga-3864.herokuapp.com/ | git@heroku.com:calm-taiga-3864.git
Git remote heroku added
> git push heroku master
..... (lots of stuff)
http://calm-taiga-3864.herokuapp.com deployed to Heroku

To git@heroku.com:calm-taiga-3864.git
 * [new branch]      master -> master
> heroku ps:scale web=1
Scaling web processes... done, now running 1
> heroku open
....

> hub create -d 'hello world app in node.js for heroku'
github.com username: ogt
github.com password for ogt (never stored): 
Updating origin
created repository: ogt/helloworld-js-heroku

> git push -u origin master
...
Total 11 (delta 2), reused 0 (delta 0)
To git@github.com:ogt/helloworld-js-heroku.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.

>
```

Here is the github repo : [https://github.com/ogt/helloworld-js-heroku/](https://github.com/ogt/helloworld-js-heroku/)
Here is the heroku app : [http://calm-taiga-3864.herokuapp.com/](calm-taiga-3864.herokuapp.com)  (20+ sec delay at first fetch)
Here is the blog post about this : [http://otdump.blogspot.com/2013/02/minimal-nodejs-heroku-app.html](../02/minimal-nodejs-heroku-app.md)

Here is how I found them:

In my machine here is what it take to run the most minimal node.js app:

```
> mkdir ~/Dropbox/Home/code/node/helloworld
> cd !$
> cat > index.html
<html>
<body>
hello world!!!
</body>
</html>
> node ../simplewebserver/web.js &
Server running at http://127.0.0.1:8081/
> open http://127.0.0.1:8081/
```

Pretty simple (given that I have already brew installed node/npm).
Now you may ask what the heck is simplewebserver/web.js? Its the simplest no-dependency requiring file serving node.js code I have found from some prior node.js play-attempts of mine.
Here is the code:

```
> cat ../node/simplewebserver/web.js 
var http = require('http');
var fs = require('fs');
var path = require('path');

http.createServer(function (request, response) {

    console.log(request.url)
     
    var filePath = '.' + request.url;
    if (filePath.match('/[^.]*$')) filePath += '/'
    if (filePath.match('/$')) filePath += 'index.html'
         
    var extname = path.extname(filePath);
    var contentType = 'text/html';
    switch (extname) {
        case '.js':
            contentType = 'text/javascript';
            break;
        case '.css':
            contentType = 'text/css';
            break;
        case '.jpeg':
            contentType = 'image/jpeg';
            break;
    }
     
    path.exists(filePath, function(exists) {
     
        if (exists) {
            fs.readFile(filePath, function(error, content) {
                if (error) {
                    response.writeHead(500);
                    response.end();
                }
                else {
                    response.writeHead(200, { 'Content-Type': contentType });
                    response.end(content, 'utf-8');
                }
            });
        }
        else {
            response.writeHead(404);
            response.end();
        }
    });
     
}).listen(8000);

console.log('Server running at http://127.0.0.1:8000/');
```

Ok, What does it take to get that minimal hello world app running on heroku?

Following the [instructions at github](https://devcenter.heroku.com/articles/nodejs#local-workstation-setup)

```
> mkdir ~/Dropbox/Home/code/node/heroku-helloworld
> cd !$
> cp ../helloworld/index.html .
> cp ../simplewebserver/web.js .

> heroku login
> cat > package.json
{
  "name": "node-example",
  "version": "0.0.1",
  "dependencies": {
  },
  "engines": {
    "node": "0.8.x",
    "npm": "1.1.x"
  }
}
> npm install
npm WARN package.json node-example@0.0.1 No README.md file found!
> cat README.md
Simplest possible hello world heroku node.js app
> npm install
> ls
/                    README.md             package.json
../                  index.html            web.js
> cat > Procfile
web: node web.js
> foreman start
12:19:11 web.1     | started with pid 35582
12:19:11 web.1     | Server running at http://127.0.0.1:8000/

> open http://127.0.0.1:8000/

...
12:19:30 web.1     | /index.html
12:19:30 web.1     | path.exists is now called `fs.exists`.
12:19:30 web.1     | /favicon.ico
^C

# edit web.js and replace path.exists with fs.exists
#refresh browser

...
12:20:42 web.1     | /index.html
12:20:42 web.1     | /favicon.ico
```

ok things work normal locally
lets add to git 

```
> cat > .gitignore
.*
!/.gitignore
> git init
> git add .
> git commit -m "init"
> heroku create
Creating calm-taiga-3864... done, stack is cedar
http://calm-taiga-3864.herokuapp.com/ | git@heroku.com:calm-taiga-3864.git
Git remote heroku added
> git push heroku master
..... (lots of stuff)
http://calm-taiga-3864.herokuapp.com deployed to Heroku

To git@heroku.com:calm-taiga-3864.git
 * [new branch]      master -> master
> heroku ps:scale web=1
Scaling web processes... done, now running 1
> heroku open
Opening calm-taiga-3864... done
```

And here I get a crash
Logs show just that the app crashed.

```
> heroku logs
2013-02-17T20:29:29+00:00 heroku[router]: at=error code=H10 desc="App crashed" method=GET path=/ host=calm-taiga-3864.herokuapp.com fwd="50.0.42.114" dyno= queue= wait= connect= service= status=503 bytes=
```

I repeat while running heroku logs tail

```
> heroku logs --tail
> heroku ps:scale web=1
> heroku open
```

and I find the offending entry :

```
..
2013-02-17T20:28:54+00:00 app[web.1]: Server running at http://127.0.0.1:8000/
2013-02-17T20:28:54+00:00 heroku[web.1]: Error R11 (Bad bind) -> Process bound to port 8000, should be 10472 (see environment variable PORT)
..
```

So it seems that my simple web server with the hardcoded port is not what heroku likes. The heroku environment wants to have control of the ports... Makes sense given that open heroku sends to port 80 so someone will need to redirect to a pre-known by heroku port. I grab the code from the suggested hello world ap and add it to my web.js

```
> grep -in PORT web.js
4 :var port = process.env.PORT || 8081; 
47:}).listen(port);
49:console.log('Server running at http://127.0.0.1:'+port+'/');
> 
```

I git update, git push to heroku and everything works perfectly this time !
Last step is to push my git a githib repo so as I can point to the various files from this blog post.

```
# fixup the enclosing dir - so as it matches the repo name (to make hub happier)
> mv ../heroku-helloword ../helloworld-js-heroku
> hub create -d 'hello world app in node.js for heroku'
> git push -u origin master
Counting objects: 11, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (8/8), done.
Writing objects: 100% (11/11), 1.41 KiB, done.
Total 11 (delta 2), reused 0 (delta 0)
To git@github.com:ogt/helloworld-js-heroku.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
> 
```

Done!!

_Posted at 2:47 PM_