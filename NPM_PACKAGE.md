# 创建NPM包

### 创建入口文件

require.resolve会指出哪个文件会被加载，当模块是一个目录时，package.json文件的main属性会告诉require要加载哪一个文件：

```javascript
if path is a directory
  if path/package.json exists
    indexFile = package.json["main"]
    require(indexFile)
```

npm install .即可安装当前目录，安装完成后可以直接require("module-name")来引入包。

### 创建可执行文件

在js文件头部增加 !/usr/bin/env node 就可以让js文件被node执行。在package.json的bin属性中增加一个键值对，重新安装，就可以直接运行bin的键值。

可以使用原生的process.argv查看命令行参数（返回一个字符串数组）。可以使用 [minimist](https://github.com/substack/minimist) 库来解析命令行参数，他会将process.argv转换成一个对象。

### 将ES6转化成ES3

将ES6文件放到src目录里，babel src \--out-dir lib \--watch可以将src目录中的文件全部转译成ES3并保存在lib目录中，\--watch会监听src目录的变动，自动转译。转译之后就可以在node中运行lib下的js文件了。

package.json里的scripts属性可以让使用者方便地调用一些简单任务：

```json
"build": "babel src --out-dir lib",
"watch": "babel src --out-dir lib --watch",
```

这样就可以使用npm run build和npm run watch命令来执行转译任务。

使用npm pack将项目打成tgz包，使用者只需要npm install这个tgz包就可以安装成功。

### PS

当出现Cannot find module 'xxx'时候先看有没有配置$NODE_PATH。

使用ES6的import时候，对于非默认导入（default export）的值，impor时要带上{}
