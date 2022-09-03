---
title: 条件类型
author: 何青烨
date: "2021-12-12"
---

错题解析
说一说常见的请求头和相应头都有什么呢？

1)请求(客户端->服务端[request])
GET(请求的方式) /newcoder/hello.html(请求的目标资源) HTTP/1.1(请求采用的协议和版本号)
Accept: _/_(客户端能接收的资源类型)
Accept-Language: en-us(客户端接收的语言类型)
Connection: Keep-Alive(维护客户端和服务端的连接关系)
Host: localhost:8080(连接的目标主机和端口号)
Referer: http://localhost/links.asp(告诉服务器我来自于哪里)
User-Agent: Mozilla/4.0(客户端版本号的名字)
Accept-Encoding: gzip, deflate(客户端能接收的压缩数据的类型)
If-Modified-Since: Tue, 11 Jul 2000 18:23:51 GMT(缓存时间)
Cookie(客户端暂存服务端的信息)
Date: Tue, 11 Jul 2000 18:23:51 GMT(客户端请求服务端的时间)

2)响应(服务端->客户端[response])
HTTP/1.1(响应采用的协议和版本号) 200(状态码) OK(描述信息)
Location: http://www.baidu.com(服务端需要客户端访问的页面路径)
Server:apache tomcat(服务端的 Web 服务端名)
Content-Encoding: gzip(服务端能够发送压缩编码类型)
Content-Length: 80(服务端发送的压缩数据的长度)
Content-Language: zh-cn(服务端发送的语言类型)
Content-Type: text/html; charset=GB2312(服务端发送的类型及采用的编码方式)
Last-Modified: Tue, 11 Jul 2000 18:23:51 GMT(服务端对该资源最后修改的时间)
Refresh: 1;url=http://www.it315.org(服务端要求客户端1秒钟后，刷新，然后访问指定的页面路径)
Content-Disposition: attachment; filename=aaa.zip(服务端要求客户端以下载文件的方式打开该文件)
Transfer-Encoding: chunked(分块传递数据到客户端）  
 Set-Cookie:SS=Q0=5Lb\*nQ; path=/search(服务端发送到客户端的暂存数据)
Expires: -1//3 种(服务端禁止客户端缓存页面数据)
Cache-Control: no-\*\*\*(服务端禁止客户端缓存页面数据)  
 Pragma: no-\_\*\*(服务端禁止客户端缓存页面数据)  
 Connection: close(1.0)/(1.1)Keep-Alive(维护客户端和服务端的连接关系)  
 Date: Tue, 11 Jul 2000 18:23:51 GMT(服务端响应客户端的时间)
在服务器响应客户端的时候，带上 Access-Control-Allow-Origin 头信息，解决跨域的一种方法。

正则
exec() 方法的功能非常强大，它是一个通用的方法，而且使用起来也比 test() 方法以及支持正则表达式的 String 对象的方法更为复杂。
如果 exec() 找到了匹配的文本，则返回一个结果数组。否则，返回 null。此数组的第 0 个元素是与正则表达式相匹配的文本，第 1 个元素是与 RegExpObject 的第 1 个子表达式相匹配的文本（如果有的话），第 2 个元素是与 RegExpObject 的第 2 个子表达式相匹配的文本（如果有的话），以此类推。除了数组元素和 length 属性之外，exec() 方法还返回两个属性。index 属性声明的是匹配文本的第一个字符的位置。input 属性则存放的是被检索的字符串 string。我们可以看得出，在调用非全局的 RegExp 对象的 exec() 方法时，返回的数组与调用方法 String.match() 返回的数组是相同的。
但是，当 RegExpObject 是一个全局正则表达式时，exec() 的行为就稍微复杂一些。它会在 RegExpObject 的 lastIndex 属性指定的字符处开始检索字符串 string。当 exec() 找到了与表达式相匹配的文本时，在匹配后，它将把 RegExpObject 的 lastIndex 属性设置为匹配文本的最后一个字符的下一个位置。这就是说，您可以通过反复调用 exec() 方法来遍历字符串中的所有匹配文本。当 exec() 再也找不到匹配的文本时，它将返回 null，并把 lastIndex 属性重置为 0。

```js
// 在JavaScript的函数中，this始终指向调用者的上下文环境
var len = 117; // 5. 全局作用域中使用 var 定义的变量默认会成为 window 的属性，及 window.len
let func = {
  len: 935,
  showLen: function () {
    console.log(this.len); // 4. this 此时指向的是 window，所以相当于打印 window.len
  },
  show: function () {
    (function (cb) {
      cb(); // 3. cb 相当于 cb.call() 默认没有传入上下文环境时 this 指向全局的 window 对象
    })(this.showLen); // 2. this 是 func 所以传入的是上面定义的 showLen 函数
  },
};

func.show(); // 1. 相当于 func.show.call(func)，此时 this 是 func
```

https://blog.csdn.net/Febby_/article/details/94763441

```js
//原来的代码
var a = 2;
function fn() {
  b();
  return;
  var a = 1;
  function b() {
    console.log(a);
  }
}
fn();

//实际上的代码
var a = 2;
function fn() {
  function b() {
    console.log(a);
  }
  var a; //变量声明提升，默认赋值为undefined
  b(); //执行函数b，在当前作用域找到a，值为undefined
  return; //return后面的语句不再执行，a没有被赋值为1
  a = 1; //在原来的位置才会赋值，但不会执行到这里
}
fn();
```

```js

网上有一道美团外卖的面试题是这样的：
Function.prototype.a = 'a';
Object.prototype.b = 'b';
function Person(){};
var p = new Person();
console.log('p.a: '+ p.a); // p.a: undefined
console.log('p.b: '+ p.b); // p.b: b  问为什么？

有不少同学第一眼看上去就觉得很疑惑，p不是应该继承了Function原型里面的属性吗，为什么p.a返回值是undefined呢？
其实，只要仔细想一想就很容易明白了，Person函数才是Function对象的一个实例，所以通过Person.a可以访问到Function
原型里面的属性，但是new Person()返回来的是一个对象，它是Object的一个实例,是没有继承Function的，所以无法访问
Function原型里面的属性。但是,由于在js里面所有对象都是Object的实例，所以，Person函数可以访问到Object原型里面的
属性，Person.b => 'b'
```

```js
for (var i = 0; i < 3; ++i) {
  setTimeout(function () {
    console.log(i);
  }, 100);
} //333
for (let i = 0; i < 3; ++i) {
  setTimeout(function () {
    console.log(i);
  }, 100);
} //012
```

```js
function fn(o, val) {
  o.b = 1; //修改o指向的对象{b:0}中的属性b的值，对象变为{b:1}
  val = 1; //修改局部变量val的值为1，不会影响全局变量num的值
}
var obj = { b: 0 }; //引用类型的变量obj指向对象{b:0}
var num = 0;
fn(obj, num); //将obj的引用地址复制给fn函数的形参o，此时obj和o指向同一个对象{b:0}；将num的值复制一份赋值给val
console.log(obj, num); //打印全局变量obj指向的对象，此时被修改为{b:1};打印全局变量num值，还是0
```

```js
//冒泡排序
for (var i = 0; i < arr.length - 1; i++) {
  for (var j = 0; j < arr.length - 1 - i; j++) {
    if (arr[j] > arr[j + 1]) {
      var temp = arr[j];

      arr[j] = arr[j + 1];

      arr[j + 1] = temp;
    }
  }
}

console.log(arr);

//选择排序
var minIndex;

var temp;

for (let i = 1; i < arr.length; i++) {
  minIndex = i - 1;

  for (let j = i; j < arr.length; j++) {
    if (arr[j] < arr[minIndex]) minIndex = j;
  }

  if (minIndex != i - 1) {
    temp = arr[i - 1];

    arr[i - 1] = arr[minIndex];

    arr[minIndex] = temp;
  }
}
console.log(arr);
//插入排序
for (let i = 1; i < arr.length; i++) {
  for (let j = i - 1; j >= 0 && arr[j] > arr[j + 1]; j--) {
    let temp = arr[j];

    arr[j] = arr[j + 1];

    arr[j + 1] = temp;
  }
}
console.log(arr);
```

<!-- 这里考的是JS的运行机制！ 事件(click,focus等等)，定时器(setTimeout和setInterval)，ajax,都是会触发异步，属于异步任务；js是单线程的，一个时间点只能做一件事，优先处理同步任务； 按照代码从上往下执行，遇到异步，就挂起，放到异步任务里，继续执行同步任务，只有同步任务执行完了，才去看看有没有异步任务，然后再按照顺序执行！ 这里for循环是同步任务，onclick是异步任务，所以等for循环执行完了，i变成4了，注意：这里因为i是全局变量，最后一个i++，使得i为4(后面的onclick函数，最后在循环外面执行，不受i<length限制)； 所以for循环每执行一次，onclick事件函数都会被挂起一次，共4次； for循环结束后，点击事件 触发了4个onclick函数，接着输出4个4！ -->
