# sublime text 3

##安装插件
1. ctrl+` 调出命令输入窗口
2. 输入下面内容并回车：

`
import urllib.request,os;pf='Package Control.sublime-package';ipp=sublime.installed_packages_path();urllib.request.install_opener(urllib.request.build_opener(urllib.request.ProxyHandler()));open(os.path.join(ipp,pf),'wb').write(urllib.request.urlopen('http://sublime.wbond.net/'+pf.replace(' ','%20')).read())
`

3. 重启sublimetext3

##自动生成js注释-DocBlockr
1. 按`ctrl+shift+p`使用`package install`安装`DocBlockr`插件
2. 先写完你的函数`function testFunction(a, b, c) { }`
3. 然后在函数的前面一行，输入
`/**`
4. 然后回车，自动生成
```js
/**
 * [testFunction description]
 * @param {[type]} a [description]
 * @param {[type]} b [description]
 * @param {[type]} c [description]
 * @return {[type]} [description]
 */
function testFunction(a, b, c) {
}
```
5. 并且在注释块中，按@键可以展开关键词：

####[YUI Compressor注释规](http://usejsdoc.org/)

##格式化js代码-HTML-CSS-JS Prettify
1. 按`ctrl+shift+p`使用`package control`安装
2. 全选代码，按默认快捷键`shift+command+H`

##[sublimeGit](https://docs.sublimegit.net/tutorial.html)



