---
layout:     post
title:      ES7 new feature
subtitle:   ES7 new feature 
date:       2018-06-19
author:     Allen
catalog: true
tags:
    - ES7
---

## Array.prototype.includes
如果传入的数组在数组（this）中返回true， 否则返回false：
```
['a', 'b', 'c'].includes('a')//true
['a', 'b', 'c'].includes('d')//false
```
includes和indexof方法很相似，唯一的区别是includes()能找到NAN， 而indexOf()不行

## 指数运算符
x**y
```
let num = 3;
num **=2;
console.log(num);//
```

## 异步函数(Brain Terlson)
promise现在越来越流行， 一个例子就是客户端fetch API， 它是替代XML HttpRequest检索文件的方案。
```
function fetchJson(url) {
  return fetch(url)
    .then(request => request.text())
    .then(text => {
      return JSON.parse(text);
    })
    .catch(error => {
      console.log(`ERROR: ${error.stack}`)
    });
}

fetchJson('----url-----').then(obj => console.log(obj));
```

co使用了Promises和generators让编程风格看起来更像异步的库。
```
const fetchJson = co(function(){
  try {
    let request = yield fetch(url);
    let text = yield request.text();
    return JSON.parse(text);
  }
  catch(error){
    console.log(`ERROR: ${error.stack}`);
  }
});
```
es7异步函数语法async基本说是实现了co所做的
```
async function fetchJson(url){
  try{
    let request = await fetch(url);
    let text = await request.text();
    return JSON.parse(text)
  }
  catch(error){
    console.log(`ERROR: ${error.stack}`);
  }
}
```

## 异步函数变体
- 函数声明： 
```
async function foo()
```
- 函数表达式
```
const foo = async function(){}
```
- 箭头函数
```
const foo = async() => {}
```
- 方法定义
```
let obj = {async foo(){}}
```