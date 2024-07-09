---
title: 加密解密
class: heading_no_counter
keywords: 加密, 解密, Encrypt, Decrypt
desc: 加密解密工具，提供AES、DES、RSA加解密及Hash编码
---

## Introduce

加密解密工具，提供AES、DES、RSA加解密及多种方式的Hash编码

![](../../assets/images/ToolsSet/TSTEncrypt.png)

## How to use

左侧为加解密区域，右侧为Hash编码区域

### 加解密

点击右侧【Generate Key】按钮可以自动生成随机密钥
1. AES加解密
  
   > 密钥为32位字符串；Vector为16位字符串，可以为空

   * 加密

     在左侧输入明文，点击【Encrypt】按钮即可在右侧生成密文

   * 解密

     在右侧输入密文，点击【Decrypt】按钮即可在左侧生成明文
  
2. DES加解密
    > 密钥为24位字符串

    * 加密

      在左侧输入明文，点击【Encrypt】按钮即可在右侧生成密文

    * 解密

      在右侧输入密文，点击【Decrypt】按钮即可在左侧生成明文

3. RSA加解密
   * 加密

     在左侧输入明文，点击【Encrypt】按钮即可在右侧生成密文

   * 解密

     在右侧输入密文，点击【Decrypt】按钮即可在左侧生成明文

   * 签名

     在左侧输入明文，点击【Sign】按钮即可在右侧生成签名

   * 验证

     在右侧输入待验证字符串，点击【Verify】按钮对字符串进行验证，验证结果会弹出对话框提示

### Hash编码

在上方文本框输入需要编码的文本，下方会自动计算出对应的Hash编码值

可以在HMAC Key文本框输入字符串，可以生成带有密钥认证Hash编码