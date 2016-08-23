# npm

##通过 npm 使用 React
我们建议在 React 中使用 CommonJS 模块系统，比如 browserify 或 webpack，本教程使用 webpack。

###第一步、安装全局包
```cmd
npm install babel -g
npm install webpack -g
npm install webpack-dev-server -g
```
> 必要在--save

```cmd
npm install babel --save
npm install webpack --save
npm install webpack-dev-server --save
```

###第二步、创建根目录
```cmd
npm init
```

###第三步、添加依赖包及插件
因为我们要使用 React, 所以我们需要先安装它，--save 命令用于将包添加至 package.json 文件。
```cmd
npm install react --save
npm install react-dom --save
```
同时我们也要安装一些 babel 插件
```cmd
$ npm install babel-core --save
$ npm install babel-loader --save
$ npm install babel-preset-react --save
$ npm install babel-preset-es2015 --save
```

###


