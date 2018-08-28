# API Documentation

## Enmap ⇐ `Map`

A enhanced Map structure with additional utility methods. Can be made persistent

**Kind**: global class  
**Extends**: `Map`

* [Enmap](api-documentation.md#Enmap) ⇐ `Map`
  * _instance_
    * [.fetchEverything\(\)](api-documentation.md#Enmap+fetchEverything) ⇒ `Promise.`
    * [.fetch\(keyOrKeys\)](api-documentation.md#Enmap+fetch) ⇒ `Promise.`
    * [.evict\(keyOrArrayOfKeys\)](api-documentation.md#Enmap+evict)
    * [.autonum\(\)](api-documentation.md#Enmap+autonum) ⇒ `number`
    * [.changed\(cb\)](api-documentation.md#Enmap+changed)
    * [.set\(key, val, path\)](api-documentation.md#Enmap+set) ⇒ `Map`
    * [.setProp\(key, path, val\)](api-documentation.md#Enmap+setProp) ⇒ `Map`
    * [.push\(key, val, path, allowDupes\)](api-documentation.md#Enmap+push) ⇒ `Map`
    * [.pushIn\(key, path, val, allowDupes\)](api-documentation.md#Enmap+pushIn) ⇒ `Map`
    * [.math\(key, operation, operand, path\)](api-documentation.md#Enmap+math) ⇒ `Map`
    * [.inc\(key, path\)](api-documentation.md#Enmap+inc) ⇒ `Map`
    * [.dec\(key, path\)](api-documentation.md#Enmap+dec) ⇒ `Map`
    * [.get\(key, path\)](api-documentation.md#Enmap+get) ⇒ `*`
    * [.getProp\(key, path\)](api-documentation.md#Enmap+getProp) ⇒ `*`
    * [.has\(key, path\)](api-documentation.md#Enmap+has) ⇒ `boolean`
    * [.hasProp\(key, path\)](api-documentation.md#Enmap+hasProp) ⇒ `boolean`
    * [.delete\(key, path\)](api-documentation.md#Enmap+delete)
    * [.deleteProp\(key, path\)](api-documentation.md#Enmap+deleteProp)
    * [.deleteAll\(bulk\)](api-documentation.md#Enmap+deleteAll)
    * [.remove\(key, val, path\)](api-documentation.md#Enmap+remove) ⇒ `Map`
    * [.removeFrom\(key, path, val\)](api-documentation.md#Enmap+removeFrom) ⇒ `Map`
    * [.array\(\)](api-documentation.md#Enmap+array) ⇒ `Array`
    * [.keyArray\(\)](api-documentation.md#Enmap+keyArray) ⇒ `Array`
    * [.random\(\[count\]\)](api-documentation.md#Enmap+random) ⇒ `*` \| `Array.`
    * [.randomKey\(\[count\]\)](api-documentation.md#Enmap+randomKey) ⇒ `*` \| `Array.`
    * [.findAll\(prop, value\)](api-documentation.md#Enmap+findAll) ⇒ `Array`
    * [.find\(propOrFn, \[value\]\)](api-documentation.md#Enmap+find) ⇒ `*`
    * [.exists\(prop, value\)](api-documentation.md#Enmap+exists) ⇒ `boolean`
    * [.filter\(fn, \[thisArg\]\)](api-documentation.md#Enmap+filter) ⇒ [`Enmap`](api-documentation.md#Enmap)
    * [.filterArray\(fn, \[thisArg\]\)](api-documentation.md#Enmap+filterArray) ⇒ `Array`
    * [.map\(fn, \[thisArg\]\)](api-documentation.md#Enmap+map) ⇒ `Array`
    * [.some\(fn, \[thisArg\]\)](api-documentation.md#Enmap+some) ⇒ `boolean`
    * [.every\(fn, \[thisArg\]\)](api-documentation.md#Enmap+every) ⇒ `boolean`
    * [.reduce\(fn, \[initialValue\]\)](api-documentation.md#Enmap+reduce) ⇒ `*`
    * [.clone\(\)](api-documentation.md#Enmap+clone) ⇒ [`Enmap`](api-documentation.md#Enmap)
    * [.concat\(...enmaps\)](api-documentation.md#Enmap+concat) ⇒ [`Enmap`](api-documentation.md#Enmap)
    * [.equals\(enmap\)](api-documentation.md#Enmap+equals) ⇒ `boolean`
  * _static_
    * [.multi\(names, Provider, options\)](api-documentation.md#Enmap.multi) ⇒ `Array.`
    * [.migrate\(source, target\)](api-documentation.md#Enmap.migrate)

### enmap.fetchEverything\(\) ⇒ `Promise.`

Fetches every key from the persistent enmap and loads them into the current enmap value.

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)  
**Returns**: `Promise.` - The enmap containing all values, as a promise..  


### enmap.fetch\(keyOrKeys\) ⇒ `Promise.`

Force fetch one or more key values from the enmap. If the database has changed, that new value is used.

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)  
**Returns**: `Promise.` - A single value if requested, or a non-persistent enmap of keys if an array is requested.

| Param | Type | Description |
| :--- | :--- | :--- |
| keyOrKeys | `string` \| `number` | A single key or array of keys to force fetch from the enmap database. |

### enmap.evict\(keyOrArrayOfKeys\)

Removes a key from the cache - useful when using the fetchAll feature.

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)

| Param | Type | Description |
| :--- | :--- | :--- |
| keyOrArrayOfKeys | `*` | A single key or array of keys to remove from the cache. |

### enmap.autonum\(\) ⇒ `number`

Generates an automatic numerical key for inserting a new value.

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)  
**Returns**: `number` - The generated key number.  
**Example**

```javascript
enmap.set(enmap.autonum(), "This is a new value");
```

### enmap.changed\(cb\)

Function called whenever data changes within Enmap after the initial load. Can be used to detect if another part of your code changed a value in enmap and react on it.

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)

| Param | Type | Description |
| :--- | :--- | :--- |
| cb | `function` | A callback function that will be called whenever data changes in the enmap. |

**Example**

```javascript
enmap.changed((keyName, oldValue, newValue) => {
  console.log(`Value of ${key} has changed from: \n${oldValue}\nto\n${newValue});
});
```

### enmap.set\(key, val, path\) ⇒ `Map`

Set the value in Enmap.

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)  
**Returns**: `Map` - The Enmap.

| Param | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| key | `string` \| `number` |  | Required. The key of the element to add to The Enmap. If the Enmap is persistent this value MUST be a string or number. |
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
enmap.set('IhazObjects', 'color', 'blue'); //modified previous object
enmap.set('ArraysToo', 2, 'three'); // changes "tree" to "three" in array.
```

### enmap.setProp\(key, path, val\) ⇒ `Map`

Modify the property of a value inside the enmap, if the value is an object or array. This is a shortcut to loading the key, changing the value, and setting it back.

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)  
**Returns**: `Map` - The EnMap.

| Param | Type | Description |
| :--- | :--- | :--- |
| key | `string` \| `number` | Required. The key of the element to add to The Enmap or array. This value MUST be a string or number. |
| path | `*` | Required. The property to modify inside the value object or array. Can be a path with dot notation, such as "prop1.subprop2.subprop3" |
| val | `*` | Required. The value to apply to the specified property. |

### enmap.push\(key, val, path, allowDupes\) ⇒ `Map`

Push to an array value in Enmap.

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)  
**Returns**: `Map` - The EnMap.

| Param | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| key | `string` \| `number` |  | Required. The key of the array element to push to in Enmap. This value MUST be a string or number. |
| val | `*` |  | Required. The value to push to the array. |
| path | `string` | `null` | Optional. The path to the property to modify inside the value object or array. Can be a path with dot notation, such as "prop1.subprop2.subprop3" |
| allowDupes | `boolean` | `false` | Optional. Allow duplicate values in the array \(default: false\). |

**Example**

```javascript
// Assuming
enmap.set("simpleArray", [1, 2, 3, 4]);
enmap.set("arrayInObject", {sub: [1, 2, 3, 4]});

enmap.push("simpleArray", 5); // adds 5 at the end of the array
enmap.push("arrayInObject", "five", "sub"); adds "five" at the end of the sub array
```

### enmap.pushIn\(key, path, val, allowDupes\) ⇒ `Map`

Push to an array element inside an Object or Array element in Enmap.

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)  
**Returns**: `Map` - The EnMap.

| Param | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| key | `string` \| `number` |  | Required. The key of the element. This value MUST be a string or number. |
| path | `*` |  | Required. The name of the array property to push to. Can be a path with dot notation, such as "prop1.subprop2.subprop3" |
| val | `*` |  | Required. The value push to the array property. |
| allowDupes | `boolean` | `false` | Allow duplicate values in the array \(default: false\). |

### enmap.math\(key, operation, operand, path\) ⇒ `Map`

Executes a mathematical operation on a value and saves it in the enmap.

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)  
**Returns**: `Map` - The EnMap.

| Param | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| key | `string` \| `number` |  | The enmap key on which to execute the math operation. |
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

### enmap.inc\(key, path\) ⇒ `Map`

Increments a key's value or property by 1. Value must be a number, or a path to a number.

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)  
**Returns**: `Map` - The EnMap.

| Param | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| key | `string` \| `number` |  | The enmap key where the value to increment is stored. |
| path | `string` | `null` | Optional. The property path to increment, if the value is an object or array. |

**Example**

```javascript
// Assuming
points.set("number", 42);
points.set("numberInObject", {sub: { anInt: 5 }});

points.inc("number"); // 43
points.inc("numberInObject", "sub.anInt"); // {sub: { anInt: 6 }}
```

### enmap.dec\(key, path\) ⇒ `Map`

Decrements a key's value or property by 1. Value must be a number, or a path to a number.

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)  
**Returns**: `Map` - The EnMap.

| Param | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| key | `string` \| `number` |  | The enmap key where the value to decrement is stored. |
| path | `string` | `null` | Optional. The property path to decrement, if the value is an object or array. |

**Example**

```javascript
// Assuming
points.set("number", 42);
points.set("numberInObject", {sub: { anInt: 5 }});

points.dec("number"); // 41
points.dec("numberInObject", "sub.anInt"); // {sub: { anInt: 4 }}
```

### enmap.get\(key, path\) ⇒ `*`

Retrieves a key from the enmap. If fetchAll is false, returns a promise.

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)  
**Returns**: `*` - The value for this key.

| Param | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| key | `string` \| `number` |  | The key to retrieve from the enmap. |
| path | `string` | `null` | Optional. The property to retrieve from the object or array. Can be a path with dot notation, such as "prop1.subprop2.subprop3" |

**Example**

```javascript
const myKeyValue = enmap.get("myKey");
console.log(myKeyValue);

const someSubValue = enmap.get("anObjectKey", "someprop.someOtherSubProp");
```

### enmap.getProp\(key, path\) ⇒ `*`

Returns the specific property within a stored value. If the key does not exist or the value is not an object, throws an error.

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)  
**Returns**: `*` - The value of the property obtained.

| Param | Type | Description |
| :--- | :--- | :--- |
| key | `string` \| `number` | Required. The key of the element to get from The Enmap. |
| path | `*` | Required. The property to retrieve from the object or array. Can be a path with dot notation, such as "prop1.subprop2.subprop3" |

### enmap.has\(key, path\) ⇒ `boolean`

Returns whether or not the key exists in the Enmap.

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)

| Param | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| key | `string` \| `number` |  | Required. The key of the element to add to The Enmap or array. This value MUST be a string or number. |
| path | `string` | `null` | Optional. The property to verify inside the value object or array. Can be a path with dot notation, such as "prop1.subprop2.subprop3" |

**Example**

```javascript
if(enmap.has("myKey")) {
  // key is there
}

if(!enmap.has("myOtherKey", "oneProp.otherProp.SubProp")) return false;
```

### enmap.hasProp\(key, path\) ⇒ `boolean`

Returns whether or not the property exists within an object or array value in enmap.

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)  
**Returns**: `boolean` - Whether the property exists.

| Param | Type | Description |
| :--- | :--- | :--- |
| key | `string` \| `number` | Required. The key of the element to check in the Enmap or array. |
| path | `*` | Required. The property to verify inside the value object or array. Can be a path with dot notation, such as "prop1.subprop2.subprop3" |

### enmap.delete\(key, path\)

Deletes a key in the Enmap.

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)

| Param | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| key | `string` \| `number` |  | Required. The key of the element to delete from The Enmap. |
| path | `string` | `null` | Optional. The name of the property to remove from the object. Can be a path with dot notation, such as "prop1.subprop2.subprop3" |

### enmap.deleteProp\(key, path\)

Delete a property from an object or array value in Enmap.

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)

| Param | Type | Description |
| :--- | :--- | :--- |
| key | `string` \| `number` | Required. The key of the element to delete the property from in Enmap. |
| path | `*` | Required. The name of the property to remove from the object. Can be a path with dot notation, such as "prop1.subprop2.subprop3" |

### enmap.deleteAll\(bulk\)

Calls the `delete()` method on all items that have it.

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)

| Param | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| bulk | `boolean` | `true` | Optional. Defaults to True. whether to use the provider's "bulk" delete feature if it has one. |

### enmap.remove\(key, val, path\) ⇒ `Map`

Remove a value in an Array or Object element in Enmap. Note that this only works for values, not keys. Complex values such as objects and arrays will not be removed this way.

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)  
**Returns**: `Map` - The EnMap.

| Param | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| key | `string` \| `number` |  | Required. The key of the element to remove from in Enmap. This value MUST be a string or number. |
| val | `*` |  | Required. The value to remove from the array or object. |
| path | `string` | `null` | Optional. The name of the array property to remove from. Can be a path with dot notation, such as "prop1.subprop2.subprop3". If not presents, removes directly from the value. |

### enmap.removeFrom\(key, path, val\) ⇒ `Map`

Remove a value from an Array or Object property inside an Array or Object element in Enmap. Confusing? Sure is.

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)  
**Returns**: `Map` - The EnMap.

| Param | Type | Description |
| :--- | :--- | :--- |
| key | `string` \| `number` | Required. The key of the element. This value MUST be a string or number. |
| path | `*` | Required. The name of the array property to remove from. Can be a path with dot notation, such as "prop1.subprop2.subprop3" |
| val | `*` | Required. The value to remove from the array property. |

### enmap.array\(\) ⇒ `Array`

Creates an ordered array of the values of this Enmap. The array will only be reconstructed if an item is added to or removed from the Enmap, or if you change the length of the array itself. If you don't want this caching behaviour, use `Array.from(enmap.values())` instead.

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)  


### enmap.keyArray\(\) ⇒ `Array`

Creates an ordered array of the keys of this Enmap The array will only be reconstructed if an item is added to or removed from the Enmap, or if you change the length of the array itself. If you don't want this caching behaviour, use `Array.from(enmap.keys())` instead.

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)  


### enmap.random\(\[count\]\) ⇒ `*` \| `Array.`

Obtains random value\(s\) from this Enmap. This relies on [array](api-documentation.md#Enmap+array).

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)  
**Returns**: `*` \| `Array.` - The single value if `count` is undefined, or an array of values of `count` length

| Param | Type | Description |
| :--- | :--- | :--- |
| \[count\] | `number` | Number of values to obtain randomly |

### enmap.randomKey\(\[count\]\) ⇒ `*` \| `Array.`

Obtains random key\(s\) from this Enmap. This relies on [keyArray](api-documentation.md#Enmap+keyArray)

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)  
**Returns**: `*` \| `Array.` - The single key if `count` is undefined, or an array of keys of `count` length

| Param | Type | Description |
| :--- | :--- | :--- |
| \[count\] | `number` | Number of keys to obtain randomly |

### enmap.findAll\(prop, value\) ⇒ `Array`

Searches for all items where their specified property's value is identical to the given value \(`item[prop] === value`\).

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)

| Param | Type | Description |
| :--- | :--- | :--- |
| prop | `string` | The property to test against |
| value | `*` | The expected value |

**Example**

```javascript
enmap.findAll('username', 'Bob');
```

### enmap.find\(propOrFn, \[value\]\) ⇒ `*`

Searches for a single item where its specified property's value is identical to the given value \(`item[prop] === value`\), or the given function returns a truthy value. In the latter case, this is identical to [Array.find\(\)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find).

All Enmap used in Discord.js are mapped using their \`id\` property, and if you want to find by id you should use the \`get\` method. See \[MDN\]\(https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Map/get\) for details.

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)

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

### enmap.exists\(prop, value\) ⇒ `boolean`

Searches for the existence of a single item where its specified property's value is identical to the given value \(`item[prop] === value`\).

Do not use this to check for an item by its ID. Instead, use \`enmap.has\(id\)\`. See \[MDN\]\(https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Map/has\) for details.

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)

| Param | Type | Description |
| :--- | :--- | :--- |
| prop | `string` | The property to test against |
| value | `*` | The expected value |

**Example**

```javascript
if (enmap.exists('username', 'Bob')) {
 console.log('user here!');
}
```

### enmap.filter\(fn, \[thisArg\]\) ⇒ [`Enmap`](api-documentation.md#Enmap)

Identical to [Array.filter\(\)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter), but returns a Enmap instead of an Array.

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)

| Param | Type | Description |
| :--- | :--- | :--- |
| fn | `function` | Function used to test \(should return a boolean\) |
| \[thisArg\] | `Object` | Value to use as `this` when executing function |

### enmap.filterArray\(fn, \[thisArg\]\) ⇒ `Array`

Identical to [Array.filter\(\)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter).

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)

| Param | Type | Description |
| :--- | :--- | :--- |
| fn | `function` | Function used to test \(should return a boolean\) |
| \[thisArg\] | `Object` | Value to use as `this` when executing function |

### enmap.map\(fn, \[thisArg\]\) ⇒ `Array`

Identical to [Array.map\(\)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map).

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)

| Param | Type | Description |
| :--- | :--- | :--- |
| fn | `function` | Function that produces an element of the new array, taking three arguments |
| \[thisArg\] | `*` | Value to use as `this` when executing function |

### enmap.some\(fn, \[thisArg\]\) ⇒ `boolean`

Identical to [Array.some\(\)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some).

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)

| Param | Type | Description |
| :--- | :--- | :--- |
| fn | `function` | Function used to test \(should return a boolean\) |
| \[thisArg\] | `Object` | Value to use as `this` when executing function |

### enmap.every\(fn, \[thisArg\]\) ⇒ `boolean`

Identical to [Array.every\(\)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every).

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)

| Param | Type | Description |
| :--- | :--- | :--- |
| fn | `function` | Function used to test \(should return a boolean\) |
| \[thisArg\] | `Object` | Value to use as `this` when executing function |

### enmap.reduce\(fn, \[initialValue\]\) ⇒ `*`

Identical to [Array.reduce\(\)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce).

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)

| Param | Type | Description |
| :--- | :--- | :--- |
| fn | `function` | Function used to reduce, taking four arguments; `accumulator`, `currentValue`, `currentKey`, and `enmap` |
| \[initialValue\] | `*` | Starting value for the accumulator |

### enmap.clone\(\) ⇒ [`Enmap`](api-documentation.md#Enmap)

Creates an identical shallow copy of this Enmap.

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)  
**Example**

```javascript
const newColl = someColl.clone();
```

### enmap.concat\(...enmaps\) ⇒ [`Enmap`](api-documentation.md#Enmap)

Combines this Enmap with others into a new Enmap. None of the source Enmaps are modified.

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)

| Param | Type | Description |
| :--- | :--- | :--- |
| ...enmaps | [`Enmap`](api-documentation.md#Enmap) | Enmaps to merge |

**Example**

```javascript
const newColl = someColl.concat(someOtherColl, anotherColl, ohBoyAColl);
```

### enmap.equals\(enmap\) ⇒ `boolean`

Checks if this Enmap shares identical key-value pairings with another. This is different to checking for equality using equal-signs, because the Enmaps may be different objects, but contain the same data.

**Kind**: instance method of [`Enmap`](api-documentation.md#Enmap)  
**Returns**: `boolean` - Whether the Enmaps have identical contents

| Param | Type | Description |
| :--- | :--- | :--- |
| enmap | [`Enmap`](api-documentation.md#Enmap) | Enmap to compare with |

### Enmap.multi\(names, Provider, options\) ⇒ `Array.`

Initialize multiple Enmaps easily.

**Kind**: static method of [`Enmap`](api-documentation.md#Enmap)  
**Returns**: `Array.` - An array of initialized Enmaps.

| Param | Type | Description |
| :--- | :--- | :--- |
| names | `Array.` | Array of strings. Each array entry will create a separate enmap with that name. |
| Provider | `EnmapProvider` | Valid EnmapProvider object. |
| options | `Object` | Options object to pass to the provider. See provider documentation for its options. |

**Example**

```javascript
// Using local variables and the mongodb provider.
const Enmap = require('enmap');
const Provider = require('enmap-mongo');
const { settings, tags, blacklist } = Enmap.multi(['settings', 'tags', 'blacklist'], Provider, { url: "some connection URL here" });

// Attaching to an existing object (for instance some API's client)
const Enmap = require("enmap");
const Provider = require("enmap-mongo");
Object.assign(client, Enmap.multi(["settings", "tags", "blacklist"], Provider, { url: "some connection URL here" }));
```

### Enmap.migrate\(source, target\)

Migrates an Enmap from version 3 or lower to a Version 4 enmap, which is locked to sqlite backend only. Version 4 uses a different way of storing data, so is not directly compatible with version 3 data. Note that this migration also makes the data unuseable with version 3, so it should only be used to migrate once.

**Kind**: static method of [`Enmap`](api-documentation.md#Enmap)

| Param | Type | Description |
| :--- | :--- | :--- |
| source | `Provider` | A valid Enmap provider. Can be any existing provider. |
| target | `Provider` | An SQLite Enmap Provider. Cannot work without enmap-sqlite as the target. |

**Example**

```javascript
// This example migrates from enmap-mongo to the new format.
// Assumes: npm install enmap@3.1.4 enmap-sqlite@latest enmap-mongo@latest
const Enmap = require("enmap");
const Provider = require("enmap-mongo");
const SQLite = require("enmap-sqlite");

let options = {
 name: 'test',
 dbName: 'enmap',
 url: 'mongodb://username:password@localhost:27017/enmap'
};

const source = new Provider(options);
const target = new SQLite({"name": "points"});

Enmap.migrate(source, target);
```

