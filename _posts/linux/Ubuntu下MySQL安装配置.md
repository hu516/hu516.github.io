# 1. 安装MySQL

   `apt install mysql-server`

# 2. 初始化配置MySQL

   `mysql_secure_installation`

   配置过程如下：

```liunx
Securing the MySQL server deployment.

Connecting to MySQL using a blank password.
#是否启用密码强度验证
VALIDATE PASSWORD PLUGIN can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD plugin?

Press y|Y for Yes, any other key for No: N
#设置root密码
Please set the password for root here.

New password: 

Re-enter new password: 
#是否移除anonymous用户
By default, a MySQL installation has an anonymous user,
allowing anyone to log into MySQL without having to have
a user account created for them. This is intended only for
testing, and to make the installation go a bit smoother.
You should remove them before moving into a production
environment.

Remove anonymous users? (Press y|Y for Yes, any other key for No) : Y
Success.

#是否禁止root用户远程登录
Normally, root should only be allowed to connect from
'localhost'. This ensures that someone cannot guess at
the root password from the network.

Disallow root login remotely? (Press y|Y for Yes, any other key for No) : N
Success.
#是否异常test数据库
By default, MySQL comes with a database named 'test' that
anyone can access. This is also intended only for testing,
and should be removed before moving into a production
environment.


Remove test database and access to it? (Press y|Y for Yes, any other key for No) : N

 ... skipping.
Reloading the privilege tables will ensure that all changes
made so far will take effect immediately.
#是否重新加载权限表
Reload privilege tables now? (Press y|Y for Yes, any other key for No) : Y
Success.

All done! 
```

# 3. 配置远程访问

1. 修改`/etc/mysql/mysql.conf.d/mysqld.cnf`配置文件，把`bind-address=127.0.0.1`改为`bind-address=0.0.0.0`

2. 重启MySQL：`service mysql restart`

3. ssh登录MySQL：`mysql -uroot -p`

   ```linux
   Enter password: 
   Welcome to the MySQL monitor.  Commands end with ; or \g.
   Your MySQL connection id is 14
   Server version: 5.7.25-0ubuntu0.18.04.2 (Ubuntu)
   
   Copyright (c) 2000, 2019, Oracle and/or its affiliates. All rights reserved.
   
   Oracle is a registered trademark of Oracle Corporation and/or its
   affiliates. Other names may be trademarks of their respective
   owners.
   
   Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
   ```

   切换到系统数据库：`use mysql;`
   
   ```linux
   mysql> use mysql;
   Reading table information for completion of table and column names
   You can turn off this feature to get a quicker startup with -A
   
   Database changed
   ```

   新增权限用户：`GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '123456' WITH GRANT OPTION;`这里的123456为你给新增权限用户设置的密码，%代表所有主机，也可以具体到你的主机ip地址
   
   ```linux
   mysql> GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '123456' WITH GRANT OPTION;
   Query OK, 0 rows affected, 1 warning (0.00 sec)
   ```
   
   修改生效：`flush privileges; `
   
   ```linux
   mysql> flush privileges;
   Query OK, 0 rows affected (0.00 sec)
   ```
   
   登出Mysql：`exit;`
   
   ```linux
   mysql> exit;
   Bye
   ```
   
   

