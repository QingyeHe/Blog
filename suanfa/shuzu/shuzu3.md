---
title: 数组搜索
author: 何青烨
date: "2022-7-4"
lang: zh-CN
---

<h2>indexOf/lastIndexof</h2>
区别：前者返回的是匹配的第一个索引值，后者则是最后一个索引值

```js
let numbers = [1, 2, 3, 4, 5, 6, 7, 2, 2, 3, 2];
console.log(numbers.indexOf(2)); //1 匹配的第一个索引值
console.log(numbers.lastIndexOf(2)); //10 匹配的最后一个索引值
```

<h2>find/findIndex(ES6)</h2>
相同：都是接收回调函数,
区别：前者返回第一个数组值，后者返回第一个索引值

```js
const multi = function (x) {
  return x % 13 === 0;
};
let numbers1 = [12, 13, 14, 26, 19];
console.log(numbers1.find(multi)); //13 没有符合条件的值则返回undefined
console.log(numbers1.findIndex(multi)); //1 没有符合条件的值则返回-1
```

<h2>includes(ES7)</h2>
两个参数，第一个是要搜索的值，第二个是搜索开始的索引值（含）

```js
let numbers2 = [1, 2, 3, 2, 3, 4, 5];
console.log(numbers2.includes(2)); //返回true
console.log(numbers2.includes(3, 4)); //true
console.log(numbers2.includes(3, 5)); //false
```

<h2>数组转换为字符串</h2>

```js
let numbers3 = [22, 32, 31, 34, 45]; //join和toString不改变数组
console.log(numbers3.toString()); //22,32,31,34,45
console.log(numbers3.join("-")); //22-32-31-34-45
console.log(typeof numbers3); //object
console.log(typeof numbers3.toString()); //string
```

延申，
数据类型间的转换方式，
判定数据类型的方法，
https://www.jb51.net/article/102972.html
模糊搜索的实现方式
