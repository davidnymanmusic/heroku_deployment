---
# You don’t need to declare anything in the frontmatter
---

# DEPLOYING YOUR API TO HEROKU
## g72 Q3

### Check your **db.js** to make sure it looks like this

<pre>
const devConfig = require('./knexfile')[process.env.NODE_ENV || 'development'];
const knex = require('knex')(devConfig);
module.exports = knex;
</pre>

### Check your **knexfile.js** to make sure it looks like this

<pre>module.exports = {
  development: {
    client: 'pg',
    connection: 'postgres://localhost:5432/<span>YOUR_DATABASE_NAME_HERE</span>
  },
    production: {
      client: 'pg',
      connection: process.env.DATABASE_URL
    }
};</pre>

### Create a  **.env** and check to make sure it looks like this
<pre>
DATABASE_URL=postgres://localhost:5432/<span>YOUR_DATABASE_NAME_HERE</span>
APP_MODE=development
PORT=<span>YOUR_LOCAL_PORT_HERE</span>
</pre>

Make sure you've dded and committed everything

```heroku create <YOUR_APP_NAME_HERE>```

```echo 'web: npm start' >> Procfile```

```add . && commit -m 'add Profile'```

```git push heroku master```

```heroku addons:create heroku-postgresql:hobby-dev```


Go to https://dashboard.heroku.com/apps

Find your app, then go to <span>More</span>, <span>Run Console</span>

Run ```bash```, then type ls to see all your files

```node_modules/.bin/knex migrate:latest```


```node_modules/.bin/knex seed:run```

(or you can run ```heroku run bash``` in your own console and migrate/seed files)
