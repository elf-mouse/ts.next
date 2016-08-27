## const

```js
// Low readability
if (x > 10) {
}

// Better!
const maxRows = 10;
if (x > maxRows) {
}
```

### const declarations must be initialized

The following is a compiler error:

```js
const foo; // ERROR: const declarations must be initialized
```

### Left hand side of assignment cannot be a constant

Constants are immutable after creation, so if you try to assign them to a new value it is a compiler error:

```js
const foo = 123;
foo = 456; // ERROR: Left-hand side of an assignment expression cannot be a constant
```

### Block Scoped

A `const` is block scoped like we saw with `let`:

```js
const foo = 123;
if (true) {
    const foo = 456; // Allowed as its a new variable limited to this `if` block
}
```

### Deep immutability

A `const` works with object literals as well, as far as protecting the variable _reference_ is concerned:

```js
const foo = { bar: 123 };
foo = { bar: 456 }; // ERROR : Left hand side of an assignment expression cannot be a constant
```

However it still allows sub properties of objects to be mutated, as shown below:

```js
const foo = { bar: 123 };
foo.bar = 456; // Allowed!
console.log(foo); // { bar: 456 }
```

For this reason I recommend using `const` with literals or immutable data structures.
