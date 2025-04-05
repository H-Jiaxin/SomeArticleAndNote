# mysql用户权限管理

> 2025年3月31日中午

### 在root权限下登录数据库

##### 1. 创建用户

使用命令`create user username identified by 'password'`创建一个新用户

可以在mysql.user表中查询到用户信息

##### 2. 授予权限

使用命令`grant privilegesCode on dbname.tablename to username@host identified by "password"`授予用户权限

`privilegesCode`表示授予的权限类型[类型](#类型)

`dbname.tablename`表示授予权限的具体数据库或表[常用](#常用)

`username@host`表示授予的用户以及允许的IP地址其中[host](#host)

在mysql.db表中可以查看新增数据库权限的信息，也可以通过`show grants for username`查看权限授予执行的命令

可以将`grant on`改为`revoke from`来收回已授予的权限

`flush privileges`表示刷新权限变更。

##### 3. 修改密码

```sql
update mysql.user set password = password('password') 
where user = 'username';
```

##### 4. 删除用户

`drop user username@host;`会删除用户及其对应的权限

<h2 id="类型">类型<h2>

- all privileges：所有权限（privileges可以省略）。

- select：读取权限。

- delete：删除权限。

- update：更新权限。

- create：创建权限。

- drop：删除数据库、数据表权限。

<h2 id="常用">常用</h2>

- .：授予该数据库服务器所有数据库的权限。

- dbName.*：授予dbName数据库所有表的权限。

- dbName.dbTable：授予数据库dbName中dbTable表的权限。

<h2 id="类型">host</h2>

- localhost 只允许该用户在本地登录，不能远程登录。

- %：允许在除本机之外的任何一台机器远程登录。

- 192.168.52.32：具体的IP表示只允许该用户从特定IP登录。

参考文章:[MySQL用户管理：添加用户、授权、删除用户 - 陈树义 - 博客园](https://www.cnblogs.com/chanshuyi/p/mysql_user_mng.html)
