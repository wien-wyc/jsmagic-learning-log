# npm和Babel学习笔记

### npm

npm是Node.js的包管理系统，和node一起安装的。主要命令有：

1. npm init：初始化node项目，会生成package.json文件。--yes参数使用默认初始化。扩展阅读：[npm 模块安装机制简介](http://www.ruanyifeng.com/blog/2016/01/npm-install.html)  [package.json 文件概述](http://javascript.ruanyifeng.com/nodejs/packagejson.html)。
2. npm install：安装模块。--save-dev参数表示将这些包作为开发依赖添加，-g参数表示全局安装。（可以在.npmrc文件中添加国内镜像：registry=https://registry.npm.taobao.org）
3. npm get prefix：得到安装node的路径

下面是几个需要全局安装的开发工具：

- [node-inspector](https://github.com/node-inspector/node-inspector) - Node.js 调试器。
- [nodemon](https://www.npmjs.com/package/nodemon) - 监听一个文件, 自动重启脚本。
- [pm2](https://www.npmjs.com/package/pm2) - 生产服务器上的进程管理器。
- [Browser Sync](https://www.browsersync.io/) - CSS 的实时编辑服务器。

### Babel

Babel是一个js转译器，用来将代码转译成不同版本的代码（ES6、ES3等）。在.babelrc中添加{"presets": ["babel-preset-es2015"]}即可将ES6代码转译成 ES3代码。目前，babel-preset-es2015中的代码会提供最大程度的浏览器兼容性。babel-preset-es2015插件提供的特性与Node.js 6有重叠部分：

- 支持 class 语法。
  - 不需要 [babel-plugin-transform-es2015-classes](http://babeljs.io/docs/plugins/transform-es2015-classes/)
- 支持 generator。
  - 不需要 [babel-plugin-transform-regenerator](http://babeljs.io/docs/plugins/transform-regenerator/)
- 支持解构（Destructuring）。
  - 不需要 [babel-plugin-transform-es2015-destructuring](https://babeljs.io/docs/plugins/transform-es2015-destructuring)
- 不支持 import/export 语法。
  - 添加插件 [babel-plugin-transform-es2015-modules-commonjs](https://babeljs.io/docs/plugins/transform-es2015-modules-commonjs)

因此只需要在.babelrc中添加{ "plugins": ["babel-plugin-transform-es2015-modules-commonjs"]}就可以获得babel-preset-es2015的全部特性。

### PS

NODE_PATH环境变量告诉node到哪里找全局的包
