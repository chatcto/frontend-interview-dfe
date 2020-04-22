*题目：一个列表，每个列表后面有个删除按钮，点击相应的删除按钮就可以删除相应的列表的其中一行，并且要以面向对象的方式实现。
*题目知识点：闭包，构造函数与原型。


*以下是静静的代码

     ```javascript
        var oUl = document.getElementById('J_List');
        var oLi = oUl.children;
        var oLength = oLi.length;
        for (var i = 0; i < oLength; i++) {
            oLi[i].onclick = function(e){
                e = e || window.event;
                var el = e.srcElement;
                if (el.className == 'user-delete') {
                    removeLi(el);
              }
            }
          }
        function removeLi(node){
            node.parentNode.parentNode.removeChild(node.parentNode);
          }
     ```
     
     *效果：通过
     *知识点：闭包、事件代理
     
     
     *虽然没有用题目中指出的用构造函数和原型，希望借此抛砖引玉，我也继续研究用上构造函数和原型来实现功能