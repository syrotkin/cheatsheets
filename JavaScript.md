## Prototype

The prototype is an object that is shared among **all** instances of a type.

```javascript
    Bird.prototype.numLegs = 2;
```

## Constructor


## Object.assign

`Object.assign` maps the properties in the source objects to those in the target object.

```javascript
let original = {firstName: 'Bob', lastName: 'Smith'};
let change = {lastName: 'Jones'};
let result = Object.assign({}, original, change);

// result is {firstName: 'Bob', lastName: 'Jones'}
```

## Spread operator

"Unwraps" an array

```javascript
const numbers = [1, 2, 3];

let another = [...numbers, 4, 5];

// another is [1, 2, 3, 4, 5]
```

## TODO: fetch()

### TODO

```javascript
fetch('')
    .then()
    .then();
```

## Array.fill

Creates an array of `n` elements and fills it with predefined values.

```javascript
Array(6).fill(null);
```

## TODO: Array.concat
