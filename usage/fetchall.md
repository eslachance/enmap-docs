---
description: >-
  By default, Enmap will always fetch the entire data from your database and
  load it in memory. For larger projects, this might not be ideal. This page
  describes how to use the fetchAll option
---

# Using the fetchAll option

As described in [the home page](../#advantage-disadvantage), one disadvantage of Enmap is that it loads all your data in memory, so you're sacrificing RAM in order to gain speed. In larger projects, this might become a concern fairly quickly - or when using larger data sets that take more memory.

For this purpose, I surrepticiously added a new option somewhere around Enmap 2.0 called "fetchAll", which defaults to "true" if you don't specify it - which is the old behaviour, and current default at the same time. But, if you set `fetchAll` to `false` in the Enmap options, data is not fetched on load. 

## What does it mean if the data isn't loaded? 

If fetchAll is set to false, no data \(by default\) will be loaded from the database - the Enmap will be completely empty. This means that doing a `.size` check returns 0, looping and filtering doesn't return anything, and get\(\) requests all return null. 

Ok but... how's that useful? It's useful because if you don't need the data, it's not loaded. To load data, there are 2 different methods available. 

## Fetching Data

* `enmap.fetchEverything()` will, of course, fetch all the data from the database - this is the method that's called on init\(\) if fetchAll is true. This means you can stagger your loading time, or that you can decide, later, under certain conditions, you do want to load everything.
* `enmap.fetch(key)` can fetch a single key from the database, saves it to enmap, and returns a promise with the fetched value. 
* `enmap.fetch([array, of, keys])` will fetch each key in the requested array, and return an array of `[key, value]` pairs for each fetched value. 

## That's it!

Yup. Those are the only things you really need to know for the current version of Enmap's fetchAll feature.

### Upcoming Features: 

I'm working on the following features in future versions of enmap, related to fetch methods: 

* Add the ability to check if the DB has a key without fetching
* Add a method to uncache a key from enmap
* Add a method to count keys in the DB \(like enmap.keyCount\(\) maybe?\)
* Figure out how to "fetch on query" without breaking the nonblocking nature of enmap.

