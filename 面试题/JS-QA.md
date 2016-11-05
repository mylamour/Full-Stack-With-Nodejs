#### JS 相关问题：

* 请解释事件代理 (event delegation)。
* 请解释 JavaScript 中 `this` 是如何工作的。

> 当一个函数被调用的时候会激活一个记录(record)，也就是指一个执行环境的上下文语境被创建了。这条记录包含着这个函数从哪被调用( 从调用栈)，怎么被调用的，传递了什么参数等等。记录中的一个属性叫做this,而它将在整个函数的执行期间起到了相对的参考作用。

> To learn this, you first have to learn what this is not, despite any assumptions or misconceptions that may lead you down those paths.<font color="green"> this is neither a reference to the function itself, nor is it a reference to the function's lexical scope. </font>

>>[You-Dont-Know-JS](https://github.com/getify/You-Dont-Know-JS)详细请看You-Dont-Know-JS系列的this&object这本书

* 请解释原型继承 (prototypal inheritance) 的原理。

> 
```js 
function getProperty(obj, prop) {
    if (obj.hasOwnProperty(prop))
        return obj[prop]
    else if (obj.__proto__ !== null)
        return getProperty(obj.__proto__, prop)
    else
        return undefined
}
```
> 
```js
Object.create = function (parent) {
  function F() {}
  F.prototype = parent;
  return new F();
};
```

> 递归查询，向上面遍历是否存在这个属性。
>>[how-prototypal-inheritance-really-works](http://blog.vjeux.com/2011/javascript/how-prototypal-inheritance-really-works.html)

* 你怎么看 AMD vs. CommonJS？
* 请解释为什么接下来这段代码不是 IIFE (立即调用的函数表达式)：`function foo(){ }();`

> 
```js
var foo = fucntion(){};
var test = new foo();
```

* 要做哪些改动使它变成 IIFE?

* 描述以下变量的区别：`null`，`undefined` 或 `undeclared`？

> 
1. undeclared是没有使用var声明的，不能在strict模式下使用，否则会报错。(通常的建议是写代码时使用`'use strict';`)
2. undefined 是 `var funnyUndefine;` 
3. null 是定义成null的值。`var funnyDefined = null;` 

>> [JS: null, undefined, and undeclared](http://lucybain.com/blog/2014/null-undefined-undeclared/)

>> [var](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var)

* 该如何检测它们？

> 使用typeof去判断某个值是否为`null`，或`undefined`,或者直接判断是否为`null`
```js
if (typeof(some_variable) != 'undefined' && some_variable != null)
{
    // Do something with some_variable
}
if(some_variable != null){
	// Do something with some_variable
}
```

> 当你用`if (something == null) { someAction }`判断时，`undefined`和`null`都将会进入并执行Action

> [How to check it](http://stackoverflow.com/questions/2559318/how-to-check-for-an-undefined-or-null-variable-in-javascript)


* 什么是闭包 (closure)，如何使用它，为什么要使用它？

> Closure是Lexical Closure的简称。在函数内部再定义一个函数，以方便外部变量可以取到局部变量

* 请举出一个匿名函数的典型用例？

> 
```js
Persons.updata(codition,updata,fun(err,data){
	if (err) throw err;
	if (data&&data.length!=0&&data.nModified!=0){
		console.log("Updata Sucess");
	}
})
```

* 你是如何组织自己的代码？是使用模块模式，还是使用经典继承的方法？

> 

* 请指出 JavaScript 宿主对象 (host objects) 和原生对象 (native objects) 的区别？

> 宿主对象是执行环境支持的一些对象，原生对象是由ECMAScipt实现的，不由宿主环境来决定的。一些原生对象是内置的，一些是执行过程中解析生成的(Some native objects are built-in; others may be constructed during the course of execution of an ECMAScript program.)

>>[介绍](http://www.cnblogs.com/viphchok/articles/5403879.html)
>>[difference](http://stackoverflow.com/questions/7614317/what-is-the-difference-between-native-objects-and-host-objects)

* 请指出以下代码的区别：`function Person(){}`、`var person = Person()`、`var person = new Person()`？

> `function Person(){}`     		传递参数为空的Person函数
> `var person = Person()`   		把函数赋值给person
> `var person = new Person()` 		实例化Person函数


* `.call` 和 `.apply` 的区别是什么？
 
> `.call()`接收的是若干个参数的列表, `.apply()`接收的是一个包含多个参数的数组。当你参数明确的时候，就用`.call()`,参数不明确的时候用`.apply()`  


* 请解释 `Function.prototype.bind`？

* 在什么时候你会使用 `document.write()`？

* 请指出浏览器特性检测，特性推断和浏览器 UA 字符串嗅探的区别？

* 请尽可能详尽的解释 Ajax 的工作原理。

> 
```js
function ajaxFunction() {  
            var xmlHttp = false;  
            try {  
                xmlHttp = new ActiveXObject("Msxml2.XMLHTTP"); // ie msxml3.0+（IE7.0及以上）  
            } catch (e) {  
                try {  
                    xmlHttp = new ActiveXObject("Microsoft.XMLHTTP"); //ie msxml2.6（IE5/6）  
                } catch (e2) {  
                    xmlHttp = false;  
                }  
            }  
            if (!xmlHttp && typeof XMLHttpRequest != 'undefined') {// Firefox, Opera 8.0+, Safari  
                xmlHttp = new XMLHttpRequest();  
            }  
            return xmlHttp;  
        }
```  
> DOM Dynamic updating of a loaded page
> XML Data exchange format
> XSLT Transforms XML into XHTML
> XMLHttp Primary communication
> JavaScript scripting language used to program an Ajax engine.


* 使用 Ajax 都有哪些优劣？

> 优势：
>>1.节省了浏览器和服务器资源，避免重复加载无关的内容
>>2.由于不必重复的刷新，用户不会感受到明显的延时。因此用户体验较好
>>3.不用下载第三方插件，用着很方便

> 劣势:	
>> 1. 破坏了后退的机制
>> 2.搜索引擎的支持不友好，SEO劣势
>> 3.安全问题

> [Ajax优缺点](http://www.cnblogs.com/mingmingruyuedlut/archive/2011/10/18/2216553.html)

* 请解释 JSONP 的工作原理，以及它为什么不是真正的 Ajax。

* 你使用过 JavaScript 模板系统吗？

  * 如有使用过，请谈谈你都使用过哪些库？

* 请解释变量声明提升 (hoisting)。

* 请描述事件冒泡机制 (event bubbling)。

* "attribute" 和 "property" 的区别是什么？

* 为什么扩展 JavaScript 内置对象不是好的做法？

* 请指出 document load 和 document DOMContentLoaded 两个事件的区别。

* `==` 和 `===` 有什么不同？

> 
```js
var a = 2;
var b = '2';
a == b // true
a ===b // flase
> 
`==`只比较字面值是否相等，而不比较类型值是否相等,`===`则是必须完全相等，不仅是值，而且还包括类型。 
 
* 请解释 JavaScript 的同源策略 (same-origin policy)。

* 如何实现下列代码：

```javascript
[1,2,3,4,5].duplicator(); // [1,2,3,4,5,1,2,3,4,5]
```
* 什么是三元表达式 (Ternary expression)？“三元 (Ternary)” 表示什么意思？

> 三元代表三个变量 `a > b ? c=a : c=b`  等于 `if (a > b){c=a}else{c=b}`

* 什么是 `"use strict";` ? 使用它的好处和坏处分别是什么？
* 请实现一个遍历至 `100` 的 for loop 循环，在能被 `3` 整除时输出 **"fizz"**，在能被 `5` 整除时输出 **"buzz"**，在能同时被 `3` 和 `5` 整除时输出 **"fizzbuzz"**。
* 为何通常会认为保留网站现有的全局作用域 (global scope) 不去改变它，是较好的选择？
* 为何你会使用 `load` 之类的事件 (event)？此事件有缺点吗？你是否知道其他替代品，以及为何使用它们？
* 请解释什么是单页应用 (single page app), 以及如何使其对搜索引擎友好 (SEO-friendly)。
* What is the extent of your experience with Promises and/or their polyfills?
* 使用 Promises 而非回调 (callbacks) 优缺点是什么？
* 使用一种可以编译成 JavaScript 的语言来写 JavaScript 代码有哪些优缺点？
* 你使用哪些工具和技术来调试 JavaScript 代码？
* 你会使用怎样的语言结构来遍历对象属性 (object properties) 和数组内容？
* 请解释可变 (mutable) 和不变 (immutable) 对象的区别。
  * 请举出 JavaScript 中一个不变性对象 (immutable object) 的例子？
  * 不变性 (immutability) 有哪些优缺点？
  * 如何用你自己的代码来实现不变性 (immutability)？
* 请解释同步 (synchronous) 和异步 (asynchronous) 函数的区别。
* 什么是事件循环 (event loop)？
  * 请问调用栈 (call stack) 和任务队列 (task queue) 的区别是什么？
* 解释 `function foo() {}` 与 `var foo = function() {}` 用法的区别


* 请解释为什么使用href = "javescript:void(0)"而非href = "#"



