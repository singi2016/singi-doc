# restful web api

## 使用到的技术

- restful api
- jwt
- authO2
- RSA
- sign

## access_token

1. 每次请求获取
2. 有效期2小时,连续使用自动延长有效期为2小时

## 签名

1. 所有请求参数正序
2. 键值对拼接,在首尾拼接app_secret
3. 哈希,最后转化为大写

