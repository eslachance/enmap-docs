# Persistent Enmaps

Persistence requires an additional Provider module.

Official Enmap Providers:

* [Enmap-SQLite](https://www.npmjs.com/package/enmap-sqlite): Recommended, supports sharding locally.
* [Enmap-Rethink](https://www.npmjs.com/package/enmap-rethink): Best for sharding if you can install a rethinkdb server. Supports updating from the database on all shards \(enmap-rethink 2.1.0 and higher\)
* [Enmap-PGSQL](https://www.npmjs.com/package/enmap-pgsql): Postgresql database provider. Supports Sharding.
* [Enmap-Mongo](https://www.npmjs.com/package/enmap-mongo): Mongodb database provider. Supports Sharding.
* [Enmap-Level:](https://www.npmjs.com/package/enmap-level) Sort of not recommended at this point, doesn't support sharding, no longer the most efficient/faster provider.

When using any provider, it's very important to understand that _it takes time to load the data from the database_. Certain providers also take some time to even open the database connection, and that's also something to consider. 

## Using _defer_

To make sure that all your data is loaded before you start working, Enmap provides a handy property called `defer` , which is a promise that is resolved once the provider is ready and all the data has been loaded into memory. There are a few ways to use `defer` , since it's a promise. 

```javascript
// Load Enmap
const Enmap = require('enmap');

// Load EnmapSQLite
const EnmapSQLite = require('enmap-sqlite');

// Initialize the sqlite database with a table named "test"
const provider = new EnmapSQLite({ name: 'test' });

// Initialize the Enmap with the provider instance.
const myColl = new Enmap({ provider: provider });

// Persistent providers load in an **async** fashion
// and provide a handy defer property:

myColl.defer.then(() => {
    // all data is loaded now.
    console.log(myColl.size + "keys loaded");
});

// You can also await it if your function is async: 
(async function() {
    await myColl.defer;
    console.log(myColl.size + "keys loaded");
    // Do stuff here!
}());

// Persistent collections should be **closed** before shutdown: 
await myColl.db.close();
```



