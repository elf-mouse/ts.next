## let

```js
var foo = 123;
if (true) {
    var foo = 456;
}
console.log(foo); // 456
```

```js
let foo = 123;
if (true) {
    let foo = 456;
}
console.log(foo); // 123
```

Another place where `let` would save you from errors is loops.

```js
var index = 0;
var array = [1, 2, 3];
for (let index = 0; index < array.length; index++) {
    console.log(array[index]);
}
console.log(index); // 0
```

### Functions create a new scope

```js
var foo = 123;
function test() {
    var foo = 456;
}
test();
console.log(foo); // 123
```

### Generated JS

```js
if (true) {
    let foo = 123;
}

// becomes //

if (true) {
    var foo = 123;
}
```

```js
var foo = '123';
if (true) {
    let foo = 123;
}

// becomes //

var foo = '123';
if (true) {
    var _foo = 123; // Renamed
}
```

### let in closures

A common programming interview question for a JavaScript developer is what is the log of this simple file:

```js
var funcs = [];
// create a bunch of functions
for (var i = 0; i < 3; i++) {
    funcs.push(function() {
        console.log(i);
    })
}
// call them
for (var j = 0; j < 3; j++) {
    funcs[j]();
}
```

One would have expected it to be `0,1,2`. Surprisingly it is going to be `3` for all three functions. Reason is that all three functions are using the variable `i` from the outer scope and at the time we execute them (in the second loop) the value of `i` will be `3` (that's the termination condition for the first loop).

A fix would be to create a new variable in each loop specific to that loop iteration. As we've learnt before we can create a new variable scope by creating a new function and immediately executing it (i.e. the IIFE pattern from classes `(function() { /* body */ })();`) as shown below:

```js
var funcs = [];
// create a bunch of functions
for (var i = 0; i < 3; i++) {
    (function() {
        var local = i;
        funcs.push(function() {
            console.log(local);
        })
    })();
}
// call them
for (var j = 0; j < 3; j++) {
    funcs[j]();
}
```

Here the functions close over (hence called a `closure`) the local variable (conveniently named `local`) and use that instead of the loop variable `i`.

> Note that closures come with a performance impact (they need to store the surrounding state)

The ES6 `let` keyword in a loop would have the same behavior as the previous example

```js
var funcs = [];
// create a bunch of functions
for (let i = 0; i < 3; i++) { // Note the use of let
    funcs.push(function() {
        console.log(i);
    })
}
// call them
for (var j = 0; j < 3; j++) {
    funcs[j]();
}
```

Using a `let` instead of `var` creates a variable `i` unique to each loop iteration.
