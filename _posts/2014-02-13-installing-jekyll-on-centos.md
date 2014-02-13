---
layout: post
title: "Installing Jekyll on CentOS"
description: ""
category: jekyll
tags: [jekyll installation]
---
{% include JB/setup %}
<br/>
### To install jekyll，we need Ruby RubyGems Zlib  
* *Installing Ruby*  
Click [Ruby](https://www.ruby-lang.org/en/downloads/) to download (.tar.gz)  
tar -vxzf ruby-version.tar.gz  
cd ruby-version/  
./configure --enable-pthread  
make  
sudo make install  
* *Installing RubyGems*  
Click [RubyGems](http://rubygems.org/pages/download) to download (.tgz)  
tar -vxzf rubygems-version.tgz  
cd rubygems-version/  
ruby setup.rb  
* *Installing zlib*  
Click [zlib](www.zlib.net) to download (.tar.gz)  
tar -vxzf zlib-version  
cd zlib-version/  
./configure  
make  
sudo make install  
cd ruby-version/ext/zlib  
ruby exconf.rb  
make  
sudo make install  
### Configure gem resource
* *local resource*  
    gem sources --remove https://rubygems.org/  
    gem sources -a http://ruby.taobao.org/  
* *global resource*  
    sudo gem sources --remove https://rubygems.org/  
    sudo gem sources -a http://ruby.taobao.org/  
  
  
**Gem needs super user's authoration to install software to some special dictionaries. So when installing via gem, don't forget sudo.**
  
**From now on, you can just follow the guidence of [jekyllrb](http://jekyllrb.com/docs/quickstart/).**  
**Let's get it started from here. ^_^**

***
