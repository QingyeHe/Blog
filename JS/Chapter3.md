---
title: 红宝书第3章
author: 何青烨
date: 2022-7-14
---

## 第三章：基本概念（语法、数据类型、流控制语句、函数）续

### 操作符

#### 1.一元操作符

- #### 递加递减操作符
  前置和后置的区别在于包含操作符的语句被求值**之前或之后**。

```js
var num1 = 2;
var num2 = 20;
console.log(--num1 + num2); //21
console.log(num1 + num2); //21

var num3 = 4;
var num4 = 20;
console.log(num3++ + num4); //24
console.log(num3 + num4); //25

var num5 = "a"; //字符串
var num6 = false; //布尔值
var num7 = 2.3; //浮点数
var num8 = {
  //对象,先valueOf方法，如果NaN再toString
  valueOf: function () {
    return -1;
  },
};

console.log(++num5); //NaN
console.log(++num6); //1
console.log(++num7); //3.3
console.log(++num8); //0
```

- #### 一元加/减操作符（略）

#### 2.位操作符

```js
//按位非（操作数的负值-1）
var num1 = 25;
var num2 = -26;
console.log(~num1); //-26
console.log(~num2); //25
//按位与以及按位或，按二进制码进行运算
console.log(25 && 3); //1  原因:11001和00011,结果是00001
console.log(25 || 3); //27 原因:11001和00011,结果是11011
//异或
console.log(25 ^ 3); //26 原因:11001和00011,结果是11010
// 左移
var num3 = 2;
console.log(num3 << 3); //16 原因:10000和00010
// 有符号的右移
var num4 = 64;
console.log(num4 >> 3); //8 原因:1000000和0001000
// 无符号的右移（遇到负数会爆炸）
var num5 = -64; // 当做负数的二进制处理
console.log(num5 >>> 5); //134217726
```

#### 3.布尔操作符

- #### 逻辑非

<div class="center">

| true                         | false                    |
| ---------------------------- | ------------------------ |
| ''（空字符串）               | 非空字符串               |
| 0                            | 非 0 数值（含 Infinity） |
| 任何非零数字值（包括无穷大） | 0 和 NaN                 |
| null/NaN/undefined           | 对象                     |

</div>

同时使用两个逻辑非`!!`等同于应用`Boolean()`转型函数。

- #### 逻辑与
  短路操作符（如果第一个操作数能够决定结果，那么就不会对第二个操作数求值）

<div class="center">

| 第一个操作符       | 第二个操作符 | 结果               |
| ------------------ | ------------ | ------------------ |
| 对象               | any          | 返回第二个操作符   |
| true               | 对象         | 返回第二个操作符   |
| 对象               | 对象         | 返回第二个操作符   |
| null/NaN/undefined | any          | null/NaN/undefined |

</div>

- #### 逻辑或

<div class="center">

| 第一个操作符       | 第二个操作符       | 结果               |
| ------------------ | ------------------ | ------------------ |
| 对象               | any                | 返回第一个操作符   |
| false              | 对象               | 返回第二个操作符   |
| 对象               | 对象               | 返回第一个操作符   |
| null/NaN/undefined | null/NaN/undefined | null/NaN/undefined |

</div>
逻辑或可以避免为变量赋null或undefined值.

```js
var num = num1 || num2;
//num1中包含优先赋给num的值，num2负责在num1不包含有效值的情况下提供后备值。
```

#### 4.乘性操作符

<div class="center">

| 乘法                                       | 除法                                      | 取模                        |
| ------------------------------------------ | ----------------------------------------- | --------------------------- |
| NaN \* any = NaN                           | 被除数与除数中有 NaN 结果为 NaN           | 无穷大 % 有限大的数值 = NaN |
| Infinity \* 0 = NaN                        | 0/0 = NaN                                 | 有限大 % 0 = NaN            |
| Infinity \* 非 0 数值 = Infinity/-Infinity | 非 0 数值 / Infinity = Infinity/-Infinity | 0 % any = 0                 |
| Infinity \* Infinity = Infinity            | Infinity / Infinity = NaN                 | 有限大 % 无穷大 = 有限大    |

</div>

#### 5.加性操作符

加法：只有一个操作数为字符串，则另一个操作数转换为字符串。

```js
var num1 = 5;
var num2 = 10;
console.log("the sum is" + num1 + num2); //510 先第一个加号，再第二个加号
console.log("the sum is" + (num1 + num2)); //15 先括号里面计算再外面的加号
console.log(5 + "5"); //55
```

减法：一个操作数为字符串，则后台调用 Number()转换为数值。

```js
console.log(5 - true); //4
console.log(NaN - 1); //NaN
console.log(5 - ""); //5
console.log(5 - "2"); //3
console.log(5 - null); //5
```

#### 6.关系操作符

其中一个为数值，则转换另一个为数值进行比较。</br>
两个操作数为字符串，则比较对应的字符编码值。

