## 在使用arch中mysql时遇到的问题

#### 遇到缺少`mysqld.sock.lock`文件的情况

**解决办法 :删除`/var/run/mysqld/mysqld.sock.lock`然后执行`mysqld -uroot`,这个文件时特殊文件,由程序自动生成.**
