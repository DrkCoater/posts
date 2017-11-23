#ECMAScript 6 Variables

By comparing the similarities and differences of similar concepts is a good way to study a topic. Similarities providing information recognize a working pattern; differences provides information to recognize the nature characteristics of the matter.

In ES6, 'const' and 'let' are the first topic in the major improvements over 'var' in ES3 and 5.

##'const' vs ('let' and 'var')
###Some basics
As we can imagine, 'const' abbreviate for constants, let and var abbreviate 'changable' variables. This is correct to some extend.

| const (ES6+) | let (ES6+) and var (ES5+) |
|--------------|---------------------------|
|Provides binding modifications, but not value modifications. | Provides both binding modification and value modifications.|

######Examples

```javascript
  // using const
  const a=16;
  a = 17; // compile error
```

```javascript
  // let or var
  let a=16;
  var b=20;
  a = 17; // ok
  b = 29; // ok
```

###Not too obvious
| const (ES6+) | let (ES6+) and var (ES5+) |
|--------------|---------------------------|
|Declared constants can not be re-assigned, but it's (properties and elements) values can be changed|Declaration allows all modifications.|
|Cannot be used in for iterative loops but it can be used in 'for in' and 'for of' loops. |Can be used any loop declarations declarations.|

######Examples
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

for (const i=0; i<10; i++) { // error
  console.log(i);
}

for (const elm of arr ) {
  console.log(elm); // ok
}

for (const key in obj ) {
  console.log(key, obj[key]); // ok
}

```

##('consts' and 'let') vs 'var'

In Scope

| const and let (ES6+) | var (ES5+) |
|----------------------|------------|
| Scope ||