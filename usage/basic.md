# Basic Data Use

Now that we have a functional Enmap structure (which we'll always refer to as `myEnmap`), we're ready to start writing data to it, and getting data from it.&#x20;

> The code samples on this page assume that you have correctly initialized `myEnmap`, and [awaited its initialization](broken-reference) if it's persistent.

## Writing Data

In terms of Enmap, "writing", "adding" and "editing" data is essentially the same thing. When using the basic `set()` method, if the key does not exist it's created, and if it does, it's modified.&#x20;

Enmap supports most _native_ JavaScript data types, with a few small exceptions.&#x20;

* Complex objects like `Set()`, `Map()`, etc, are not supported.
* Class instances and Functions are not supported.

As a general rule, except for null and undefined, anything that can be handled by `JSON.stringify()` will work as expected in Enmap. This includes:&#x20;

* String
* Number
* Integer
* Boolean
* _Object_
* _Array_

> Objects and Arrays are a little more complex to deal with, so they have their own page. See [Working with Objects](objects.md) for more information.&#x20;

The usage for the `set()` method is simple:&#x20;

```
<Enmap>.set(key, value);
```

* `key` must be a string or integer. A key should be unique, otherwise it will be overwritten by new values using the same key.&#x20;
* `value` must be a supported native data type as mentioned above.

Here are a few examples of writing simple data values:&#x20;

```javascript
myEnmap.set('boolean', true);
myEnmap.set('integer', 42);
myEnmap.set('someFloat', 73.2345871);
myEnmap.set("Test2", "test2");
```

## Retrieving Data

Getting data back from an Enmap is just as simple as writing to it. All you need is the `key` of what you want to retrieve, and you get its value back!

```javascript
const floatValue = myEnmap.get('someFloat');
const test = myEnmap.get('Test2');

// you can even use booleans in conditions: 
if(myEnmap.get('boolean')) {
  // boolean is true!
}
```

That's pretty much it for only retrieiving a single data value. There are more complex operations that are available, take a look at [Array Methods](arrays.md) for the more advanced things you can do on Enmap's data!
