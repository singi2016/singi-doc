# `RSA`

## 生成`RSA`公钥和私钥

```
class Rsa
{
    public $privateKey = '';

    public $publicKey = '';

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

```
openssl_private_decrypt($data, $decrypted, $publicKey);
```

## 私钥解密

```
openssl_private_decrypt($data, $decrypted, $privateKey);

```