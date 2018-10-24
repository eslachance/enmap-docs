# Using the fetchAll option

As described in [the home page](../#advantage-disadvantage), one disadvantage of Enmap is that it loads all your data in memory, so you're sacrificing RAM in order to gain speed. In larger projects, this might become a concern fairly quickly - or when using larger data sets that take more memory.

For this purpose, there are features in Enmap that enable less caching, by sacrificing some speed and ease of use. That is to say, with data not being fully loaded, there are some things that can't be done easily - see below for details.

The options are as follow:

* `fetchAll`: Defaults to `true`, which means fetching all keys on load. Setting it to `false` means that no keys are fetched, so it loads faster and uses less memory.

  `autoFetch`: Defaults to `true`. When enabled, will automatically fetch any key that's requested using get, getProp, etc. This is a "syncroneous" operation, which means it doesn't need any of this promise or callback use.

```javascript
const Enmap = require("enmap");

const points = new Enmap({
  persistent: true,
  name: "points",
  fetchAll: false,
  autoFetch: true
});
```

## What does it mean if the data isn't loaded?

If fetchAll is set to false, no data \(by default\) will be loaded from the database - the Enmap will be completely empty. This means that doing a `.size` check returns 0, looping and filtering doesn't return anything, and get\(\) requests all return null.

Ok but... how's that useful? It's useful because if you don't need the data, it's not loaded. To load data, there are 2 different methods available.

## Fetching Data

* `enmap.fetchEverything()` will, of course, fetch all the data from the database - this is the method that's called on init\(\) if fetchAll is true. This means you can stagger your loading time, or that you can decide, later, under certain conditions, you do want to load everything.
* `enmap.fetch(key)` can fetch a single key from the database, saves it to enmap, and returns a promise with the fetched value. 
* `enmap.fetch([array, of, keys])` will fetch each key in the requested array, and return an array of `[key, value]` pairs for each fetched value. 
* `enmap.count` will give you the number of keys in the database itself, including uncached ones \(.size is only cached values\).
* `enmap.indexes` will give you a list of keys in the database, including uncached ones.

## That's it!

Yup. Those are the only things you really need to know for the current version of Enmap's fetchAll feature.

### Upcoming Features:

I'm working on the following features in future versions of enmap, related to fetch methods:

* Add the ability to check if the DB has a key without fetching \(a sort of "uncached has\(\)"\)
* Add an auto-uncache feature so that "stale" keys are cleaned. This would combine well with autoFetch in that it would ultimately keep memory usage low.

