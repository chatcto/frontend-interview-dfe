___
title: '常用'
___

## 输入 字符串 aaaaaabbbbbccccddac 输出 a6b5c4d2a1c1
用JavaScript 语言
或其他语言都可以

## react 状态 是同步还是异步
```js
    constructor(props) {
        super(props)
        this.state = {num: 1}
    }

    componentDidMount() {
        this.setState({num:3})
        console.log(num)
    }
```

## 请说出下面代码执行的结果


## react
react 状态 是同步还是异步
```js
    constructor(props) {
        super(props)
        this.state = {num: 1}
    }

    componentDidMount() {
        this.setState({num:2})
        this.setState({num:4})
        this.setState({num:3})
        console.log(num)
    }
```
## React 中 keys 的作用是什么？

## shouldComponentUpdate 是做什么的

## 高阶函数
var fn = curry(function(a, b, c) {
    return [a, b, c];
});

fn("a", "b", "c") // ["a", "b", "c"]
fn("a", "b")("c") // ["a", "b", "c"]
fn("a")("b")("c") // ["a", "b", "c"]
fn("a")("b", "c") // ["a", "b", "c"]

## this 指向问题
obj = {
    name: 'a',
    getName : function () {
        console.log(this.name);
    }
}

var fn = obj.getName
obj.getName()
var fn2 = obj.getName()
fn()
fn2()

## 项目做过哪些性能优化？

## 讲解一下HTTPS的工作原理

## webpack 写一个插件的思路

## 手写代码，简单实现apply

## webpack 怎么提取公共的 函数库

## package版本意思
~ ^

## 使用过的koa2中间件

## Vue 双向绑定实现原理？

## 手写代码，简单实现bind

## WeakMap 和 Map 的区别?

## redux 中间件

## 接入redux的过程

## 介绍Redux数据流的流程

## 绑定connect的过程

## bind、call、apply的区别

## Redux如何实现多个组件之间的通信，多个组件使用相同状态如何进行管理

## 多个组件之间如何拆分各自的state，每块小的组件有自己的状态，它们之间还有一些公共的状态需要维护，如何思考这块

## react dom 怎么被浏览器识别， 具体流程

## 失败 请求三次

## ES6中的map和原生的对象有什么区别

## 如何实现一个 react-thunk

## HTTP/2 新特性总结

## Set 和 Map 数据结构

## 说出常用的Linux命令

## webpack 性能优化有哪些

## SplitChunksPlugin 配置参数详解

## webpack配置懒加载

## 如何编写一个 Loader

## Tree Shaking 概念

## Shimming 的作用

## Jenkins 怎么写 shell

## nginx都做过什么

## eslint规范

## git钩子

## http 和 http2 有哪些区别 有什么好处

## history 实现原理

## 自动dispatch

## 异常捕获用什么

## 服务端渲染SSR

setTimeout(function () {
        console.log(1);
    });
    new Promise(function(resolve,reject){
        console.log(2) 
        resolve(3)
    }).then(function(val){
        console.log(val);
    })
    console.log(4)

2 4 3 1

```
//请写出输出内容
async function async1() {


    console.log('async1 start');
    await async2();
    console.log('async1 end');
}
async function async2() {
    console.log('async2');
}

console.log('script start');

setTimeout(function() {
    console.log('setTimeout');
}, 0)

async1();

new Promise(function(resolve) {
    console.log('promise1');
    resolve();
}).then(function() {
    console.log('promise2');
});
console.log('script end');

/*
输出结果：

script start
async1 start
async2
promise1
script end
async1 end
promise2
setTimeout
*/
```
![2019-08-14-17-57-11](http://s.shudong.wang/2019-08-14-17-57-11.png)
