## 面试题

### 1.双向绑定的原理,vue-roter的原理
  - `Object.defineProperty` 绑定对象中的数据 
  ```js 
var data = {}
var temp;

Object.defineProperty(data, 'txt', {
  set: function (value) {
    // console.log('获取data的值为：', value);
    text.innerText = value;
    p1.innerText = value;
    temp = value;
  },
  get: function () {
    return temp;
  }
})
  ```

  -  vue-roter的处理过程
  ```js 
// 路由处理的过程:
// 1 修改浏览器地址栏中的哈希值
// 2 Vue路由监听到哈希值的改变
// 3 到路由规则中,查找匹配的路由规则( 哈希值 和 path路由规则  匹配)
// 4 找到该路由规则对应的组件,展示在 router-view 组件对应的出口
// 5 在页面中就看到该路由的内容了
  ```


### 2.ES6中Promise的原理，常用的新语法
- promise的原理和基本使用

```javascript
// ES6 中的 Promise 是 JS 中异步编程的一个解决方案
// 在没有 Promise 之前，JS 中是通过 回调函数 来实现 异步编程的
// 实际上，Promise仅仅是提供了一种编写代码的方式，内部还是通过 回调函数 来实现的异步编程
// Promise 解决了 回调地狱 的问题
```


~~~js
// Promise 的基本使用：

// 1 Promise 是一个构造函数
// 2 可以把 Promise 看作是一个容器，这个容器内部封装了异步操作

// 3 Promise的参数是一个回调函数
// 4 回调函数有两个参数
//  resolve 表示异步操作成功
//  reject 表示异步操作失败
//  也就是说：如果异步操作成功，应该调用 resolve；如果异步操作失败，应该调用 reject

const p = new Promise(function (resolve, reject) {
// 异步操作
setTimeout(() => {
  const num = Math.random()
  // 随机生成一个小于 0.5 的随机数
  if (num < 0.5) {
    resolve(num)
  } else {
    reject(num)
  }
}, 500)
})

// 使用Promise创建的对象
p
// then() 方法用来获取异步操作成功的结果
 .then(function (res) {
  console.log('成功了', res)
})
// catch 方法用来获取异步操作失败的结果
 .catch(function (err) {
  console.log('失败了', err)
})
```
~~~
  - ES6常用语法
    + 数组扩展运算符
    + 属性名表达式
    + 解构
    + promise
    + 对象中函数的简写新型
    + 箭头函数
    + 默认参数
    + 模板字符串
    + 块级作用域`let`, `const`
    + 导入导出 `export`, `import fn form "./a"`


### 3.ajax缺点， 原理
  - axax 原理
    + XMLHttpRequest以异步的方式发送HTTP请求，因此在发送请求时，一样需要遵循HTTP协议。
    + 使用户请求和服务器响应异步化，并不是所有的请求都提交给服务器，像一些数据验证和数据处理都交给Ajax引擎来完成，只有确认需要向服务器读取新数据时才右Ajax引擎向服务器提交请求。
    ```js
      //使用XMLHttpRequest发送get请求的步骤
      //1. 创建一个XMLHttpRequest对象
      var xhr = new XMLHttpRequest;//构造函数没有参数的情况,括号可以省略
      //2. 设置请求行
      //第一个参数:请求方式  get/post
      //第二个参数:请求的地址 需要在url后面拼上参数列表
      xhr.open("get", "08.php?name=hucc");
      //3. 设置请求头
      //浏览器会给我们默认添加基本的请求头,get请求时无需设置
      //4. 设置请求体
      //get请求的请求体为空,因为参数列表拼接到url后面了
      xhr.send(null);
    ```
    + get请求,设置请求行时,需要把参数列表拼接到url后面
    + get请求不用设置请求头
    + get请求的请求体为null

    + post请求,设置请求行时,参数列表不能拼接到url后面
    + post必须设置请求头中的content-type为application/x-www-form-urlencoded
    + post请求需要将参数列表设置到请求体中.

    ```js
      //给xhr注册一个onreadystatechange事件，当xhr的状态发生状态发生改变时，会触发这个事件。
      xhr.onreadystatechange = function () {
        if(xhr.readyState == 4){
          //1. 获取状态行
          console.log("状态行:"+xhr.status);
          //2. 获取响应头
          console.log("所有的相应头:"+xhr.getAllResponseHeaders());
          console.log("指定相应头:"+xhr.getResponseHeader("content-type"));
          //3. 获取响应体
          console.log(xhr.responseText);
        }
      }
      //0：请求未初始化。
      //1：请求已经建立，但是还没有开始发送。
      //2：请求已发送，正在处理中
      //3：请求在处理中；通常响应中已有部分数据可用了，但是服务器还没有完成响应的生成。
      //4：响应已完成；您可以获取并使用服务器的响应了。(我们只需要关注状态4即可)
    ```

  - ajax 缺点
    + Ajax干掉了Back与History功能，即对浏览器机制的破坏
    在动态更新页面的情况下，用户无法回到前一页的页面状态，因为浏览器仅能记忆历史纪录中的静态页面
    + 安全问题
    AJAX技术给用户带来很好的用户体验的同时也对IT企业带来了新的安全威胁，Ajax技术就如同对企业数据建立了一个直接通道。这使得开发者在不经意间会暴露比以前更多的数据和服务器逻辑。
    + 对搜索引擎支持较弱
    + 破坏程序的异常处理机制
    + 违背URL与资源定位的初衷
    + 不能很好地支持移动设备
    + 客户端肥大，太多客户段代码造成开发上的成本

### 4.深克隆，浅克隆
  - 浅拷贝：只会拷贝对象的一层属性，如果属性中还有对象，没有继续拷贝。
  - 拷贝一个对象的时候，拷贝多层，如果发现属性是对象的时候，需要继续拷贝。
  
  - 克隆节点
  ```js
