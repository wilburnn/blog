---
title: JS Questions - Variable & Type
date: "2021-06-03"
description: "JS Questions - Variable & Type"
---

JS 的问题大部分来自 [前端自检清单](https://juejin.cn/post/6844903830887366670)，部分有改动。

## Table of Contents

- [Data types](#data-types)
- [Type judgment](#type-judgment)
- [Object to primitive conversion](#object-to-primitive-conversion)
- [Pass by reference or pass by value?](#pass-by-reference-or-pass-by-value)
- [What is the difference between null and undefined?](#what-is-the-difference-between-null-and-undefined)
- [What is the difference between == and ===?]()

---

### Data types

- Primitive values:
    - Boolean
    - Null
    - Undefined
    - Number
    - String
    - BigInt
    - Symbol
- Objects

###### References

- [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures)

⬆️ [Back to top](#table-of-contents)

---

### Type judgment

① typeof

The typeof operator returns a string indicating the type of the unevaluated operand.

    console.log(typeof 42);  // 'number'
    console.log(typeof null);  // 'object'

② instanceof

- The instanceof operator tests to see if the prototype property of a constructor appears anywhere in the prototype chain of an object. The return value is a boolean value.
- Exclude primitive

③ Object.prototype.toString()

The toString() method returns a string representing the object.

###### References

- [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof)
- [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/instanceof](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/instanceof)
- [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/toString](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/toString)

⬆️ [Back to top](#table-of-contents)

---

### Object to primitive conversion

To do the conversion, JavaScript tries to find and call three object methods:

1. Call `obj[Symbol.toPrimitive](hint)` - the method with the symbolic key `Symbol.toPrimitive`(system symbol), if such method exists.
2. Otherwise if hint is `'string'`
    - try `obj.toString()` and `obj.valueOf()`, whatever exists.
3. Otherwise if hint is `'number'` or `'default'`
    - try `obj.valueOf()` and `obj.toString()`, whatever exists.

<!-- -->
    let user = {
      name: 'John',
      money: 1000,
      
      // for hint = 'string'
      toString() {
        return `{name: '${this.name}'}`;
      },

      // for hint = 'number' or 'default'
      valueOf() {
        return this.money;
      }
    };
    alert(user);  // toString => {name: 'John'}
    alert(+user);  // valueOf => 1000
    alert(user + 500);  // valueOf => 1500

###### References

- [https://javascript.info/object-toprimitive#toprimitive](https://javascript.info/object-toprimitive#toprimitive)
  
⬆️ [Back to top](#table-of-contents)

---

### Pass by reference or pass by value?

Changing the value of a variable never changes the underlying primitive or object. However, changing a property of an object referenced by a variable does change the underlying object.

    function setName(obj) {
      obj.name = 'Nicholas';    
    }
    var person = new Object();  // person(a variable) refers to an object
    setName(person);  // obj(parameter) and person(argument) refer to same object
    console.log(person.name);  // 'Nicholas'

###### References

- [https://stackoverflow.com/questions/6605640/javascript-by-reference-vs-by-value](https://stackoverflow.com/questions/6605640/javascript-by-reference-vs-by-value)

⬆️ [Back to top](#table-of-contents)

---

### What is the difference between null and undefined?

`undefined` means a variable has been declared but has not yet been assigned a value, such as:

    var testVar;
    alert(testVar);  // shows undefined
    alert(typeof testVar);  // shows undefined

`null` is an assignment value. It can be assigned to a variable as a representation of no value:

    null === undefined;  // false
    null == undefined;  // true
    null === null;  // true

###### References

- [https://stackoverflow.com/questions/5076944/what-is-the-difference-between-null-and-undefined-in-javascript](https://stackoverflow.com/questions/5076944/what-is-the-difference-between-null-and-undefined-in-javascript)

⬆️ [Back to top](#table-of-contents)

---

### What is the difference between == and ===?

If the operands are of different types, the `==` operator attempts to convert them to the same type before comparing.

###### References

- [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Strict_equality](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Strict_equality)

⬆️ [Back to top](#table-of-contents)