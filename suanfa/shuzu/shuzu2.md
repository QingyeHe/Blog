---
title: 数组ES6
author: 何青烨
date: "2022-7-4"
lang: zh-CN
---

<h2>1.for...of</h2>

```js
let numbers1 = [1, 2, 3, 4, 5, 6];
for (const n of numbers1) {
  console.log(n % 2 === 0 ? "even" : "odd");
} //直接输出[odd,even,odd,even,odd,even]
```

<h2>2.@@iterator</h2>

```js
// @@iterator没有改变数组
let numbers2 = [1, 2, 3, 4, 5, 6];
let iterator = numbers2[Symbol.iterator]();
console.log(iterator.next().value); //1
console.log(iterator.next().value); //2
```

<h2>3.entries/keys/values</h2>
当前的浏览器还没有完全支持ES2015的新功能。
测试这些代码最好的办法是使用Babel。
http://t.cn/EGE4fTB查看和运行示例

三者区别，entries 取出键值对，keys 取出索引值+布尔值（找不到为 true），values 取出数组值+布尔值（找不到为 true）。

```js
// 1.entries，entries改变了数组
let numbers3 = [2, 4];
let entries = numbers3.entries();
console.log(entries.next().value); //[0,2]
// console.log(entriesa.next().value);//[1,4]
// console.log(entriesa.next().value);//undefined
for (const n of entries) {
  console.log(n);
} //[1,4]

//2.keys:索引值+false/true,找不到的时候done为true
let numbers4 = [1, 3];
let akeys = numbers4.keys();
console.log(akeys.next()); //{value: 0, done: false}
console.log(akeys.next()); //{value: 1, done: false}
console.log(akeys.next()); //{value: undefined, done: true}

//3.values:数组值+false/true
let numbers5 = [1, 3, 5];
let avalues = numbers5.values();
console.log(avalues.next()); //{value: 1, done: false}
console.log(avalues.next()); //{value: 3, done: false}
console.log(avalues.next()); //{value: 5, done: false}
console.log(avalues.next()); //{value: undefined, done: true}
```

<h2>4.Array.from/Array.of</h2>
异同点：Array.from(numbers6) 与 Array.of(...numbers6)结果相同

:boom: 区别待找

```js
// Array.from ,可以传入过滤的函数。
let numbers6 = [11, 22, 33];
//let numberFrom = Array.from(numbers6)
let numberFrom = Array.of(...numbers6);
console.log(numberFrom); //[11,22,33]
let numberFrom1 = Array.from(numbers6, (x) => x % 3 === 0);
console.log(numberFrom1); //[false,false,true]
```

<h2>5.fill</h2>

```js
// fill静态值填充数组，改变了数组
// （静态值，索引开始的位置（含），索引结束的置（不含）
let numbers7 = Array.of(1, 2, 3, 4, 5, 6);
//numbers7.fill(0)
//console.log(numbers7); [0,0,0,0,0,0]
numbers7.fill(0, 1, 3);
console.log(numbers7); //[1,0,0,4,5,6] 包括1和2，不包括3!!
```

<h2>6.copyWithin</h2>

```js
//copyWithin指的是复制一段到指定位置 （放置的位置,起始索引值（含）,末尾索引值（不含））
let numbers8 = [23, 24, 25, 26];
numbers8.copyWithin(2, 0, 2);
console.log(numbers8); //[23,24,23,24]
```

<h2>7.includes</h2>
涉及搜索，将在下一篇中提及。
<h2>8.find</h2>
涉及搜索，将在下一篇中提及。
<h2>9.findIndex</h2>
涉及搜索，将在下一篇中提及。
