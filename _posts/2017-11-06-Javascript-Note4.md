## AngularJS 

1. AngularJS是一个JavaScript的框架。它可以通过\<script\>标签添加到HTML页面中。AngularJS通过**指令**扩展HTML，且通过**表达式**绑定数据到HTML.
	* ng-directives, 扩展html.
	* ng-app 定义了一个AngularJS的应用程序, 指令在网页加载完毕时会自动引导（自动初始化）应用程序.
	* ng-model 把元素值绑定到应用程序,用于表单元素的，支持双向绑定。对普通元素无效；
	* ng-bind 把应用程序数据绑定到HTML视图,用于普通元素，不能用于表单元素，应用程序单向地渲染数据到元素；
	* ng-init 指令初始化 AngularJS 应用程序变量
	* ng-controller 定义了控制器。
	* ng-repeat 指令会重复一个 HTML 元素
		
		```javascript
			<!DOCTYPE html>
			<html>
			<head>
			<meta charset="utf-8">
			<script src="http://cdn.static.runoob.com/libs/angular.js/1.4.6/angular.min.js"></script> 
			</head>
			<body>
			
			<p>尝试修改以下表单。</p>		
			<div ng-app="myApp" ng-controller="myCtrl">
			名: <input type="text" ng-model="firstName"><br>
			姓: <input type="text" ng-model="lastName"><br>
			<br>
			姓名: {{firstName + " " + lastName}}
			</div>
			<script>
			var app = angular.module('myApp', []);
			app.controller('myCtrl', function($scope) {
			    $scope.firstName= "John";
			    $scope.lastName= "Doe";
			});
			</script>
			</body>
			</html>
		```

2. AngularJS 表达式写在双大括号内：{{ expression }}.AngularJS 表达式把数据绑定到 HTML，这与 ng-bind 指令有异曲同工之妙。AngularJS 中的数据绑定，同步了 AngularJS 表达式与 AngularJS 数据。{{ firstName }} 是通过 ng-model="firstName" 进行同步。

3. 除了 AngularJS 内置的指令外，我们还可以创建自定义指令。
你可以使用 .directive 函数来添加自定义的指令。要调用自定义指令，HTML元素上需要添加自定义指令名。使用驼峰法来命名一个指令， runoobDirective, 但在使用它时需要以 - 分割, runoob-directive:

	```html
	<!DOCTYPE html>
	<html>
	<head>
	<meta charset="utf-8">
	<script src="http://cdn.static.runoob.com/libs/angular.js/1.4.6/angular.min.js"></script> 
	</head>
	<body ng-app="myApp">
	<runoob-directive></runoob-directive>
	<script>
	var app = angular.module("myApp", []);
	app.directive("runoobDirective", function() {
	    return {
	        template : "<h1>自定义指令!</h1>"
	    };
	});
	</script>
	</body>
	</html>
	```
4. AngularJS应用组成分为View即HTML，Model即视图中的可用数据，Controller即Javascript函数，可以添加或者修改属性.

5. AngularJS可以指定一个作用域.所有的应用都有一个$rootScope，它可以作用在 ng-app 指令包含的所有 HTML 元素中。$rootScope 可作用于整个应用中。是各个 controller 中 scope 的桥梁。用 rootscope 定义的值，可以在各个 controller 中使用。

	```javascript
	<div ng-app="myApp" ng-controller="myCtrl">
	<ul>
	    <li ng-repeat="x in names">{{x}}</li>
	</ul>
	</div>
	<script>
	var app = angular.module('myApp', []);
	app.controller('myCtrl', function($scope) {
	    $scope.names = ["Emil", "Tobias", "Linus"];
	});
	</script>
	```
6. 在大型的应用程序中，通常是把控制器存储在外部文件中。只需要把 \<script\> 标签中的代码复制到名为 personController.js 的外部文件中即可：

	```javascript
	<div ng-app="myApp" ng-controller="personCtrl">
		First Name: <input type="text" ng-model="firstName"><br>
		Last Name: <input type="text" ng-model="lastName"><br>
		<br>
		Full Name: {{firstName + " " + lastName}}
	</div>
	<script src="personController.js"></script>
	```

7. 过滤器可以使用一个管道字符（|）添加到表达式和指令中。如下代码会将名字自动转化为小写字母.

	```
	<div ng-app="myApp" ng-controller="personCtrl">
	<p>姓名为 {{ lastName | uppercase }}</p>
	</div>
	```
	以下实例自定义一个过滤器 reverse，将字符串反转：
	
	```javascript
	<!DOCTYPE html>
	<html>
	<meta charset="utf-8">
	<script src="http://cdn.static.runoob.com/libs/angular.js/1.4.6/angular.min.js"></script>
	<body>
	<div ng-app="myApp" ng-controller="myCtrl">
	姓名: {{ msg | reverse }}
	</div>
	<script>
	var app = angular.module('myApp', []);
	app.controller('myCtrl', function($scope) {
	    $scope.msg = "Runoob";
	});
	app.filter('reverse', function() { //可以注入依赖
	    return function(text) {
	        return text.split("").reverse().join("");
	    }
	});
	</script>
	</body>
	</html>
	```
