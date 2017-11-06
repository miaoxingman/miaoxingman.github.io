## JavaScript Note2 - jQuery

1. jQuery 是使用非常广泛的一个库，它的主要用途为.
  	* 消除浏览器差异：你不需要自己写冗长的代码来针对不同的浏览器来绑定事件，编写AJAX等代码；
  	* 简洁的操作DOM的方法：写$('#test')肯定比document.getElementById('test')来得简洁；
  	* 轻松实现动画、修改CSS等各种操作。

2. 目前jQuery有1.x和2.x两个主要版本，区别在于2.x移除了对古老的IE 6、7、8的支持，因此2.x的代码更精简。选择哪个版本主要取决于你是否想支持IE 6~8。从jQuery官网可以下载最新版本。jQuery只是一个jquery-xxx.js文件，但你会看到有compressed（已压缩）和uncompressed（未压缩）两种版本，使用时完全一样，但如果你想深入研究jQuery源码，那就用uncompressed版本。

3. $是著名的jQuery符号。实际上，jQuery把所有功能全部封装在一个全局变量jQuery中，而$也是一个合法的变量名，它是变量jQuery的别名：
	* window.jQuery === $ (true)

4. 选择器是jQuery的核心。一个选择器写出来类似$('#dom-id')。
	* 如果是某个DOM节点有id属性，jQuery查找如下 var div = $('#abc')
	* 如果按照tag查找，则只需要写上tag名就好. var tag = $('p')
	* 如果是按照class查找，则需要再class之前添加一个. var class = $('.red')
	* 还可以按照属性查找. var email = $('[name=email]')
		* var icons = $('[name\^=icon]') 所有name属性以icon开头的DOM
		* var names = $('[name$=with]') 所有name属性以with结尾的DOM
	* 组合查找
		* var tr = $('tr.red') 找出<tr class='red...'> ... </tr>
	* 多项查找
		* $(p, div) 把所有的<p> 和 <div>都找出来.
	* 层级选择器. $('ul.lang li');
	* 过滤器
		* $('ul.lang li : first-child');

5. jQuery对象的text()和html()方法分别获取节点的文本和原始HTML文本, 可以使用这两个API直接修改HTML.

6. 要高亮显示动态语言，调用jQuery对象的css('name', 'value')方法
	* ('#test-css li.dy>span').css('background-color', '#ffd351').css('color', 'red');

7. 显示和隐藏DOM元素使用非常普遍，jQuery直接提供show()和hide()方法.

8. 对于表单元素，jQuery对象统一提供val()方法获取和设置对应的value属性.

9. 要添加新的DOM节点，除了通过jQuery的html()这种暴力方法外，还可以用append()方法.

10. 要删除DOM节点，拿到jQuery对象后直接调用remove()方法就可以了

11. 因为JavaScript在浏览器中以单线程模式运行，页面加载后，一旦页面上所有的JavaScript代码被执行完后，就只能依赖触发事件来执行JavaScript代码。浏览器在接收到用户的鼠标或键盘输入后，会自动在对应的DOM节点上触发相应的事件。如果该节点已经绑定了对应的JavaScript处理函数，该函数就会自动调用。由于不同的浏览器绑定事件的代码都不太一样，所以用jQuery来写代码，就屏蔽了不同浏览器的差异，我们总是编写相同的代码。
	* $('#test-link').on('click', function() {console.log('clicked');});

12. jQuery能够绑定的事件主要包括.
	* 鼠标事件
		* click: 鼠标单击时触发；
		* dblclick：鼠标双击时触发；
		* mouseenter：鼠标进入时触发
		* mouseleave：鼠标移出时触发
		* mousemove：鼠标在DOM内部移动时触发
		* hover：鼠标进入和退出时触发两个函数，相当于mouseenter加上mouseleave。
	* 键盘事件
		* 键盘事件仅作用在当前焦点的DOM上，通常是\<input\>和\<textarea\>
		* keydown：键盘按下时触发
		* keyup：键盘松开时触发
		* keypress：按一次键后触发。
	* 其他事件
		* focus：当DOM获得焦点时触发
		* blur：当DOM失去焦点时触发
		* change：当\<input\>、\<select\>或\<textarea\>的内容改变时触发
		* submit：当\<form\>提交时触发
		* ready：当页面被载入并且DOM树完成初始化后触发。
	* 有些事件，如mousemove和keypress，我们需要获取鼠标位置和按键的值，否则监听这些事件就没什么意义了。所有事件都会传入Event对象作为参数，可以从Event对象上获取到更多的信息
	* 一个已被绑定的事件可以解除绑定，通过off('click', function)实现
		* 可以使用off('click')一次性移除已绑定的click事件的所有处理函数
		* 无参数调用off()一次性移除已绑定的所有类型的事件处理函数。
	* 一个需要注意的问题是，事件的触发总是由用户操作引发的,当用户在文本框中输入时，就会触发change事件。但是，如果用JavaScript代码去改动文本框的值，将不会触发change事件.有些时候，我们希望用代码触发change事件，可以直接调用无参数的change()方法来触发该事件.

13. 用JavaScript实现动画，原理非常简单：我们只需要以固定的时间间隔（例如，0.1秒），每次把DOM元素的CSS样式修改一点（例如，高宽各增加10%），看起来就像动画了。

14. 用Javascript写AJAX要考虑各个浏览器的兼容性，而用jQuery则不需要。jQuery在全局对象jQuery（也就是$）绑定了ajax()函数，可以处理AJAX请求。ajax(url, settings)函数需要接收一个URL和一个可选的settings对象，常用的选项如下：
	* async 是否异步执行AJAX请求，默认为true，千万不要指定为false；
	* method 发送的Method，缺省为'GET'，可指定为'POST'、'PUT'等；
	* contentType 发送POST请求的格式，默认值为'application/x-www-form-urlencoded; charset=UTF-8'，也可以指定为text/plain、application/json；
	* data 发送的数据，可以是字符串、数组或object。如果是GET请求，data将被转换成query附加到URL上，如果是POST请求，根据contentType把data序列化成合适的格式
	* headers 发送的额外的HTTP头，必须是一个object；
	* dataType 接收的数据格式，可以指定为'html'、'xml'、'json'、'text'等，缺省情况下根据响应的Content-Type猜测。

15. 可以利用Promise跟$.ajax()结合从而优雅的处理成功和失败的各种情况.
16. 对常用的AJAX操作，jQuery提供了一些辅助方法。
	* get
	* post
	* getJSON
17. 扩展jQuery或者编写jQuery插件的方法是给jQuery绑定一个新的方法.
	* $.fn.highlight1 = function {return this;};
	* return this 的原因是为了支持链式操作.














