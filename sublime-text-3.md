# sublime text 3
##自动生成js注释
1. 使用package control安装DocBlockr插件
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


