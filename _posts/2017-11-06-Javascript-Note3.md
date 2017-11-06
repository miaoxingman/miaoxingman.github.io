## ECMAScript6 - Note 1

1. ECMAScript是JavaScript的规格，JavaScript是ECMAScript的一种实现.

2. ES6 是一个历史名词也是一个泛指。含义是5.1版本之后的JavaScript下一代标准，涵盖ES2015, ES2016, ES2017. ECMAScript标准在每年的6月份正式发布一次，作为当年的正式版本。接下来的时间，就在这个版本的基础上做改动，直到下一年的6月份，草案就自然变成了新一年的版本。这样一来，就不需要以前的版本号了，只要用年份标记就可以了。

3. Babel是一个广泛使用的ES6转码器，可以将ES6的代码转换为ES5的代码。Babel提供了很多的plugin用来转码语法、API以及设置对某些后缀类型进行转码.

4. ES5中只有两种声明变量的方法，var和function. ES6中添加了let, const, classl import。做出这些改变的原因是var命令会发生变量提升现象。即变量可以在声明之前使用，值为undefined。这种现象多多少少是有些奇怪的，按照一般的逻辑，变量应该在声明语句之后才可以使用。ES5的另一个缺陷是只存在全局作用域和函数作用域，没有块级作用域，这样子会造成内层的变量会覆盖外层变量，以及for循环变量泄露为全局变量等问题。ES6则明确规定如果区块中存在let和const命令，这个区块对这些命令声明的变量，从一开始就形成了封闭作用域。凡是在声明之前就使用这些变量，就会报错。总之，在代码块内，使用let命令声明变量之前，该变量都是不可用的。这在语法上，称为“暂时性死区”（temporal dead zone，简称 TDZ）。

5. 下面代码中，变量i是let声明的，当前的i只在本轮循环有效，所以每一次循环的i其实都是一个新的变量，所以最后输出的是6。你可能会问，如果每一轮循环的变量i都是重新声明的，那它怎么知道上一轮循环的值，从而计算出本轮循环的值？这是因为 JavaScript 引擎内部会记住上一轮循环的值，初始化本轮的变量i时，就在上一轮循环的基础上进行计算。

	```javascript
	var a = [];
	for (let i = 0; i < 10; i++) {
	  a[i] = function () {
	    console.log(i);
	  };
	}
	a[6](); // 6
	```
6. ES6允许按照一定的模式，从数组和对象中提取值，对变量进行赋值，这种操作被称为解构赋值。只要某种数据结构具有 Iterator 接口，都可以采用数组形式的解构赋值。解构赋值的用途有，交换变量、从函数返回多个值、函数参数的定义、提出json数据、函数参数的默认值、遍历map.

	```javascript
	const book = new Map();
	book["beijing"] = 10086;
	book["shanhai"] = 20086;
	book.set("1", "good");
	book.set("2", "bad");
	for (let [k,v] of book) {
	    alert(`${k} = ${v}`);
	}
	```
	``` javascript
	function test_return() {
	    return ["hello", "world", "how are you"];
	}
	undefined
	[a1, a2, a3] =test_return();
	(3) ["hello", "world", "how are you"]
	```

7. ES5如果unicode码点大于一定的范围会引起显示问题，而ES6则规定只要将码点放入大括号就可以正确的解读该字符.
	> "\u{20BB7}" "𠮷"

8. ES6为字符串添加了遍历器接口，使得字符串可以被for...of循环遍历。除了遍历字符串，这个遍历器最大的优点是可以识别大于0xFFFF的码点，传统的for循环无法识别这样的码点。

9. 传统上，JavaScript只有indexOf方法，可以用来确定一个字符串是否包含在另一个字符串中。ES6又提供了三种新方法。
	* includes()：返回布尔值，表示是否找到了参数字符串。
	* startsWith()：返回布尔值，表示参数字符串是否在原字符串的头部。
	* endsWith()：返回布尔值，表示参数字符串是否在原字符串的尾部。

