# [ejs](http://ejs.co/)
###-`Effective JavaScript templating`

###安装`npm`
```
npm install ejs
```

###渲染HTML`render()`
```js
var ejs = require('ejs'),
    people = ['geddy', 'neil', 'alex'],
    html = ejs.render('<%= people.join(", "); %>', {people: people});
```
###标签`<% %>`
* <% js代码，控制流，不输出
* <%= 原样输出
* <%- 输出(HTML会被解析)
* <%# 注释,不执行，不输出
* <%% 输出 '<%'
* %> 结束标签
* -%> 换行删除空格

###自定义标签`delimiter`
```js
var ejs = require('ejs'),
    users = ['geddy', 'neil', 'alex'];

// Just one template
ejs.render('<?= users.join(" | "); ?>', {users: users},
    {delimiter: '?'});
// => 'geddy | neil | alex'

// Or globally
ejs.delimiter = '$';
ejs.render('<$= users.join(" | "); $>', {users: users});
// => 'geddy | neil | alex'
```

###引入文件`include`
```html
<ul>
  <% users.forEach(function(user){ %>
    <%- include('user/show', {user: user}); %>
  <% }); %>
</ul>
```