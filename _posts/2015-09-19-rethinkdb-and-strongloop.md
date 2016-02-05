---
layout: post
published: true
title: Building StrongLoop app powered by RethinkDB
date: "2015-09-19 00:00:00"
categories: 
  - tutorials
---

This is my version from [Getting Started with the RethinkDB Connector for the LoopBack Node.js Framework](https://strongloop.com/strongblog/rethinkdb-connector-loopback-node-js-framework/) . Assuming you've [installed StrongLoop](https://strongloop.com/get-started/), you can now create app using following commands 

``` 
$ slc loopback

     _-----_
    |       |    .--------------------------.
    |--(o)--|    |  Let's create a LoopBack |
   `---------´   |       application!       |
    ( _´U`_ )    '--------------------------'
    /___A___\
     |  ~  |
   __'.___.'__
 ´   `  |° ´ Y `

? What's the name of your application? demo-sl-rdb
? Enter name of the directory to contain the project: demo-sl-rdb
   create demo-sl-rdb/
     info change the working directory to demo-sl-rdb

Generating .yo-rc.json

I'm all done. Running npm install for you to install the required dependencies. If this fails, try running the command yourself.

   create .editorconfig
   create .jshintignore
   create .jshintrc
   create README.md
   create server\boot\authentication.js
   create server\boot\explorer.js
   create server\boot\rest-api.js
   create server\boot\root.js
   create server\middleware.json
   create server\server.js
   create .gitignore
   create client\README.md
npm WARN deprecated jsonstream@1.0.3: use JSONStream instead
npm WARN prefer global ycssmin@1.0.1 should be installed with -g
npm WARN prefer global ycssmin@1.0.1 should be installed with -g
demo-sl-rdb@1.0.0 F:\DEV\strongloop\demo\demo-sl-rdb
├─┬ compression@1.5.2
│ ├─┬ accepts@1.2.13
│ │ ├── mime-types@2.1.6
│ │ └── negotiator@0.5.3
│ ├── bytes@2.1.0
│ ├─┬ compressible@2.0.5
│ │ └── mime-db@1.18.0
│ ├── debug@2.2.0
│ ├── on-headers@1.0.0
│ └── vary@1.0.1
├── cors@2.7.1
├─┬ errorhandler@1.4.2
│ └── escape-html@1.0.2
├─┬ jshint@2.8.0
│ ├─┬ cli@0.6.6
│ │ └─┬ glob@3.2.11
│ │   ├── inherits@2.0.1
│ │   └─┬ minimatch@0.3.0
│ │     ├── lru-cache@2.7.0
│ │     └── sigmund@1.0.1
│ ├─┬ console-browserify@1.1.0
│ │ └── date-now@0.1.4
│ ├── exit@0.1.2
│ ├─┬ htmlparser2@3.8.3
│ │ ├── domelementtype@1.3.0
│ │ ├── domhandler@2.3.0
│ │ ├─┬ domutils@1.5.1
│ │ │ └─┬ dom-serializer@0.1.0
│ │ │   ├── domelementtype@1.1.3
│ │ │   └── entities@1.1.1
│ │ ├── entities@1.0.0
│ │ └─┬ readable-stream@1.1.13
│ │   ├── core-util-is@1.0.1
│ │   ├── isarray@0.0.1
│ │   └── string_decoder@0.10.31
│ ├── lodash@3.7.0
│ ├─┬ minimatch@2.0.10
│ │ └─┬ brace-expansion@1.1.0
│ │   ├── balanced-match@0.2.0
│ │   └── concat-map@0.0.1
│ ├── shelljs@0.3.0
│ └── strip-json-comments@1.0.4
├─┬ loopback@2.22.1
│ ├── async@0.9.2
│ ├── bcryptjs@2.2.2
│ ├─┬ body-parser@1.14.0
│ │ ├── content-type@1.0.1
│ │ ├─┬ http-errors@1.3.1
│ │ │ └── statuses@1.2.1
│ │ ├── iconv-lite@0.4.11
│ │ ├─┬ on-finished@2.3.0
│ │ │ └── ee-first@1.1.1
│ │ ├── qs@5.1.0
│ │ ├─┬ raw-body@2.1.3
│ │ │ └── unpipe@1.0.0
│ │ └─┬ type-is@1.6.8
│ │   └── media-typer@0.3.0
│ ├── canonical-json@0.0.4
│ ├─┬ continuation-local-storage@3.1.4
│ │ ├─┬ async-listener@0.5.6
│ │ │ └── shimmer@1.0.0
│ │ └── emitter-listener@1.0.1
│ ├── depd@1.1.0
│ ├── ejs@2.3.4
│ ├─┬ express@4.13.3
│ │ ├── array-flatten@1.1.1
│ │ ├── content-disposition@0.5.0
│ │ ├── cookie@0.1.3
│ │ ├── cookie-signature@1.0.6
│ │ ├── depd@1.0.1
│ │ ├── finalhandler@0.4.0
│ │ ├── merge-descriptors@1.0.0
│ │ ├── methods@1.1.1
│ │ ├── path-to-regexp@0.1.7
│ │ ├─┬ proxy-addr@1.0.8
│ │ │ ├── forwarded@0.1.0
│ │ │ └── ipaddr.js@1.0.1
│ │ ├── qs@4.0.0
│ │ ├── range-parser@1.0.2
│ │ ├─┬ send@0.13.0
│ │ │ ├── depd@1.0.1
│ │ │ ├── destroy@1.0.3
│ │ │ └── mime@1.3.4
│ │ ├── serve-static@1.10.0
│ │ └── utils-merge@1.0.0
│ ├── inflection@1.7.1
│ ├─┬ loopback-connector-remote@1.0.3
│ │ └── sl-blip@1.0.0
│ ├── loopback-phase@1.2.0
│ ├─┬ nodemailer@1.4.0
│ │ ├─┬ buildmail@1.2.4
│ │ │ ├── addressparser@0.3.2
│ │ │ ├── libbase64@0.1.0
│ │ │ └── libqp@1.0.0
│ │ ├─┬ hyperquest@1.2.0
│ │ │ ├─┬ duplexer2@0.0.2
│ │ │ │ └── readable-stream@1.1.13
│ │ │ └─┬ through2@0.6.5
│ │ │   ├── readable-stream@1.0.33
│ │ │   └── xtend@4.0.0
│ │ ├── libmime@1.0.0
│ │ ├─┬ nodemailer-direct-transport@1.0.2
│ │ │ └── smtp-connection@1.3.1
│ │ └─┬ nodemailer-smtp-transport@1.0.3
│ │   ├── clone@1.0.2
│ │   └── nodemailer-wellknown@0.1.7
│ ├── nodemailer-stub-transport@0.1.5
│ ├── sl-blip@1.0.0
│ ├── stable@0.1.5
│ ├─┬ strong-remoting@2.21.0
│ │ ├── eventemitter2@0.4.14
│ │ ├─┬ jayson@1.2.1
│ │ │ ├─┬ commander@1.3.2
│ │ │ │ └── keypress@0.1.0
│ │ │ ├── eyes@0.1.8
│ │ │ └─┬ jsonstream@1.0.3
│ │ │   └── jsonparse@1.0.0
│ │ ├── js2xmlparser@0.1.9
│ │ ├─┬ mux-demux@3.7.9
│ │ │ ├── duplex@1.0.0
│ │ │ ├── json-buffer@2.0.11
│ │ │ ├─┬ msgpack-stream@0.0.12
│ │ │ │ ├─┬ bops@0.0.6
│ │ │ │ │ ├── base64-js@0.0.2
│ │ │ │ │ └── to-utf8@0.0.1
│ │ │ │ ├── msgpack-js@0.3.0
│ │ │ │ └── through@2.3.4
│ │ │ ├─┬ stream-combiner@0.0.2
│ │ │ │ └── duplexer@0.0.4
│ │ │ ├── stream-serializer@1.1.2
│ │ │ ├── through@2.3.8
│ │ │ └── xtend@1.0.3
│ │ ├── qs@2.4.2
│ │ ├─┬ request@2.62.0
│ │ │ ├── aws-sign2@0.5.0
│ │ │ ├─┬ bl@1.0.0
│ │ │ │ └─┬ readable-stream@2.0.2
│ │ │ │   ├── process-nextick-args@1.0.3
│ │ │ │   └── util-deprecate@1.0.1
│ │ │ ├── caseless@0.11.0
│ │ │ ├─┬ combined-stream@1.0.5
│ │ │ │ └── delayed-stream@1.0.0
│ │ │ ├── extend@3.0.0
│ │ │ ├── forever-agent@0.6.1
│ │ │ ├─┬ form-data@1.0.0-rc3
│ │ │ │ └── async@1.4.2
│ │ │ ├─┬ har-validator@1.8.0
│ │ │ │ ├── bluebird@2.10.0
│ │ │ │ ├─┬ chalk@1.1.1
│ │ │ │ │ ├── ansi-styles@2.1.0
│ │ │ │ │ ├── escape-string-regexp@1.0.3
│ │ │ │ │ ├─┬ has-ansi@2.0.0
│ │ │ │ │ │ └── ansi-regex@2.0.0
│ │ │ │ │ ├── strip-ansi@3.0.0
│ │ │ │ │ └── supports-color@2.0.0
│ │ │ │ ├─┬ commander@2.8.1
│ │ │ │ │ └── graceful-readlink@1.0.1
│ │ │ │ └─┬ is-my-json-valid@2.12.2
│ │ │ │   ├── generate-function@2.0.0
│ │ │ │   ├─┬ generate-object-property@1.2.0
│ │ │ │   │ └── is-property@1.0.2
│ │ │ │   ├── jsonpointer@2.0.0
│ │ │ │   └── xtend@4.0.0
│ │ │ ├─┬ hawk@3.1.0
│ │ │ │ ├── boom@2.8.0
│ │ │ │ ├── cryptiles@2.0.5
│ │ │ │ ├── hoek@2.16.2
│ │ │ │ └── sntp@1.0.9
│ │ │ ├─┬ http-signature@0.11.0
│ │ │ │ ├── asn1@0.1.11
│ │ │ │ ├── assert-plus@0.1.5
│ │ │ │ └── ctype@0.5.3
│ │ │ ├── isstream@0.1.2
│ │ │ ├── json-stringify-safe@5.0.1
│ │ │ ├── oauth-sign@0.8.0
│ │ │ ├── stringstream@0.0.4
│ │ │ ├── tough-cookie@2.0.0
│ │ │ └── tunnel-agent@0.4.1
│ │ ├─┬ sse@0.0.6
│ │ │ └── options@0.0.6
│ │ └─┬ xml2js@0.4.12
│ │   ├── sax@1.1.3
│ │   └── xmlbuilder@3.1.0
│ ├── uid2@0.0.3
│ └── underscore.string@3.2.2
├─┬ loopback-boot@2.12.2
│ ├── commondir@0.0.1
│ ├── lodash@3.6.0
│ ├── semver@4.3.6
│ └── toposort@0.2.12
├─┬ loopback-datasource-juggler@2.40.1
│ ├── async@1.0.0
│ ├─┬ loopback-connector@2.3.0
│ │ └── async@1.4.2
│ ├── node-uuid@1.4.3
│ ├── qs@3.1.0
│ └── traverse@0.6.6
├─┬ loopback-explorer@1.8.0
│ ├─┬ debug@1.0.4
│ │ └── ms@0.6.2
│ ├─┬ express@3.21.2
│ │ ├── basic-auth@1.0.3
│ │ ├── commander@2.6.0
│ │ ├─┬ connect@2.30.2
│ │ │ ├── basic-auth-connect@1.0.0
│ │ │ ├── body-parser@1.13.3
│ │ │ ├── connect-timeout@1.6.2
│ │ │ ├── cookie-parser@1.3.5
│ │ │ ├─┬ csurf@1.8.3
│ │ │ │ └─┬ csrf@3.0.0
│ │ │ │   ├── base64-url@1.2.1
│ │ │ │   ├── rndm@1.1.0
│ │ │ │   └── scmp@1.0.0
│ │ │ ├── depd@1.0.1
│ │ │ ├─┬ express-session@1.11.3
│ │ │ │ ├── crc@3.3.0
│ │ │ │ ├── depd@1.0.1
│ │ │ │ └── uid-safe@2.0.0
│ │ │ ├── method-override@2.3.5
│ │ │ ├─┬ morgan@1.6.1
│ │ │ │ └── depd@1.0.1
│ │ │ ├─┬ multiparty@3.3.2
│ │ │ │ ├── readable-stream@1.1.13
│ │ │ │ └─┬ stream-counter@0.2.0
│ │ │ │   └── readable-stream@1.1.13
│ │ │ ├── pause@0.1.0
│ │ │ ├── qs@4.0.0
│ │ │ ├─┬ response-time@2.3.1
│ │ │ │ └── depd@1.0.1
│ │ │ ├─┬ serve-index@1.7.2
│ │ │ │ └── batch@0.5.2
│ │ │ └── vhost@3.0.1
│ │ ├─┬ debug@2.2.0
│ │ │ └── ms@0.7.1
│ │ ├── depd@1.0.1
│ │ └─┬ mkdirp@0.5.1
│ │   └── minimist@0.0.8
│ ├── lodash@2.4.2
│ └─┬ swagger-ui@2.0.24
│   ├── coffee-script@1.6.3
│   ├─┬ handlebars@1.0.12
│   │ ├─┬ optimist@0.3.7
│   │ │ └── wordwrap@0.0.3
│   │ └─┬ uglify-js@2.3.6
│   │   ├── async@0.2.10
│   │   └─┬ source-map@0.1.43
│   │     └── amdefine@1.0.0
│   ├─┬ less@1.4.2
│   │ ├── mime@1.2.11
│   │ ├── mkdirp@0.3.5
│   │ └── ycssmin@1.0.1
│   └─┬ swagger-client@2.0.36
│     ├── btoa@1.1.1
│     └─┬ shred@0.8.10
│       ├── ax@0.1.8
│       ├── cookiejar@1.3.1
│       └── sprintf@0.1.1
└─┬ serve-favicon@2.3.0
  ├── etag@1.7.0
  ├── fresh@0.3.0
  ├── ms@0.7.1
  └── parseurl@1.3.0

npm WARN EPACKAGEJSON demo-sl-rdb@1.0.0 No license field.

Next steps:

  Change directory to your app
    $ cd demo-sl-rdb

  Create a model in your app
    $ slc loopback:model

  Optional: Enable StrongOps monitoring
    $ slc strongops

  Run the app
    $ slc run .
```

In order to use RethinkDB as your backend, you need to install a RethinkDB connector by updating your `package.json` 

```
"loopback-connector-rethinkdb": "git://github.com/fuwaneko/loopback-connector-rethinkdb",

```

Run `npm install` then register RethinkDB as a new project Data Source as following:

```
slc loopback:datasource
? Enter the data-source name: rethinkdb
? Select the connector for rethinkdb: other
? Enter the connector name without the loopback-connector- prefix: rethinkdb
```

You can now create a model that can be persisted into RethinkDB

```
$ slc loopback:model
? Enter the model name: tasks
? Select the data-source to attach tasks to: rethinkdb (rethinkdb)
? Select model's base class: PersistedModel
? Expose tasks via the REST API? Yes
? Custom plural form (used to build REST URL): tasks
Let's add some tasks properties now.

Enter an empty property name when done.
? Property name: title
   invoke   loopback:property
? Property type: string
? Required? No

Let's add another tasks property.
Enter an empty property name when done.
? Property name: description
   invoke   loopback:property
? Property type: string
? Required? No

Let's add another tasks property.
Enter an empty property name when done.
? Property name:
```

You can find your model - data source config in `APP/server/model-config.json` and model properties within `APP/common/models`. One trick I found if you would like to specify custom Id property (e.g. "TaskId") that works with RethinkDB, in your `APP/common/models/tasks.json` you could specify Id properties as following:

```
"taskId": {
 "type": "string",
 "id": true 
},
```

Once you've created necessary models, update your `APP/server/config.json` with RethinkDB host URL, port, database name, and table names:

```
...,
  "rethinkdb": {
    "host": "192.168.50.4",
    "port": 28015,
    "authKey": "",
    "db": "demo",
    "tables": {
      "Task": "id"
    }
  },
"legacyExplorer": false
```
You also need to insert RethinkDB URL into `APP/server/datasources.json` to act as connection string

```
  "rethinkdb": {
    "url": "http://192.168.50.4:28015/demo",
    "name": "rethinkdb",
    "connector": "rethinkdb"
  }
```

That's basically what you need to setup your StrongLoop app to work with RethinkDB. But before you run the app, make sure that you setup necessary database and table in your RethinkDB. Browse to your RethinkDB Data Explorer at `http://192.168.50.4:8080` then run following command `r.dbCreate("demo")` to create database and `r.db("demo").tableCreate('tasks', {primaryKey: 'taskId'})` to create table based on your model name.

Now you can run your StrongLoop app using `slc run .` command and browse to `localhost:3000`. Try to post using

```
{
  "title": "demo task 1",
  "description": "demo description"
}
```
you'll get 

```
{
  "taskId": "8ec003f2-8b38-4ec1-9f3f-486116ee44c8",
  "title": "demo task 1",
  "description": "demo description",
  "_rev": {
    "isNewInstance": true
  }
}
```

Happy Exploring!
