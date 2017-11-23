# ECMAScript 6 Variables

By comparing the similarities and differences of similar concepts is a good way to study a topic. Similarities providing information recognize a working pattern; differences provides information to recognize the nature characteristics of the matter.

In ES6, 'const' and 'let' are the first topic in the major improvements over 'var' in ES3 and 5.

## 'const' vs ('let' and 'var')

In ES6
'const' is for declaring a constant
'let' is for declaring a variable

Pre-ES6
'var' is for declaring all (global, variables and constants).

### 'const' and 'let' basic differences

Most obvious to our understanding, 'const' abbreviates for constant, let and var abbreviate 'to be changed' variable. It is important to know that the value of a declared 'const' can still be modified after its declaration. So, don't be afraid of using 'const' whenever its suitable.

| const (ES6+) | let (ES6+) and var (ES5+) |
|--------------|---------------------------|
|Provides binding modifications, but not value modifications. | Provides both binding modification and value modifications.|

```javascript
  // using const
  const a = 16;
  a = 17; // compile error
```

```javascript
  // let or var
  let a = 16;
  var b = 20;
  a = 17; // ok
  b = 29; // ok
```

### Not too obvious

| const (ES6+) | let (ES6+) and var (ES5+) |
|--------------|---------------------------|
|Declared constants can not be re-assigned, but it's (properties and elements) values can be changed|Declaration allows all modifications.|
|Cannot be used in for iterative loops but it can be used in 'for in' and 'for of' loops. |Can be used any loop declarations declarations.|

- 'const' declarations, can not re-assign after const declaration

```javascript
const obj = {
  a: 16,
  b: 20,
};
obj.a = 19; // ok
obj.b = 21; // ok

obj = {
  a: 19,
  b: 21
}; // error

const arr = [1, 2, 3];
arr.push(4); // ok
arr = [1, 2, 3, 4]; // error
```

- 'const' *cannot* be used in iterative loops, it can be use in 'for in' or 'for of' loops

```javascript
for (const i = 0; i < 10; i++) { // error
  console.log(i);
}

for (const elm of arr ) {
  console.log(elm); // ok
}

for (const key in obj ) {
  console.log(key, obj[key]); // ok
}
```

## ('const' and 'let') vs 'var'

The main differences between const/let and var are behaviors in scope blocks.

| Block Types | const and let (ES6+) | var (ES5+) |
|:-----------:|----------------------|------------|
| **hoisting** | can not be used before its declaration | ok to access and use before declaration
| **conditional blocks** | conditional blocks are also scope blocks | conditional blocks are *NOT* scope blocks
| **loop blocks** | any looks are also scope blocks | loops does *NOT* create scope blocks
| **function blocks** | functions are treated as scope blocks, same as var. | function is the only way to create scope level blocks
| **global block binding** | does not pollute the window object | access and modifies the window object

- Variable hoisting

```javascript
console.log(typeof a); // error a is used before its declaration
a = 1; // error a is used before its declaration
let a = 0;

console.log(typeof b); // ok, but undefined'
b = 2; // ok
var b = 1;
```

- Loop blocks does not create scope block for 'let' or 'const'.

```javascript
for (let i=0; i<10; i++) {
  console.log('in loop, i is:', i); // 0 ~ 9
}
console.log('loop ended, i is:', i); // error, i is undefined

for (var i=0; i<10; i++) {
  console.log('in loop, i is:', i); // i is 0 ~ 9
}
console.log('loop ended, i is:', i); // i is 10
```

- Conditional blocks does not create scope block for 'let' or 'const'.

```javascript
if (false) {
  let a = 0;
}
console.log('a is', a); // error, a is undefined

if (false) {
  var a = 0;
}
console.log('a is', a); // a is 0
```

- 'const', 'let' and 'var' behaves the same in Function blocks, in fact, function is the only way for 'var' to create a scope block.

```javascript

// There is a issue of using var in for loop block decoration
var functions = [];
for (var i = 0; i<10; i++) {
  functions.push(function() {
    console.log('i: ', i);
  });
}

functions.forEach(function(func) {
  func(); // this will output 10 for ten times
})

// ************************* //

// to fix this:
var functions = [];
for (var i = 0; i<10; i++) {
  functions.push((function(value) {
    // This is a private scope block owned by each function.
    // The value is stored in this scope block
    return function() {
      console.log('i: ', value);
    };
  }());
}

functions.forEach(function(func) {
  func(); // this will output each of i from 0 to 9
})

// ************************* //

// let declaration in for loop will not have this problem
var functions = [];
for (let i = 0; i<10; i++) {
  functions.push(function() {
    console.log('i: ', i);
  });
}

functions.forEach(function(func) {
  func(); // this will output each of i from 0 to 9
})
```

- Global block binding

```javascript
var testing = 'testing';
if (testing === window['testing']) {
  console.log('the same'); // this will print out the same
}

const testing = 'testing'; // same as let declaration
if (testing === window['testing']) { // they are not the same
  console.log('the same'); // this will NOT get print out
}

```

## References

- [Understanding ECMAScript 6](https://leanpub.com/understandinges6/read/)
- [ECMAScript 6 Primer in Chinese](http://es6.ruanyifeng.com/)
- [Mozilla ES6 Documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)