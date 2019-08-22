---
title: 继承
---

### 继承

> 在 ES5 中，我们可以使用如下方式解决继承的问题

```js
function Super() {}
Super.prototype.getNumber = function() {
  return 1
}

function Sub() {}
let s = new Sub()
Sub.prototype = Object.create(Super.prototype, {
  constructor: {
    value: Sub,
    enumerable: false,
    writable: true,
    configurable: true
  }
})
```

- 以上继承实现思路就是将子类的原型设置为父类的原型
- 在 `ES6` 中，我们可以通过 `class` 语法轻松解决这个问题

```js
class MyDate extends Date {
  test() {
    return this.getTime()
  }
}
let myDate = new MyDate()
myDate.test()
```

- 但是 `ES6` 不是所有浏览器都兼容，所以我们需要使用 `Babel` 来编译这段代码。
- 如果你使用编译过得代码调用 `myDate.test() `你会惊奇地发现出现了报错

> 因为在 `JS` 底层有限制，如果不是由 `Date `构造出来的实例的话，是不能调用 `Date` 里的函数的。所以这也侧面的说明了：`ES6` 中的 `class` 继承与 `ES5` 中的一般继承写法是不同的。

- 既然底层限制了实例必须由 `Date` 构造出来，那么我们可以改变下思路实现继承

```js
function MyData() {

}
MyData.prototype.test = function () {
  return this.getTime()
}
let d = new Date()
Object.setPrototypeOf(d, MyData.prototype)
Object.setPrototypeOf(MyData.prototype, Date.prototype)
```

- 以上继承实现思路：先创建父类实例 => 改变实例原先的 `_proto__ `转而连接到子类的 `prototype `=> 子类的 `prototype` 的 `__proto__` 改为父类的 `prototype`。
- 通过以上方法实现的继承就可以完美解决 `JS` 底层的这个限制
