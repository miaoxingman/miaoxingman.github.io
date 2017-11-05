## JavaScript Note-1
  
  1. javascript 可以嵌入到网页的任何地方，不过一般放在<head>中。嵌入javacript有两种方法. 
  2. javascript 中的数据类型可以通过typeof()得到，数据类型的类型为string
      a. typeof("good") === "string"
  3. javascript中的==代表自动转换数据类型之后再比较; ===则不会转换类型直接比较，如果两个数据的类型不一样也返回false.
  
  ```javascript
      2 === "2"
      false
      2 == "2"
      true
  ```
  4. javascript中的null代表一个空的值，而undefined代表值未定义.
  5. 正如其他的动态语言一样，javascript的数组中可以包含任意的数据类型.
  6. Javascript的对象是由一组key-value组成的无序集合.
  7. javascript ES6新增了一种模板字符串，可以在string中使用${}直接替换变量.
 
 	```
      name = "world";
      alert("hello ${name}");
 	```
  8. 与java和python一样，JavaScript中的字符串也是不可变的。
  9. Javascript中的对象是一组无序的key-value组合，如果判断一个属性是否属于某对象可以使用 in 或者 hasOwnProperty()， 二者的区别是使用in时候能够检查该对象继承到的属性，而hasOwnProperty()是自身的属性而不是继承得到的.
  10. Javascript中的对象的key必须是string类型，为了可以使用其他的数据类型作为key，ES6引入了Map和Set两个数据结构.
  11. 遍历Array的时候可以使用下标，但是遍历Map和Set的时候无法使用下标。为了统一集合类型，ES6引入了Iterable类型，Map、Set、Array都属于Iterable类型。具有Iterable的类型的集合可以通过for ... of 循环来遍历.
 
      a. for ... of 的好处是只会遍历实现了iterable的对象，因此即使我们动态的向一个对象插入元素也不会被遍历.
   
          i. var a = [ 'a', 'b', 'c', 'd']
          ii. for (var s of a) {
          iii. console.log(s)}
          iv. a.forEach(function (element, index, array) {
          v. console.log(element);});
  12. Javascript 允许传入任意个参数而不影响调用，因此传入的参数比定义的参数多也没有问题. Javascript中有一个关键字arguments，它只在函数内部起作用，并且永远指向当前函数调用者传入的所有参数.

      a. arguments.length 可以判断传入的参数的个数.
  13. function(a, b, ...rest) 中的reset参数只能写在最后并且用...标识。它代表将传入的arguments参数的第一个和第二个赋值给a,b; 剩余的参数赋值给rest.
  14. 在javascript中使用var定义的变量存在变量提升的问题，ES6之后应该使用let和const.
  15. 跟python类似，javascript所有的全局变量会绑定到window中.
  16. ES6之后，JavaScript支持解构赋值.
 
      a. let [x, [y, z]] = ['hello', ['world', '!']];
  17. 在一个对象中绑定函数，称为这个对象的方法。在对象的方法中可以使用this关键字访问对象的属性.
  18. 如果一个函数的变量能够接受另一个函数作为参数，这个函数就称之为高阶函数。
 
      a. javascript中的高阶函数有Array种的map(), reduce(), filter(), sort()
  
      b. javascript Array中的sort在排序的时候，将所有元素先转为string,再排序.
  19. 高阶函数除了能够接受函数作为参数外，还可以把函数作为返回结果.
      a. 这种用法常常被称为闭包，闭包用起来简单，但是实现起来并不容易。因为在闭包中使用var的循环变量或者后续会发生变化的变量，最后得到的结果都是非预期的.
  20. ES6新增了一种新的函数称为箭头函数。箭头函数相当于匿名函数.
  
      a. (x,y) => x * x  + y * y;
      
      b. 箭头函数和匿名函数的区别是箭头函数内部的this是词法作用域.
  
  21. Javascript ES6 引入了Generator, 一个generator看上去像一个函数但是可以返回多次。ES6的generator参考了python的实现，都是通过yield关键字实现。
 
      a. generator更像是一个可以记住状态的函数.
 
      b. generator另外的一个函数式将异步的回调变为同步的代码。(AJAX)
 
  22. javascript 中的一切都是对象，但是有些对象更特别。这里的特别是指出去对象类型为"number", "string", "boolen", "function", "undefined"之外的类型，他们的对象类型统一为“object”
 ```javascript
      a. typeof(null)
          i. "object"
      b. typeof(undefined)
          i. "undefined"
      c. typeof({})
          i. "object"
  ```
  23. Javascript 还提供了包装对象，类似于java中int和Integer的关系. 需要指出的是当使用包装对象的时候，string和String并不是一个类型.

      a. 一个是对象的类型是"string"，一个的对象类型是“object”
  24. rules

      a. 不要使用new Number()、new Boolean()、new String()创建包装对象；

      b. 用parseInt()或parseFloat()来转换任意类型到number；

      c. 用String()来转换任意类型到string，或者直接调用某个对象的toString()方法；

      d. 通常不必把任意类型转换为boolean再判断，因为可以直接写if (myVar) {...}；

      e. typeof操作符可以判断出number、boolean、string、function和undefined；

      f. 判断Array要使用Array.isArray(arr)；

      g. 判断null请使用myVar === null；

      h. 判断某个全局变量是否存在用typeof window.myVar === 'undefined'；

      i. 函数内部判断某个变量是否存在用typeof myVar === 'undefined'。

      j. 任何对象都有toString()方法吗？null和undefined就没有！确实如此，这两个特殊值要除外，虽然null还伪装成了object类型。

  25. Javascript Date对象中的月份从0开始.
  26. Json是JavaScript的一个子集，因此Json支持的数据类型是JavaScript的数据类型.

      a. Json的数据类型
