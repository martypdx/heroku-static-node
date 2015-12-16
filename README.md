# Static site on heroku using node.js

You really shouldn't use heroku for this, but if you need to stub something out...

## Setup

Create a heroku app. If you don't supply an app name, heroku will create one for you.

```bash
heroku create [your-app-name]
```

If directory is a git repo, then heroku will add the app as a remote. If you already created your git remote, then use the following to assign heroku app (app-name is required):

```bash
heroku git:remote -a app-name
```

Don't forget to commit and push your changes to heroku:

```bash
git commit -am 'initial commit'
git push heroku master
```

Then since we're not using a `Procfile`, don't forget to run (once):

```bash
heroku ps:scale web=1
```

You can open your site from the command line via:

```bash
heroku open
```

## Serving static files

Here is the entirety of the node `index.js` file:

```js
var static = require('node-static');
var fileServer = new static.Server('www');

require('http').createServer(function (request, response) {
    request.addListener('end', function () {
        fileServer.serve(request, response);
    }).resume();
}).listen(process.env.PORT || 8080);
```

Notice:
* The directory to serve is passed to the `new static.Server` constructor call
* Use of `process.env.PORT` which is what heroku will set to run your server.

## package.json

Because we're not using a `Procfile`, you need to include:

```json
  "scripts": {
    "start": "node index.js"
  },
```

And include the `node-static` dependency:

```json
  "dependencies": {
    "node-static": "^0.7.7"
  }
```
