---
title: JS Questions - Prototypes & Inheritance
date: "2021-08-23"
description: Prototypes & Inheritance
---

JS 的问题大部分来自 [前端自检清单](https://juejin.cn/post/6844903830887366670)，部分有改动。

## Table of Contents

- [Prototypes](#prototypes)
- [instanceof](#instanceof)
- [new User(...)](#new-user)
- [What are the pros and cons of extending built-in JavaScript objects?](#what-are-the-pros-and-cons-of-extending-built-in-javascript-objects)

---

### Prototypes

- In JavaScript, all objects have a hidden `[[prototype]]` property that's either another object or `null`.
- We can use `obj.__proto__` to access it (a historical getter/setter).
- By default all functions have `F.prototype = { constructor: F }`.
- All built-in objects follow the same pattern: 
    - The methods are stored in the prototype (`Array.prototype`, `Object.prototype`, `Date.prototype`, etc.)
    - The object itself stores only the data (array items, object properties, the date)

###### References

- [https://javascript.info/prototypes](https://javascript.info/prototypes)

⬆️ [Back to top](#table-of-contents)

---

### instanceof

The `instanceof` operator tests to see if the prototype property of a constructor appears anywhere in the prototype chain of an object.

    function myInstanceof(left, right) {
      if (typeof left !== 'object || left === null) {
        return false
      }
      let proto = Object.getPrototypeOf(left)
      while (true) {
        if (proto === null) {
          return false
        } 
        if (proto === right.prototype) {
          return true
        }
        proto = Object.getPrototypeOf(proto)
      }
    }

###### References

- [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/instanceof](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/instanceof)

⬆️ [Back to top](#table-of-contents)

---

### new User(...)

When a function is executed with new, it does the following steps:
1. A new empty object is created and assigned to this.
2. The function body executes. Usually it modifies this, adds new properties to it.
3. The value of this is returned.


<!-- -->
    function User(name) {
      // this = {};  (implicitly)

      // add properties to this
      this.name = name;
      this.isAdmin = false;

      // return this;  (implicitly)
    }

###### References

- [https://javascript.info/constructor-new](https://javascript.info/constructor-new)

⬆️ [Back to top](#table-of-contents)

---

### What are the pros and cons of extending built-in JavaScript objects?

以下内容来自《JavaScript 高级程序设计》

#### 原型链继承

    function SuperType() {
      this.colors = ['red', 'blue', 'green']
    }
    
    function SubType() {}

    // 继承 SuperType
    SubType.prototype = new SuperType()

    let instance1 = new SubType()
    instance1.colors.push('black')
    console.log(instance1.colors)  // 'red, blue, green, black'

    let instance2 = new SubType()
    console.log(instance2.colors)  // 'red, blue, green, black'

缺点：

- 原型中包含的引用值会在所有实例间共享
- 子类型在实例化时不能给父类型的构造函数传参

#### 盗用构造函数（经典继承）

    function SuperType() {
      this.colors = ['red', 'blue', 'green']
    }
    
    function SubType() {
      SuperType.call(this)
    }

    let instance1 = new SubType()
    instance1.colors.push('black')
    console.log(instance1.colors)  // 'red, blue, green, black'

    let instance2 = new SubType()
    console.log(instance2.colors)  // 'red, blue, green'
优点：

- 可以在子类构造函数中向父类构造函数传参

缺点：

- 必须在构造函数中定义方法，函数不能重用
- 子类无法访问父类原型上定义的方法

#### 组合继承

    function SuperType(name) {
      this.name = name
      this.colors = ['red', 'blue', 'green']
    }

    SuperType.prototype.sayName = function() {
      console.log(this.name)
    }

    function SubType(name, age) {
      // 继承属性
      SuperType.call(this.name)
      this.age = age
    }

    SubType.prototype = new SuperType()

    SubType.prototype.sayAge = function() {
      console.log(this.age)
    }

    let instance1 = new SubType('Nicholas', 29)
    instance1.colors.push('black')
    console.log(instance1.colors)  // 'red, blue, green, black'
    instance1.sayName()  // 'Nicholas'
    instance1.sayAge()  // 29

    let instance2 = new SubType('Greg', 27)
    console.log(instance2.colors)  // 'red, blue, green'
    instance2.sayName()  // 'Greg'
    instance2.sayAge()  // 27

优点：

- 使用原型链继承原型上的属性和方法
- 通过盗用构造函数继承实例属性

#### 原型式继承

    function object(o) {
      function F() {}
      F.prototype = o
      return new F()
    }

    let person = {
      name: 'Nicholas',
      frineds: ['Shelby', 'Court', 'Van']
    }
    
    let anotherPerson = object(person)
    anotherPerson.name = 'Greg'
    anotherPerson.friends.push('Rob')

    let yetAnotherPerson = object(person)
    yetAnotherPerson.name = 'Linda'
    yetAnotherPerson.friends.push('Barbie')

    console.log(person.friends)  // 'Shelby, Court, Van, Rob, Barbie'

优点：

- 适合不需要单独创建构造函数，但仍然需要在对象间共享信息的场合

缺点：

- 属性中包含的引用值始终会在相关对象间共享

#### 寄生式继承

    function createAnother(original) {
      let clone = object(original)
      clone.sayHi = function() {
        console.log('hi')
      }
    }
    return clone

    let person = {
      name: 'Nicholas',
      frineds: ['Shelby', 'Court', 'Van']
    }

    let anotherPerson = createAnother(person)
    anotherPerson.sayHi()  // 'hi'

优点：

- 适合主要关注对象，而不在乎类型和构造函数的情景

缺点：

- 通过寄生式继承给对象添加函数会导致函数难以重用

#### 寄生式组合继承

    function inheritPrototype(subType, superType) {
      let prototype = object(superType.prototype)  // 创建对象
      prototype.constructor = subType  // 增强对象
      subType,prototype = prototype  // 赋值对象
    }

    function SuperType(name) {
      this.name = name
      this.colors = ['red', 'blue', 'green']
    }

    SuperType.prototype.sayName = function() {
      console.log(this.name)
    }
    
    function SubType(name, age) {
      SuperType.call(this.name)
      this.age = age
    }

    inheritPrototype(SubType, SuperType)

    SubType.prototype.sayAge = function() {
      console.log(this.age)
    }

⬆️ [Back to top](#table-of-contents)