```
          i. number, 跟Javascript的类型一致；
          ii. boolean，就是javascirpt的true or false
          iii. string，跟Javascript的类型一致
          iv. null，跟Javascript的类型一致
          v. array，跟Javascript的类型一致
          vi. object，跟Javascript的类型一致
```

      b. json的字符集必须是utf8

      c. javascript内置的JSON可以用来序列化和反序列化json字符串和JavaScript对象.
          i. JSON.stringify()
          ii. JSON.parse()
  27. Javascript中不区分类和实例的概念，而是通过原型(prototype)来实现面向对象. 每个javascript的对象都有一个原型，原型也是一个对象.
      a. Javascript 在查找属性的时候会首先在对象上面查找，如果找不到回去对象的原型上面查找，如果还没有就一直上溯找到就到Object.prototype对象，最后如果没有找到返回undefined.
          i. Arrary的原型链
              1. arr ----> Array.prototype ----> Object.prototype ----> null
          ii. 函数的原型链
              1. foo ----> Function.prototype ----> Object.prototype ----> null
      b. 构造函数.
          i. 除了直接使用{}构建一个对象之外，Javascript还可以使用一种构造函数来创建对象.
              1. function Student(name) {}
              2. var xiaoming = new Student();
  28. javascript 中的原型继承.
      a. 定义新的构造函数，并且在内部用call() 调用希望继承的构造函数.
      b. 借助中间函数F实现原型继承，最好通过封装的inherits函数.
      c. 继续在新的构造函数的原型上面定义新的方法.
  29. ES6引入了新的class关键字，因此实现对象和继承会更加容易.
      a. 类的定义.
          i. class Student { construct(name) {this.name = name};}
          ii. var xiaoming  = new Student("xiaoming")
      b. class的继承.
          i. class GoodStudent extends Student { constructor(name) {super(name}}
          ii. var good = new GoodStudent("good");
      c. ES6引入的class和原有的JavaScript原型继承有什么区别呢？实际上它们没有任何区别，class的作用就是让JavaScript引擎去实现原来需要我们自己编写的原型链代码。简而言之，用class的好处就是极大地简化了原型链代码。
  30. 浏览器与javascript
      a. 从IE10开始支持ES6
      b. Chrome内置了v8的javascript引擎，很早就支持ES6
      c. ....
  31. javascript可以获得浏览器提供的很多对象并进行操作.
      a. window 不仅仅是全局的作用域还用来表示浏览器窗口
      b. navigator 表示浏览器信息
      c. screen 表示屏幕信息
      d. location 表示当前页面的url信息.
      e. document 表示当前的页面,由于HTML在浏览器中以DOM形式表示为树状结构，document对象就是整个树的根节点.
          i. document.title = "xxx" 可以修改当前页面
          ii. document.cookie 可以获得当前页面的cookie
      f. history
          i. 保存了浏览器的历史
  32. 由于页面的HTML文档被浏览器解析只有是一棵DOM树，因此如果要改变HTML的结构，就需要使用Javascript来操作DOM.
  33. 因为DOM是一棵树，因此对HTML页面的操作就是.
      a. 更新
      b. 遍历
      c. 添加
      d. 删除
  34. 在操作DOM之前，我们需要通过各种方式拿到这个DOM接口，最常用的方法就是
      a. 直接操作DOM
          i. document.getElementById()
          ii. document.getElementByTagName()
          iii. document.getElementByClassName()
      b. 由于ID在HTML中是唯一的，所以document.getElementById()可以直接定位唯一的一个DOM节点，其他两个API总是返回一组DOM节点，要精确的选择DOM，可以先指定父节点，然后再从父节点开始选择，以缩小范围.
      c. 另外一种方法是使用querySelector()来获取节点.
  35. 拿到一个DOM节点后，我们可以对它进行更新。可以直接修改节点的文本，方法有两种,两者的区别在于读取属性时，innerText不返回隐藏元素的文本，而textContent返回所有文本。
      a. 一种是修改innerHTML属性，这个方式非常强大，不但可以修改一个DOM节点的文本内容，还可以直接通过HTML片段修改DOM节点内部的子树：
      b. 第二种是修改innerText或textContent属性，这样可以自动对字符串进行HTML编码，保证无法设置任何HTML标签：
  36. 当我们获得了某个DOM节点，想在这个DOM节点内插入新的DOM，应该如何做？如果这个DOM节点是空的，例如，<div></div>，那么，直接使用innerHTML = '<span>child</span>'就可以修改DOM节点的内容，相当于“插入”了新的DOM节点。如果这个DOM节点不是空的，那就不能这么做，因为innerHTML会直接替换掉原来的所有子节点。有两个办法可以插入新的节点.
      a. 一个是使用appendChild，把一个子节点添加到父节点的最后一个子节点
      b. 更多的时候我们会从零创建一个新的节点，然后插入到指定位置.
  37. 用javascript操作表单和操作dom时类似的，因为表单本身也是DOM树. HTML中表示表单的控件主要有.
      a. 文本框，对应的<input type="text">，用于输入文本；
      b. 口令框，对应的<input type="password">，用于输入口令；
      c. 单选框，对应的<input type="radio">，用于选择一项;
      d. 复选框，对应的<input type="checkbox">，用于选择多项；
      e. 下拉框，对应的<select>，用于选择一项；
      f. 隐藏文本，对应的<input type="hidden">，用户不可见，但表单提交时会把隐藏文本发送到服务器。
  38. Javascript操作表单.
      a. 如果我们获得了一个<input>节点的引用，就可以直接调用value获得对应的用户输入值
      b. 设置值和获取值类似，对于text、password、hidden以及select，直接设置value就可以
      c. 最后，JavaScript可以以两种方式来处理表单的提交（AJAX方式在后面章节介绍）
          i. 方式一是通过<form>元素的submit()方法提交一个表单，例如，响应一个<button>的click事件
          ii. 第二种方式是响应<form>本身的onsubmit事件，在提交form时作修改
  39. javascript操作文件.
      a. 在HTML表单中，可以上传文件的唯一控件就是<input type="file">
  40. JavaScript的一个重要的特性就是单线程执行模式。在JavaScript中，浏览器的JavaScript执行引擎在执行JavaScript代码时，总是以单线程模式执行，也就是说，任何时候，JavaScript代码都不可能同时有多于1个线程在执行。
  41. AJAX不是JavaScript的规范，它只是一个哥们“发明”的缩写：Asynchronous JavaScript and XML，意思就是用JavaScript执行异步网络请求。
      a. 传统的HTTP中，一旦用户点击“Submit”按钮开始一个Form的提交，浏览器就会刷新页面，然后在新页面里告诉你操作是成功了还是失败了。如果不幸由于网络太慢或者其他原因，就会得到一个404页面。
      b. 这就是Web的运作原理：一次HTTP请求对应一个页面。
      c. 如果要让用户留在当前页面中，同时发出新的HTTP请求，就必须用JavaScript发送这个新请求，接收到数据后，再用JavaScript更新页面，这样一来，用户就感觉自己仍然停留在当前页面，但是数据却可以不断地更新。
      d. 这就是AJAX，需要注意得是AJAX请求是异步执行的，也就是说，要通过回调函数获得响应。
  42. XMLHttpRequest
  43. Javascript默认情况下要求发送AJAX请求时，URL的域名必须跟当前的页面完全一致. 如果想完成跨域请求.
      a. 一是通过Flash插件发送HTTP请求，这种方式可以绕过浏览器的安全限制，但必须安装Flash，并且跟Flash交互。不过Flash用起来麻烦，而且现在用得也越来越少了。
      b. 二是通过在同源域名下架设一个代理服务器来转发，JavaScript负责把请求发送到代理服务器：
      c. 第三种方式称为JSONP，它有个限制，只能用GET请求，并且要求返回JavaScript。这种方式跨域实际上是利用了浏览器允许跨域引用JavaScript资源：
  44. CORS
      a. CORS全称Cross-Origin Resource Sharing，是HTML5规范定义的如何跨域访问资源。
      b. Origin表示本域，也就是浏览器当前页面的域。当JavaScript向外域（如sina.com）发起请求后，浏览器收到响应后，首先检查Access-Control-Allow-Origin是否包含本域，如果是，则此次跨域请求成功，如果不是，则请求失败，JavaScript将无法获取到响应的任何数据。


  45. Javascript中所有的代码都是异步的.
      a. setTimeout(()=> console.log("a"), 2000);
      b. setTimeout(function t() {console.log("done");}, 1000);
      c. 可见Promise最大的好处是在异步执行的流程中，把执行代码和处理结果的代码清晰地分离了：
  46. 



































