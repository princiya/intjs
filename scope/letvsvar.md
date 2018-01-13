Code snippets explaining variables and scope in JavaScript.

------

*Scope for `let` vs `var`*

```
function scope() {
    if (true) {
        let tmp;
    }
    console.log(tmp); // ReferenceError: tmp is not defined here because `let` is block scoped
                      // and is declared outside the scope of the executing code
}
```

```
function scope() {
    if (true) {
        var tmp;
    }
    console.log(tmp); // Logs `undefined`, because the variable has been declared but not initialised.
                      // There isn't any error in this case
}
```

--------

*[Hoisting](#hoisting)*
*`ReferenceError` vs `undefined`*

```
function scope() {
  console.log(hoist); // ReferenceError: hoist is not defined
                      // Trying to access an undeclared variable
}
```


```
function scope() {
  console.log(hoist); // Logs `undefined`

  var hoist = 'The variable has been hoisted.';
}
```

```
// This is how the JavaScript interpreter sees the hoisted code:

function scope() {
  var hoist;

  console.log('hoist');

  hoist = 'The variable has been hoisted.';
}
```

------

*Declaration vs Definition of a variable*

```
var tmp; // Declaration

var tmp = 123; // Declaration and definition (assignment)
```
--------

*Variable defined, but not declared*

```
function scope() {
  tmp = 123;

  console.log(tmp); // Logs 123
}

// Reference `tmp` from outside the function scope
console.log(tmp); // Logs 123
                  // Variable `tmp` is defined but not declared inside the function
                  // In this case, `tmp` is treated as a global variable
```

--------

*`var` vs `let` in loops*

```
for(var i = 1; i <= 5; i++) {
  setTimeout(function() {
    console.log('Value of i : ' + i);
  },100);
}

*Output:*

Value of i : 6
Value of i : 6
Value of i : 6
Value of i : 6
Value of i : 6
```
A `var` in the head of a `for` loop creates a single storage space for that variable.
Every i in the bodies of the `setTimeout` functions refers to the same binding, which is why they all return the same value.

```
for(let i = 1; i <= 5; i++) {
  setTimeout(function() {
    console.log('Value of i : ' + i);
  },100);
}

*Output:*

Value of i : 1
Value of i : 2
Value of i : 3
Value of i : 4
Value of i : 5
```
In a `let`, a new storage space is created for each iteration of the loop.
Each `i` refers to the binding of one specific iteration and preserves the value that was current at that time.
Therefore, each `setTimeout` function returns a different value.
