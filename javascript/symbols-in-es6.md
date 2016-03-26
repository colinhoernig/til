# Symbols in ES6
_03/25/2016_

Symbols are a new primitive type in ES6.  They basically act as unique identifiers.
No two symbols are ever the same.  Symbols take one string parameters, acting as
a description.

```javascript
let first_symbol = Symbol('first_symbol');
let second_symbol = Symbol('second_sybmol');

first_symbol === second_symbol // false
typeof first_symbol // symbol
```

A great use for symbols is as unique property keys on classes and object literals:

```javascript
const UNIQUE_KEY = Symbol();
let obj = {};

obj[UNIQUE_KEY] = "Value here";
console.log(obj[UNIQUE_KEY]); // "Value here"

obj = {
  [UNIQUE_KEY]: "New value here"
};
console.log(obj[UNIQUE_KEY]); // "New value here"
```

In ES6, we use `Object.getOwnPropertyNames(obj)` to get own properties (excluding Symbols).
If we want to get symbols, `Object.getOwnPropertySymbols(obj)`.
To get all keys: `Reflect.ownKeys(obj)`

To learn more, [this](http://www.2ality.com/2014/12/es6-symbols.html) is a great resource on ES6 Symbols.
