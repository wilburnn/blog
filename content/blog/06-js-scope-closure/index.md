---
title: JS Questions - Scope & Closure
date: "2021-08-24"
description: "Scope & Closure"
---

JS 的问题大部分来自 [前端自检清单](https://juejin.cn/post/6844903830887366670)，部分有改动。

## Table of Contents

- [Execution Context and Call Stack](#execution-context-and-call-stack)
- [Lexical Environment](#lexical-environment)
- [Closure](#closure)
- [Block, Block scope](#block-block-scope)
- [Hoisting](#hoisting)
- [Temporal dead zone](#temporal-dead-zone)
- [this](#this)

---

### Execution Context and Call Stack

- JavaScript is a synchronous and single-threaded language.
- Everything in JavaScript happens inside an Execution context.
- Execution context inside that there are two things.
    - Memory component (creation phrase), variable and functions can be stored in a key value format, also called **variable environment**.
    - Code component (execution phrase), a place where whole JavaScript code is executed, also called **thread of execution**.
- Whenever a function is invoked in JavaScript, a functional Execution Context is created and memory is allocated. 
- Once the memory is allocated to the variables and functions, then the code is executed synchronously, one line at a time.

```js
var x = 1
a()
b()
console.log(x)

function a() {
  var x = 10
  console.log(x)
}

function b() {
  var x = 100
  console.log(x)
}
```

###### References

⬆️ [Back to top](#table-of-contents)

---

### Lexical Environment

- In JavaScript, every running function, code block `{...}`, and the script as a whole have an internal (hidden) associated object known as the Lexical Environment.
- The Lexical Environment object consists of two parts:
    1. Environment Record – an object that stores all local variables as its properties (and some other information like the value of this).
    2. A reference to the outer lexical environment, the one associated with the outer code.

#### The difference between execution context and lexical environment

- The key about the Lexical Environment is it has a link to any outer Environment(i.e. its scope chain), so it is used to resolve identifiers outside the current Execution Context.
- A corresponding Lexical Environment is created for every Execution Context.
- The Lexical Environment cares about where the code sits physically(lexically) in your application

```js
var value = 1;

function foo() {
  console.log(value)
}

function bar() {
  var value = 2
  foo()
}

bar()
```

###### References

- [https://javascript.info/closure#lexical-environment](https://javascript.info/closure#lexical-environment)
- [https://stackoverflow.com/questions/35759544/what-is-the-difference-and-relationship-between-execution-context-and-lexical-en](https://stackoverflow.com/questions/35759544/what-is-the-difference-and-relationship-between-execution-context-and-lexical-en)

⬆️ [Back to top](#table-of-contents)

---

### Closure

- A closure is a function that remembers its outer variables and can access them.
- A closure is a function with its lexical environment. Whenever a function is returned, even if its vanished in execution context, but it still remembers the reference it was pointing to.
- Uses of closures: 
    - Module design pattern
    - Currying
    - Functions like once
    - Maintaing state in async world
    - SetTimeout
    - Iterators

```js
function z() {
  var a = 900
  function x() {
    var a = 7
    function y() {
      console.log(a, b)
    }
    y()
  }
  x()
}

z()
```

#### setTimeout

```js
function x() {
  for (var i = 1; i <= 5; i++) {
    setTimeout(function () {
      console.log(i)
    }, i * 1000)
  }
  console.log('Namaste JavaScript')
}
x()

function x() {
  for (var i = 1; i <= 5; i++) {
    function close(x) {
      setTimeout(function () {
        console.log(x)
      }, x * 1000)
    }
    close(i)
  }
  console.log('Namaste JavaScript')
}
x()
```

#### Data privacy

```js
function counter() {
  var count = 0
  return function incrementCounter() {
    count++
    console.log(count)
  }
}

var counter1 = counter()
counter1()
```

#### Smart garbage collection by V8 JS engine

```js
function a() {
  var x = 0, z = 10
  return function b() {
    console.log(x)
  }
}

var y = a()
y()
```

###### References

- [https://javascript.info/closure#step-4-returning-a-function](https://javascript.info/closure#step-4-returning-a-function)

⬆️ [Back to top](#table-of-contents)

---

### Block, Block scope

- Block is defined in curly braces.
    - We group multiple statements together in a block so that  we can use it where JavaScript expects one statement.
- Block scope means what all variables and functions we can access inside the block.
- Script scope, Block scope, Global scope are different things(in chrome).
- var variables have no block scope, their visibility is scoped to current function, or global, if declared outside function. 

```js
var a = 100

{
  var a = 10
  let b = 20
  const c = 30
  console.log(a)
  console.log(b)
  console.log(c)
}

console.log(a)
console.log(b)
console.log(c)
```

⬆️ [Back to top](#table-of-contents)

---

### Hoisting

- JavaScript Hoisting refers to the process whereby the compiler allocates memory for variable and function declarations prior to execution of code.
- Variable declarations are scanned and are made undefined.
- Function declarations are scanned and are made avaliable.

```js
var a = 2

function a() {
  console.log(3)
}

console.log(typeof a)
```

###### References

- [https://developer.mozilla.org/en-US/docs/Glossary/Hoisting](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting)

⬆️ [Back to top](#table-of-contents)

---

### Temporal dead zone

- let and const are hoisted. We can not use them before initialization is result of "temporal dead zone".
- JS **use different memory than Global scope(indeed as an object, allocated in memory)** to store let and const, which is reason between "temporal dead zone".

⬆️ [Back to top](#table-of-contents)

---

### this

this is the context of a function invocation.

- Function invocation
    - this is the global object in a function invocation.
    - this is undefined in a function invocation in strict mode.
- Method invocation
    - this is the object that owns the method in a method invocation.
- Constructor invocation(new)
    - this is the newly created object in a constructor invocation.
- Indirect invocation(`.call()` or `.apply()` method)
    - this is the first argument of `.call()` or `.apply()` in an indirect invocation.
    - the indirect invocation is useful when a function should be executed with a specific context.
    - call() accepts an argument list, apply() accepts a single array of arguments. 
- Bound function
    - this is the first argument of .bind() when invoking a bound function.
- Arrow function
    - this is the enclosing context where the arrow function is defined

###### References

- [https://dmitripavlutin.com/gentle-explanation-of-this-in-javascript/](https://dmitripavlutin.com/gentle-explanation-of-this-in-javascript/)

⬆️ [Back to top](#table-of-contents)
