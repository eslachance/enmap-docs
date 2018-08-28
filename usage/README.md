# Usage Documentation

Inside your script, initialize a new Enmap:

```javascript
const Enmap = require("enmap");

// Initialize an instance of Enmap
const myCollection = new Enmap();

// Adding data is simply a `set` command: 
myCollection.set("myKey", "a value");

// Getting a value is done by key 
let result = myCollection.get("myKey");
```



