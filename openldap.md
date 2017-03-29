# openldap安装
1. 下载
    - 地址：ftp://ftp.openldap.org/pub/OpenLDAP/openldap-release/openldap-2.4.44.tgz
2. 解压
```
tar xzfv openldap-2.4.44.tgz
cd openldap-2.4.44
./configure --prefix=/usr/local/openldap
'configure: error: BDB/HDB: BerkeleyDB not available'
'BDB and HDB backends require Oracle Berkeley DB 4.4 - 4.8,or 5.0 - 5.1'
```
3. 安装5.1版本的BerkeleyDB
    - 地址：http://download.oracle.com/berkeley-db/db-5.1.29.tar.gz
    - 安装
    ```
    tar xzvf db-5.1.29.tar.gz
    cd db-5.1.29/build_unix
    ../dist/configure --prefix=/usr/local/BerkeleyDB
    sudo make
    sudo make install
    ```
4. 编译安装
```
cd openldap-2.4.44
./configure --prefix=/usr/local/openldap CPPFLAGS="-I/usr/local/BerkeleyDB/include" LDFLAGS="-L/usr/local/BerkeleyDB/lib -Wl,-rpath,/usr/local/BerkeleyDB/lib"
sudo make depend
sudo make
sudo make test
sudo make install
```
