# `RSA`

## 生成`RSA`公钥和私钥

```
/**
 * 获取公钥私钥
 * @return array
 */
function getPublicKeyAndPrivateKey(){
    $resource = openssl_pkey_new();
    openssl_pkey_export($resource, $privateKey);
    $detail = openssl_pkey_get_details($resource);
    return ['publicKey'=>$detail['key'],'privateKey'=>$privateKey];
}
```

## 公钥加密

> 明文加密时的长度为[2048bit/8-11]=245,过长会加密失败

```
/**
 * 公钥加密
 * @param $plaintext
 * @param $publicKey
 * @return string
 */
function encryptWithPublicKey($plaintext,$publicKey){
    $crypto = '';
    if ($plaintext){
        foreach (str_split($plaintext, 245) as $chunk) {
            openssl_public_encrypt($chunk, $encryptData, $publicKey);
            $crypto .= $encryptData;
        }
        $crypto = base64_encode($crypto);
    }
    return $crypto;
}
```

## 私钥解密

```
/**
 * 私钥解密
 * @param $encryptData
 * @param $privateKey
 * @return mixed
 */
function decryptWithPrivateKey($encryptData, $privateKey){
    $crypto = '';
    foreach (str_split(base64_decode($encryptData), 256) as $chunk) {
        openssl_private_decrypt($chunk, $decryptData, $privateKey);
        $crypto .= $decryptData;
    }
    return $crypto;
}
```

## 私钥签名

```
/**
 * 私钥签名
 * @param $original_str
 * @param $private_key
 * @return string
 */
function signWithPrivateKey($original_str, $private_key)
{
    openssl_sign($original_str, $sign, $private_key);
    openssl_free_key($private_key);
    $sign = base64_encode($sign);//最终的签名
    return $sign;
}
```

## 公钥验签

```
/**
 * 公钥验签
 * @param $original_str
 * @param $sign
 * @param $public_key
 * @return bool
 */
function checkSignWithPublicKey($original_str, $sign, $public_key)
{
    $sign = base64_decode($sign);//得到的签名
    $result = (bool)openssl_verify($original_str, $sign, $public_key);
    openssl_free_key($public_key);
    return $result;
}
```