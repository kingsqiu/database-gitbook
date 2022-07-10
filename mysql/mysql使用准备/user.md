# 用户与权限

### 需要考虑的情况

- 多数用户只需要对表进行读和写，但少数用户甚至需要能创建和删除表；
- 某些用户需要读表，但可能不需要更新表；
- 允许用户添加数据，但不允许他们删除数据；
- 某些用户（管理员）可能需要处理用户账号的权限，但多数用户不需要；
- 让用户通过存储过程访问数据，但不允许他们直接访问数据；
- 根据用户登录的地点限制对某些功能的访问。



## 创建用户

CREATE USER

```sql
CREATE USER ben IDENTIFIED BY 'P@$$W0RD'
```

指定散列口令：IDENTIFIED BY指定的口令为纯文本，MySQL将在保存到user表之前对其进行加密。



其他方式：

- GRANT
- 直接插入行到user表（不过为安全起见，一般不这样做）

MySQL用来存储用户账号信息的表（以及表模式）极为重要，对它们的任何毁坏都可能严重地伤害到MySQL服务器。因此，相对于直接处理来说，最好是用标记和函数来处理这些表。



创建用户后必须接着分配访问权限，否则不能看到数据，不能执行任何数据库操作。



### 修改用户名

仅MySQL 5或之后的版本支持RENAME USER。为了在以前的MySQL中重命名一个用户，可使用UPDATE直接更新user表。

```sql
RENAME USER 旧用户名 TO 新用户名
```



## 删除用户

```sql
DROP USER 用户名
```

自MySQL 5以来，DROP USER删除用户账号和所有相关的账号权限。在MySQL 5以前，DROP USER只能用来删除用户账号，不能删除相关的权限。

因此，如果使用旧版本的MySQL，需要先用REVOKE删除与账号相关的权限，然后再用DROP USER删除账号。



## 设置访问权限


为设置权限，需要使用GRANT语句。要求至少给出以下信息：

- 要授予的权限；
- 被授予访问权限的数据库或表；
- 用户名。
- 控制权限的层次（不必要）
  - 整个服务器
  - 整个数据库
  - 特定的表
  - 特定的列
  - 特定的存储过程


### 权限一览

| 权限                    | 说明                                                         |
| :---------------------- | :----------------------------------------------------------- |
| ALL                     | 除GRANT OPTION外的所有权限                                   |
| ALTER                   | 使用ALTER TABLE                                              |
| ALTER ROUTINE           | 使用ALTER PROCEDURE和DROP PROCEDURE                          |
| CREATE                  | 使用CREATE TABLE                                             |
| CREATE ROUTINE          | 使用CREATE PROCEDURE                                         |
| CREATE TEMPORARY TABLES | 使用CREATE TEMPORARY TABLE                                   |
| CREATE USER             | 使用CREATE USER、DROP USER、RENAME USER和REVOKE ALL PRIVILEGES |
| CREATE VIEW             | 使用CREATE VIEW                                              |
| DELETE                  | 使用DELETE                                                   |
| DROP                    | 使用DROP TABLE                                               |
| EXECUTE                 | 使用CALL和存储过程                                           |
| FILE                    | 使用SELECT INTO OUTFILE和LOAD DATA INFILE                    |
| GRANT OPTION            | 使用GRANT和REVOKE                                            |
| INDEX                   | 使用CREATE INDEX 和DROP INDEX                                |
| INSERT                  | 使用INSERT                                                   |
| LOCK TABLES             | 使用LOCK TABLES                                              |
| PROCESS                 | 使用SHOW FULL PROCESSLIST                                    |
| RELOAD                  | 使用FLUSH                                                    |
| REPLICATION CLIENT      | 服务器位置的访问                                             |
| REPLICATION SLAVE       | 由复制从属使用                                               |
| SELECT                  | 使用SELECT                                                   |
| SHOW DATABASES          | 使用SHOW DATABASES                                           |
| SHOW VIEW               | 使用SHOW CREATE VIEW                                         |
| SHUTDOWN                | 使用mysqladmin shutdown（用来关闭MySQL）                     |
| SUPER                   | 使用CHANGE MASTER、KILL、LOGS、PURGE、MASTER和SET GLOBAL。还允许mysqladmin调试登录 |
| UPDATE                  | 使用UPDATE                                                   |
| USAGE                   | 无访问权限                                                   |

### 常规步骤

```sql
#看到赋予用户账号的权限
SHOW GRANTS FOR 用户名
#赋予权限，可用逗号分割
GRANT 权限，权限，。。。权限 on 特定区域 to 用户名
#撤销权限，把GRANT换成REVOKE即可。
```

### 未来的授权

在使用GRANT和REVOKE时，用户账号必须存在， 但对所涉及的对象没有这个要求。这允许管理员在创建数据库和表之前设计和实现安全措施。

这样做的副作用是，当某个数据库或表被删除时（用DROP语句），相关的访问权限仍然存在。而且，如果将来重新创建该数据库或表，这些权限仍然起作用。

## 更改密码

为了更改用户口令，可使用SET PASSWORD语句。新口令必须如下加密：

```sql
SET PASSWORD = Password('new password');
```

SET PASSWORD更新用户口令。新口令必须传递到Password()函数进行加密。在不指定用户名时，SET PASSWORD更新当前登录用户的口令。
