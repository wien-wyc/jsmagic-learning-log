# 函数和lodash

### 函数

当返回值是一个函数，则函数内部的变量作用域仅仅在该函数内部，外部无法使用。函数式一种特殊的对象，可以给函数添加属性，但是有两个属性是不能改的，name和length，前者返回函数的名字，后者返回该函数接受的参数的数量。如果一个变量所在的作用域离当前作用域更近，那么它会遮盖掉离得更远的作用域里面的同名变量，这被称为“变量遮盖“。

[MDN - 闭包](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Closures) [作用域与闭包](https://github.com/alsotang/node-lessons/tree/master/lesson11)

### lodash

once函数比较简单，关键在于要缓存原来的计算结果，且不能将结果存在最内层的计算函数中。memoize函数一开始没有理解，教程中举的例子容易造成误解，到后来才理解只是缓存了多次调用的结果。然后增加的第二个参数的意思是以此函数的返回值作为缓存的key缓存结果，而不是单单用传入的参数作为缓存的key值。代码如下：

```javascript
const _ = {
	'once': function(fun) {
		let result;
		return function() {
			if (!fun.mark) {
				fun.mark = true;
				result = fun();
			}
			return result;
		}
	},
	'memoize': function(fun, cache_fun) {
		let result;
		let arg_result = {}; 
		return function(arg) {
			let key = arg;
			if (cache_fun) {
				key = cache_fun(arg);
			}
			if (key in arg_result) {
				result = arg_result[key];
			} else {
				result = fun(arg);
				arg_result[key] = result;
			}
			return result;
		}
	}
};

module.exports = _;
```

