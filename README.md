# stringtree-migrate-driver-sqljs

A sql.js driver for [stringtree-migrate](https://github.com/stringtree/stringtree-migrate) - the simple, flexible, database-independent, way to manage automated schema updates.

## Installation

    $ npm install stringtree-migrate-driver-sql.js

## Usage Example:
```js
 var sqljs = require('sql.js');
 var db = new sqljs.Database();

 var scripts = [
   { level: 1, up: "create table ugh ( aa int )" },
   { level: 23, up: [
       "insert into ugh (aa) values (33)",
       "insert into ugh (aa) values (44)"
     ]
   }
 ];

 var driver = require('stringtree-migrate-driver-sqljs')({ database: db });
 var migrate = require('stringtree-migrate')(driver, scripts);
 ...
 // ensure database is at level 23 or greater
 migrate.ensure(23, function(err, level) {
   .. code that needs the db ..;
 });

 ..or

 // ensure database has had all available updates applied
 migrate.ensure(function(err, level) {
   .. code that needs the db ..;
 });
```

For more details, see https://github.com/stringtree/stringtree-migrate

### Configuration

The _config_ object is optional. If not supplied the driver will create its own database. However, if you wish the migrator to use the same sql.js database as your code, you may pass it in as a _database_ parameter.

## Related resources

* https://github.com/stringtree/stringtree-migrate
* https://github.com/stringtree/stringtree-migrate-driver-testsuite
