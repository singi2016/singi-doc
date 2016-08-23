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

###第四步、创建文件
```cmd
touch index.html
touch App.jsx
touch main.js
touch webpack.config.js
```
###第五步、设置编译器，服务器，载入器
打开 webpack.config.js 文件添加以下代码:
```js
var config = {
   entry: './main.js',
	
   output: {
      path:'./',
      filename: 'index.js',
   },
	
   devServer: {
      inline: true,
      port: 7777
   },
	
   module: {
      loaders: [ {
         test: /\.jsx?$/,
         exclude: /node_modules/,
         loader: 'babel',
			
         query: {
            presets: ['es2015', 'react']
         }
      }]
   }
	
}

module.exports = config;
```
* entry: 指定打包的入口文件 main.js。
* output：配置打包结果，path定义了输出的文件夹，filename则定义了打包结果文件的名称。
* devServer：设置服务器端口号为 7777，端口后你可以自己设定 。
* module：定义了对模块的处理逻辑，这里可以用loaders定义了一系列的加载器，以及一些正则。当需要加载的文件匹配test的正则时，就会调用后面的loader对文件进行处理，这正是webpack强大的原因。

现在打开 package.json 文件，找到 "scripts" 中的 "test" "echo \"Error: no test specified\" && exit 1" 使用以下代码替换：
```json
"start": "webpack-dev-server --hot"
```

替换后的 package.json 文件 内容如下：
```js
{
  "name": "runoob-react-test",
  "version": "1.0.0",
  "description": "菜鸟教程 react 测试",
  "main": "index.js",
  "scripts": {
	"start": "webpack-dev-server --hot"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "react": "^0.14.7",
    "react-dom": "^0.14.7"
  }
}
```
>现在我们可以使用 npm start 命令来启动服务。--hot 命令会在文件变化后重新载入，这样我们就不需要在代码修改后重新刷新浏览器就能看到变化。
