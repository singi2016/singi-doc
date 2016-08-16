#express

##1. [跨域](https://github.com/expressjs/cors)
```js
const cors = require('cors');
app.use(cors());//设置跨域访问
```
##2. 加密-crypto
```js
crypto.createHash('sha256').update('password').digest('hex');
```
##3. 