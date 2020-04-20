---
title: React 进阶面试题
---

### 1 什么是高阶组件?你在工作中是如何应用的?

<!-- > `Keys `是 `React` 用于追踪哪些列表中元素被修改、被添加或者被移除的辅助标识 -->

- React高阶组件是类比于`高阶函数`，它接受React的组件作为输入，然后输出一个新的React组件。
- 高阶组件可以让代码更具有`复用性，逻辑性和抽象性`
- 高阶组件可以对`render`方法进行劫持，可以控制props和state
- 避免在`render`中使用高阶组建
- 对`refs`没有用，因为`ref`是自己处理的
- 实际的开发中会用到的地方比如redux的connect函数，react-router中的withRouter，处理全局的loading和权限处理等


### 2 展示组件（Presentational component) 和容器组件（Container component）之间有何不同？

- 第一个方面，她们关注点不同。容器组件它更多的是逻辑的处理，比如说更新状态和读取状态，而展示性组件更关注的是UI的展现，
- 第二个方面是对于redux是否有感知。容器组件是有的，展示性组件是没有的。
- 第三个方面是读取数据方面。容器组件从redux的store中读取，而展示性组件是通过props中去获取
- 第四个方面是写数据方面，容器组件是通过dispatch一个action，展示性组件是通过props中的回调函数
- 第五个方面是如何创建. 容器组件大部分是通过react-redux去创建的，函数组件是手工编写

### 3 React中的refs的作用是什么？

- 通过ref访问到组件实例
- 通过refs访问真实dom

- 三种创建ref方式
  - 直接指定ref = 'xxx'  ref是一个字符串，React不推荐使用
  - 通过React.creteRef()创建，创建的ref 有current熟悉，函数组件如果需要使用，需要使用React.forwardRef转发ref
    ，hoc组件传递ref也存在同样的问题，需要使用React.forwardRef转发
  - 通过函数ref={input => this.userName = input }, 获取值需要使用this.userName.value

### 4 React性能优化的方法
- 渲染角度优化
  - 使用immutable.js
  - 不要在render中修改状态
  - 不在元素中使用内联样式， 使用css隐藏节点而不是强制加载和卸载
  - 使用SSR，可以在服务端生成html返回到客户端
  - 使用React.Fragment减少不必要DOM
- 组件层面优化
  - 组件懒加载。组件或UI库也可以使用动态导入的方式，只在用户使用到的时候加载。页面组件可以使用react-loadable
  - 使用pureComponent代替component，以达到一些没必要的渲染，或者在使用shouldComponent进行一个优化
  - 组件尽可能的拆分，给列表类组件提供唯一不变的key，尽量不要使用下标作为key
  - 在constructor中使用bind来绑定this，而不在使用时绑定或减少使用箭头函数，因为constructor只在组件初始化时执行一次，而使用时绑定是每次render都会执行，箭头函数也是如此
  - 按需引入props，避免多余更新
- 数据获取层面优化
  - 不要在componentWillMount中请求数据
  - redux与reselect结合使用，reselect动作的原理是只要相关的状态没有改变，那么就直接使用上一次的缓存结果
  - 结合业务场景使用localstorage、sessionstorage等缓存机制
- 代码打包编译层面优化
  - 结合打包工具webpack、gulp等使用，一般常用webpack，利用webpack打包分离去重实现动态导入，减少重复性代码块
  - webpack结合plugin+loader使用


### 5 你对immutable有了解吗？它有什么作用？

- Immutable实现的原理
  - Immutable实现的原理是利用结构共享形成持久化数据结构，也就是使用旧数据创建新数据时，要保证旧数据同时可用且不变。同时为了避免 deepCopy 把所有节点都复制一遍带来的性能损耗，Immutable使用了结构共享，即如果对象树中一个节点发生变化，只修改这个节点和受它影响的父节点，其它节点则进行共享

