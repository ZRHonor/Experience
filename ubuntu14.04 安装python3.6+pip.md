# ubuntu14.04 安装python3.6+pip

参考链接

[Ubuntu 16.04 安装Python 3.6.1及pip](https://blog.csdn.net/lanhaixuanvv/article/details/78248338)

[python3.6的pip管理器出问题 ssl模块未安装](https://blog.csdn.net/u013427969/article/details/67648207)

[更改Ubuntu默认python版本的两种方法](https://blog.csdn.net/fang_chuan/article/details/60958329)

1. 下载python安装包<https://www.python.org/ftp/python/3.6.1/Python-3.6.1.tgz>

   并解压

   ```
   tar -xzvf ./Python-3.6.1.tgz
   cd ./Python-3.6.1
   ```

2. 修改 Modules/Setup

   取消注释以下行

   ```
   ......
   zlib zlibmodule.c-I$(prefix)/include -L$(exec_prefix)/lib -lz
   ......
   _socket socketmodule.c timemodule.c
   ......
   _ssl _ssl.c \
   -DUSE_SSL -I$(SSL)/include -I$(SSL)/include/openssl \
   -L$(SSL)/lib -lssl -lcrypt
   ```

   注：如果有乱码可以注释下面一行

   ```
   readline readline.c-lreadline -ltermcap
   ```

3. 安装zlib

   ```
   wget http://www.zlib.net/zlib-1.2.11.tar.gz
   tar -xzvf ./zlib-1.2.11.tar.gz
   cd ./zlib-1.2.11
   ./configure
   make
   sudo make install
   ```

4. 安装ssl

   到openssl官网下载压缩包  <http://www.openssl.org/source/>

   解压进入安装包编译 
    我这里下载的是openssl-1.0.2l.tar.gz

   ```
   tar -xzvf ./openssl-1.0.2l.tar.gz
   cd ./openssl-1.0.2l
   ./config
   make
   sudo make install
   ```

5. 编译安装python3.6

   ```
   cd ./Python-3.6.1
   ./configure
   make
   sudo make install
   ```

6. 更改默认python版本

   ```
   alias python='usr/local/bin/python3.6'
   alias pip='usr/local/bin/pip3.6'
   ```


