# MySQL存储引擎、数据类型、工作流程

mysql5.6支持的存储引擎包括InnoDB、MyISAM、MEMORY、CSV、BLACKHOLE、FEDERATED、MRG_MYISAM、ARCHIVE、PERFORMANCE_SCHEMA。其中NDB和InnoDB提供事务安全表，其他存储引擎都是非事务安全表。



## 存储引擎

###### InnoDB

MySql 5.6 版本默认的存储引擎。InnoDB 是一个事务安全的存储引擎，它具备提交、回滚以及崩溃恢复的功能以保护用户数据。InnoDB 的行级别锁定以及 Oracle 风格的一致性无锁读提升了它的多用户并发数以及性能。InnoDB 将用户数据存储在聚集索引中以减少基于主键的普通查询所带来的 I/O 开销。为了保证数据的完整性，InnoDB 还支持外键约束。

###### MyISAM

MyISAM既不支持事务、也不支持外键、其优势是访问速度快，但是表级别的锁定限制了它在读写负载方面的性能，因此它经常应用于只读或者以读为主的数据场景。

###### Memory

在内存中存储所有数据，应用于对非关键数据由快速查找的场景。Memory类型的表访问数据非常快，因为它的数据是存放在内存中的，并且默认使用HASH索引，但是一旦服务关闭，表中的数据就会丢失

###### BLACKHOLE

黑洞存储引擎，类似于 Unix 的 /dev/null，Archive 只接收但却并不保存数据。对这种引擎的表的查询常常返回一个空集。这种表可以应用于 DML 语句需要发送到从服务器，但主服务器并不会保留这种数据的备份的主从配置中。

###### CSV

它的表真的是以逗号分隔的文本文件。CSV 表允许你以 CSV 格式导入导出数据，以相同的读和写的格式和脚本和应用交互数据。由于 CSV 表没有索引，你最好是在普通操作中将数据放在 InnoDB 表里，只有在导入或导出阶段使用一下 CSV 表。

###### NDB

(又名 NDBCLUSTER)——这种集群数据引擎尤其适合于需要最高程度的正常运行时间和可用性的应用。注意：NDB 存储引擎在标准 MySql 5.6 版本里并不被支持。目前能够支持

MySql 集群的版本有：基于 MySql 5.1 的 MySQL Cluster NDB 7.1；基于 MySql 5.5 的 MySQL Cluster NDB 7.2；基于 MySql 5.6 的 MySQL Cluster NDB 7.3。同样基于 MySql 5.6 的 MySQL Cluster NDB 7.4 目前正处于研发阶段。

###### Merge

允许 MySql DBA 或开发者将一系列相同的 MyISAM 表进行分组，并把它们作为一个对象进行引用。适用于超大规模数据场景，如数据仓库。

###### Federated

提供了从多个物理机上联接不同的 MySql 服务器来创建一个逻辑数据库的能力。适用于分布式或者数据市场的场景。

###### Example

这种存储引擎用以保存阐明如何开始写新的存储引擎的 MySql 源码的例子。它主要针对于有兴趣的开发人员。这种存储引擎就是一个啥事也不做的 "存根"。你可以使用这种引擎创建表，但是你无法向其保存任何数据，也无法从它们检索任何索引。



## 数据类型

#### 串数据类型

定长串：接受长度固定的字符串。定长串不允许多于指定的字符数目。它们分配的存储空间与指定的一样多。

变长串：存储可变长度的文本，有些具有最大的定长，有些事完全变长。只有指定的数据得到保存。

区别：

- MySQL处理定长列远比处理变长列快的多

- MySQL不允许对变长列（或一个列的可变部分）进行索引

  | 数据类型   | 说明                                                         |
  | ---------- | ------------------------------------------------------------ |
  | CHAR       | 1~255个字符的定长串。它的长度必须在创建时指定，否则MySQL假定为CHAR(1) |
  | ENUM       | 接受最多64k个串组成的一个预定义集合的某个串                  |
  | LONGTEXT   | 与TEXT相同，但最大长度为4GB                                  |
  | MEDIUMTEXT | 与TEXT相同，但最大长度为16K                                  |
  | SET        | 接受最多64个串组成的一个预定义集合的零个或多个串             |
  | TEXT       | 最大长度为64K的变长文本                                      |
  | TINYTEXT   | 与TEXT相同，但最大长度为255字节                              |
  | VARCHAR    | 长度可变，最多不超过255字节。如果在创建时指定为VARCHAR(n)，则可存储0到n个字符的变长串（其中n<=255) |

