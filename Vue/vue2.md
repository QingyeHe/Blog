---
title: 变化侦测
author: 何青烨
date: 2022-7-5
---

Vue.js 会自动通过状态生成 DOM，并将其输出到页面上显示出来，这个过程叫渲染。
变化侦测的作用是侦测数据的变化。当数据变化时，会通知视图进行相应的更新。

变化侦测分为推和拉，
拉：当状态发生变化时，它不知道哪个状态变了，只知道状态有可能变了，然后会发送一个信号告诉框架，框架内部收到信号后，会进行一个暴力比对来找出哪些 DOM 节点需要重新渲染。
推：当状态发生变化时，Vue.js 立刻就知道了，而且在一定程度上知道哪些状态变了。

拉--Angular-脏检查，React-虚拟 DOM；
推--Vue.js ，2.0 调整为中等粒度，从具体 DOM 节点到组件。

<h2>如何追踪变化</h2>
在JavaScript（简称JS）中，如何侦测一个对象的变化？</br>
使用Object.defineProperty和ES6的Proxy

封装函数的功能：每当从 data 的 key 中读取数据时，get 函数被触发；每当往 data 的 key 中设置数据时，set 函数被触发。

```js
function defineReactive(data, key, val) {
  Object.defineProperty(data, key, {
    enumerable: true,
    configurable: true,
    get: function () {
      return val;
    },
    set: function (newVal) {
      if (val === newVal) {
        return;
      }
      val = newVal;
    },
  });
}
```

<h2>如何收集依赖</h2>

> 先收集依赖，即把用到数据 name 的地方收集起来，然后等属性发生变化时，把之前收集好的依赖循环触发一遍就好了。总结起来，其实就一句话，在 getter 中收集依赖，在 setter 中触发依赖

在 Vue.js 2.0 中，模板使用数据等同于组件使用数据，所以当数据发生变化时，会将通知发送到组件，然后组件内部再通过虚拟 DOM 重新渲染。

<h2>依赖收集在哪里</h2>

```js
function defineReactive(data, key, val) {
  let dep = []; //新增
  Object.defineProperty(data, key, {
    enumerable: true,
    configurable: true,
    get: function () {
      dep.push(window.target); //新增 存储被收集的依赖
      return val;
    },
    set: function (newVal) {
      if (val === newVal) {
        return;
      }
      //新增 循环dep以触发收集到的依赖
      for (let i = 0; i < dep.length; i++) {
        dep[i](newVal, val);
      }
      val = newVal;
    },
  });
}
```
