# this

this指的就是调用函数的对象。函数运行时通过环境改变 this 指向的对象，并不会生成新的对象。

* 纯粹的函数调用。this代表全局对象global。
* 作为对象的方法调用。this指的是这个对象。
* 作为构造函数调用。this指的是构造这个的新的对象。
* apply调用。this指apply函数的第一个参数（参数为空时默认为全局对象）。

把一个方法作为回调函数使用时，或把方法赋值给一个变量并调用变量时，this不能得到预期效果，因为回调函数中func是在不使用 . 语法的情况下被调用的，所以this指向全局对象。解决这个问题的标准做法是使用bind函数，bind可以创建一个this的值被绑定的函数。

this的值完全取决于一个函数式如何被调用的。

* 使用 . 语法，this指向这个对象。
* 没有用到 . 语法的话，this就是global对象。
* 使用new操作符，this指向新的对象。

### ps

arguments是js函数的一个特殊的内置变量，是一个对象。最好使用如下方式将参数提取成数组：

```javascript
var args = new Array(arguments.length);

for(var i = 0; i < args.length; ++i) {
    args[i] = arguments[i];
}
```

