# 今日头条web前端社招笔试题
>限时50分钟,请把握好时间。

---

### 1. 存在元素A满足以下条件
- A元素左右距离10px
- A元素在窗口水平垂直居中
- A元素中的文字A水平垂直居中
- A元素中字体设置为20px
- A的高度始终为A宽度的50%（如果不会，可以降低要求，把高度设为100px）

请用html/css实现上述条件
答案：正在整理中。。。
```css

```
### 2. arguments是数组吗？若不是，如何变为数组？
答案: 不是。变为数组有如下四种方法，第一种slice效率最高。
```js
var arr = Array.prototype.slice.apply(arguments);
var arr = Array.prototype.concat.apply([], arguments);
var arr = Array.apply([], arguments);
var arr = [];
for(var i=0,len=arguments.length;i<len;i++){
    arr.push(arguments[i]);
}
```

### 3. 说出下面程序执行的结果
  ```js
    if([]==false){console.log(1)}
    if({}==false){console.log(2)}
    if([]==0){console.log(3)}
    if([1]==[1]){console.log(4)}
  ```
答案：
```js
1
3
```
```js
解析：记住下面的就好。
注意:当两个值都是对象 (引用值) 时, 比较的是两个引用值在内存中是否是同一个对象(即引用地址是否相同)
[],{}单独为true
[],{}两者自身不值等，互相不值等
[]==false 为true 解析步骤隐式转换=> []==(ToNumber(false)=0) => (ToPrimitive([])='') == 0 =>(ToNumber('')=0) == 0
{}==false 为false
```
### 4. 如题（可以使用ES6）
```js
function print(){
  var name = 'zhangsan';
  var skills = ['js', 'vue', 'angular'];
  for(var i=0,len = skills.length;i<len;i++){
    setTimeout(function(){
      console.log(name + ' learn skill '+ i + ' ' +skills);
      console.log('.................');
    },0)
    console.log(i)
  }
}
print();
```  
最小化改动上面程序,实现下面的打印结果
```js
1
2
3
zhangsan learn skill 1 js
.................
zhangsan learn skill 2 vue
.................
zhangsan learn skill 3 angular
.................
```
答案:
```js
第一种答案:
for(let i=0,len = skills.length;i<len;i++){
        setTimeout(function(){
            console.log(name + ' learn skill '+ (i+1) + ' ' +skills);
            console.log('.................');
        },0)
        console.log(i+1)
    }
第二种答案:    
for(let i=0,len = skills.length;i<len;){
        setTimeout(function(){
            console.log(name + ' learn skill '+ i + ' ' +skills);
            console.log('.................');
        },0)
        console.log(++i)
    }
```

### 5.实现函数的bind方法，使程序结果能打印出来success
```js
function Aniaml(name, color){
  this.name = name;
  this.color = color;
}
Animal.prototype.say=function(){
  return `I'm ${name}, my color is ${color}`;
}
var Cat = Animal.bind(null, 'cat');
var cat = new Cat('white');
var res = cat.say();
if(res && cat instanceof Cat && cat instanceof Animal){
  console.log('success');
}
```
答案：正在整理中。。。

### 6.说出下面程序执行的结果
```js
async function async1(){
  console.log('async1 start');
  await async2();
  console.log('async1 end');
}
async function async2(){
  console.log('async2');
}
console.log('script start');
setTimeout(function(){
  console.log('setTimeout');
},0);
async1();
new Promise(function(resolve){
  console.log('promise 1');
  resolve();
}).then(function(){
  console.log('promise 2');
})
console.log('script end');
```
答案:
```js
script start
async1 start
async2
promise 1
script end
promise 2
async1 end
setTimeout
解析:
Promise和setTimeout执行顺序相关说明参考：
https://www.zhihu.com/question/36972010

async await和Pormise then的执行顺序相关说明参考:
暂时没有找到原理
```

### 7.实现函数节流throttle，时间至少是100ms
答案：正在整理中。。。

### 8.有一个数组data，其值是一系列的无序，不重复的数字，取出n个，使其和sum。写出函数的算法，并说明其时间复杂度和空间复杂度，写出一个解即可。
```js
function getSum(data, n, sum){

}
```
答案：正在整理中。。。
