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
 * rsa加密,每245个未加密字符加密后的长度为366个字节
 * POST最大为8M的话,最多可发送5.3M字节数据
 * @param $plaintext
 * @param $publicKey
 * @return string
 */
function rsa_encrypt($plaintext,$publicKey){
    //公钥加密
    $crypted_length = 245;//明文分段加密长度为245个字符(2048/8)
    $crypto = '';
    if ($plaintext){
        $plaintext = json_encode($plaintext);
        foreach (str_split($plaintext, $crypted_length) as $chunk) {
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