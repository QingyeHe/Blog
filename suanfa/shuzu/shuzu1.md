---
title: 数组常见用法
author: 何青烨
date: "2022-7-1"
---

<h2>1.在首部增加一个元素或删除一个元素</h2>
<h3>·原生</h3>

头部增加一个元素(往右移动)

```js
const addFirst = function (myArray, value) {
  for (let i = myArray.length; i >= 0; i--) {
    myArray[i] = myArray[i - 1];
  }
  myArray[0] = value;
};

let number = [1, 2, 3, 4, 5];
addFirst(number, 0);
console.log(number); //[0,1,2,3,4,5]
```

头部删除一个元素（往左移动）

```js
const deleteFirst = function (myArray) {
  for (let i = 0; i < myArray.length; i++) {
    myArray[i] = myArray[i + 1];
  }
  //myArray[myArray.length - 1] = value;
};
let number = [1, 2, 3, 4, 5];
deleteFirst(number);
console.log(number); //[2,3,4,5,undefined] 没有删除干净,也有解决方法
```

<h3>unshift与shift</h3>

```js
let number = [1, 2, 3, 4, 5];
number.unshift(23);
console.log(number); //[23,1,2,3,4,5] unshift改变了数组
```

```js
let number = [1, 2, 3, 4, 5];
number.shift();
console.log(number); //[2,3,4,5] shift改变了数组
```

<h3>splice</h3>

```js
let number = [1, 2, 3, 4, 5];
number.splice(0, 0, 88); //在索引为0的地方，不删除元素，添加88元素
console.log(number); //[88,1,2,3,4,5]
```

```js
let number = [1, 2, 3, 4, 5];
number.splice(0, 1); //在索引为0的地方，删除1个元素
console.log(number); //[2,3,4,5]
```

<h2>2.在尾部增加一个元素或删除一个元素</h2>
<h3>原生</h3>

```js
const addLast = function (myArray, value) {
  myArray[myArray.length] = value;
};
let number = [21, 22, 23, 24, 25];
addLast(number, 26);
console.log(number); //[21,22,23,24,25,26]
```

```js
const deleteLast = function (myArray) {
  const kong = [];
  for (let i = 0; i < myArray.length; i++) {
    myArray[myArray.length - 1] = undefined;
    if (myArray[i] !== undefined) {
      //kong.push(myArray[i]) push也可以用
      kong[kong.length] = myArray[i];
    }
  }
  console.log(kong); //[21,22,23,24]
};
let number = [21, 22, 23, 24, 25];
deleteLast(number);
```

<h3>push与pop</h3>

```js
let number = [21, 22, 23, 24, 25];
number.push(26);
console.log(number); //[21,22,23,24,25,26]
```

```js
let number = [21, 22, 23, 24, 25];
number.pop();
console.log(number); //[21,22,23,24]
```

<h3>splice</h3>

```js
let number = [21, 22, 23, 24, 25];
number.splice(number.length, 0, 26);
console.log(number); //[21,22,23,24,25,26]
```

```js
let number = [21, 22, 23, 24, 25];
number.splice(number.length - 1, 1); //记住splice第一位是索引号
console.log(number); //[21,22,23,24]
```

<h2>3.在中间的任意位置增加/删除元素</h2>

<h3>splice</h3>

```js
let number = [21, 22, 23, 24, 25];
number.splice(1, 0, 33, 34, 35); //记住splice第一位是索引号
console.log(number); //[21, 33, 34, 35, 22, 23, 24, 25]
```

```js
let number = [21, 22, 23, 24, 25];
number.splice(1, 2); //记住splice第一位是索引号
console.log(number); //[21,24, 25]
```

<h2>4.数组的使用场景</h2>

<h3>concat</h3>

```js
let number1 = [1, 2, 3];
let number2 = [4, 5, 6];
let number3 = [7, 8, 9];
const number = number1.concat(number2, number3);
console.log(number); //[1,2,3,4,5,6,7,8,9] concat没有改变数组
```

<h3>every/some</h3>

```js
const evenArray = function (x) {
  return x % 2 === 0;
};
let number = [12, 14, 15, 16];
number.every(evenArray);
console.log(number.every(evenArray)); //false，一直到false返回结果
console.log(number); //[12,14,15,16] every不改变数组
```

```js
const evenArray = function (x) {
  return x % 2 === 0;
};
let number = [12, 14, 15, 16];
number.every(evenArray);
console.log(number.some(evenArray)); //true，一直到true返回结果
console.log(number); //[12,14,15,16] some不改变数组
```

<h3>forEach</h3>

```js
const evenArray = function (x) {
  return x % 2 === 0;
};
let number = [12, 14, 15, 16];
let kong = [];
number.forEach((item) => kong.push(evenArray(item)));
console.log(kong); //[true,true,false,true]
```

<h3>map/filter(用法需要扩展)</h3>

```js
const evenArray = function (x) {
  return x % 2 === 0;
};
let number = [12, 14, 15, 16];
let kong = number.map(evenArray);
console.log(kong); //[true,true,false,true] 不改变数组
```

```js
const evenArray = function (x) {
  return x % 2 === 0;
};
let number = [12, 14, 15, 16];
let kong = number.filter(evenArray);
console.log(kong); //[12,14,16] 不改变数组
```

<h3>reduce（用法需要扩展）</h3>

```js
const evenArray = function (x) {
  return x % 2 === 0;
};
let number = [12, 14, 15, 16];
let kong = number.reduce(function (a, b, c, d) {
  return a + b;
});
console.log(kong); //[57] 不改变数组
```

<h2>5.二维数组</h2>

```js
const twoMatrix = function (myMatrix) {
  const kong = [];
  for (let i = 0; i < myMatrix.length; i++) {
    for (let j = 0; j < myMatrix[i].length; j++) {
      kong.push(myMatrix[i][j]);
    }
  }
  return kong;
};
let day = [];
day[0] = [1, 2, 3, 4, 5];
day[1] = [11, 22, 33, 44, 55];
console.table(twoMatrix(day)); //开发中常见二维数组
```

改变数组的方法：
push()
pop()
shift()
unshift()
splice()
sort()
reverse()
forEach()
不会改变数组的方法：
filter()
concat()
slice()
map()
