MySQL 权限详解
=============

MySQL权限级别介绍
---------------
* 全局性的管理权限，作用于整个 MySQL 实例级别
* 数据库级别的权限，作用于某个指定的数据库上或所有的数据库上
* 数据库对象级别的权限，作用于指定的数据库对象上（表、视图）

MySQL权限详解
------------
* **ALL** - ALL Privileges权限代表全局或者全数据库对象级别的所有权限
* **Alter** - 允许修改表结构的权限，但必须要求有 create 和 insert 权限配合。如果 rename 表名，则要求有 alter 和 drop 原表，create 和 insert 新表的权限
* **Alter Routine** - 允许修改或删除存储过程、函数的权限
* **Create** - 允许创建新的数据库和表的权限
* **Create Routine** - 允许创建存储过程、函数的权限
* **Create Table Space** - 允许创建、修改、删除表空间和日志组的权限
* **Create temporary tables** - 允许创建临时表的权限
* **Create User** - 允许创建、修改、重命名 user 的权限
* **Create View** - 允许创建视图的权限
* **Delete** - 允许删除行数据的权限
* **Drop** - 允许删除数据库、表、视图的权限，包括 `truncatetable` 命令
* **Event** - 允许查询、创建、修改、删除 MySQL 事件
* **Execute** - 允许执行存储过程和函数的权限
* **File** - 允许在 MySQL 可以访问的目录进行读写磁盘文件操作，可使用命令包括 `load data infile`、`select ... into outfile`、`load file()` 函数
* **Grant Option** - 是否允许此用户授权或者收回给其他用户你给予的权限
* **Index** - 是否允许创建和删除索引
* **Insert** - 是否允许在表里插入数据，同时在执行`analyze table`、`optimize table`、`repair table` 语句的时候也需要 insert 权限
* **Lock** - 允许对拥有 select 权限的表进行锁定，以防止其他链接对此表的读或写
* **Process** - 允许查看 MySQL 中的进程信息，比如执行 `show processlist`
* **Reference** - 是否允许创建外键，权限是在5.7.6版本之后引入
* **Reload** - 允许执行 flush 命令，指明重新加载权限表到系统内存中， `refresh` 命令代表关闭和重新开启日志文件并刷新所有的表
* **Replication Client** - 允许执行 `show master status`、`show slave status`、`show binary logs` 命令
* **Replication Slave** - 允许 slave 主机通过此用户连接 master 以便建立主从复制关系
* **Select** - 允许从表中查看数据，某些不查询表数据的 select 执行则不需 要此权限，如`Select 1+1`、`Select PI()+2`; 而且 select 权限在执行 update/delete 语句中含有 where 条件的情况下也是需要的
* **Show Databases** - 代表通过执行 `show databases` 命令查看所有的数据库名
* **Show View** - 代表通过执行 `show create view` 命令查看视图创建的语句 `mysqladmin processlist`、`show engine` 等命令
* **Shutdown** - 允许关闭数据库实例，执行语句包括 `mysqladmin shutdown`
* **Super** - 允许执行一系列数据库管理命令，包括 `kill` 强制关闭某个连接 命令，`change master to` 创建复制关系命令，以及 `create/alter/drop server` 等命 令
* **Trigger** - 允许创建、删除、执行、显示触发器的权限
* **Update** - 允许修改表中的数据的权限
* **Usage** - 创建一个用户之后的默认权限，其本身代表连接登录权限

MySQL系统权限表
--------
* **`user`** - 存放用户账户信息以及全局级别（所有数据库）权限，决定了来自哪些主机的哪些用户可以访问数据库实例，如果有全局权限则意味着对所有数据库都有此权限
* **`db`** - 存放数据库级别的权限，决定了来自哪些主机的哪些用户可以访问此数据库
* **`tables_priv`** - 存放表级别的权限，决定了来自哪些主机的哪些用户可以 访问数据库的这个表
* **`columns_priv`** - 存放列级别的权限，决定了来自哪些主机的哪些用户可以访问数据库表的这个字段
* **`procs_priv`** - 存放存储过程和函数级别的权限

权限存储在 mysql 库的 
`user`, 
`db`, 
`table_priv`, 
`columns_priv`, 
`procs_priv` 
这几个系统表中，待 MySQL 实例启动后就加载到内存中。

![alt MySQL权限表](http://cdn.mingsixue.com/static/20191108135012-mysql.png)

### User 和 db 权限表结构： ###
User权限表结构中的特殊字段
* **Plugin**、**Password**、**authentication_string** - 这三个字段存放用户认证信息
* **Password_expired** - 设置成 `Y` 则表明允许 DBA 将此用户的密码设置成过期而且过期后要求用户的使用者重置密码（`alter user/set password` 重置密码）
* **Password_last_changed** - 作为一个时间戳字段代表密码上次修改时间，执 行 `create user/alter user/set password/grant` 等命令创建用户或修改用户密码时此数值自动更新
* **Password_lifetime** - 代表从 password_last_changed 时间开始此密码过期的天数
* **Account_locked** - 代表此用户被锁住，无法使用

### procs_priv 权限表结构： ###
* **Routine_type** - 枚举类型，代表是存储过程还是函数

### 权限认证中的大小写敏感问题： ###
* 字段 `user`、`password`、`authencation_string`、`db`、`table_name` 大小写敏感
* 字段 `host`、`column_name`、`routine_name` 大小写不敏感
* User 用户大小写敏感
* Host 主机名大小写不敏感

MySQL授权用户
-----------
* MySQL 的授权用户由两部分组成：用户名和登录主机名
* 表达用户的语法为 `'user_name'@'host_name'`
* 单引号不是必须，但如果其中包含特殊字符则是必须的
* `@localhost` 代表匿名登录的用户
* Host_name 可以是主机名或者 ipv4/ipv6 地址。
    + `localhost` 代表本机
    + `127.0.0.1` 代表 ipv4 的本机地址
    + `::1` 代表 ipv6 的本机地址
* Host_name 字段允许使用 `%` 和 `_` 两个匹配字符，比如 % 代表所有主机， %.mysql.com 代表来自 mysql.com 这个域名下的所有主机，192.168.1.% 代表所有来自 192.168.1 网段的主机

MySQL修改权限的生效
-----------------
* 执行 `Grant`、`revoke`、`setpassword`、`renameuser` 命令修改权限之后，MySQL会自动将修改后的权限信息同步加载到系统内存中
* 如果执行 `insert/update/delete` 操作上述的系统权限表之后，则必须再执行刷新权限命令才能同步到系统内存中，刷新权限命令包括: `flush privileges/mysqladmin` `flush-privileges/mysqladmin reload`
* 如果是修改 `tables` 和 `columns` 级别的权限，则客户端的下次操作新权限就会生效
* 如果是修改 `database` 级别的权限，则新权限在客户端执行 `use database` 命令后生效
* 如果是修改 `global` 级别的权限，则需要重新创建连接新权限才能生效
* `--skip-grant-tables` 可以跳过所有系统权限表而允许所有用户登录，只在特殊情况下暂时使用


-----
参考文章：

[MySQL权限详解](https://www.cnblogs.com/Csir/p/7889953.html)

[MySQL官方文档Privileges Provided by MySQL](https://dev.mysql.com/doc/refman/5.7/en/privileges-provided.html)

-----
时间：2019/11/08

Tags：mysql、mysql权限、数据库权限