---
layout:     post
title:      JS Foundation 
subtitle:   JS Foundation 
date:       2018-07-11
author:     Allen
catalog: true
tags:
    - JS
    - this
    - prototype
---

### this scope

函数 foo 在全局调用， 在浏览器下 this 指向 window，当然要是考虑严格模式， this.a 会报错 a is not defined

```
a = 1;
function foo() {
  console.log(this.a); // 1
}
foo();
```
被不同的对象调用，this 分别指向它的调用者

```
function foo() {
  console.log(this.a);
}
var obj1 = {
  foo: foo,
  a: 1
}

var obj2 = {
  foo: foo,
  a: 2
}
obj1.foo() // 1
obj2.foo() // 2
```

下面虽然函数 foo 声明在全局，但被利用 call、apply、bind 显式的绑定了对象，this 指向显式绑定的对象

```
function foo() {
  console.log(this.a);
}
var obj1 = {
  a: 1
}
var obj2 = {
  a: 2
}
var obj3 = {
  a: 3
}
foo.call(obj1) // 1
foo.apply(obj2) // 2
foo.bind(obj3)() // 3

```

使用new来调用，this指向了该对象

使用new调用函数有4个步骤

1. 创建构造一个全新的对象
2. 这个新对象会被prototype连接
3. 这个新对象会被绑定到函数调用this
4. 如果这个函数没有返回其他对象，那么new表达式中的函数调用会自动返回这个新对象

总结

- 看调用者，函数被谁调用，this指向谁
- 是否被new创建， 是的话this指向new出来的对象
- 是否有`call`, `apply`, `bind`改了this指向

### 原型
js对象有个特殊的[prototype]属性， 所有的对象在创建时`prototype`属性都被赋予一个非空的值

**Proptype**

```
var anotherObj = { a: 1}
var obj = Object.create(anotherObj)
console.log(obj.a);  // 1
```

`Object.create()`会把一个对象的prototype关联到另外一个对象上， 上面的obj的`prototype`被关联到了对象`anotherobj`上了， 当访问对象`obj`的属性a时，如果对象`obj`上没有该属性那么`prototype`链就会被遍历，直到找到后才返回，`prototype`链最终会指向js内置的`object.prototype`上

 **类函数**

```
function Foo() {
  // ...
}
var a = new Foo()

```

上面例子中的`Foo`是个类函数，也可以叫做构造函数。Foo 其实也只是一个函数， 没有 new 操作符， Foo() 也能正常执行，只是当且仅当使用 new 时，函数调用会变成 ‘构造函数调用’。

**原型链**

```
function Foo() {
  // ...
}
Foo.prototype // {}
```

所有的函数都会有一个`prototype`的属性且不可被枚举，`prototype`为函数的原型

```
function Foo() {
  // ...
}
var a = new Foo()
a.__proto__ // {}
```

所有的对象默认有一个名为`__proto__`的属性， `prototype`和`__proto__`联系是：

`a.__proto__ == Foo.prototype`

每个对象的`__proto__`属性指向函数的原型，因为每个对象都有`__proto__`属性指向函数的`prototype`添加属性和方法，每个对象都能访问到

```
function Foo() {
  // ...
}
Foo.prototype.age = 233
var a = new Foo()
var b = new Foo()
a.age // 233
b.age // 233
```
**对象关联**

如果在第一个对象上没有找到需要的属性或者方法引用，JavaScript引擎会继续在 [Prototype] 关联的对象上进行查找。同理，如果在后者中也没有找到需要的引用就会继续查找它的 [Prototype] ，以此类推。这一系列对象的链接被称为 ‘原型链’ 。

原型链的本质就是对象之间的关联关系，对象关联

```
var Obj1 = {
  name: '曾田生',
  setID: function(ID) {
    console.log(ID)
  }
}

var Obj2 = Object.create(Obj1)

Obj2.age = 233

var Obj3 = Object.create(Obj2)

console.log(Obj3.age)  // 233
console.log(Obj3.name) // 曾田生
Obj3.setID('ABCD')     // ABCD
console.log(Obj3)

```

使用`Object.create`讲一个个对象关联起来，当访问到自身没有对象的方法或者属性时，就会去他关联的对象查找，这个就是`protoype`的机制

--- 
### 总结

1. 在js里面，万物皆对象，方法也是对象，方法的原型`function.prototype`也是对象。所以他们都有对象共同的特点。可称为隐式原型，一个对象的隐式原型指向构造该对象的构造函数的原型，这也保证了实例能够访问在构造函数原型中定义的属性和方法。
2. 方法这个特殊的对象，除了和其他对象一样有`__proto__`属性之外，还有自己的属性，原型属性`prototype`，这个属性是一个指针，指向一个对象。这个对象的用途就是就是包涵所有实例共有的属性和方法。
3. 简单来说对象有属性`__proto__`，指向该对象的构造函数的原型对象,方法除了有属性`__proto__`，还有属性`prototype`,指向该方法的原型对象。

