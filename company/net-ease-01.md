---
title: 网易2018校招内推二面题
---

## 网易2018校招内推二面题

/**
这道题是网易2018校招内推二面题，要求手写一个select组件。


* 题目：点一下select组件会出来一个列表，点击列表项select自动填充所选择的内容。

* 我的思路
1.先用DOM驱动直接写法写出来
2.在这个基础上封装，使用面向对象思想
3.面试官说面向对象太复杂，于是简化成一个函数
4.后面感觉MVVM的写法也是可以的
* 答案(这里的样式借鉴了JavaScript30的)
>HTML代码
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Select组件</title>
    <link rel="stylesheet" href="index.css">
</head>
<body>
    <form action="" class="select-form">
        <input type="text" class="select" placeholder="select组件" readonly>
        <ul class="list display-none">
            <li>这是一个List</li>
            <li>这是一个List</li>
        </ul>
    </form>
    <!-- <script type="text/javascript" src="index.js"></script> -->
    <!-- <script type="text/javascript" src="index.js"></script> -->
    <script type="text/javascript" src="index-optimizing.js"></script>
</body>
</html>
```
>CSS代码
```css
html {
    box-sizing: border-box;
    background: hsla(193, 30%, 64%, 0.78);
    font-family: 'Kaiti', 'SimHei', 'Hiragino Sans GB ', 'helvetica neue';
    font-size: 20px;
    font-weight: 200;
}
*,
*:before,
*:after {
    box-sizing: inherit;
}
input {
    width: 100%;
    padding: 20px;
    font-family: 'Kaiti', 'helvetica neue';
}
.select-form {
    max-width: 700px;
    margin: 50px auto;
}
input.select {
    margin: 0;
    text-align: center;
    outline: 0;
    border: 10px solid #F7F7F7;
    width: 120%;
    left: -10%;
    position: relative;
    top: 10px;
    z-index: 2;
    border-radius: 5px;
    font-size: 40px;
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.12), inset 0 0 2px rgba(0, 0, 0, 0.19);
}
.list {
    margin: 0;
    padding: 0;
    position: relative;
    /*perspective:20px;*/
}
.list li {
    background: white;
    list-style: none;
    border-bottom: 1px solid #D8D8D8;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.14);
    margin: 0;
    padding: 20px;
    transition: background 0.2s;
    display: flex;
    justify-content: center;
}
.list li:nth-child(even) {
    transform: perspective(100px) rotateX(3deg) translateY(2px) scale(1.001);
    background: linear-gradient(to bottom, #ffffff 0%, #EFEFEF 100%);
}
.list li:nth-child(odd) {
    transform: perspective(100px) rotateX(-3deg) translateY(3px);
    background: linear-gradient(to top, #ffffff 0%, #EFEFEF 100%);
}
a {
    color: black;
    background: rgba(0, 0, 0, 0.1);
    text-decoration: none;
}
.display-none{
    display: none;
}
```


>未封装版本
```js
const url =
    "http://202.203.209.96/v5api/api/ClassCourse/20171/05120071205/20151/04";
const select = document.querySelector(".select");
const list = document.querySelector(".list");
const courses = [];
fetch(url)
    .then(blob => blob.json())
    .then(data => courses.push(...data))
    .then(initList);
select.addEventListener("click", toggleList);
list.addEventListener("click", selectList);
function initList() {
    // list.classList.add("display-none")
    const html = courses
        .map(course => {
            const teacher = course.JSXM_JS;
            const title = course.NAME_KC;
            // 构造 HTML 值
            return `
          <li>
              <span>${teacher}-${title}</span>
          </li>
      `;
        })
        .join("");
    list.innerHTML = html;
}
function toggleList() {
    list.classList.toggle("display-none");
}
function selectList(event) {
    const target = event.target;
    // console.dir(target)
    if (target.tagName.toLowerCase() === "span") {
        select.placeholder = target.textContent;
    } else if (target.tagName.toLowerCase() === "li") {
        select.placeholder = target.children[0].textContent;
    }
    window.toggleList();
}
```

>面向对象版本
```js
const url = 'http://202.203.209.96/v5api/api/ClassCourse/20171/05120071205/20151/04';
let select, list, courses = []
fetch(url)
    .then(blob => blob.json())
    .then(data => courses.push(...data))
    .then(() => new Select(".select", ".list", courses))
class Select {
    constructor(selectName, listName, data) {
        select = document.querySelector(selectName)
        this.initList(listName, data)
    }
    initList(listName, courseData) {
        list = document.querySelector(listName)
        // let _select = this
        const html = courseData.map(course => {
            const teacher = course.JSXM_JS
            const title = course.NAME_KC
            // 构造 HTML
            return `
                <li>
                    <span>${teacher}-${title}</span>
                </li>
            `;
        }).join('')
        list.innerHTML = html
        select.addEventListener('click', () => this.toggleList())
        list.addEventListener('click', (e) => this.selectList(e))
    }
    toggleList() {
        list.classList.toggle("display-none")
    }
    selectList(event) {
        const target = event.target
        // console.dir(target)
        if (target.tagName.toLowerCase() === 'span') {
            select.placeholder = target.textContent
        } else if (target.tagName.toLowerCase() === 'li') {
            select.placeholder = target.children[0].textContent
        }
        this.toggleList()
    }
}
```

>最终版本
```js
//最终版本
const url = 'http://202.203.209.96/v5api/api/ClassCourse/20171/05120071205/20151/04';
let select, list, courses = []
fetch(url)
    .then(blob => blob.json())
    .then(data => courses.push(...data))
    .then(() => createSelect(".select", ".list", courses))
function createSelect(selectName, listName, data) {
    select = document.querySelector(selectName)
    initList(listName, data)
}
function initList(listName, courseData) {
    list = document.querySelector(listName)
    const html = courseData.map(course => {
        const teacher = course.JSXM_JS
        const title = course.NAME_KC
        // 构造 HTML
        return `
                    <li>
                        <span>${teacher}-${title}</span>
                    </li>
                `;
    }).join('')
    list.innerHTML = html
    select.addEventListener('click', () => this.toggleElement(list))
    // list.addEventListener('click', (e) => this.selectList(e))
    list.addEventListener('click', (e) => {
        this.selectValue(e, select)
        this.toggleElement(list)
    })
}
function toggleElement(el) {
    el.classList.toggle("display-none")
}
function selectValue(src, des) {
    const target = src.target
    if (target.tagName.toLowerCase() === 'span') {
        des.placeholder = target.textContent
    } else {
        des.placeholder = target.children[0].textContent
    }
}

```
**/
