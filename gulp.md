# gulp

##实现网页自动刷新

##插件：
* gulp 
* gulp-webserver 本地服务器
* gulp-livereload 网页自动刷新

##demo 
项目根目录下，新建` gulpfile.js`文件,使用下面的代码
```js
var gulp = require('gulp');
var webserver = require('gulp-webserver'); 
 
gulp.task('webserver', function() {
  gulp.src('./')//表示根目录，根据需要自行修改
    .pipe(webserver({
      livereload: true,//开启自动刷新
      open: true
    }));
});

// 监听任务
gulp.task('watch',function(){
  gulp.watch( '*.html') // 监听根目录下所有.html文件
});

gulp.task('default', ['webserver','watch']);
```

##运行
进入到`gulpfile.js`文件目录下，命令行运行，即可自动打开浏览器，默认打开根目录下的`index.html`。
```cmd
> gulp
```

