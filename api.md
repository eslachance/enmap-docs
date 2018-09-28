---
description: 'The full, boring, unadultered enmap docs.'
---

# API Reference

## Enmap ⇐ `Map`

A enhanced Map structure with additional utility methods. Can be made persistent

**Kind**: global class  
**Extends**: `Map`

* [Enmap](api.md#Enmap) ⇐ `Map`
  * _instance_
    * [.count](api.md#enmap-count-integer) ⇒ `integer`
    * [.indexes](api.md#enmap-indexes-array) ⇒ `array.`
    * [.set\(key, val, path\)](api.md#enmap-set-key-val-path-enmap) ⇒ [`Enmap`](api.md#Enmap)
    * [.get\(key, path\)](api.md#enmap-get-key-path) ⇒ `*`
    * [.fetchEverything\(\)](api.md#enmap-fetcheverything-enmap) ⇒ [`Enmap`](api.md#Enmap)
    * [.fetch\(keyOrKeys\)](api.md#enmap-fetch-keyorkeys-enmap) ⇒ [`Enmap`](api.md#Enmap)
    * [.evict\(keyOrArrayOfKeys\)](api.md#enmap-evict-keyorarrayofkeys-enmap) ⇒ [`Enmap`](api.md#Enmap)
    * [.autonum\(\)](api.md#enmap-autonum-number) ⇒ `number`
    * [.changed\(cb\)](api.md#enmap-changed-cb)
    * [.close\(\)](api.md#enmap-close-promise) ⇒ `Promise.`
    * [.setProp\(key, path, val\)](api.md#enmap-setprop-key-path-val-enmap) ⇒ [`Enmap`](api.md#Enmap)
    * [.push\(key, val, path, allowDupes\)](api.md#enmap-push-key-val-path-allowdupes-enmap) ⇒ [`Enmap`](api.md#Enmap)
    * [.pushIn\(key, path, val, allowDupes\)](api.md#enmap-pushin-key-path-val-allowdupes-enmap) ⇒ [`Enmap`](api.md#Enmap)
    * [.math\(key, operation, operand, path\)](api.md#enmap-math-key-operation-operand-path-map) ⇒ `Map`
    * [.inc\(key, path\)](api.md#enmap-inc-key-path-map) ⇒ `Map`
    * [.dec\(key, path\)](api.md#enmap-dec-key-path-map) ⇒ `Map`
    * [.getProp\(key, path\)](api.md#enmap-getprop-key-path) ⇒ `*`
    * [.ensure\(key, defaultvalue\)](api.md#enmap-ensure-key-defaultvalue) ⇒ `*`
    * [.has\(key, path\)](api.md#enmap-has-key-path-boolean) ⇒ `boolean`
    * [.hasProp\(key, path\)](api.md#enmap-hasprop-key-path-boolean) ⇒ `boolean`
    * [.delete\(key, path\)](api.md#enmap-delete-key-path-enmap) ⇒ [`Enmap`](api.md#Enmap)
    * [.deleteProp\(key, path\)](api.md#enmap-deleteprop-key-path)
    * [.deleteAll\(\)](api.md#enmap-deleteall)
    * [.remove\(key, val, path\)](api.md#enmap-remove-key-val-path-map) ⇒ `Map`
    * [.removeFrom\(key, path, val\)](api.md#enmap-removefrom-key-path-val-map) ⇒ `Map`
    * [.array\(\)](api.md#enmap-array-array) ⇒ `Array`
    * [.keyArray\(\)](api.md#enmap-keyarray-array) ⇒ `Array`
    * [.random\(\[count\]\)](api.md#enmap-random-count-or-array) ⇒ `*` \| `Array.`
    * [.randomKey\(\[count\]\)](api.md#enmap-randomkey-count-or-array) ⇒ `*` \| `Array.`
    * [.findAll\(prop, value\)](api.md#enmap-findall-prop-value-array) ⇒ `Array`
    * [.find\(propOrFn, \[value\]\)](api.md#enmap-find-proporfn-value) ⇒ `*`
    * [.exists\(prop, value\)](api.md#enmap-exists-prop-value-boolean) ⇒ `boolean`
    * [.filter\(fn, \[thisArg\]\)](api.md#enmap-filter-fn-thisarg-enmap) ⇒ [`Enmap`](api.md#Enmap)
    * [.filterArray\(fn, \[thisArg\]\)](api.md#enmap-filterarray-fn-thisarg-array) ⇒ `Array`
    * [.map\(fn, \[thisArg\]\)](api.md#enmap-map-fn-thisarg-array) ⇒ `Array`
    * [.some\(fn, \[thisArg\]\)](api.md#enmap-some-fn-thisarg-boolean) ⇒ `boolean`
    * [.every\(fn, \[thisArg\]\)](api.md#enmap-every-fn-thisarg-boolean) ⇒ `boolean`
    * [.reduce\(fn, \[initialValue\]\)](api.md#enmap-reduce-fn-initialvalue) ⇒ `*`
    * [.clone\(\)](api.md#enmap-clone-enmap) ⇒ [`Enmap`](api.md#Enmap)
    * [.concat\(...enmaps\)](api.md#enmap-concat-enmaps-enmap) ⇒ [`Enmap`](api.md#Enmap)
    * [.equals\(enmap\)](api.md#enmap-equals-enmap-boolean) ⇒ `boolean`
  * _static_
    * [.multi\(names, options\)](api.md#enmap-multi-names-options-array) ⇒ `Array.`

### enmap.count ⇒ `integer`

Retrieves the number of rows in the database for this enmap, even if they aren't fetched.

**Kind**: instance property of [`Enmap`](api.md#Enmap)  
**Returns**: `integer` - The number of rows in the database.  


### enmap.indexes ⇒ `array.`

Retrieves all the indexes \(keys\) in the database for this enmap, even if they aren't fetched.

**Kind**: instance property of [`Enmap`](api.md#Enmap)  
**Returns**: `array.` - Array of all indexes \(keys\) in the enmap, cached or not.  


### enmap.set\(key, val, path\) ⇒ [`Enmap`](api.md#Enmap)

Sets a value in Enmap.

**Kind**: instance method of [`Enmap`](api.md#Enmap)  
**Returns**: [`Enmap`](api.md#Enmap) - The enmap.

| Param | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| key | `string` \| `number` |  | Required. The key of the element to add to The Enmap. |
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

### enmap.get\(key, path\) ⇒ `*`

Retrieves a key from the enmap. If fetchAll is false, returns a promise.

**Kind**: instance method of [`Enmap`](api.md#Enmap)  
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

### enmap.fetchEverything\(\) ⇒ [`Enmap`](api.md#Enmap)

Fetches every key from the persistent enmap and loads them into the current enmap value.

**Kind**: instance method of [`Enmap`](api.md#Enmap)  
**Returns**: [`Enmap`](api.md#Enmap) - The enmap containing all values.  


### enmap.fetch\(keyOrKeys\) ⇒ [`Enmap`](api.md#Enmap)

Force fetch one or more key values from the enmap. If the database has changed, that new value is used.

**Kind**: instance method of [`Enmap`](api.md#Enmap)  
**Returns**: [`Enmap`](api.md#Enmap) - The Enmap, including the new fetched value\(s\).

| Param | Type | Description |
| :--- | :--- | :--- |
| keyOrKeys | `string` \| `number` | A single key or array of keys to force fetch from the enmap database. |

### enmap.evict\(keyOrArrayOfKeys\) ⇒ [`Enmap`](api.md#Enmap)

Removes a key or keys from the cache - useful when disabling autoFetch.

**Kind**: instance method of [`Enmap`](api.md#Enmap)  
**Returns**: [`Enmap`](api.md#Enmap) - The enmap minus the evicted keys.

| Param | Type | Description |
| :--- | :--- | :--- |
| keyOrArrayOfKeys | `*` | A single key or array of keys to remove from the cache. |

### enmap.autonum\(\) ⇒ `number`

Generates an automatic numerical key for inserting a new value. This is a "weak" method, it ensures the value isn't duplicated, but does not guarantee it's sequential \(if a value is deleted, another can take its place\). Useful for logging, but not much else.

**Kind**: instance method of [`Enmap`](api.md#Enmap)  
**Returns**: `number` - The generated key number.  
**Example**

```javascript
enmap.set(enmap.autonum(), "This is a new value");
```

### enmap.changed\(cb\)

Function called whenever data changes within Enmap after the initial load. Can be used to detect if another part of your code changed a value in enmap and react on it.

**Kind**: instance method of [`Enmap`](api.md#Enmap)

| Param | Type | Description |
| :--- | :--- | :--- |
| cb | `function` | A callback function that will be called whenever data changes in the enmap. |

**Example**

```javascript
enmap.changed((keyName, oldValue, newValue) => {
  console.log(`Value of ${keyName} has changed from: \n${oldValue}\nto\n${newValue});
});
```

### enmap.close\(\) ⇒ `Promise.`

Shuts down the database. WARNING: USING THIS MAKES THE ENMAP UNUSEABLE. You should only use this method if you are closing your entire application. Note that honestly I've never had to use this, shutting down the app without a close\(\) is fine.

**Kind**: instance method of [`Enmap`](api.md#Enmap)  
**Returns**: `Promise.` - The promise of the database closing operation.  


### enmap.setProp\(key, path, val\) ⇒ [`Enmap`](api.md#Enmap)

Modify the property of a value inside the enmap, if the value is an object or array. This is a shortcut to loading the key, changing the value, and setting it back.

**Kind**: instance method of [`Enmap`](api.md#Enmap)  
**Returns**: [`Enmap`](api.md#Enmap) - The enmap.

| Param | Type | Description |
| :--- | :--- | :--- |
| key | `string` \| `number` | Required. The key of the element to add to The Enmap or array. This value MUST be a string or number. |
| path | `*` | Required. The property to modify inside the value object or array. Can be a path with dot notation, such as "prop1.subprop2.subprop3" |
| val | `*` | Required. The value to apply to the specified property. |

### enmap.push\(key, val, path, allowDupes\) ⇒ [`Enmap`](api.md#Enmap)

Push to an array value in Enmap.

**Kind**: instance method of [`Enmap`](api.md#Enmap)  
**Returns**: [`Enmap`](api.md#Enmap) - The enmap.

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

### enmap.pushIn\(key, path, val, allowDupes\) ⇒ [`Enmap`](api.md#Enmap)

Push to an array element inside an Object or Array element in Enmap.

**Kind**: instance method of [`Enmap`](api.md#Enmap)  
**Returns**: [`Enmap`](api.md#Enmap) - The enmap.

| Param | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| key | `string` \| `number` |  | Required. The key of the element. This value MUST be a string or number. |
| path | `*` |  | Required. The name of the array property to push to. Can be a path with dot notation, such as "prop1.subprop2.subprop3" |
| val | `*` |  | Required. The value push to the array property. |
| allowDupes | `boolean` | `false` | Allow duplicate values in the array \(default: false\). |

### enmap.math\(key, operation, operand, path\) ⇒ `Map`

Executes a mathematical operation on a value and saves it in the enmap.

**Kind**: instance method of [`Enmap`](api.md#Enmap)  
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

**Kind**: instance method of [`Enmap`](api.md#Enmap)  
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

**Kind**: instance method of [`Enmap`](api.md#Enmap)  
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

### enmap.getProp\(key, path\) ⇒ `*`

Returns the specific property within a stored value. If the key does not exist or the value is not an object, throws an error.

**Kind**: instance method of [`Enmap`](api.md#Enmap)  
**Returns**: `*` - The value of the property obtained.

| Param | Type | Description |
| :--- | :--- | :--- |
| key | `string` \| `number` | Required. The key of the element to get from The Enmap. |
| path | `*` | Required. The property to retrieve from the object or array. Can be a path with dot notation, such as "prop1.subprop2.subprop3" |

### enmap.ensure\(key, defaultvalue\) ⇒ `*`

Returns the key's value, or the default given, ensuring that the data is there. This is a shortcut to "if enmap doesn't have key, set it, then get it" which is a very common pattern.

**Kind**: instance method of [`Enmap`](api.md#Enmap)  
**Returns**: `*` - The value from the database for the key, or the default value provided for a new key.

| Param | Type | Description |
| :--- | :--- | :--- |
| key | `string` \| `number` | Required. The key you want to make sure exists. |
| defaultvalue | `*` | Required. The value you want to save in the database and return as default. |

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

### enmap.has\(key, path\) ⇒ `boolean`

Returns whether or not the key exists in the Enmap.

**Kind**: instance method of [`Enmap`](api.md#Enmap)

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

**Kind**: instance method of [`Enmap`](api.md#Enmap)  
**Returns**: `boolean` - Whether the property exists.

| Param | Type | Description |
| :--- | :--- | :--- |
| key | `string` \| `number` | Required. The key of the element to check in the Enmap or array. |
| path | `*` | Required. The property to verify inside the value object or array. Can be a path with dot notation, such as "prop1.subprop2.subprop3" |

### enmap.delete\(key, path\) ⇒ [`Enmap`](api.md#Enmap)

Deletes a key in the Enmap.

**Kind**: instance method of [`Enmap`](api.md#Enmap)  
**Returns**: [`Enmap`](api.md#Enmap) - The enmap.

| Param | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| key | `string` \| `number` |  | Required. The key of the element to delete from The Enmap. |
| path | `string` | `null` | Optional. The name of the property to remove from the object. Can be a path with dot notation, such as "prop1.subprop2.subprop3" |

### enmap.deleteProp\(key, path\)

Delete a property from an object or array value in Enmap.

**Kind**: instance method of [`Enmap`](api.md#Enmap)

| Param | Type | Description |
| :--- | :--- | :--- |
| key | `string` \| `number` | Required. The key of the element to delete the property from in Enmap. |
| path | `*` | Required. The name of the property to remove from the object. Can be a path with dot notation, such as "prop1.subprop2.subprop3" |

### enmap.deleteAll\(\)

Deletes everything from the enmap. If persistent, clears the database of all its data for this table.

**Kind**: instance method of [`Enmap`](api.md#Enmap)  


### enmap.remove\(key, val, path\) ⇒ `Map`

Remove a value in an Array or Object element in Enmap. Note that this only works for values, not keys. Complex values such as objects and arrays will not be removed this way.

**Kind**: instance method of [`Enmap`](api.md#Enmap)  
**Returns**: `Map` - The EnMap.

| Param | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| key | `string` \| `number` |  | Required. The key of the element to remove from in Enmap. This value MUST be a string or number. |
| val | `*` |  | Required. The value to remove from the array or object. |
| path | `string` | `null` | Optional. The name of the array property to remove from. Can be a path with dot notation, such as "prop1.subprop2.subprop3". If not presents, removes directly from the value. |

### enmap.removeFrom\(key, path, val\) ⇒ `Map`

Remove a value from an Array or Object property inside an Array or Object element in Enmap. Confusing? Sure is.

**Kind**: instance method of [`Enmap`](api.md#Enmap)  
**Returns**: `Map` - The EnMap.

| Param | Type | Description |
| :--- | :--- | :--- |
| key | `string` \| `number` | Required. The key of the element. This value MUST be a string or number. |
| path | `*` | Required. The name of the array property to remove from. Can be a path with dot notation, such as "prop1.subprop2.subprop3" |
| val | `*` | Required. The value to remove from the array property. |

### enmap.array\(\) ⇒ `Array`

Creates an ordered array of the values of this Enmap. The array will only be reconstructed if an item is added to or removed from the Enmap, or if you change the length of the array itself. If you don't want this caching behaviour, use `Array.from(enmap.values())` instead.

**Kind**: instance method of [`Enmap`](api.md#Enmap)  


### enmap.keyArray\(\) ⇒ `Array`

Creates an ordered array of the keys of this Enmap The array will only be reconstructed if an item is added to or removed from the Enmap, or if you change the length of the array itself. If you don't want this caching behaviour, use `Array.from(enmap.keys())` instead.

**Kind**: instance method of [`Enmap`](api.md#Enmap)  


### enmap.random\(\[count\]\) ⇒ `*` \| `Array.`

Obtains random value\(s\) from this Enmap. This relies on [array](api.md#Enmap+array).

**Kind**: instance method of [`Enmap`](api.md#Enmap)  
**Returns**: `*` \| `Array.` - The single value if `count` is undefined, or an array of values of `count` length

| Param | Type | Description |
| :--- | :--- | :--- |
| \[count\] | `number` | Number of values to obtain randomly |

### enmap.randomKey\(\[count\]\) ⇒ `*` \| `Array.`

Obtains random key\(s\) from this Enmap. This relies on [keyArray](api.md#Enmap+keyArray)

**Kind**: instance method of [`Enmap`](api.md#Enmap)  
**Returns**: `*` \| `Array.` - The single key if `count` is undefined, or an array of keys of `count` length

| Param | Type | Description |
| :--- | :--- | :--- |
| \[count\] | `number` | Number of keys to obtain randomly |

### enmap.findAll\(prop, value\) ⇒ `Array`

Searches for all items where their specified property's value is identical to the given value \(`item[prop] === value`\).

**Kind**: instance method of [`Enmap`](api.md#Enmap)

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

**Kind**: instance method of [`Enmap`](api.md#Enmap)

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

**Kind**: instance method of [`Enmap`](api.md#Enmap)

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

### enmap.filter\(fn, \[thisArg\]\) ⇒ [`Enmap`](api.md#Enmap)

Identical to [Array.filter\(\)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter), but returns a Enmap instead of an Array.

**Kind**: instance method of [`Enmap`](api.md#Enmap)

| Param | Type | Description |
| :--- | :--- | :--- |
| fn | `function` | Function used to test \(should return a boolean\) |
| \[thisArg\] | `Object` | Value to use as `this` when executing function |

### enmap.filterArray\(fn, \[thisArg\]\) ⇒ `Array`

Identical to [Array.filter\(\)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter).

**Kind**: instance method of [`Enmap`](api.md#Enmap)

| Param | Type | Description |
| :--- | :--- | :--- |
| fn | `function` | Function used to test \(should return a boolean\) |
| \[thisArg\] | `Object` | Value to use as `this` when executing function |

### enmap.map\(fn, \[thisArg\]\) ⇒ `Array`

Identical to [Array.map\(\)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map).

**Kind**: instance method of [`Enmap`](api.md#Enmap)

| Param | Type | Description |
| :--- | :--- | :--- |
| fn | `function` | Function that produces an element of the new array, taking three arguments |
| \[thisArg\] | `*` | Value to use as `this` when executing function |

### enmap.some\(fn, \[thisArg\]\) ⇒ `boolean`

Identical to [Array.some\(\)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some).

**Kind**: instance method of [`Enmap`](api.md#Enmap)

| Param | Type | Description |
| :--- | :--- | :--- |
| fn | `function` | Function used to test \(should return a boolean\) |
| \[thisArg\] | `Object` | Value to use as `this` when executing function |

### enmap.every\(fn, \[thisArg\]\) ⇒ `boolean`

Identical to [Array.every\(\)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every).

**Kind**: instance method of [`Enmap`](api.md#Enmap)

| Param | Type | Description |
| :--- | :--- | :--- |
| fn | `function` | Function used to test \(should return a boolean\) |
| \[thisArg\] | `Object` | Value to use as `this` when executing function |

### enmap.reduce\(fn, \[initialValue\]\) ⇒ `*`

Identical to [Array.reduce\(\)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce).

**Kind**: instance method of [`Enmap`](api.md#Enmap)

| Param | Type | Description |
| :--- | :--- | :--- |
| fn | `function` | Function used to reduce, taking four arguments; `accumulator`, `currentValue`, `currentKey`, and `enmap` |
| \[initialValue\] | `*` | Starting value for the accumulator |

### enmap.clone\(\) ⇒ [`Enmap`](api.md#Enmap)

Creates an identical shallow copy of this Enmap.

**Kind**: instance method of [`Enmap`](api.md#Enmap)  
**Example**

```javascript
const newColl = someColl.clone();
```

### enmap.concat\(...enmaps\) ⇒ [`Enmap`](api.md#Enmap)

Combines this Enmap with others into a new Enmap. None of the source Enmaps are modified.

**Kind**: instance method of [`Enmap`](api.md#Enmap)

| Param | Type | Description |
| :--- | :--- | :--- |
| ...enmaps | [`Enmap`](api.md#Enmap) | Enmaps to merge |

**Example**

```javascript
const newColl = someColl.concat(someOtherColl, anotherColl, ohBoyAColl);
```

### enmap.equals\(enmap\) ⇒ `boolean`

Checks if this Enmap shares identical key-value pairings with another. This is different to checking for equality using equal-signs, because the Enmaps may be different objects, but contain the same data.

**Kind**: instance method of [`Enmap`](api.md#Enmap)  
**Returns**: `boolean` - Whether the Enmaps have identical contents

| Param | Type | Description |
| :--- | :--- | :--- |
| enmap | [`Enmap`](api.md#Enmap) | Enmap to compare with |

### Enmap.multi\(names, options\) ⇒ `Array.`

Initialize multiple Enmaps easily.

**Kind**: static method of [`Enmap`](api.md#Enmap)  
**Returns**: `Array.` - An array of initialized Enmaps.

| Param | Type | Description |
| :--- | :--- | :--- |
| names | `Array.` | Array of strings. Each array entry will create a separate enmap with that name. |
| options | `Object` | Options object to pass to the provider. See provider documentation for its options. |

**Example**

```javascript
// Using local variables and the mongodb provider.
const Enmap = require('enmap');
const { settings, tags, blacklist } = Enmap.multi(['settings', 'tags', 'blacklist']);

// Attaching to an existing object (for instance some API's client)
const Enmap = require("enmap");
Object.assign(client, Enmap.multi(["settings", "tags", "blacklist"]));
```

