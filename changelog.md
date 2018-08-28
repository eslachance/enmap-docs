# Changelog

## Version 4.0

* **Removed all Provider support.** Enmap is now locked to an `sqlite` database. This is because having a single provider is much easier to maintain, and gives me possibilities for features that were not previously available. The entire autoFetch/fetchAll system is possible only through the use of `better-sqlite3`, which is sync but non-blocking. Existing providers will remain valid for enmap 3, and updates could still happen to enmap 3 and providers in the future, especially bug fixing. [See Upgrading](install/upgrade.md) for more details.
* **New option**: `autoFetch`: Automatically fetches uncached keys when getting data from enmap. See [Using the fetchAll option](usage/fetchall.md) for more details.
* **Better error descriptions**: All methods now verify the database is ready before running. This prevents confusion if trying to get or set data before the database is loaded. 
* **New method**: `count` : This method returns the total number of keys for the enmap, even if they aren't cached. [More Details](api.md#enmap-count-integer)
* **New method**: `indexes` : This method returns an array of keys for the enmap, even if they aren't cached. Similar to `enmap.keyArray()` , but useful when fetchAll is false. [More Details](api.md#enmap-indexes-array)
* **New method**: `evict` : This method takes a key name or array of key names, and removes them from the cache. It does not delete the data, only "uncaches" it from Enmap. Useful when fetchAll is false, and you want to reduce memory usage. [More Details](api.md#enmap-evict-keyorarrayofkeys-enmap).
* **New method**: `ensure` : This method can be used to ensure that a key exists in the enmap, and create it if it doesn't. It's a shortcut to the "if !has\(key\) set\(key, value\) get\(key\)" pattern in code. [More Details](api.md#enmap-ensure-key-defaultvalue). 