```js
console.log("Brick" < "alpha"); //true，大写字母的字符编码全部小于小写字母的字符编码。
console.log("Brick".toLowerCase() < "alpha".toLowerCase()); //false 转换为小写再比较
console.log("23" < "3"); //true,两个都是字符串，且字符编码2比3小
console.log("23" < 3); //false,转换为数值，23>3
console.log("A" > 5); //false,NaN与任何数比较都为false
console.log("A" <= 5); //false,NaN与任何数比较都为false
```

#### 7.相等操作符

- #### 相等和不相等(先转换再比较)

<div class="center">

| 第一个操作符 | 第二个操作符 | 结果                         |
| ------------ | ------------ | ---------------------------- |
| 布尔值       | any          | false 转换为 0,true 转换为 1 |
| 字符串       | 数值         | 将字符串转为数值             |
| 对象         | 非对象       | 调用对象的 valueOf 方法      |
| null         | undefined    | 相等（==）                   |

</div>
特殊情况举例(在比较相等性之前，undefined和null无法转为其他任何值)

<div class="center">

| 表达式          | 值    | 表达式         | 值    |
| --------------- | ----- | -------------- | ----- |
| null==undefined | true  | true == 1      | true  |
| 'NaN' == NaN    | false | undefined == 0 | false |
| 5 == NaN        | false | null == 0      | false |
| NaN != NaN      | true  | '5' == 5       | true  |

</div>

- #### 全等和不全等(仅比较不转换)

<div class="center">

| 表达式             | 值        |
| ------------------ | --------- |
| '55' != 55         | false     |
| '55' !== 55        | true      |
| '55' == 55         | true      |
| '55' === 55        | false     |
| null == undefined  | true      |
| null === undefined | **false** |

</div>

#### 8.条件操作符

三元表达式(略)

#### 9.赋值操作符

`*=` `/=` `%=` `+=` `-=` `<<=` `>>=` </br>
`num = num * 10` `num*=10`

#### 10.逗号操作符

一条语句执行多个操作:var num = 10,name = 'ane',age = 12 </br>
用于赋值（返回表达式最后一项）:var num = (2,3,4,5,6) //num 返回 6

### 语句

#### 1.if 语句

`if(condition) statement1 else statement2`
ECMAScript 会自动调用 Boolean()转换函数转换 condition

#### 2.do-while 语句(后测试循环语句)

```js
var i = 0;
do {
  i++;
} while (i < 10);
console.log(i); //10,循环体中的代码至少要被执行一次
```

#### 3.while 语句和 4.for 语句(前测试循环语句)

while 在循环体内的代码被执行之前，就会对出口条件求值。因此，循环体内的代码有可能永远不会被执行。

```js
var count = 10;
for (var i = 0; i < count; i++) {
  console.log(i); //0-9
}
console.log(i); //10

var count1 = 10;
var i1 = 0;
while (i1 < count1) {
  console.log(i1); //0-9
  i1++;
}
```

#### 5.for-in 语句

用于枚举对象的属性

```js
var result = {
  name: "anne",
  age: 23,
  address: "LRT",
};
for (var prop in result) {
  console.log(prop); //name,age,address
}
```

#### 6.label 语句

代码中添加标签,通常与 break 和 continue 一起使用。

```js
imlabel: for (var i = 0; i < 10; i++) {}
```

#### 7.break 和 continue 语句

break-退出所有循环；continue-退出循环,从顶部开始。

```js
var num = 0;
outermost: for (var i = 0; i < 10; i++) {
  for (var j = 0; j < 10; j++) {
    if (i == 5 && j == 5) {
      break outermost;
    }
    num++;
  }
}
console.log(num); //55

var num = 0;
outermost: for (var i = 0; i < 10; i++) {
  for (var j = 0; j < 10; j++) {
    if (i == 5 && j == 5) {
      continue outermost;
    } //从i=6开始
    num++;
  }
}
console.log(num); //95
```

#### 8.with 语句

大量使用导致性能下降，大型开发不推荐。

#### 9.switch 语句

```js
switch (i) {
  case 15:
    console.log(1);
    break;
  case 25:
    console.log(2);
    break;
  case 35:
    console.log(3);
    break;
  case 45:
    console.log(4);
    break;
}
```

### 函数

```js
function say(a, b) {
  return a + b;
  alert("hello"); //永远不会被执行
}
function say(a, b) {
  return; //停止执行后返回undefined
  alert("hello"); //永远不会被执行
}
```

#### 1.理解参数

ECMAScript 的参数在内部是以数组表示的，通过 arguments 可以访问到这个数组。arguments 对象可以与命名参数一起使用，并且与对应命名参数的值保持同步。

```js
function doAdd(num1, num2) {
  arguments[1] = 10;
  alert(arguments[0] + num2); //这里num2一直为10
}
doAdd(1); //只传入一个参数，则arguments[1]为undefined
```

#### 2.没有重载

重载:可以为一个函数编写两个定义，只要这两个定义的签名（接受的参数的类型和数量）不同即可。

而 ECMAScript 中没有签名，定义相同函数时，以最后的函数为准。

```js
function addone(num1) {
  return num1 + 100;
}
function addone(num1) {
  return num1 + 200;
}
addone(50); //250
```
