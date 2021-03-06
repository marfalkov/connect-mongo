# connect-mongo

  MongoDB session store for Connect

  [![Build Status](https://secure.travis-ci.org/kcbanner/connect-mongo.png?branch=master)](http://travis-ci.org/kcbanner/connect-mongo)

## Installation

connect-mongo supports only connect `>= 1.0.3`.

via npm:

    $ npm install connect-mongo

## Options

  - `db` Database name
  - `collection` Collection (optional, default: `sessions`) 
  - `host` MongoDB server hostname (optional, default: `127.0.0.1`)
  - `port` MongoDB server port (optional, default: `27017`)
  - `username` Username (optional)
  - `password` Password (optional)
  - `auto_reconnect` This is passed directly to the MongoDB `Server` constructor as the auto_reconnect
                     option (optional, default: false).
  - `url` Connection url of the form: `mongodb://user:pass@host:port/database/collection`.
          If provided, information in the URL takes priority over the other options.
  - `mongooseConnection` in the form: `someMongooseDb.connections[0]` to use an existing mongoose connection. (optional)
  - `clear_interval` Interval in seconds to clear expired sessions (optional, default: `-1`).
          Values <= 0 disable expired session clearing.
  - `stringify` If true, connect-mongo will serialize sessions using `JSON.stringify` before
                setting them, and deserialize them with `JSON.parse` when getting them.
                (optional, default: true). This is useful if you are using types that 
                MongoDB doesn't support.

The second parameter to the `MongoStore` constructor is a callback which will be called once the database connection is established.
This is mainly used for the tests, however you can use this callback if you want to wait until the store has connected before
starting your app.

## Example

With express:

    var express = require('express');
    var MongoStore = require('connect-mongo')(express);

    app.use(express.session({
        secret: settings.cookie_secret,
        store: new MongoStore({
          db: settings.db
        })
      }));

With connect:

    var connect = require('connect');
    var MongoStore = require('connect-mongo')(connect);


## Tests

You need `mocha`.

    make test

The tests use a database called `connect-mongo-test`.

## License 

(The MIT License)

Copyright (c) 2011 Casey Banner &lt;kcbanner@gmail.com&gt;

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
