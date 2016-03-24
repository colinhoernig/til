# JavaScript `this` Keyword - Binding Rules
_03/23/2016_

##### _These are notes taken from Kyle Simpson's "Frontend Masters" Advanced Javascript course. If you want to learn more, I highly recommend taking his course and/or reading his [You Don't Know JS](https://github.com/getify/You-Dont-Know-JS) book series._

While executing, *every function* has a reference to its current execution context.
We refer to that reference as the `this` keyword.

How the function is called, when it's called, changes the context of `this` ("dynamic scope").

4 rules for `this` binding.  All depend on the call site (where the function gets executed, `yourFunc()`).
These rules have an order of precedence.  All you need to know is where a function is called and how it is called (or: what does the call site look like?)

Find the call site, and then ask these questions:

  1. Was the function called with `new`?
  2. Was the function called with `call` or `apply` specifying `this`?
  3. Was the function called via a owning object (context)?
  4. DEFAULT: global object (except `strict` mode)

---

  1. #### `new` Keyword

  The `new` keyword turns any function call into a constructor call.

  ```javascript
  function foo() {
    this.baz = "baz";
    console.log(this.bar + " " + baz); // undefined undefined
    // implicitly return this
  }

  var bar = "bar";
  var baz = new foo(); // { baz: "baz" }
  console.log(baz.baz); // "baz"
  ```

  Four things take place by using `new` in front of a function call:
  
    A brand new object (`{}`) is created  
    The new object gets linked to a different object *  
    The new object gets bound as the `this` keyword for the function call  
    If that function does not return anything, it implicitly returns `this`

  2. #### Explicit Binding

  If you use `.call()` or `.apply()` at the call site, they accept a `this` arg as their first param.  This explicitly states which `this` binding we wish to occur.

  ```javascript
  function() {
    console.log(this.bar);
  }

  var bar = "bar1";
  var obj = { bar: "bar2" };

  foo();          // "bar1"
  foo.call(obj);  // "bar2"
  ```

  3. #### Implicit Binding

  ```javascript
  function foo() {
    console.log(this.bar);
  }

  var bar = "bar1";
  var o2 = { bar: "bar2", foo: foo };
  var o3 = { bar: "bar3", foo: foo };

  foo();      // "bar1"
  o2.foo();   // "bar2"
  o3.foo();   // "bar3"
  ```

  When there is an object property reference at the call site, implicit binding applies and the base (context) object becomes `this`.

  The implicit binding rule has an owning/containing context object at the call site `o2.foo()`.

  4. #### Default (catch-all) Binding

  As none of the other rules apply, the default binding rule holds.

  The default binding rule has a plain function call `foo()`.

  If `strict` mode (of code within calling function), `this` defaults to undefined.  Otherwise, default `this` to the global object.

---

### Hard binding

Want to make sure your function is always called with a predictable `this` context? Hard bind it.

```javascript
function bind(fn, o) {
  return function() {
    fn.call(o);
  }
}

function foo() {
  console.log(this.bar);
}

var obj = { bar: "bar" };
var obj2 = { bar: "bar2" };

foo = bind(foo, obj);

foo();          // "bar"
foo.call(obj2); // "bar"
```

We could add it to the Function prototype...but we don't need to because it's built into ES5 ([polyfill if necessary](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind#Polyfill))

```javascript
if (!Function.prototype.bind2) {
  Function.prototype.bind2 = function(o) {
    var fn = this; // the function
    return function() {
      return fn.apply(o, arguments);
    };
  }
}

function foo(baz) {
  console.log(this.bar + " " + baz);
}

var obj = { bar: "bar" };
foo = foo.bind2(obj);

foo("baz"); // "bar baz"
```
