---
description: 'The full, boring, unadultered enmap docs.'
---

# Enmap API Documentation

**Kind**: global class  
**Extends**: [Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)

* [Enmap](api.md#enmap-map) ⇐ `Map`
  * [new Enmap\(iterable, \[options\]\)](api.md#new-enmap-iterable-options)
  * _instance_
    * [.count](api.md#enmap-count-integer) ⇒ `integer`
    * [.indexes](api.md#enmap-indexes-array-less-than-string-greater-than) ⇒ `array.<string>`
    * [.autonum](api.md#enmap-autonum-number) ⇒ `number`
    * [.set\(key, val, path\)](api.md#enmap-set-key-val-path-enmap) ⇒ \[`Enmap`\]
    * [.update\(key, valueOrFunction\)](api.md#enmap-update-key-valueorfunction) ⇒ `*`
    * [.get\(key, path\)](api.md#enmap-get-key-path) ⇒ `*`
    * [.observe\(key, path\)](api.md#enmap-observe-key-path) ⇒ `*`
    * [.fetchEverything\(\)](api.md#enmap-fetcheverything-enmap) ⇒ \[`Enmap`\]
    * [.fetch\(keyOrKeys\)](api.md#enmap-fetch-keyorkeys-enmap-enmap-or) ⇒ [`Enmap`](api.md#enmap-map) \| `*`
    * [.evict\(keyOrArrayOfKeys\)](api.md#enmap-evict-keyorarrayofkeys-enmap) ⇒ \[`Enmap`\]
    * [.changed\(cb\)](api.md#enmap-changed-cb)
    * [.close\(\)](api.md#enmap-close-promise-less-than-greater-than) ⇒ `Promise.<*>`
    * [.push\(key, val, path, allowDupes\)](api.md#enmap-push-key-val-path-allowdupes-enmap) ⇒ \[`Enmap`\]
    * [.math\(key, operation, operand, path\)](api.md#enmap-math-key-operation-operand-path-enmap) ⇒ \[`Enmap`\]
    * [.inc\(key, path\)](api.md#enmap-inc-key-path-enmap) ⇒ \[`Enmap`\]
    * [.dec\(key, path\)](api.md#enmap-dec-key-path-enmap) ⇒ \[`Enmap`\]
    * [.ensure\(key, defaultValue, path\)](api.md#enmap-ensure-key-defaultvalue-path) ⇒ `*`
    * [.has\(key, path\)](api.md#enmap-has-key-path-boolean) ⇒ `boolean`
    * [.includes\(key, val, path\)](api.md#enmap-includes-key-val-path-boolean) ⇒ `boolean`
    * [.delete\(key, path\)](api.md#enmap-delete-key-path-enmap) ⇒ \[`Enmap`\]
    * [.clear\(\)](api.md#enmap-clear)
    * [.destroy\(\)](api.md#enmap-destroy-null) ⇒ `null`
    * [.remove\(key, val, path\)](api.md#enmap-remove-key-val-path-enmap) ⇒ \[`Enmap`\]
    * [.export\(\)](api.md#enmap-export-string) ⇒ `string`
    * [.import\(data, overwrite, clear\)](api.md#enmap-import-data-overwrite-clear-enmap) ⇒ \[`Enmap`\]
    * [.array\(\)](api.md#enmap-array-array) ⇒ `Array`
    * [.keyArray\(\)](api.md#enmap-keyarray-array-less-than-string-or-number-greater-than) ⇒ `Array.<(string|number)>`
    * [.random\(\[count\]\)](api.md#enmap-random-count-or-array-less-than-greater-than) ⇒ `*` \| `Array.<*>`
    * [.randomKey\(\[count\]\)](api.md#enmap-randomkey-count-or-array-less-than-greater-than) ⇒ `*` \| `Array.<*>`
    * [.findAll\(prop, value\)](api.md#enmap-findall-prop-value-array) ⇒ `Array`
    * [.find\(propOrFn, \[value\]\)](api.md#enmap-find-proporfn-value) ⇒ `*`
    * [.findKey\(propOrFn, \[value\]\)](api.md#enmap-findkey-proporfn-value-string-or-number) ⇒ `string` \| `number`
    * [.sweep\(fn, \[thisArg\]\)](api.md#enmap-sweep-fn-thisarg-number) ⇒ `number`
    * [.filter\(fn, \[thisArg\]\)](api.md#enmap-filter-fn-thisarg-enmap) ⇒ \[`Enmap`\]
    * [.filterArray\(fn, \[thisArg\]\)](api.md#enmap-filterarray-fn-thisarg-array) ⇒ `Array`
    * [.map\(fn, \[thisArg\]\)](api.md#enmap-map-fn-thisarg-array) ⇒ `Array`
    * [.some\(fn, \[thisArg\]\)](api.md#enmap-some-fn-thisarg-boolean) ⇒ `boolean`
    * [.every\(fn, \[thisArg\]\)](api.md#enmap-every-fn-thisarg-boolean) ⇒ `boolean`
    * [.reduce\(fn, \[initialValue\]\)](api.md#enmap-reduce-fn-initialvalue) ⇒ `*`
    * [.clone\(\)](api.md#enmap-clone-enmap) ⇒ \[`Enmap`\]
    * [.concat\(...enmaps\)](api.md#enmap-concat-enmaps-enmap) ⇒ \[`Enmap`\]
  * _static_
    * [.multi\(names, options\)](api.md#enmap-multi-names-options-array-less-than-map-greater-than) ⇒ `Array.<Map>`

## new Enmap\(iterable, \[options\]\)

Initializes a new Enmap, with options.

| Param | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| iterable | `iterable` \| `string` |  | If iterable data, only valid in non-persistent enmaps. If this parameter is a string, it is assumed to be the enmap's name, which is a shorthand for adding a name in the options and making the enmap persistent. |
| \[options\] | `Object` |  | Additional options for the enmap. See [https://enmap.evie.codes/usage\#enmap-options](https://enmap.evie.codes/usage#enmap-options) for details. |
| \[options.name\] | `string` |  | The name of the enmap. Represents its table name in sqlite. If present, the enmap is persistent. If no name is given, the enmap is memory-only and is not saved in the database. As a shorthand, you may use a string for the name instead of the options \(see example\). |
| \[options.fetchAll\] | `boolean` |  | Defaults to `true`. When enabled, will automatically fetch any key that's requested using get, or other retrieval methods. This is a "syncroneous" operation, which means it doesn't need any of this promise or callback use. |
| \[options.dataDir\] | `string` |  | Defaults to `./data`. Determines where the sqlite files will be stored. Can be relative \(to your project root\) or absolute on the disk. Windows users , remember to escape your backslashes! |
| \[options.cloneLevel\] | `string` |  | Defaults to deep. Determines how objects and arrays are treated when inserting and retrieving from the database. See [https://enmap.evie.codes/usage\#enmap-options](https://enmap.evie.codes/usage#enmap-options) for more details on this option. |
| \[options.ensureProps\] | `boolean` |  | defaults to `true`. If enabled and the value in the enmap is an object, using ensure\(\) will also ensure that every property present in the default object will be added to the value, if it's absent. See ensure API reference for more information. |
| \[options.autoEnsure\] | `*` |  | default is disabled. When provided a value, essentially runs ensure\(key, autoEnsure\) automatically so you don't have to. This is especially useful on get\(\), but will also apply on set\(\), and any array and object methods that interact with the database. |
| \[options.autoFetch\] | `boolean` |  | defaults to `true`. When enabled, attempting to get\(\) a key or do any operation on existing keys \(such as array push, etc\) will automatically fetch the current key value from the database. Keys that are automatically fetched remain in memory and are not cleared. |
| \[options.serializer\] | `function` |  | Optional. If a function is provided, it will execute on the data when it is written to the database. This is generally used to convert the value into a format that can be saved in the database, such as converting a complete class instance to just its ID. This function may return the value to be saved, or a promise that resolves to that value \(in other words, can be an async function\). |
| \[options.deserializer\] | `function` |  | Optional. If a function is provided, it will execute on the data when it is read from the database. This is generally used to convert the value from a stored ID into a more complex object. This function may return a value, or a promise that resolves to that value \(in other words, can be an async function\). |
| \[options.wal\] | `boolean` | `false` | Check out Write-Ahead Logging: [https://www.sqlite.org/wal.html](https://www.sqlite.org/wal.html) |

**Example**

```javascript
const Enmap = require("enmap");
// Non-persistent enmap:
const inMemory = new Enmap();

// Named, Persistent enmap with string option
const myEnmap = new Enmap("testing");

// Enmap that does not fetch everything, but does so on per-query basis:
const myEnmap = new Enmap({name: "testing", fetchAll: false});

// Enmap that automatically assigns a default object when getting or setting anything.
const autoEnmap = new Enmap({name: "settings", autoEnsure: { setting1: false, message: "default message"}})
```

## enmap.count ⇒ `integer`

Retrieves the number of rows in the database for this enmap, even if they aren't fetched.

**Kind**: instance property of [`Enmap`](api.md#enmap-map)  
**Returns**: `integer` - The number of rows in the database.  


## enmap.indexes ⇒ `array.<string>`

Retrieves all the indexes \(keys\) in the database for this enmap, even if they aren't fetched.

**Kind**: instance property of [`Enmap`](api.md#enmap-map)  
**Returns**: `array.<string>` - Array of all indexes \(keys\) in the enmap, cached or not.  


## enmap.autonum ⇒ `number`

Generates an automatic numerical key for inserting a new value. This is a "weak" method, it ensures the value isn't duplicated, but does not guarantee it's sequential \(if a value is deleted, another can take its place\). Useful for logging, actions, items, etc - anything that doesn't already have a unique ID.

**Kind**: instance property of [`Enmap`](api.md#enmap-map)  
**Returns**: `number` - The generated key number.  
**Example**

```javascript
enmap.set(enmap.autonum, "This is a new value");
```

## enmap.set\(key, val, path\) ⇒ [`Enmap`](api.md#enmap-map)

Sets a value in Enmap.

**Kind**: instance method of [`Enmap`](api.md#enmap-map)  
**Returns**: [`Enmap`](api.md#enmap-map) - The enmap.

| Param | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| key | `string` |  | Required. The key of the element to add to The Enmap. |
| val | `*` |  | Required. The value of the element to add to The Enmap. If the Enmap is persistent this value MUST be stringifiable as JSON. |
| path | `string` | `null` | Optional. The path to the property to modify inside the value object or array. Can be a path with dot notation, such as "prop1.subprop2.subprop3" |

**Example**

```javascript
// Direct Value Examples
enmap.set('simplevalue', 'this is a string');
enmap.set('isEnmapGreat', true);
enmap.set('TheAnswer', 42);
enmap.set('IhazObjects', { color: 'black', action: 'paint', desire: true });
enmap.set('ArraysToo', [1, "two", "tree", "foor"])

// Settings Properties
enmap.set('IhazObjects', 'blue', 'color'); //modified previous object
enmap.set('ArraysToo', 'three', 2); // changes "tree" to "three" in array.
```

## enmap.update\(key, valueOrFunction\) ⇒ `*`

Update an existing object value in Enmap by merging new keys. **This only works on objects**, any other value will throw an error. Heavily inspired by setState from React's class components. This is very useful if you have many different values to update and don't want to have more than one .set\(key, value, prop\) lines.

**Kind**: instance method of [`Enmap`](api.md#enmap-map)  
**Returns**: `*` - The updated, merged value.

| Param | Type | Description |
| :--- | :--- | :--- |
| key | `string` | The key of the object to update. |
| valueOrFunction | `*` | Either an object to merge with the existing value, or a function that provides the existing object and expects a new object as a return value. In the case of a straight value, the merge is recursive and will add any missing level. If using a function, it is your responsibility to merge the objects together correctly. |

**Example**

```javascript
// Define an object we're going to update
enmap.set("obj", { a: 1, b: 2, c: 3 });

// Direct merge
enmap.update("obj", { d: 4, e: 5 });
// obj is now { a: 1, b: 2, c: 3, d: 4, e: 5 }

// Functional update
enmap.update("obj", (previous) => ({
  ...obj,
  f: 6,
  g: 7
}));
// this example takes heavy advantage of the spread operators.
// More info: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax
```

## enmap.get\(key, path\) ⇒ `*`

Retrieves a key from the enmap. If fetchAll is false, returns a promise.

**Kind**: instance method of [`Enmap`](api.md#enmap-map)  
**Returns**: `*` - The value for this key.

| Param | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| key | `string` |  | The key to retrieve from the enmap. |
| path | `string` | `null` | Optional. The property to retrieve from the object or array. Can be a path with dot notation, such as "prop1.subprop2.subprop3" |

**Example**

```javascript
const myKeyValue = enmap.get("myKey");
console.log(myKeyValue);

const someSubValue = enmap.get("anObjectKey", "someprop.someOtherSubProp");
```

## enmap.observe\(key, path\) ⇒ `*`

Returns an observable object. Modifying this object or any of its properties/indexes/children will automatically save those changes into enmap. This only works on objects and arrays, not "basic" values like strings or integers.

**Kind**: instance method of [`Enmap`](api.md#enmap-map)  
**Returns**: `*` - The value for this key.

| Param | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| key | `*` |  | The key to retrieve from the enmap. |
| path | `string` | `null` | Optional. The property to retrieve from the object or array. |

## enmap.fetchEverything\(\) ⇒ [`Enmap`](api.md#enmap-map)

Fetches every key from the persistent enmap and loads them into the current enmap value.

**Kind**: instance method of [`Enmap`](api.md#enmap-map)  
**Returns**: [`Enmap`](api.md#enmap-map) - The enmap containing all values.  


## enmap.fetch\(keyOrKeys\) ⇒ [`Enmap`](api.md#enmap-map) \| `*`

Force fetch one or more key values from the enmap. If the database has changed, that new value is used.

**Kind**: instance method of [`Enmap`](api.md#enmap-map)  
**Returns**: [`Enmap`](api.md#enmap-map) \| `*` - The Enmap, including the new fetched values, or the value in case the function argument is a single key.

| Param | Type | Description |
| :--- | :--- | :--- |
| keyOrKeys | `string` \| `number` \| `Array.<(string|number)>` | A single key or array of keys to force fetch from the enmap database. |

## enmap.evict\(keyOrArrayOfKeys\) ⇒ [`Enmap`](api.md#enmap-map)

Removes a key or keys from the cache - useful when disabling autoFetch.

**Kind**: instance method of [`Enmap`](api.md#enmap-map)  
**Returns**: [`Enmap`](api.md#enmap-map) - The enmap minus the evicted keys.

| Param | Type | Description |
| :--- | :--- | :--- |
| keyOrArrayOfKeys | `string` \| `number` \| `Array.<(string|number)>` | A single key or array of keys to remove from the cache. |

## enmap.changed\(cb\)

Function called whenever data changes within Enmap after the initial load. Can be used to detect if another part of your code changed a value in enmap and react on it.

**Kind**: instance method of [`Enmap`](api.md#enmap-map)

| Param | Type | Description |
| :--- | :--- | :--- |
| cb | `function` | A callback function that will be called whenever data changes in the enmap. |

**Example**

```javascript
enmap.changed((keyName, oldValue, newValue) => {
  console.log(`Value of ${keyName} has changed from: \n${oldValue}\nto\n${newValue}`);
});
```

## enmap.close\(\) ⇒ `Promise.<*>`

Shuts down the database. WARNING: USING THIS MAKES THE ENMAP UNUSEABLE. You should only use this method if you are closing your entire application. This is useful if you need to copy the database somewhere else, or if you're somehow losing data on shutdown.

**Kind**: instance method of [`Enmap`](api.md#enmap-map)  
**Returns**: `Promise.<*>` - The promise of the database closing operation.  


## enmap.push\(key, val, path, allowDupes\) ⇒ [`Enmap`](api.md#enmap-map)

Push to an array value in Enmap.

**Kind**: instance method of [`Enmap`](api.md#enmap-map)  
**Returns**: [`Enmap`](api.md#enmap-map) - The enmap.

| Param | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| key | `string` |  | Required. The key of the array element to push to in Enmap. This value MUST be a string or number. |
| val | `*` |  | Required. The value to push to the array. |
| path | `string` | `null` | Optional. The path to the property to modify inside the value object or array. Can be a path with dot notation, such as "prop1.subprop2.subprop3" |
| allowDupes | `boolean` | `false` | Optional. Allow duplicate values in the array \(default: false\). |

**Example**

```javascript
// Assuming
enmap.set("simpleArray", [1, 2, 3, 4]);
enmap.set("arrayInObject", {sub: [1, 2, 3, 4]});

enmap.push("simpleArray", 5); // adds 5 at the end of the array
enmap.push("arrayInObject", "five", "sub"); // adds "five" at the end of the sub array
```

## enmap.math\(key, operation, operand, path\) ⇒ [`Enmap`](api.md#enmap-map)

Executes a mathematical operation on a value and saves it in the enmap.

**Kind**: instance method of [`Enmap`](api.md#enmap-map)  
**Returns**: [`Enmap`](api.md#enmap-map) - The enmap.

| Param | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| key | `string` |  | The enmap key on which to execute the math operation. |
| operation | `string` |  | Which mathematical operation to execute. Supports most math ops: =, -, \*, /, %, ^, and english spelling of those operations. |
| operand | `number` |  | The right operand of the operation. |
| path | `string` | `null` | Optional. The property path to execute the operation on, if the value is an object or array. |

**Example**

```javascript
// Assuming
points.set("number", 42);
points.set("numberInObject", {sub: { anInt: 5 }});

points.math("number", "/", 2); // 21
points.math("number", "add", 5); // 26
points.math("number", "modulo", 3); // 2
points.math("numberInObject", "+", 10, "sub.anInt");
```

## enmap.inc\(key, path\) ⇒ [`Enmap`](api.md#enmap-map)

Increments a key's value or property by 1. Value must be a number, or a path to a number.

**Kind**: instance method of [`Enmap`](api.md#enmap-map)  
**Returns**: [`Enmap`](api.md#enmap-map) - The enmap.

| Param | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| key | `string` |  | The enmap key where the value to increment is stored. |
| path | `string` | `null` | Optional. The property path to increment, if the value is an object or array. |

**Example**

```javascript
// Assuming
points.set("number", 42);
points.set("numberInObject", {sub: { anInt: 5 }});

points.inc("number"); // 43
points.inc("numberInObject", "sub.anInt"); // {sub: { anInt: 6 }}
```

## enmap.dec\(key, path\) ⇒ [`Enmap`](api.md#enmap-map)

Decrements a key's value or property by 1. Value must be a number, or a path to a number.

**Kind**: instance method of [`Enmap`](api.md#enmap-map)  
**Returns**: [`Enmap`](api.md#enmap-map) - The enmap.

| Param | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| key | `string` |  | The enmap key where the value to decrement is stored. |
| path | `string` | `null` | Optional. The property path to decrement, if the value is an object or array. |

**Example**

```javascript
// Assuming
points.set("number", 42);
points.set("numberInObject", {sub: { anInt: 5 }});

points.dec("number"); // 41
points.dec("numberInObject", "sub.anInt"); // {sub: { anInt: 4 }}
```

## enmap.ensure\(key, defaultValue, path\) ⇒ `*`

Returns the key's value, or the default given, ensuring that the data is there. This is a shortcut to "if enmap doesn't have key, set it, then get it" which is a very common pattern.

**Kind**: instance method of [`Enmap`](api.md#enmap-map)  
**Returns**: `*` - The value from the database for the key, or the default value provided for a new key.

| Param | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| key | `string` |  | Required. The key you want to make sure exists. |
| defaultValue | `*` |  | Required. The value you want to save in the database and return as default. |
| path | `string` | `null` | Optional. If presents, ensures both the key exists as an object, and the full path exists. Can be a path with dot notation, such as "prop1.subprop2.subprop3" |

**Example**

```javascript
// Simply ensure the data exists (for using property methods):
enmap.ensure("mykey", {some: "value", here: "as an example"});
enmap.has("mykey"); // always returns true
enmap.get("mykey", "here") // returns "as an example";

// Get the default value back in a variable:
const settings = mySettings.ensure("1234567890", defaultSettings);
console.log(settings) // enmap's value for "1234567890" if it exists, otherwise the defaultSettings value.
```

## enmap.has\(key, path\) ⇒ `boolean`

Returns whether or not the key exists in the Enmap.

**Kind**: instance method of [`Enmap`](api.md#enmap-map)

| Param | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| key | `string` |  | Required. The key of the element to add to The Enmap or array. This value MUST be a string or number. |
| path | `string` | `null` | Optional. The property to verify inside the value object or array. Can be a path with dot notation, such as "prop1.subprop2.subprop3" |

**Example**

```javascript
if(enmap.has("myKey")) {
  // key is there
}

if(!enmap.has("myOtherKey", "oneProp.otherProp.SubProp")) return false;
```

## enmap.includes\(key, val, path\) ⇒ `boolean`

Performs Array.includes\(\) on a certain enmap value. Works similar to [Array.includes\(\)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes).

**Kind**: instance method of [`Enmap`](api.md#enmap-map)  
**Returns**: `boolean` - Whether the array contains the value.

| Param | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| key | `string` |  | Required. The key of the array to check the value of. |
| val | `string` \| `number` |  | Required. The value to check whether it's in the array. |
| path | `*` |  | Required. The property to access the array inside the value object or array. Can be a path with dot notation, such as "prop1.subprop2.subprop3" |

## enmap.delete\(key, path\) ⇒ [`Enmap`](api.md#enmap-map)

Deletes a key in the Enmap.

**Kind**: instance method of [`Enmap`](api.md#enmap-map)  
**Returns**: [`Enmap`](api.md#enmap-map) - The enmap.

| Param | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| key | `string` |  | Required. The key of the element to delete from The Enmap. |
| path | `string` | `null` | Optional. The name of the property to remove from the object. Can be a path with dot notation, such as "prop1.subprop2.subprop3" |

## enmap.clear\(\)

Deletes everything from the enmap. If persistent, clears the database of all its data for this table.

**Kind**: instance method of [`Enmap`](api.md#enmap-map)  


## enmap.destroy\(\) ⇒ `null`

Completely destroys the entire enmap. This deletes the database tables entirely. It will not affect other enmap data in the same database, however. THIS ACTION WILL DESTROY YOUR DATA AND CANNOT BE UNDONE.

**Kind**: instance method of [`Enmap`](api.md#enmap-map)  


## enmap.remove\(key, val, path\) ⇒ [`Enmap`](api.md#enmap-map)

Remove a value in an Array or Object element in Enmap. Note that this only works for values, not keys. Note that only one value is removed, no more. Arrays of objects must use a function to remove, as full object matching is not supported.

**Kind**: instance method of [`Enmap`](api.md#enmap-map)  
**Returns**: [`Enmap`](api.md#enmap-map) - The enmap.

| Param | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| key | `string` |  | Required. The key of the element to remove from in Enmap. This value MUST be a string or number. |
| val | `*` \| `function` |  | Required. The value to remove from the array or object. OR a function to match an object. If using a function, the function provides the object value and must return a boolean that's true for the object you want to remove. |
| path | `string` | `null` | Optional. The name of the array property to remove from. Can be a path with dot notation, such as "prop1.subprop2.subprop3". If not presents, removes directly from the value. |

**Example**

```javascript
// Assuming
enmap.set('array', [1, 2, 3])
enmap.set('objectarray', [{ a: 1, b: 2, c: 3 }, { d: 4, e: 5, f: 6 }])

enmap.remove('array', 1); // value is now [2, 3]
enmap.remove('objectarray', (value) => value.e === 5); // value is now [{ a: 1, b: 2, c: 3 }]
```

## enmap.export\(\) ⇒ `string`

Exports the enmap data to a JSON file. **WARNING**: Does not work on memory enmaps containing complex data!

**Kind**: instance method of [`Enmap`](api.md#enmap-map)  
**Returns**: `string` - The enmap data in a stringified JSON format.  


## enmap.import\(data, overwrite, clear\) ⇒ [`Enmap`](api.md#enmap-map)

Import an existing json export from enmap from a string. This data must have been exported from enmap, and must be from a version that's equivalent or lower than where you're importing it.

**Kind**: instance method of [`Enmap`](api.md#enmap-map)  
**Returns**: [`Enmap`](api.md#enmap-map) - The enmap with the new data.

| Param | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| data | `string` |  | The data to import to Enmap. Must contain all the required fields provided by export\(\) |
| overwrite | `boolean` | `true` | Defaults to `true`. Whether to overwrite existing key/value data with incoming imported data |
| clear | `boolean` | `false` | Defaults to `false`. Whether to clear the enmap of all data before importing \(**WARNING**: Any exiting data will be lost! This cannot be undone.\) |

## enmap.array\(\) ⇒ `Array`

Creates an ordered array of the values of this Enmap. The array will only be reconstructed if an item is added to or removed from the Enmap, or if you change the length of the array itself. If you don't want this caching behaviour, use `Array.from(enmap.values())` instead.

**Kind**: instance method of [`Enmap`](api.md#enmap-map)  


## enmap.keyArray\(\) ⇒ `Array.<(string|number)>`

Creates an ordered array of the keys of this Enmap The array will only be reconstructed if an item is added to or removed from the Enmap, or if you change the length of the array itself. If you don't want this caching behaviour, use `Array.from(enmap.keys())` instead.

**Kind**: instance method of [`Enmap`](api.md#enmap-map)  


## enmap.random\(\[count\]\) ⇒ `*` \| `Array.<*>`

Obtains random value\(s\) from this Enmap. This relies on [array](api.md#Enmap+array).

**Kind**: instance method of [`Enmap`](api.md#enmap-map)  
**Returns**: `*` \| `Array.<*>` - The single value if `count` is undefined, or an array of values of `count` length

| Param | Type | Description |
| :--- | :--- | :--- |
| \[count\] | `number` | Number of values to obtain randomly |

## enmap.randomKey\(\[count\]\) ⇒ `*` \| `Array.<*>`

Obtains random key\(s\) from this Enmap. This relies on [keyArray](api.md#Enmap+keyArray)

**Kind**: instance method of [`Enmap`](api.md#enmap-map)  
**Returns**: `*` \| `Array.<*>` - The single key if `count` is undefined, or an array of keys of `count` length

| Param | Type | Description |
| :--- | :--- | :--- |
| \[count\] | `number` | Number of keys to obtain randomly |

## enmap.findAll\(prop, value\) ⇒ `Array`

Searches for all items where their specified property's value is identical to the given value \(`item[prop] === value`\).

**Kind**: instance method of [`Enmap`](api.md#enmap-map)

| Param | Type | Description |
| :--- | :--- | :--- |
| prop | `string` | The property to test against |
| value | `*` | The expected value |

**Example**

```javascript
enmap.findAll('username', 'Bob');
```

## enmap.find\(propOrFn, \[value\]\) ⇒ `*`

Searches for a single item where its specified property's value is identical to the given value \(`item[prop] === value`\), or the given function returns a truthy value. In the latter case, this is identical to [Array.find\(\)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find).

All Enmap used in Discord.js are mapped using their \`id\` property, and if you want to find by id you should use the \`get\` method. See \[MDN\]\(https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Map/get\) for details.

**Kind**: instance method of [`Enmap`](api.md#enmap-map)

| Param | Type | Description |
| :--- | :--- | :--- |
| propOrFn | `string` \| `function` | The property to test against, or the function to test with |
| \[value\] | `*` | The expected value - only applicable and required if using a property for the first argument |

**Example**

```javascript
enmap.find('username', 'Bob');
```

**Example**

```javascript
enmap.find(val => val.username === 'Bob');
```

## enmap.findKey\(propOrFn, \[value\]\) ⇒ `string` \| `number`

Searches for the key of a single item where its specified property's value is identical to the given value \(`item[prop] === value`\), or the given function returns a truthy value. In the latter case, this is identical to [Array.findIndex\(\)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex).

**Kind**: instance method of [`Enmap`](api.md#enmap-map)

| Param | Type | Description |
| :--- | :--- | :--- |
| propOrFn | `string` \| `function` | The property to test against, or the function to test with |
| \[value\] | `*` | The expected value - only applicable and required if using a property for the first argument |

**Example**

```javascript
enmap.findKey('username', 'Bob');
```

**Example**

```javascript
enmap.findKey(val => val.username === 'Bob');
```

## enmap.sweep\(fn, \[thisArg\]\) ⇒ `number`

Removes entries that satisfy the provided filter function.

**Kind**: instance method of [`Enmap`](api.md#enmap-map)  
**Returns**: `number` - The number of removed entries

| Param | Type | Description |
| :--- | :--- | :--- |
| fn | `function` | Function used to test \(should return a boolean\) |
| \[thisArg\] | `Object` | Value to use as `this` when executing function |

## enmap.filter\(fn, \[thisArg\]\) ⇒ [`Enmap`](api.md#enmap-map)

Identical to [Array.filter\(\)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter), but returns a Enmap instead of an Array.

**Kind**: instance method of [`Enmap`](api.md#enmap-map)

| Param | Type | Description |
| :--- | :--- | :--- |
| fn | `function` | Function used to test \(should return a boolean\) |
| \[thisArg\] | `Object` | Value to use as `this` when executing function |

## enmap.filterArray\(fn, \[thisArg\]\) ⇒ `Array`

Identical to [Array.filter\(\)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter).

**Kind**: instance method of [`Enmap`](api.md#enmap-map)

| Param | Type | Description |
| :--- | :--- | :--- |
| fn | `function` | Function used to test \(should return a boolean\) |
| \[thisArg\] | `Object` | Value to use as `this` when executing function |

## enmap.map\(fn, \[thisArg\]\) ⇒ `Array`

Identical to [Array.map\(\)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map).

**Kind**: instance method of [`Enmap`](api.md#enmap-map)

| Param | Type | Description |
| :--- | :--- | :--- |
| fn | `function` | Function that produces an element of the new array, taking three arguments |
| \[thisArg\] | `*` | Value to use as `this` when executing function |

## enmap.some\(fn, \[thisArg\]\) ⇒ `boolean`

Identical to [Array.some\(\)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some).

**Kind**: instance method of [`Enmap`](api.md#enmap-map)

| Param | Type | Description |
| :--- | :--- | :--- |
| fn | `function` | Function used to test \(should return a boolean\) |
| \[thisArg\] | `Object` | Value to use as `this` when executing function |

## enmap.every\(fn, \[thisArg\]\) ⇒ `boolean`

Identical to [Array.every\(\)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every).

**Kind**: instance method of [`Enmap`](api.md#enmap-map)

| Param | Type | Description |
| :--- | :--- | :--- |
| fn | `function` | Function used to test \(should return a boolean\) |
| \[thisArg\] | `Object` | Value to use as `this` when executing function |

## enmap.reduce\(fn, \[initialValue\]\) ⇒ `*`

Identical to [Array.reduce\(\)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce).

**Kind**: instance method of [`Enmap`](api.md#enmap-map)

| Param | Type | Description |
| :--- | :--- | :--- |
| fn | `function` | Function used to reduce, taking four arguments; `accumulator`, `currentValue`, `currentKey`, and `enmap` |
| \[initialValue\] | `*` | Starting value for the accumulator |

## enmap.clone\(\) ⇒ [`Enmap`](api.md#enmap-map)

Creates an identical shallow copy of this Enmap.

**Kind**: instance method of [`Enmap`](api.md#enmap-map)  
**Example**

```javascript
const newColl = someColl.clone();
```

## enmap.concat\(...enmaps\) ⇒ [`Enmap`](api.md#enmap-map)

Combines this Enmap with others into a new Enmap. None of the source Enmaps are modified.

**Kind**: instance method of [`Enmap`](api.md#enmap-map)

| Param | Type | Description |
| :--- | :--- | :--- |
| ...enmaps | [`Enmap`](api.md#enmap-map) | Enmaps to merge |

**Example**

```javascript
const newColl = someColl.concat(someOtherColl, anotherColl, ohBoyAColl);
```

## Enmap.multi\(names, options\) ⇒ `Array.<Map>`

Initialize multiple Enmaps easily.

**Kind**: static method of [`Enmap`](api.md#enmap-map)  
**Returns**: `Array.<Map>` - An array of initialized Enmaps.

| Param | Type | Description |
| :--- | :--- | :--- |
| names | `Array.<string>` | Array of strings. Each array entry will create a separate enmap with that name. |
| options | `Object` | Options object to pass to each enmap, excluding the name.. |

**Example**

```javascript
// Using local variables.
const Enmap = require('enmap');
const { settings, tags, blacklist } = Enmap.multi(['settings', 'tags', 'blacklist']);

// Attaching to an existing object (for instance some API's client)
const Enmap = require("enmap");
Object.assign(client, Enmap.multi(["settings", "tags", "blacklist"]));
```

