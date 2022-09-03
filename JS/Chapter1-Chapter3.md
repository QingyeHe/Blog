---
title: 红宝书第1-3章
author: 何青烨
date: 2022-7-5
---

> 今天看了 JS 第三版 Page1-Page30

<h2>第一章：一个完整的 JavaScript</h2>

<div class="center">

| J          | &   | S   |
| ---------- | --- | --- |
| ECMAScript | DOM | BOM |

</div></br>

### 1.ECMAScript 与浏览器无依靠关系，浏览器是其宿主环境之一（eg.Nodejs）.规定了语法、类型、语句、关键字、保留字、操作符、对象。

::: details 点击查看 ECMAScript 不同版本（待补充）

```js
console.log("你好，VuePress！");
```

:::

### 2.DOM 是针对 XML 但经过扩展用于 HTML 的 API，用于控制页面内容和结构。

::: details 点击查看 XML 和 HTML 不同版本（待补充）
XS
:::

### 3.BOM 支持可以访问和操作浏览器窗口的浏览器对象模型，还扩展了功能。

::: details 点击查看扩展功能

- 弹出新浏览器窗口的功能
- 移动缩放和关闭浏览器窗口
- 提供浏览器详细信息的 navigator 对象
- 提供浏览器所加载页面的详细信息的 location 对象
- 提供用户显示器分辨率详细信息的 screen 对象
- 对 cookies 的支持
- XMLHttpRequest 和 IE 的 ActiveXObject 等自定义对象
  :::

<h2>第二章：HTML中使用JS</h2></br>
有两个页面引入同一个外部JS文件，则只下载一次，节省缓存。</br>
标签如果放在头部，则等到全部JS代码都被下载解析和执行之后才开始呈现页面内容。（除defer和async）

::: warning

<script\> 和 <img\>中的 src 都可以跨域

:::

<div class="center">

| 延迟脚本 defer | 与                     | 异步脚本 async               |
| -------------- | ---------------------- | ---------------------------- |
| 相同点         | 只适用于外部脚本       | 浏览器立即下载脚本但并不执行 |
| 不同点         | defer 按指定的顺序执行 | async 并不保证按先后顺序执行 |

</div>

<h2>第三章：基本概念（语法、数据类型、流控制语句、函数）</h2>

### 严格模式

对 ECMAScript 3 中的不确定行为进行处理，对不安全的操作抛出错误。

```js
//头部引入
"use strict";
```

### 关键字和保留字（ES5 和 ES6）

<div class="center">

| ×      | ES5                                                                                                                                                                                                             | ES6                                                                                   |
| ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| 关键字 | `break` `do` `instanceof` `typeof` `case` `else` `new` `var` `catch` `finally` `return` `void` `continue` `for` `switch` `while` `debugger` `function` `this` `with` `default` `if` `throw` `delete` `in` `try` | **新增** </nbsp> `export` `class` `extends` `const` `super` `yield` `import`          |
| 保留字 | `class` `enum` `extends` `super` `const` `export` `import` `implements` `package` `public` `interface` `private` `static` `let` `protected` `yield`                                                             | `enum` `implements` `package` `public` `interface` `static` `let` `protected` `await` |

</div>

### 变量 var（ES5） 及 const/let（ES6） :boom:

```js
var message; //undefined
var me = "hello";
me = 100; //100 修改变量值的同时改变数据类型

function test() {
  var ms = 1;
}
test();
alert(ms); //undefined var是局部变量

function test() {
  ms = 1;
}
test();
alert(ms); //1 var是全局变量
```

### 数据类型（基本数据类型：`undefined` `null` `string` `boolean` `number`复杂数据类型：`object`）</br>

#### 1.typeof 操作符

```js
var message = "anne";
alert(typeof message); //string
alert(typeof 95); //number
alert(typeof null); //object
```

#### 2.Undefined

```js
// 只声明变量但未初始化
var mes1;
console.log(mes1 == undefined); //true
// 未声明变量未初始化
console.log(mes2); //返回错误！
// 使用typeof对上述两者检测，结果一样
console.log(typeof mes1); //undefined
console.log(typeof mes2); //undefined
```

#### 3.Null

null 是一个空对象指针，可以用于检查变量是否已经保存一个对象的引用。

> 只要意在保存对象的变量还没有真正保存对象，就应该明确地让该变量保存 null 值。

```js
//undefined派生自null值
console.log(undefined == null); //true
```

#### 4.Boolean

字面值 true 和 false 区分大小写。

<div class="center">

| 数据类型  | 转换为 true                  | 转换为 false |
| --------- | ---------------------------- | ------------ |
| Boolean   | true                         | false        |
| String    | 任何非空字符串               | ""(空字符串) |
| Number    | 任何非零数字值（包括无穷大） | 0 和 NaN     |
| Object    | 任何对象                     | null         |
| Undefined | ×                            | undefined    |

</div>

#### 5.Number

```js
// 八进制与十六进制
const num1 = 070; //有效的八进制转换，忽略前导0
const num2 = 079; //无效的八进制转换，按十进制处理
const num3 = 0xb; //11
const num4 = 0x2e; //16*2+14
console.log(num1, num2, num3, num4); //56,79,11,46
```

