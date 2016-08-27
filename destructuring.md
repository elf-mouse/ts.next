## Destructuring

TypeScript supports the following forms of Destructuring (literally named after de-structuring i.e. breaking up the structure):

1. Object Destructuring
2. Array Destructuring

It is easy to think of destructuring as an inverse of structuring. The method of structuring in JavaScript is the object literal:

```js
var foo = {
    bar: {
        bas: 123
    }
};
```

Without the awesome _structuring_ support built into JavaScript creating new objects on the fly would indeed be very cumbersome. Destructuring brings the same level of convenience to getting data out of a structure.

### Object Destructuring

Destructuring is useful because it allows you to do in a single line, what would otherwise require multiple lines. Consider the following case:

```js
var rect = { x: 0, y: 10, width: 15, height: 20 };

// Destructuring assignment
var {x, y, width, height} = rect;
console.log(x, y, width, height); // 0,10,15,20
```

Here in the absence of destructuring you would have to pick off `x`,`y`,`width`,`height` one by one from `rect`.

To assign an extracted variable to a new variable name you can do the following:

```js
// structure
const obj = {"some property": "some value"};

// destructure
const {"some property": someProperty} = obj;
console.log(someProperty === "some value"); // true
```

Additionally you can get deep data out of a structure using destructuring. This is shown in the following example:

```js
var foo = { bar: { bas: 123 } };
var {bar: {bas}} = foo; // Effectively `var bas = foo.bar.bas;`
```

### Array Destructuring

A common programming question : Swap two variables without using a third one. The TypeScript solution:

```ts
var x = 1, y = 2;
[x, y] = [y, x];
console.log(x, y); // 2,1
```

Note that array destructuring is effectively the compiler doing the `[0], [1], ...` and so on for you. There is no guarantee that these values will exist.

### Array Destructuring with rest

You can pick up any number of elements from the array and get an array of the remaining elements using array destructuring with rest.

```js
var [x, y, ...remaining] = [1, 2, 3, 4];
console.log(x, y, remaining); // 1, 2, [3,4]
```

### JS Generation

```js
var x = 1, y = 2;
[x, y] = [y, x];
console.log(x, y); // 2,1

// becomes //

var x = 1, y = 2;
_a = [y,x], x = _a[0], y = _a[1];
console.log(x, y);
var _a;
```
