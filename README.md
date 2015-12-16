# Static site on heroku using node.js

You really shouldn't use heroku for this, but if you need to stub something out.

## Setup

```bash
heroku create your-app-name
git commit -am 'initial commit'
heroku ps:scale web=1
```
