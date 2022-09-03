---
title: 红宝书第4章
author: 何青烨
date: 2022-7-18
---

## 第四章：变量、作用域和内存问题

### 基本类型和引用类型的值

#### 1.动态的属性

基本类型：Undefined/Null/Boolean/Number/String，按值访问，操作保存在变量中的实际的值。

引用类型：保存在内存中的对象。复制保存着对象的某个变量时，操作的是对象的引用；为对象添加属性时，操作的是实际对象。

- 引用类型的值可以添加/删除属性和方法，基本类型则不行。

```js
var person = new Object();
person.name = "anne";
person.add = function () {
  console.log(1);
};
console.log(person); // 属性name,方法add

var person1 = "Jone";
person1.name = "anne";
person1.add = function () {
  console.log(1);
};
console.log(person1); //Jone
```

#### 2.复制变量值

两张图（待补充）

```js
// 基本类型
var num1 = 5;
var num1 = num2;
// 引用类型
var obj1 = new Object();
var obj2 = obj1;
obj1.name = "Anne";
console.log(obj2.name); //Anne
```

#### 3.传递参数

参数传递都是按值传递。向参数传递基本类型的值，被传递的值会被复制给一个局部变量。向参数传递引用类型的值，复制内存中的地址给一个局部变量，而这个局部变量的变化会反映在函数外部。

```js
function setName(obj) {
  obj.name = "anne";
  obj = new Object();
  obj.name = "john";
}
var person = new Object();
setName(person);
console.log(person.name); //anne
```

#### 4.检测类型

```js
//typeof 检测哪一种基本类型
console.log(typeof null); //Object
console.log(typeof null === "object"); //true
console.log(typeof typeof null); //String
console.log(typeof typeof typeof null); //String
//instanceof 检测哪一种引用类型
var arr = [1, 2, 2];
console.log(arr instanceof Array); //true
```

### 执行环境及作用域

#### 1.延长作用域链

#### 2.没有块级作用域

### 垃圾收集

#### 1.标记清除

#### 2.引用计数

#### 3.性能问题

#### 4.管理内存
