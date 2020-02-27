---
title: Openssl generates pem and der certificates
author: 毛宇鹏
date: 2020-02-27 10:46:59
subtitle:
showTitle: 使用Openssl一键生成pem和der证书
description: 通过脚本文件一键生成pem和der证书, 方便开发中测试证书双向验证
tags:
    - openssl
    - shell
categories:
    - openssl
---


### 将以下代码另存为后缀名为sh的文件

```bash
#!/bin/bash
PASS=
Init_Selection() {
    clear
    echo "+------------------------------------------------------------------------+"
    echo "|                       _ _  _  _        _  _  _  _                    |"
    echo "|                      / / //_|/_//_//_//_//_'/ //_/                   |"
    echo "|                                 _/   /         _/                    |"
    echo "+------------------------------------------------------------------------+"
    echo "|                            openssl证书生成脚本v1.0                      |"
    echo "+------------------------------------------------------------------------+"
    echo "|                         https://www.maoyupeng.club                     |"
    echo "+------------------------------------------------------------------------+"
    
    Echo_Green "请输入证书密码"
    read -p "Password:" PASS
    action_build 
    
}

action_build() 
{
	echo "创建AES256加密密钥..."
	openssl genrsa -passout pass:${PASS} -out rsa_aes_private.pem 2048
	echo "生成公钥..."
	openssl rsa -in rsa_aes_private.pem -passin pass:${PASS} -pubout -out rsa_public.pem
	echo "PEM私钥转DER..."
	openssl rsa -in rsa_aes_private.pem -passin pass:${PASS} -out rsa_private_key.der -outform der
	echo "PEM公钥转DER..."
	openssl rsa -in rsa_public.pem -out rsa_public_key.der -pubin -outform der
	echo "Finish!"

}


Echo_Green()
{
  echo $(Color_Text "$1" "32")
}

Echo_Yellow()
{
  echo $(Color_Text "$1" "33")
}

Init_Selection
```

### 然后打开终端, 赋予权限

```bash
chmod -R 755 ./*.sh
```

### 最后执行脚本文件, 根据提示输入生成证书的密码

```bash
./xxx.sh
```

等待片刻, 证书生成成功


