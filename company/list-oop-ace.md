## 阿里秋招内推编程题
/**
 * 题目：使用面向对象的方式维护一个列表，每个列表有一个删除按钮，点击删除按钮移除当前行。
 * 答案：
   ```javascript
   // 此处也可换成ES6的写法
   function Contact() {
     this.init();
   }
   // your code here
   Contact.prototype.init = function () {
     //获取ul
     oul = document.querySelector('#J_List');

     //给body添加事件委托 事件委托必须给添加所操作元素的父元素
     document.body.addEventListener('click',function(e){
         //兼容性处理
         var e = e || window.event;
         // 检查事件源e.targe是否为user-delete
         if (e.target.className || e.srcElement.className == "user-delete") {
             var obj = e.target || e.srcElement;
             //获取父元素li
             var parent = obj.parentElement;

             //删除li
             oul.removeChild(e.srcElement.parentElement)
         }
      });

   };
   new Contact();
   ```
   * 备注：利用事件委托可以避免给每个li添加事件,性能也会比直接添加事件高,试想如果你有1000个li总不能给1000个li遍历添加click吧~
 */
