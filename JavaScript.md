## Prototype

The prototype is an object that is shared among **all** instances of a type.

```javascript
    Bird.prototype.numLegs = 2;
```

## Constructor

* It looks like you can't skip the word `function`. It has to be written out.
* The name of the function (`dummy` in the example) does not matter, but some linters complain if an anonymous function is used.

```javascript
const Cat = function dummy() {     
    this.name = 'Tom';
    this.meow = () => { console.log('meow'); };
    this.createKitten = () => ({ name: 'Kitten' });
};

console.log(Cat); // prints [Function: dummy] or [Function: Cat] if an anonymous function is used
var c = new Cat();
console.log(c.name); // prints 'Tom'
c.meow(); // prints 'meow'
console.log(c.createKitten().name); // prints 'Kitten'
```

The example is based on this example: https://www.w3schools.com/js/js_object_constructors.asp


## Object.assign

`Object.assign` maps the properties in the source objects to those in the target object.

```javascript
let original = {firstName: 'Bob', lastName: 'Smith'};
let change = {lastName: 'Jones'};
let result = Object.assign({}, original, change);

// result is {firstName: 'Bob', lastName: 'Jones'}
```

## Spread operator

"Unwraps" an object. You can rewrite the previous example using the spread operator.

```javascript
let original = {firstName: 'Bob', lastName: 'Smith'};
let change = {lastName: 'Jones'};
let result = { ...original, ...change };

// result is {firstName: 'Bob', lastName: 'Jones'}
```

"Unwraps" an array

```javascript
const numbers = [1, 2, 3];

let another = [...numbers, 4, 5];

// another is [1, 2, 3, 4, 5]
```

## fetch()

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

## Array.concat

```javascript
[1].concat([2]);

// returns a new array: [1, 2]
```

## Check if an object has a property: in
```javascript
let array = [1, 2];
"length" in array
// returns true

let person = { name: "A"};
"name" in person
// returns true
```

## Check if an array has an element: `includes`
```
const array1 = [1, 2, 3];

console.log(array1.includes(2));
// expected output: true
```
See: [Array.prototype.includes()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)

## (Another way): Check if an array has an element: `indexOf`
```javascript
[1, 2, 3].indexOf(2)
// returns 1

[1, 2, 3].indexOf(4)
// returns -1
```

## `concat` (Array.prototype.concat): concatenate arrays or values:
You can concat arrays or values:
```javascript
const array1 = ['a', 'b', 'c'].concat(['d', 'e', 'f']);
// > Array ["a", "b", "c", "d", "e", "f"]
const array2 = ['a', 'b', 'c'].concat('d');
// > Array ["a", "b", "c", "d"]
```