8. AngularJS 中你可以创建自己的服务，或使用内建服务。在 AngularJS 中，服务是一个函数或对象，可在你的 AngularJS 应用中使用。这些服务可以获取到Angular应用声明周期的每一个阶段，并且和$watch整合，让Angular可以监控应用，处理事件变化。普通的DOM对象则不能在Angular应用声明周期中和应用整合。
	* $http 是 AngularJS 应用中最常用的服务。 服务向服务器发送请求，应用响应服务器传送过来的数据。
	* AngularJS $timeout 服务对应了 JS window.setTimeout 函数。
	* AngularJS $interval 服务对应了 JS window.setInterval 函数。
	* 你可以创建自定义服务，链接到你的模块中：

	```javascript
	<!DOCTYPE html>
	<html>
	<head>
	<meta charset="utf-8">
	<script src="http://cdn.static.runoob.com/libs/angular.js/1.4.6/angular.min.js"></script>
	</head>
	<body>
	<div ng-app="myApp" ng-controller="myCtrl">
	<p>255 的16进制是:</p>
	<h1>{{hex}}</h1>
	</div>
	
	<p>自定义服务，用于转换16进制数：</p>
	<script>
	var app = angular.module('myApp', []);
	app.service('hexafy', function() {
		this.myFunc = function (x) {
	        return x.toString(16);
	    }
	});
	app.controller('myCtrl', function($scope, hexafy) {
	  $scope.hex = hexafy.myFunc(255);
	});
	</script>
	</body>
	</html>
	```
9. $http 是 AngularJS 中的一个核心服务，用于读取远程服务器的数据。
	* $http.get('/someUrl', config).then(successCallback, errorCallback);
	* $http.post('/someUrl', data, config).then(successCallback, errorCallback);

10. 在 AngularJS 中我们可以使用 ng-option 指令来创建一个下拉列表，列表项通过对象和数组循环输出。我们也可以使用ng-repeat 指令来创建下拉列表.
11. AngularJS表格.

	```javascript
	<div ng-app="myApp" ng-controller="customersCtrl"> 
	<table>
	  <tr ng-repeat="x in names">
	    <td>{{ x.Name }}</td>
	    <td>{{ x.Country }}</td>
	  </tr>
	</table>
	```
12. AngularJS 为 HTML DOM 元素的属性提供了绑定应用数据的指令。
	* ng-disabled 指令直接绑定应用程序数据到 HTML 的 disabled 属性。
	* ng-show 指令隐藏或显示一个 HTML 元素。
	* ng-hide 指令用于隐藏或显示 HTML 元素。

13. AngularJS 有自己的 HTML 事件指令.
	* ng-click 指令定义了 AngularJS 点击事件。

14. AngularJS 模块, 模块定义了一个应用程序。模块是应用程序中不同部分的容器。
模块是应用控制器的容器。控制器通常属于一个模块。
	* 你可以通过 AngularJS 的 angular.module 函数来创建模块。
	* JavaScript 中应避免使用全局函数。因为他们很容易被其他脚本文件覆盖。AngularJS 模块让所有函数的作用域在该模块下，避免了该问题。

15. AngularJS 表单是输入控件的集合.

16. AngularJS 全局 API 用于执行常见任务的 JavaScript 函数集合。

17. AngularJS 的首选样式表是 Twitter Bootstrap， Twitter Bootstrap 是目前最受欢迎的前端框架。

18. 依赖注入（Dependency Injection，简称DI）是一种软件设计模式，在这种模式下，一个或更多的依赖（或服务）被注入（或者通过引用传递）到一个独立的对象（或客户端）中，然后成为了该客户端状态的一部分。该模式分离了客户端依赖本身行为的创建，这使得程序设计变得松耦合，并遵循了依赖反转和单一职责原则。与服务定位器模式形成直接对比的是，它允许客户端了解客户端如何使用该系统找到依赖.AngularJS 提供很好的依赖注入机制。以下5个核心组件用来作为依赖注入：
	* value
	* factory
	* service
	* provider
	* constant
19. AngularJS 路由允许我们通过不同的 URL 访问不同的内容。通过 AngularJS 可以实现多视图的单页Web应用（single page web application，SPA）。通常我们的URL形式为 http://runoob.com/first/page，但在单页Web应用中 AngularJS 通过 # + 标记 实现.

	当我们点击以上的任意一个链接时，向服务端请的地址都是一样的 (http://runoob.com/)。 因为 # 号之后的内容在向服务端请求时会被浏览器忽略掉。 所以我们就需要在客户端实现 # 号后面内容的功能实现。 AngularJS 路由 就通过 # + 标记 帮助我们区分不同的逻辑页面并将不同的页面绑定到对应的控制器上。




















