---
title: "Ubuntu 20.04 手动编译安装 Ruby 2.3.x + OpenSSL 1.0.x"
date: 2021-02-08T15:29:38+08:00
tags: ["ruby", "ubuntu"]
draft: true
---

### 编译安装OpenSSL 1.0.x

```shell
wget https://www.openssl.org/source/old/1.0.2/openssl-1.0.2u.tar.gz
tar -zxvf openssl-1.0.2u.tar.gz
cd openssl-1.0.2u
./config shared --prefix=/opt/openssl-1.0.2u
```

### 安装 jemalloc

```shell
sudo apt install libjemalloc-dev
```

### 编译安装 Ruby 2.3.x

```shell
wget http://cache.ruby-china.com/pub/ruby/2.3/ruby-2.3.8.tar.gz
tar -zxvf ruby-2.3.8.tar.gz
cd ruby-2.3.8
./configure --prefix=/opt/ruby238 --with-openssl-dir=/opt/openssl-1.0.2u/ --with-jemalloc
make -j8
make install
```

检查 jemalloc 编译情况:

```
ruby -r rbconfig -e "puts RbConfig::CONFIG['LIBS']"
-lpthread -ljemalloc -lgmp -ldl -lcrypt -lm
```

### 其他

```shell
# 代码风格检查 rubocop
gem install parallel -v 1.19.2
gem install rubocop -v 0.81.0

# solargraph IDE 插件后端
gem install nokogiri -v 1.10.10
gem install solargraph -v 0.39.17
gem install rubocop-performance -v 1.5.2

# pry
gem install pry
```

#### 报错

```txt
$ gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/
Error fetching https://gems.ruby-china.com/:
        SSL_connect returned=1 errno=0 state=error: certificate verify failed (https://gems.ruby-china.com/specs.4.8.gz)
```

#### 解决

```shell
export SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt
export SSL_CERT_DIR=/etc/ssl/certs
```

### 参考

- [2.3.1 build fails on Ubuntu 18.04 with libssl-dev installed](https://github.com/rbenv/ruby-build/issues/1215)
- [Compilation and Installation](https://wiki.openssl.org/index.php/Compilation_and_Installation)
