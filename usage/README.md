# Usage Documentation

Mostly, this documentation will be concentrating on the "persistent" version of enmap - the one where data is saved automatically.

If you don't want persistence, the only difference is how you initialize the enmap: 

```javascript
const Enmap = require("enmap");
const myEnmap = new Enmap();

// you can now use your enmap directly
```

### Persistent Enmaps

Using persistent enmaps require the additional install of the `better-sqlite-pool` module. 

If using a persistent enmap, you need to add options: 

```javascript
const Enmap = require("enmap");

// Normal enmap with default options
const myEnmap = new Enmap({name: "points"});

// non-cached, auto-fetch enmap: 
const otherEnmap = new Enmap({
  name: "settings",
  autoFetch: true,
  fetchAll: false
});
```



