# Waiting For Initilalization

When using persistent enmaps, it's very important to understand that _it takes time to load the data from the database_. Attempting to use the enmap before it's fully loaded can lead to errors, so we need to make sure it's ready before using it.

## Using _defer_

To make sure that all your data is loaded before you start working, Enmap provides a handy property called `defer` , which is a promise that is resolved once the provider is ready and all the data has been loaded into memory. There are a few ways to use `defer` , since it's a promise. 

```javascript
const Enmap = require('enmap');
const myEnmap = new Enmap({ name: 'test' });

// Using the standard .then() promise method: 

myEnmap.defer.then( () => {
  console.log(myEnmap.size + " keys loaded");
  myEnmap.set("blah", "foo"); // works
  myEnmap.get("thing"); // also works
});

// Using async/await as an immediate function: 
(async function() {
  await myEnmap.defer;
  console.log(myEnmap.size + " keys loaded");
  // Ready to use!
}());

// In an EventEmitter context:
myEmitter.on("eventName", async (arg) => {
  await myEnmap.defer;
  console.log(myEnmap.size + " keys loaded");
});
```

> For more information on async/await and promises, see [My JavaScript Guide](https://evie.gitbook.io/js/promises).

## Checking for Ready

Enmap also provides a `isReady`  option that tells you if the database is loaded. You can use that however you want, though the preferred method is using `defer`.

```javascript
if(myEnmap.isReady) { 
  // database is ready
} else {
  // database isn't loaded yet
}
```



