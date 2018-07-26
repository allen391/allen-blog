---
layout:     post
title:      JS data structure(ZH)
subtitle:   JS data structure(array)
date:       2018-07-26
author:     Allen
catalog: true
tags:
    - JS
    - Data Structure
    - Array
---

### 概念
栈是一种遵循后进先出（LIFO）原则的有序集合。新添加的或待删除的元素都保存在栈的末尾，称作栈顶，另一端就叫栈底。

在栈里，新元素都靠近栈顶，旧元素都接近栈底。

栈也被用在编程语言的编译器和内存中保存变量、方法调用等，比如函数的调用栈。

### 栈的实现

**创建一个类来表示栈**

```
// Stack类
function Stack () {
  this.items = [];

  this.push = push;
  this.pop = pop;
  this.peek = peek;
  this.isEmpty = isEmpty;
  this.clear = clear;
  this.size = size;
  this.print = print;
}
```

栈里面有一些声明的方法：

- push(element)：添加一个（或几个）新元素到栈顶
- pop()：移除栈顶的元素，同时返回被移除的元素
- peek()：返回栈顶的元素，不对栈做任何修改
- isEmpty()：如果栈里没有任何元素就返回true，否则返回false
- clear()：移除栈里的所有元素
- size()：返回栈里的元素个数

**实现栈的辅助方法** 

```
// 添加新元素到栈顶
function push (element) {
  this.items.push(element);
}

// 移除栈顶元素，同时返回被移除的元素
function pop () {
  return this.items.pop();
}

// 查看栈顶元素
function peek () {
  return this.items[this.items.length - 1];
}

// 判断是否为空栈
function isEmpty () {
  return this.items.length === 0;
}

// 清空栈
function clear () {
  this.items = [];
}

// 查询栈的长度
function size () {
  return this.items.length;
}

// 打印栈里的元素
function print () {
  console.log(this.items.toString());
}
```

**创建实例进行测试**

```
// 创建Stack实例
var stack = new Stack();

console.log(stack.isEmpty());     // true
stack.push(5);                    // undefined
stack.push(8);                    // undefined
console.log(stack.peek());        // 8
stack.push(11);                   // undefined
console.log(stack.size());        // 3
console.log(stack.isEmpty());     // false
stack.push(15);                   // undefined
stack.pop();                      // 15
console.log(stack.size());        // 3
stack.print();                    // 5,8,11
stack.clear();                    // undefined
console.log(stack.size());        // 0
三、结束
```














