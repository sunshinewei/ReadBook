###  MySQL下载

http://dev.mysql.com/downloads/mysql/ 

### 安装
1.添加环境变量  (解压后的bin文件夹下)
2.修改my-default.ini，此文件是初始化信息：（或者新建my.ini文件）
<pre><code>
[mysqld]  
port = 3306  
basedir=D:/software/mysql-5.7.21-winx64 
datadir=D:/software/mysql-5.7.21-winx64/data
max_connections=200  
character-set-server=utf8  
default-storage-engine=INNODB  
sql_mode=NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES  
[mysql]  
default-character-set=utf8  
</code></pre>
3.以管理员的身份进入cmd，切换到bin目录下，输入mysqld -install
4.执行以下语句进行MySQL的初始化
<code>mysqld --initialize-insecure --user=mysql  </code>\
5.执行以下命令以启动mysql服务
<code>net start mysql</code>
6.启动MySQL之后，root用户的密码为空，设置密码，命令如下:
<code>
mysqladmin -u root -p password 新密码  
Enter password: 旧密码  
</code>
