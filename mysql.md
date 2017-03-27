# 源码编译mysql5.7.17

- 编译平台环境
    - ubuntu 16.04

- 安装编译依赖
    - `sudo apt install make cmake gcc g++ perl bison libaio-dev libncurses5 libncurses5-dev libnuma-dev`
    - 参考：https://dev.mysql.com/doc/refman/5.7/en/source-installation.html

- mysql源码获取
    - 版本：5.7.17
    - 地址：https://dev.mysql.com/downloads/mysql/
    - 选项：Source Code --> Generic Linux (Architecture Independent) -->mysql-5.7.17.tar.gz

- 解压获取源代码
    - `tar xzvf mysql-5.7.17.tar.gz`
    - `cd mysql-5.7.17`

- 在`mysql-5.7.17`中执行`cmake .`检测mysql的安装环境条件
    - 提示`-- MySQL currently requires boost_1_59_0`
    - 现阶段`sudo apt install libboost-all-dev`安装的版本为58,因此需要手动安装boost_1_59
        - 下载`boost_1_59_0`源代码
        - 地址：https://sourceforge.net/projects/boost/files/boost/1.59.0/boost_1_59_0.tar.gz
        - `tar xzvf boost_1_59_0.tar.gz`
        - `cd boost_1_59_0`
        - `sudo ./bootstrap.sh`
        - `sudo ./b2 install`

- 编译安装mysql
    - `cd mysql-5.7.17`
    - `cmake . -DBUILD_CONFIG=mysql_release -DCPACK_MONOLITHIC_INSTALL=ON -DCMAKE_INSTALL_PREFIX=/usr/local/mysql -DDEFAULT_CHARSET=utf8 -DDEFAULT_COLLATION=utf8_general_ci -DMYSQLX_TCP_PORT=33060 -DMYSQL_UNIX_ADDR=/usr/local/mysql/mysql.sock -DMYSQL_TCP_PORT=3306 -DMYSQLX_UNIX_ADDR=/usr/local/mysql/mysqlx.sock -DMYSQL_DATADIR=/usr/local/mysql/data -DSYSCONFDIR=/usr/local/mysql/etc -DENABLE_DOWNLOADS=ON -DWITH_BOOST=system`
    - `sudo make`
    - `sudo make install`

- 初始化设置mysql
    - 创建mysql组跟用户
        - `sudo groupadd mysql`
        - `sudo useradd -r -g mysql -s /bin/false mysql`
    - 更改mysql目录权限
        - `cd /usr/local/mysql`
        - `sudo chown -R mysql .`
        - `sudo chgrp -R mysql .`
    - 初始化mysql,生成root用户的临时密码,如`root@localhost: sL3>%PEjt-ir`
        - `sudo bin/mysqld --initialize --user=mysql`
    - 开启SSL功能
        - `sudo bin/mysql_ssl_rsa_setup`
    - 更改mysql目录权限
        - `sudo chown -R mysql .`
        - `sudo chgrp -R mysql .`
    - 测试启动mysql
        - `sudo bin/mysqld_safe --user=mysql`
    - 启动mysql,输入临时密码后更改密码,停止mysql
        - `sudo support-files/mysql.server start`
        - `sudo bin/mysql -u root -p`
        - `alter user 'root'@'localhost' identified by 'root';`
        - `sudo support-files/mysql.server stop`
    - 将mysql服务放置init.d目录下
        - `sudo cp support-files/mysql.server /etc/init.d/mysql.server`
        - service控制mysql服务
            - `service mysql.server start|stop|restart|reload|force-reload|status`
