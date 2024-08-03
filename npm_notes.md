# npm命令

## npm镜像源的查看与设置

```
//查看镜像配置结果
npm config get registry
npm config get disturl
```

```
//设置为淘宝源
npx nrm use taobao
//设置为官方源
npx nrm use npm
```

## 查看已安装包列表

```
npm list -g
```

## 安装指定版本包

```
npm install jquery@3.0.0
```

## 卸载包

```
npm uninstall jquery
```

## 查看模块版本号

```
npm list jquery
```

## 安装依赖的包

```
npm install -save jquery // -save:运行时依赖
npm install -save-dev jquery // -save-dev:开发时依赖
```

## 初始化package.json文件

```
npm init --yes // 初始化默认的包内容
npm init // 自定义初始化包内容
```

package.json文件内容解析

```
package.json
{
  "name": "npm", /* 可自定义包名 */
  "version": "1.0.0", /* 可自定义包版本号 */
  "description": "NPM-Lession Name: 【NPM】包管理工具 #node package manager\r Video URL:https://www.bilibili.com/video/BV1Dv411W7XP?p=3&vd_source=dec0df5946c5a4e7864de4bc96371c49\r Notes:  这是NPM基础视频教程，这个文件夹内的文件相当于课堂笔记。",
  "main": "index.js",/* 主入口文件 */
  "scripts": {/* 可自定义命令脚本。调用命令：npm run test*/
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],/* 关键字 */
  "author": "",/* 包作者 */
  "license": "ISC"/* 开源协议 */
  "dependencies": { /* 运行时依赖 */
    "jquery": "^3.7.1"
    /* 
    "5.0.3"表示安装指定的5.0.3版本
    "~5.0.3"表示安装5.0.X中最新的版本
    "^5.0.3"表示安装5.X.X中最新的版本
    */
  }
  "devDependencies": { /* 开发时依赖 */
    "jquery": "^3.7.1"
  }
}
```

只要有了json文件，运行npm install就能自动下载包到node_modules里面。

## 引入包

在入口文件（index.js）中引入包

```
const $ = require('jquery')// 引入jq包

let num = require('./oem.js');// 引入自定义的js文件
```

为解决ES5和6之间兼容性问题，需要把ES6转换成ES5的代码。有两种方式：

1、客户端在线转换

2、服务器端提前编译转换（babel）（常用）

## babel转化ES6 code

### 1.安装babel包

```
npm i --save-dev babel-cli -g
```

### 2.项目目录下新建一个.babelrc（babel配置文件），加入配置代码

```
{
    "presets": ["es2015", "stage-2"],// 设置转码规则
    "plugins": ["transform-runtime"]// 设置插件
}
```

### 3.安装剩下要用到的包

```
npm install babel-core babel-preset-es2015 babel-plugin-transform-runtime babel-preset-stage-2 --save-dev
```

### 4.新建src和lib目录到根目录（src放ES6转换前的源码，lib放转换完成ES5代码）

### 5.编译

```
//手动编译
babel src -w -d lib

//在package.json中加入build脚本命令
"scripts":{"build":"babel src -w -d lib"},

//调用
npm run build
```

