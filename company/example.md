## 面试题讨论

在这个版块，大家可以贴出自己的面试题与大家分享，可以寻求答案也可以给大家提供参考。我们欢迎各种形式的讨论，具体格式如下：

/**
 * 题目：如何构建原生的Ajax
 * 答案：

    ```javascript
       var ajax = function(param) {
       var xhr = XMLHttpRequest ? new XMLHttpRequest() : new ActiveXObject("Microsoft.XMLHTTP");
       var type = (param.type || 'get').toUpperCase();
       var url = param.url;
       if (!url) {
          return
       }
       var data = param.data,
           dataArr = [];
       for (var k in data) {
          dataArr.push(k + '=' + data[k]);
       }
       dataArr.push('_=' + Math.random());
       if (type == 'GET') {
          url = url + '?' + dataArr.join('&');
          xhr.open(type, url);
          xhr.send();
       } else {
         xhr.open(type, url);
         xmlhttp.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
         xhr.send(dataArr.join('&'));
       }
       xhr.onload = function() {
         if (xhr.status == 200 || xhr.status == 304) {
            var res;
            if (param.success && param.success instanceof Function) {
               res = xhr.responseText;
               if (typeof res === 'string') {
                  res = JSON.parse(res);
                  param.success.call(xhr, res);
               }
            }
          }
        };
      };
    ```
  * 效果：通过/未通过
  * 技巧：多准备基础知识，手动练习代码
  * 知识点：XMLHttpRequest
 */
