
pa11y-webservice
================

pa11y-webservice provides scheduled accessibility reports for multiple URLs. It runs [pa11y][pa11y] on a list of URLs, which you can update and query the results of via a JSON web-service.

**Current Version:** *1.8.1*  
**Build Status:** [![Build Status][travis-img]][travis]  
**Node Version Support:** *0.12*


Setup
-----

pa11y-webservice requires [Node.js][node] 0.12+ and [PhantomJS][phantom]. See the [pa11y documentation][pa11y-docs] for more information on these dependencies. pa11y-webservice also requires [MongoDB][mongo] to be installed and running.

You'll then need to clone this repo locally and install dependencies with `npm install`. Now we need to add some confguration before we can run the application. We can do this in two ways:

### Option 1: Using Environment Variables

Each configuration can be set with an environment variable rather than a config file. For example to run the application on port `8080` you can use the following:

```sh
PORT=8080 node index.js
```

The [available configurations are documented here](#configurations).

### Option 2: Using Config Files

You'll need to copy and modify different config files depending on your environment (set with `NODE_ENV`):

```sh
cp config/development.sample.json config/development.json
cp config/production.sample.json config/production.json
cp config/test.sample.json config/test.json
```

Each of these files defines configurations for a different environment. If you're just running the application locally, then you should be OK with just development and test configurations. The [available configurations are documented here](#configurations).

Now that you've got your application configured, you can run in each mode by changing the `NODE_ENV` environment variable:

```sh
NODE_ENV=development node index.js
```

See [development instructions](#development) for more information about running locally (and restarting automatically when files change).


Documentation
-------------

The web-service which pa11y-webservice exposes is documented in the wiki:

- [Web-Service endpoints][wiki-web-service]
- [Resource types][wiki-resources]


Client Libraries
----------------

- Node.js client library: [pa11y-webservice-client-node][pa11y-webservice-client-node]


Configurations
--------------

The boot configurations for pa11y-webservice are as follows. Look at the sample JSON files in the repo for example usage.

### database
*(string)* The mongodb [connection string][mongo-connection-string] for your database. Set via a config file or the `DATABASE` environment variable.

### host
*(string)* The host to run the application on. This is normally best left as `"0.0.0.0"` – which means the application will run on any incoming connections. Set via a config file or the `HOST` environment variable.

### port
*(number)* The port to run the application on. Set via a config file or the `PORT` environment variable.

### cron
*(string)* A crontab which describes when to generate reports for each task in the application. Set via a config file or the `CRON` environment variable.


Development
-----------

To develop pa11y-webservice, you'll need to clone the repo and get set up as outlined in the [setup guide](#setup).

You'll need to start the application in test mode with:

```sh
NODE_ENV=test node index.js
```

Now you'll be able to run the following commands:

```sh
make       # Run the lint and test tasks together
make lint  # Run linters with the correct config
make test  # Run integration tests
```

Code with lint errors or failing tests will not be accepted, please use the build tools outlined above.


Fixtures
--------

For demoing pa11y-webservice, you can insert some example tasks and results by running one of the following commands (depending on your environment):

```sh
NODE_ENV=development make fixtures
NODE_ENV=test make fixtures
```


License
-------

[Copyright 2013 Springer Nature](LICENSE.txt).  
pa11y-webservice is licensed under the [GNU General Public License 3.0][gpl].



[brew]: http://mxcl.github.com/homebrew/
[gpl]: http://www.gnu.org/licenses/gpl-3.0.html
[mongo]: http://www.mongodb.org/
[mongo-connection-string]: http://docs.mongodb.org/manual/reference/connection-string/
[node]: http://nodejs.org/
[pa11y]: https://github.com/springernature/pa11y
[pa11y-docs]: https://github.com/springernature/pa11y#installing
[pa11y-webservice-client-node]: https://github.com/springernature/pa11y-webservice-client-node
[phantom]: http://phantomjs.org/
[travis]: https://travis-ci.org/springernature/pa11y-webservice
[travis-img]: https://travis-ci.org/springernature/pa11y-webservice.png?branch=master
[wiki-web-service]: https://github.com/springernature/pa11y-webservice/wiki/Web-Service-Endpoints
[wiki-resources]: https://github.com/springernature/pa11y-webservice/wiki/Resource-Types
