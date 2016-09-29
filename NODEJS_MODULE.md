# 模块化JavaScript

### CommonJS

NodeJs采用CommonJS作为模块系统。[JavaScript ES6 模块指南](https://segmentfault.com/a/1190000004100661)

* 使用require来加载一个模块，与ES6的import一样。
* 使用module.exports导出模块，与ES6的export一样。

CommonJS中每一个文件都是一个模块，这是一个导出了doSomething函数的模块：

```javascript
// (function (module)
{module.exports = function doSomething() {}
// })(...)
```

这就像把代码包裹在一个闭包里，然后把对象module作为参数传递进去一样。

CommonJS的模块名就是文件名，使用require加载一个文件时，会返回模块的module.exports。[exports 和 module.exports 的区别](https://cnodejs.org/topic/5231a630101e574521e45ef8)

### ES6

使用ES6的导出时，需要在（变量，类，函数）定义前加上export关键字：

```javascript
export const foo = "foo";
import {foo} from "./constants";
```

这两个变量（foo）在import和export中必须一致。当我们使用babel命令来转译export文件时，会发现Babel给这个模块添加了__esModule属性，这是用来改善 ES6 模块和 CommonJS 模块之间的兼容性的。ES6可以使用default关键字作为默认导出,导入默认导出的值则可以改变变量名，因为default已经被用作关键字了:

```javascript
export default "foo";
import answer from "./constants";
```

还有一种通配符导入import * as fs from "fs";

### 兼容性

ES6和CommonJS大部分情况都是相互兼容的。引入NodeJS中的fs文件系统模块时，可以这样被加载：const fs = require("fs");使用Babel也可以用默认导入的方法加载fs模块：import fs from "fs";但是import fs真正访问的是模块的default属性，即默认导出。Babel会通过__esModule属性检查一个模块是不是ES6模块，如果不是，Babel会通过这样一个函数：

```javascript
function _interopRequireDefault(obj) {
  return obj.__esModule ? obj : { default: obj };
}
```

将这个（CommonJS）模块包裹起来达到这样的效果：const fs = {default: require("fs")};

### Webpack

[Webpack](http://webpack.github.io/)可以将 CommonJS 项目转换成浏览器可读的普通 JavaScript，有很多 [功能](http://webpack.github.io/docs/) 和 [配置项](http://webpack.github.io/docs/configuration.html) ，主要做了这些事：

* 将所有 CommonJS 模块收集到一个文件里
* 在浏览器中提供一个假的 require 函数
* 保证每个模块只执行一次，且按照正确的顺序
* 将 ES6/JSX 转换为 ES3（标准的 JavaScript）

为了把 ES6/JSX 转换为 ES3，我们还需要安装 Webpack 的 Babel 加载器 （babel-loader)

使用如下命令打包 webpack \[entry-file] [bundle-file] --module-bind "js=babel"，js=babel意思是用babel命令转译扩展名为.js的文件。

### PS

突然茅塞顿开。知道为什么要用babel-node了，NodeJS 6只支持98%的ES6语法，因此需要babel的插件去支持剩下的2%特性，就得使用 [babel-plugin-transform-es2015-modules-commonjs](https://babeljs.io/docs/plugins/transform-es2015-modules-commonjs) 去支持import和export语法。

ES6的import语法不能再REPL中使用，只能写在文件中，并让bable-node运行。

Webpack的执行模块函数这部分不是很懂：modules[moduleId].call(module.exports, module, module.exports, \__webpack_require__);
