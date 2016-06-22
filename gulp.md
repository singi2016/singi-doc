# gulp

##实现网页自动刷新

##插件：
* [gulp](http://www.gulpjs.com.cn/) 自动化构建工具
* [gulp-webserver](https://www.npmjs.com/package/gulp-webserver) 本地服务器

##demo 
项目根目录下，新建` gulpfile.js`文件,使用下面的代码
```js
var gulp = require('gulp');
var webserver = require('gulp-webserver'); 
 
gulp.task('webserver', function() {
  gulp.src('./')//表示根目录，根据需要自行修改
    .pipe(webserver({
      livereload: true,//开启自动刷新
      directoryListing:true,//目录
      open: true
    }));
});

// 监听任务
gulp.task('watch',function(){
  gulp.watch( '*.*') // 监听根目录下所有类型的文件
});

gulp.task('default', ['webserver','watch']);
```

##运行
进入到`gulpfile.js`文件目录下，命令行运行，即可自动打开浏览器，默认打开根目录下的`index.html`。
```cmd
> gulp
```

