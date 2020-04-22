## 阿里巴巴提前批前端编程测试题

这道题是阿里巴巴2017年7月秋招提前批，前端岗位的编程测评题，原题是给出了html和css代码，让考生写js代码,js代码提示可以用ES6写，并且要用面向对象的思维写。js部分给了一个init()和两句注释。


* 题目：提供一个列表，每个列表后面有个删除按钮，点击相应的删除按钮就可以删除相应的列表的其中一行，并且要以面向对象的方式实现。
* 我的思路
1.第一反应：
1.1获取页面中的所有删除按钮元素
1.2点击事件监听
1.3列表获取及移除
2.事件委托优化：
2.1获取页面中的列表元素
2.2点击事件监听
2.3列表获取及移除
3.加入面向对象(OOP)思维
3.1.把列表和联系人都看作是一个对象,把相关的功能封装到对象里去
3.2.获取页面中的列表元素并监听点击事件
3.3.列表获取及移除
_3.JS的委托面向对象思维
_3.1.创建一个DOMPlayer对象专门操作DOM
_3.2.创建一个List对象并且和DOMPlayer建立原型链关联
_3.3.创建list实例,直接调用相关方法
4.其他的考虑
4.1事件监听的移除
4.2前端和后端的交互
* 答案：
 ```js
//第一反应
init()
function init() {
    const deleteBtn = document.querySelectorAll(".user-delete")
    deleteBtn.forEach(d => {
        d.addEventListener("click", removeItem)
    })
}

function removeItem(event) {
    event.target.parentNode.remove()
}

// 事件委托优化
init()
function init() {
    const J_List = document.querySelector("#J_List")
    J_List.addEventListener("click", removeListItem)
}
function removeListItem(e) {
    e.target.className.includes("user-delete") && e.target.parentNode.remove()
}

//OOP思维
class List {
    constructor(contacts) {
        this.contacts = contacts
    }
    initList() {
        const J_List = document.querySelector("#J_List")
        J_List.addEventListener("click", this.removeListItem)
    }
    removeListItem(e) {
        e.target.className.includes("user-delete") && e.target.parentNode.remove()
    }
}
class Contact {
    constructor(id, name = "", sex = "", tel = "", province = "") {
        this.id = id
        this.name = name
        this.sex = sex
        this.tel = tel
        this.province = province
    }
    removeItem() {
        //
    }
}
init()
function init() {
    let list = new List(null)
    list.initList()
}

//委托对象思维
let DOMPlayer = {
    initDOM(domName, eventName) {
        const el = document.querySelector(domName)
        el.addEventListener(eventName, this.removeItem)
    },
    //更多方法
}

init()
function init() {
    let List = Object.create(DOMPlayer)
    List.initList = function (e) {
        this.initDOM("#J_List", "click")
    }
    List.removeItem = function (e) {
        e.target.className.includes("user-delete") && e.target.parentNode.remove()
    }
    let list = Object.create(List)
    list.initList()
}
```
* 效果：通过
* 技巧：多准备基础知识，手动练习代码
* 知识点：操作DOM,JS与面向对象