**不管使用何种形式的串数据类型，串值都必须括在引号内（通常单引号更好）。**



**如果数值是计算（求和、平均等）中使用的数值，则应该存储在数值数据类型列中。如果作为字符串（可能只包含数字）使用，则应该保存在串数据类型列中。**
**例如：邮政编码的01234如果存储在数值中，保存的值将是1234。**



#### 数值数据类型

MySQL支持多种数值数据类型，每种存储的数值具有不同的取值范围。

数值和串不一样，不应该扩在引号内。

有的数值数据类型支持使用十进制小数点（和小数），而有的则只支持整数。

**符号：**所有数值数据类型（除BIT和BOOLEAN外）都可以有符号或无符号。有符号数值列可以存储正或负的数值，无符号数值列只能存储正数。默认情况为有符号，但如果知道自己不需要存储负值，可以使用UNSIGNED关键字，这样做将允许存储两倍大小的值。

| 数据类型        | 说明                                                         |
| --------------- | ------------------------------------------------------------ |
| BIT             | 位字段，1~64位。（在MySQL5之前，BIT在功能上等价于TINYINT)    |
| BIGINT          | 整数值，支持-9223372036854775808~9223372036854775807（如果是UNSIGNED，为0~18446744073709551615）的数 |
| BOOLEAN(或BOOL) | 布尔标志，或者为0或者为1，主要用于开/关（on/off)标志         |
| DECIMAL(或DEC)  | 精度可变的浮点值                                             |
| DOUBLE          | 双精度浮点值                                                 |
| FLOAT           | 单精度浮点值                                                 |
| INT(或INTEGER)  | 整数值，支持-2147483648~2147483647（如果是UNSIGNEN，为0~4294967295）的数 |
| MEDIUMINT       | 整数值，支持-8388608~8388607(如果是UNSIGNED，为0~16777215)的数 |
| REAL            | 4字节的浮点值                                                |
| SMALLINT        | 整数值，支持-32768~32767（如果是UNSIGNED，为0~65535）的数    |
| TINYINT         | 整数值，支持-128~127（如果为UNSIGNED，为0~255）的数          |

**MySQL中没有专门存储货币的数据类型，一般情况下使用DECIMAL(8, 2)**



#### 日期和时间数据类型

| 数据类型  | 说明                                                         |
| --------- | ------------------------------------------------------------ |
| DATE      | 表示1000-01-01~9999-12-31的日期，格式为YYYY-MM-DD            |
| DATETIME  | DATE和TIME的组合                                             |
| TIMESTAMP | 功能和DATETIME相同（但范围较小）                             |
| TIME      | 格式为HH:MM:SS                                               |
| YEAR      | 用2位数字表示，范围是70（1970）~69（2069年），用四位数字表示，范围是1901~2155年 |



#### 二进制数据类型

二进制数据类型可存储任何数据（甚至包括二进制信息），如图像、多媒体、字处理文档等

| 数据类型   | 说明                  |
| ---------- | --------------------- |
| BLOB       | Blob最大长度为64KB    |
| MEDIUMBLOB | Blob最大长度为16MB    |
| LONGBLOB   | Blob最大长度为4GB     |
| TINYBLOB   | Blob最大长度位255字节 |



## 工作流程

![](https://s3.bmp.ovh/imgs/2022/07/10/84a9c7961e839e89.png)

MySQL架构总共四层，在上图中以虚线作为划分。
　　首先，最上层的服务并不是MySQL独有的，大多数给予网络的客户端/服务器的工具或者服务都有类似的架构。比如：连接处理、授权认证、安全等。
　　第二层的架构包括大多数的MySQL的核心服务。包括：查询解析、分析、优化、缓存以及所有的内置函数（例如：日期、时间、数学和加密函数）。同时，所有的跨存储引擎的功能都在这一层实现：存储过程、触发器、视图等。

　　第三层包含了存储引擎。存储引擎负责MySQL中数据的存储和提取。服务器通过API和存储引擎进行通信。这些接口屏蔽了不同存储引擎之间的差异，使得这些差异对上层的查询过程透明化。存储引擎API包含十几个底层函数，用于执行“开始一个事务”等操作。但存储引擎一般不会去解析SQL（InnoDB会解析外键定义，因为其本身没有实现该功能），不同存储引擎之间也不会相互通信，而只是简单的响应上层的服务器请求。

　　第四层包含了文件系统，所有的表结构和数据以及用户操作的日志最终还是以文件的形式存储在硬盘上。