//参数：deep :默认false,表示浅复制，只会复制一个标签，并不会复制内容
//     deep:  true,    表示深复制，会复制所有的内容
//克隆一个p
//会在内存中克隆一个节点， 这个节点克隆出来之后，就不会影响到原来的节点了
var newP = p.cloneNode(true);
  ```

### 5.同步异步操作
  - 同步和异步概念：
    + 同步: 指的就是事情要一件一件做。等做完前一件才能做后一件任务
    + 异步: 不受当前任务的影响，两件事情同时进行，做一件事情时，不影响另一件事情的进行。
    + 编程中：异步程序代码执行时不会阻塞其它程序代码执行,从而提升整体执行效率。

### 6.jQuery 与 Zepto 区别
  1. `width()` 和 `height()`的区别：Zepto 由盒模型（box-sizing）决定， 用`width()`返回赋值的 width，用`.css('width')`返回加的border 等结果; jQuery 会忽略盒模型，始终返回内容宽/高（不包含 padding、border ）
  2. `offset()` 区别： Zepto返回`{top,left,width,height}`; jQuery 返回 `{width,height}`。
  3. Zepto 无法获取隐藏元素的宽高 jQuery 可以
  4. Zepto 中没有原型定义extend方法而 jQuery 有
  5. 针对移动端程序，Zepto有一些基本的触摸事件可以用来做触摸屏交互（tap事件、swipe事件），Zepto是不支持IE浏览器的，就像jQuery的团队在2.0版中不再支持旧版的IE（6 7 8）一样
  6. Dom操作的区别：添加id时jQuery不会生效而Zepto会生效。（下文）
  ```js
var $insert = $('<p>Zepto 插入</p>', {
  id: 'insert-by-zepto'
})
  ```
  7. 事件委托的区别：
  ```js
    var $doc = $(document);
    $doc.on('click', '.a', function () {
        alert('a事件');
        $(this).removeClass('a').addClass('b');
    });
    $doc.on('click', '.b', function () {
        alert('b事件');
    });
    // 在Zepto中，当a被点击后，依次弹出了内容为”a事件“和”b事件“，说明虽然事件委托在.a上可是却也触发了.b上的委托。但是在 jQuery 中只会触发.a上面的委托弹出”a事件“。Zepto中，document上所有的click委托事件都依次放入到一个队列中，点击的时候先看当前元素是不是.a，符合则执行，然后查看是不是.b，符合则执行。而在jQuery中，document上委托了2个click事件，点击后通过选择符进行匹配，执行相应元素的委托事件。
  ```

  