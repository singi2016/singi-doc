# AES

> php 5.6+

```
/**
 * AES加密
 */

function aes_encript($plaintext ,$key='ebg.conzhu.net', $cipher='AES-256-CBC'){
    $ivlen = openssl_cipher_iv_length($cipher);
    $iv = openssl_random_pseudo_bytes($ivlen);
    $ciphertext_raw = openssl_encrypt($plaintext, $cipher, $key, $options=OPENSSL_RAW_DATA, $iv);
    $hmac = hash_hmac('sha256', $ciphertext_raw, $key, $as_binary=true);
    return  base64_encode( $iv.$hmac.$ciphertext_raw );
}

/**
 * AES解密
 * @param $ciphertext
 * @param string $key
 * @param string $cipher
 * @return string
 */
function aes_decrypt($ciphertext, $key='ebg.conzhu.net',$cipher='AES-256-CBC'){
    $c = base64_decode($ciphertext);
    $ivlen = openssl_cipher_iv_length($cipher);
    $iv = substr($c, 0, $ivlen);
    $hmac = substr($c, $ivlen, $sha2len=32);
    $ciphertext_raw = substr($c, $ivlen+$sha2len);
    $original_plaintext = openssl_decrypt($ciphertext_raw, $cipher, $key, $options=OPENSSL_RAW_DATA, $iv);
    $calcmac = hash_hmac('sha256', $ciphertext_raw, $key, $as_binary=true);
    if (function_exists('hash_equals')){
        if (hash_equals($hmac, $calcmac)){
            return $original_plaintext;
        }else{
            return false;
        }
    }else{
        if ($hmac === $calcmac){
            return $original_plaintext;
        }else{
            return false;
        }
    }
}
```

/**
 * 3DES加密
 * @param string $data 待加密的数据
 * @param string $key 加密密钥
 * @return string
 */
function encrypt_3des($data, $key)
{
    return base64_encode(openssl_encrypt($data, "des-ede3", $key));
}

/**
 * 3DES解密
 * @param string $data 待解密的数据
 * @param string $key 解密密钥
 * @return string
 */
function decrypt_3des($data, $key)
{
    $decrypt_text = openssl_decrypt(base64_decode($data), "des-ede3", $key);
    return $decrypt_text;
}