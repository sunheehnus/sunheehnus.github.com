---
layout: post
title: "Firefox Goagent on my CentOS6.4"
description: ""
category: Configuration
tags: [installation]
---
{% include JB/setup %}
### 申请Google App Engine，创建appid
用gmail帐号登录申请
### 下载并配置[goagent](https://code.google.com/p/goagent/)最新版
1. unzip goagent-goagent-v3.1.5-32-gc00854c.zip
2. GoAgent需要使用[python2.7](http://python.org/downloads/)，CentOS6.4自带python2.6，需要手动编译安装  
    * `tar vxzf Python-2.7.6.tgz`
    * `cd Python-2.7.6`
    * `./configure --prefix=/usr/local/python27` **防止覆盖系统自带的python2.6**
    * `make`
    * `sudo make install` **该prefix下需要superuser权限**
    * `ln -s /usr/local/python27/bin/python2.7 /usr/bin/python2.7`
3. 安装[gevent](https://pypi.python.org/pypi/gevent#downloads)
    * `tar vxzf gevent-1.0.tar.gz`
    * `cd gevent-1.0/`
    * `sudo ./setup.py install`
4. 安装[greenlet](http://pypi.python.org/pypi/greenlet)
    * `unzip greenlet-0.4.0.zip`
    * `cd greenlet-0.4.0`
    * `sudo ./setup.py install`
5. 使用yum安装其他软件包
    * `sudo yum groupinstall "Development Tools"`
    * `sudo yum install openssl openssl-devel pyOpenSSL`
    * `sudo yum install python python-devel libevent libevent-devel`
6. 配置goagent
    * `cd goagent/`
    * `python server/uploader.zip` **输入相应的appid，邮箱，密码**
    * 根据上一步成功的提示，修改local/proxy.ini中的appid
    * goagent使用python2.7，更改local/proxy.py首行为#!/usr/bin/python2.7
    * `chmod 775 local/proxy.py`
7. 导入证书
    * Firefox->Preferences->Advances->Certificates->View Certificates->Authorities->Import(goagent-goagent-v3.1.5-32-gc00854c/local/CA.crt)
    * aggree everything
8. 设置浏览器代理地址为127.0.0.1:8087(应该使用AutoProxy插件代替)
    * 安装插件AutoProxy
    * 添加代理服务器goagent 127.0.0.1 8087
    * 添加规则订阅,选择gfwList订阅
    * 更改默认代理为GoAgent
### 运行客户端
* `cd goagent-goagent-v3.1.5-32-gc00854c`
* `./local/proxy.py`

***
Let's enjoy the Internet!