- Immutable的优点
  - 节约内存
  - JavaScript 中的对象一般是可变的（Mutable），因为使用了引用赋值，新的对象简单的引用了原始对象，改变新的对象将影响到原始对象。为了解决这个问题，一般的做法是使用shallowCopy（浅拷贝）或 deepCopy（深拷贝）来避免被修改，但这样做造成了CPU和内存的浪费。Immutable 可以很好地解决这些问题
  - Undo/Redo，Copy/Paste，时间轴等功能容易实现
  - 因为每次数据都是不一样的，只要把这些数据放到一个数组里储存起来，想回退到哪里就拿出对应数据即可，很容易开发出撤销重做这种功能
  - 并发安全
  - Immutable Data一旦创建，就不能再被更改,也就不需要并发锁
  - Immutable使用
  - 与React搭配使用，Immutable简洁高效的判断数据是否变化，提高渲染速度及性能
  - 与Redux/flux搭配使用


### 6 你对Redux有了解吗？

  - Redux是一种解决方案，不只适用于React，同样适用于Vue和原生js等。
  - Redux中只有一棵状态树，遵循数据从上到下（瀑布流）的哲学，进行统一的数据管理
  - 提供了一个createStore的方法来进行创建仓库的操作，提供两个参数action动作，和处理逻辑的reducer
  - createStore的方法提供了三个核心方法 getState获取数据  dispatch派发动作  subscribe订阅
  - createStore是一个高阶函数 参数是函数 返回的也是一个函数


### 7 什么是受控组件和非受控组件？

  - 受控组件
   - 其值由React控制的输入表单元素称为“受控组件”
   - 受控组件不保存其自身的内部状态; 该组件纯粹根据props呈现内容
   - 特点1. 设置value值，value由state控制，2. value值一般在onChange事件中通过setState进行修改
   - 使用场景：需要对组件的value值进行修改时，使用受控组件。比如：页面中有一个按钮，每点击一次按钮受控组件的值加1.
   - 在 react 中，Input textarea 等组件默认是非受控组件,但是也可以转化成受控组件，就是通过 onChange 事件获取当前输入内容，将当前输入内容作为 value 传入，此时就成为受控组件

  - 非受控组件
   - 表现形式上，react中没有添加value属性（单选按钮和复选框对应的是checked）的表单组件元素就是非受控组件
   - 表单数据由 DOM 处理的组件是非受控组件。
   - 特点 1. 不设置value值，2. 通过ref获取dom节点然后再取value值
   - 使用场景 ：任何时候都不需要改变组件的value值，这时候可以使用非受控组件


### 8 什么是React Hooks?

  - React Hooks 是 React 16.7.0-alpha 版本推出的新特性。React Hooks 要解决的问题是状态共享，是继 render-props 和HOC之后的第三种状态逻辑复用方案，不会产生 JSX 嵌套地狱问题。React Hooks 的设计目的，就是加强版函数组件，完全不使用"类"，就能写出一个全功能的组件。
  - React Hooks 的意思是，组件尽量写成纯函数，如果需要外部功能和副作用，就用钩子把外部代码"钩"进来。useState()用于为函数组件引入状态（state）。纯函数不能有状态，所以把状态放在钩子里面
  - 如果需要在组件之间共享状态，可以使用useContext()
  - React 本身不提供状态管理功能，通常需要使用外部库。这方面最常用的库是 Redux。
    Redux 的核心概念是，组件发出 action 与状态管理器通信。状态管理器收到 action 以后，使用 Reducer 函数算出新的状态，Reducer 函数的形式是(state, action) => newState。
    useReducers()钩子用来引入 Reducer 功能。
    const [state, dispatch] = useReducer(reducer, initialState)


### 9 React国际化

  - 切换语言是一个低频需求，但语言包可能会比较大，可以按需加载
  - 限制词语或句子的长度，在语言切换时，长度可能会变化，比如英文单词可能比中文单词长，会影响布局
  - 注意颜色在不同语言、文化中的差异
  - 注意日期和货币格式在不同国家和地区的差异显示
