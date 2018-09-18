# `RSA`

## 生成`RSA`公钥和私钥

```
class Rsa
{
    public $privateKey;
    public $publicKey;
    public function __construct()
    {
        $resource = openssl_pkey_new();
        openssl_pkey_export($resource, $this->privateKey);
        $detail = openssl_pkey_get_details($resource);
        $this->publicKey = $detail['key'];
    }
}
```

## 公钥加密

> 明文加密时的长度为[2048/8-11]=245,过长会加密失败

```
function encrypt($originalData){
        $crypto = '';
        foreach (str_split($originalData, 245) as $chunk) {
            openssl_public_encrypt($chunk, $encryptData, $this->rsaPublicKey);
            $crypto .= $encryptData;
        }
        return base64_encode($crypto);
    }
```

## 私钥解密

```
function decrypt($encryptData){
    $crypto = '';
    foreach (str_split(base64_decode($encryptData), 256) as $chunk) {
        openssl_private_decrypt($chunk, $decryptData, $this->rsaPrivateKey);
        $crypto .= $decryptData;
    }
    return $crypto;
}
```