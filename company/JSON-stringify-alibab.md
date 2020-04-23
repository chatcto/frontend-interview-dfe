/**
 * 题目：JSON.stringify 的功能是，将一个 JavaScript 字面量对象转化为一个 JSON 格式的字符串。例如

    ```javascript
    const obj = {a:1, b:2}
    JSON.stringify(obj) // => '{"a":1,"b":2}'
    // 当要转化的对象有“环”存在时（子节点属性赋值了父节点的引用），为了避免死循环，JSON.stringify 会抛出异常，例如：

    const obj = {
      foo: {
        name: 'foo',
        bar: {
          name: 'bar'
          baz: {
            name: 'baz',
            aChild: null // 将指向obj.bar
          }
        }
      }
    }
    obj.foo.bar.baz.aChild = obj.foo // foo->bar-baz->aChild->foo形成环
    JSON.stringify(obj) // => TypeError: Converting circular structure to JSON
    // 请完善以下“环”检查器函数 cycleDetector，当入参对象中有环时返回 true，否则返回 false。
    function cycleDetector(obj) {
      // 请添加代码
    }
    ```
 *
 * 答案：

    ```javascript
    function cycleDetector (obj) {
      // 请添加代码
        let result = true;
        try {
            JSON.stringify(obj);
        } catch (e) {
            result = false;
        } finally {
            return result;
        }
      }
    ```
 */