10. 模板字符串（template string）是增强版的字符串，用反引号（`）标识。它可以当作普通字符串使用，也可以用来定义多行字符串，或者在字符串中嵌入变量。

	``` javascript
	fn  = new Function(`console.log("good");`);
	fn();
	```
11. ES6的正则表达式.
	* http://es6.ruanyifeng.com/#docs/regex

12. 数值的扩展
	* ES6 提供了二进制和八进制数值的新的写法，分别用前缀0b（或0B）和0o（或0O）表示。
	* ES6 在Number对象上，新提供了Number.isFinite()和Number.isNaN()两个方法。
	* ES6 将全局方法parseInt()和parseFloat()，移植到Number对象上面，行为完全保持不变。
	* Number.isInteger()用来判断一个值是否为整数。需要注意的是，在 JavaScript 内部，整数和浮点数是同样的储存方法，所以3和3.0被视为同一个值。
	* ES6 在Number对象上面，新增一个极小的常量Number.EPSILON。根据规格，它表示1与大于1的最小浮点数之间的差。

13. ES6 函数的扩展
	* ES6 允许为函数的参数设置默认值，即直接写在参数定义的后面。
	* 参数变量是默认声明的，所以不能用let或const再次声明。
	
		```javascript
		function Point(x = 0, y = 0) {
		    this.x = x;
		    this.y = y;
		}
		const p = new Point();
		const q = newPoint(1.0, 2.0);
		```
	* 从 ES5 开始，函数内部可以设定为严格模式

		```
		function doSomething(a, b) {
			'use strict';
			 // code
		}
		```
	* 箭头函数可以绑定this对象，大大减少了显式绑定this对象的写法（call、apply、bind)
	* 尾调用（Tail Call）是函数式编程的一个重要概念，本身非常简单，一句话就能说清楚，就是指某个函数的最后一步是调用另一个函数。

		``` javascript
		function f(x){
		  return g(x);
		}
		```
14. 尾调用之所以与其他调用不同，就在于它的特殊的调用位置。 我们知道，函数调用会在内存形成一个“调用记录”，又称“调用帧”（call frame），保存调用位置和内部变量等信息。如果在函数A的内部调用函数B，那么在A的调用帧上方，还会形成一个B的调用帧。等到B运行结束，将结果返回到A，B的调用帧才会消失。如果函数B内部还调用函数C，那就还有一个C的调用帧，以此类推。所有的调用帧，就形成一个“调用栈”（call stack）。 尾调用由于是函数的最后一步操作，所以不需要保留外层函数的调用帧，因为调用位置、内部变量等信息都不会再用到了，只要直接用内层函数的调用帧，取代外层函数的调用帧就可以了。
	* 这就叫做“尾调用优化”（Tail call optimization），即只保留内层函数的调用帧。如果所有函数都是尾调用，那么完全可以做到每次执行时，调用帧只有一项，这将大大节省内存。这就是“尾调用优化”的意义。

15. 函数调用自身，称为递归。如果尾调用自身，就称为尾递归。递归非常耗费内存，因为需要同时保存成千上百个调用帧，很容易发生“栈溢出”错误（stack overflow）。但对于尾递归来说，由于只存在一个调用帧，所以永远不会发生“栈溢出”错误。非尾递归的 Fibonacci 数列实现如下。

	```javascript
	function Fibonacci (n) {
	  if ( n <= 1 ) {return 1};
	  return Fibonacci(n - 1) + Fibonacci(n - 2);
	}
	
	Fibonacci(10) // 89
	Fibonacci(100) // 堆栈溢出
	Fibonacci(500) // 堆栈溢出
	```
	尾递归优化过的 Fibonacci 数列实现如下。

	```javascript
	function Fibonacci2 (n , ac1 = 1 , ac2 = 1) {
	  if( n <= 1 ) {return ac2};
	  return Fibonacci2 (n - 1, ac2, ac1 + ac2);
	}
	
	Fibonacci2(100) // 573147844013817200000
	Fibonacci2(1000) // 7.0330367711422765e+208
	Fibonacci2(10000) // Infinity
	```
	由此可见，“尾调用优化”对递归操作意义重大，所以一些函数式编程语言将其写入了语言规格。ES6 是如此，第一次明确规定，所有 ECMAScript 的实现，都必须部署“尾调用优化”。这就是说，ES6 中只要使用尾递归，就不会发生栈溢出，相对节省内存。

16. 数组的扩展
	* 数组是复合的数据类型，直接复制的话，只是复制了指向底层数据结构的指针，而不是克隆一个全新的数组。
	* 扩展运算符提供了数组合并的新写法。
	* Array.of方法用于将一组值，转换为数组
	* Array.from方法用于将两类对象转为真正的数组：类似数组的对象（array-like object）和可遍历（iterable）的对象（包括ES6新增的数据结构Set和Map）
	* 数组实例的find方法，用于找出第一个符合条件的数组成员。它的参数是一个回调函数，所有数组成员依次执行该回调函数，直到找出第一个返回值为true的成员，然后返回该成员。如果没有符合条件的成员，则返回undefined。 









