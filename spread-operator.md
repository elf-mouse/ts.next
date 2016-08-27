## Spread Operator

### Apply

A common use case is to spread an array into the function arguments. Previously you would need to use `Function.prototype.apply`:

```js
function foo(x, y, z) { }
var args = [0, 1, 2];
foo.apply(null, args);
```

Now you can do this simply by prefixing the arguments with `...` as shown below:

```js
function foo(x, y, z) { }
var args = [0, 1, 2];
foo(...args);
```

Here we are spreading the `args` array into positional `arguments`.

### Destructuring

```js
var [x, y, ...remaining] = [1, 2, 3, 4];
console.log(x, y, remaining); // 1, 2, [3,4]
```

### Array Assignment

```js
var list = [1, 2];
list = [...list, 3, 4];
console.log(list); // [1,2,3,4]
```

### Summary

`apply` is something that you would inevitably do in JavaScript, so it's good to have a better syntax where you don't have that ugly `null` for the `this` argument. Also having a dedicated syntax for moving arrays out of (destructuring) or into (assignment) other arrays provides neat syntax for when you are doing array processing on partial arrays.
