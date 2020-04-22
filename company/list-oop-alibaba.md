## 阿里秋招内推编程题
/**
 * 题目：使用面向对象的方式维护一个列表，每个列表有一个删除按钮，点击删除按钮移除当前行。
 * 答案：
   ```javascript
     class List {
         constructor (sel) {
             this.el = Array.from(document.querySelectorAll(sel));
             let self = this;
             this.el.forEach(item=>{
                 item.addEventListener('click', function (e) {
                     if (e.target.className.indexOf('del') > -1) {
                         self.removeItem.call(self, e.target);
                     }
                 });
             });
         }
         removeItem (target) {
             let self = this;
             let findParent = function (node) {
                 let parent = node.parentNode;
                 let root = self.el.find(item=>item === parent);
                 if (root) {
                     root.removeChild(node);
                 } else {
                     findParent(parent);
                 }
             };
             findParent(target);
         }
     }

     window.addEventListener('DOMContentLoaded', function () {
         new List('.list');
     });
   ```
   * 备注：如想观看运行效果，请使用Chrome浏览器访问source目录下的alibaba/list-oop.html
 */