- #### 浮点数值

**0.1+0.2！=0.3 的问题**

> 计算机中用二进制来存储小数，大部分小数转成二进制之后都是无限循环的值，因此存在取舍问题，也就是精度丢失。

> 如上所述：0.1 和 0.2 在转换成二进制后会无限循环，由于标准位数的限制后面多余的位数会被截掉，此时就已经出现了精度的损失，相加后因浮点数小数位的限制而截断的二进制数字在转换为十进制就会变成 0.30000000000000004。

> 对于这个问题，一个直接的解决方法就是设置一个误差范围，通常称为“机器精度”。对 JavaScript 来说，这个值通常为 2^(-52)，在 ES6 中，为我们提供了 Number.EPSILON 属性，而它的值就是 2^(-52)，只要我们判断 0.1+0.2-0.3 是否小于 Number.EPSILON，如果小于，就可以判断为 0.1+0.2 ===0.3 --CSDN aiguangyuan

```js
Math.abs(0.1 + 0.2 - 0.3) < Number.EPSILON
  ? console.log(true)
  : console.log(false); //true
```

- #### 数值范围

  [`5e-324`,`1.7976931348623157e+308`] 即 [`Number.MIN_VALUE`,`Number.MAX_VALUE`]

  ```js
  <!-- isFinite可以判断是否处于数值范围之内，注意精度的问题 -->
  const num = Number.MIN_VALUE + Number.MAX_VALUE;
  console.log(isFinite(num));//true
  ```

- #### NaN

任何涉及 NaN 的操作都会返回 NaN(eg.NaN/10);NaN 与任何值都不相等，包括 NaN.

```js
// isNaN可以判断“不是数值”的值，先试图转换为数值类型，然后进行判断。
console.log(isNaN(NaN)); // true
console.log(isNaN(10)); // false
console.log(isNaN("10")); // 转换为10，false
console.log(isNaN(true)); // 转换为1，false
console.log(isNaN("blue")); // 无法转换为数值，true
console.log(NaN == NaN); //false
```

- #### 数值转换

非数值转换为数值：`Number()`/`parseInt()`/`parseFloat()`

**Number()** 可以用于任何数据类型

```js
console.log(Number(true)); // 布尔值，转换为1
console.log(Number(10)); //数字值，简单返回
console.log(Number(null)); //null值，返回0
console.log(Number(undefined)); //undefined,返回NaN
console.log(Number("00123")); //string,忽略前导0，123
console.log(Number("")); //string,空字符串，0
console.log(Number("hello")); //string,无法转换，NaN
```

**parseInt()** 可以用于字符串转换为数值

```js
// parseInt()从第一个数字字符或符号的字符开始解析，直到遇到非数字字符。
// 可解析8进制与16进制数
console.log(parseInt("123blue")); //123
console.log(parseInt("")); //NaN
console.log(parseInt("070")); //70
console.log(parseInt("2.6")); //小数点非有效字符，返回2
console.log(parseInt("AF", 16)); //16进制转换，返回175
console.log(parseInt("AF")); //NaN
```

**parseFloat()** 可以用于字符串转换为数值

与 parseInt()区别，1.第一个小数点有效，第二个无效；2.始终忽略前导 0，且只解析 10 进制数，16 进制数为 0。

```js
console.log(parseFloat("123blue")); //123
console.log(parseFloat("0xA")); //0，在int中为10.
console.log(parseFloat("22.33.44")); //22.33
```

#### 6.String

- #### 字符串特点

字符串一旦创建，值不可改变。想要改变只能销毁再重新创建。

```js
var lang = "Java";
lang = lang + "Script"; //创建新字符串填充JavaScript，再销毁原先的Java和Script
console.log(lang); //JavaScript
```

- #### 转换为字符串

转换为字符串，一般的用`toString()`，null/undefined 用`String()`

```js
var age = 11; //数值
var old = true; //布尔值
var num = 10; //进制转换

console.log(age.toString()); //11 字符串
console.log(old.toString()); //true 字符串
console.log(num.toString(2)); //1010
console.log(num.toString(8)); //12
console.log(num.toString(16)); //a

//应用string()方法时，如果value有toString()方法则优先toString()
var name = null;
var hi;
console.log(String(name)); //null
console.log(String(hi)); //undefined
console.log(typeof String(hi)); //string
```

#### 7.Object 类型(详见第 5 章节和第 6 章节)

> Object 类型是所有它的实例的基础，即，Object 类型所具有的任何属性和方法也同样存在于更具体的对象中。

Object 的每个实例都具有下列属性和方法。

- constructor:保存着用于创建当前对象的函数。如 new Object()中的 Object()
- hasOwnProperty:用于检查给定属性在**当前对象实例**中，而非实例的原型。
- isPrototypeOf(Object):用于检查传入对象是否是当前对象的原型。
- propertyIsEnumerable:用于检查给定属性是否可以使用 for-in 来枚举。
- toLocaleString():返回对象的字符串表示，与执行环境的地区对应。
- toString():返回对象的字符串表示。
- valueOf():返回对象的字符串、数值、布尔值表示。通常与 toString()结果相同。
