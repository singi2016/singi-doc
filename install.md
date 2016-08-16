# npm install

##1. [跨域cors](https://github.com/expressjs/cors)
```cmd
npm install cors
```
```js
const cors = require('cors');
app.use(cors());//设置跨域访问
```
##2. 加密-crypto
```js
crypto.createHash('sha256').update('password').digest('hex');
```
##3.[缓存redis](https://www.npmjs.com/package/redis)
```cmd
npm install redis
```
##4 [数据库mysql](https://www.npmjs.com/package/mysql)
```cmd
npm install mysql
```
```js
var mysql = require('mysql');
var pool  = mysql.createPool({
  connectionLimit : 10,
  host            : 'example.org',
  user            : 'bob',
  password        : 'secret',
  database        : 'my_db'
});
 
pool.query('SELECT 1 + 1 AS solution', function(err, rows, fields) {
  if (err) throw err;
 
  console.log('The solution is: ', rows[0].solution);
});
```
