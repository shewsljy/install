# centos6.8编译安装nginx

1. 安装依赖
    - `yum install -y gcc gcc-c++ automake pcre pcre-devel zlib zlib-devel openssl openssl-devel`
    - gcc gcc-c++ automake 编译工具
    - pcre pcre-devel 支持rewrite模块
    - zlib zlib-devel 支持gzip模块
    - openssl openssl-devel 支持ssl模块
2. 编译安装
    - `mkdir -p /root/{applications,src}`
    - `cp nginx-1.10.3.tar.gz src/`
    - `cd src`
    - `tar xzf nginx-1.10.3.tar.gz`
    - `cd nginx-1.10.3`
    - `./configure --prefix=/root/applications/nginx --with-http_ssl_module`
    - `make`
    - `make install`