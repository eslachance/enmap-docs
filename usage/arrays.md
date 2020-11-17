# Array Methods

While Enmap is a Map enhanced with Array methods, Enmap also offers some enhanced array methods for the data stored inside of it. Talk about ArrayCeption! 

So what do I mean by methods for your stored data? I mean that you can store arrays inside Enmap, and directly push, pull, add and remove from those arrays. There are methods to work both on direct arrays, as well as arrays stored inside of an object. 

Let's take a look at two example entries in enmap that we can use. The first is a direct array, the second is an array inside an object. 

```javascript
myEnmap.set("simpleArray", [1,2,3,4,5]);

myEnmap.set("arrInObj", {
  name: "Bob",
  aliases: ["Bobby", "Robert"]
});
```

## Adding to the array

There are two methods to _push_ to an array, one for simple arrays and one for arrays inside objects. Pushing in an enmap array is the same as a regular array push: it adds the element to the end of the array.

```javascript
myEnmap.push("simpleArray", 6);
// now [1,2,3,4,5,6]

myEnmap.push("arrInObj", "Robby", "aliases");
// now ["Bobby", "Robert", "Robby"]
```

> The third parameter in push is the "path" to the array in an object. It works the same as the properties path used in [Working With Objects](objects.md).

## Removing from the array

Similarly, you can remove from an array. Note, however, that this will _only_ work if you're removing a string or number. Removing an object from an array is not supported. 

```javascript
myEnmap.remove("simpleArray", 2);
// now [1,3,4,5,6]

myEnmap.remove("arrInObject", "Bobby", "aliases");
// now ["Robert", "Robby"]
```

