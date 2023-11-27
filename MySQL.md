# 数据库入门

数据库（Database）指长期存储在计算机内的、有组织的、可共享的数据集合。

数据库管理系统（DBMS）是数据库系统的核心软件之一，是位于用户与操作系统之间的数据管理软件，用于建立，使用和维护数据库。它的主要功能包括数据定义、数据操作、数据库的运行管理、数据库的建立和维护等几个方面。

常说 XX 数据库，其实实质上是 XX 数据库管理系统

**数据库分类**

- 关系型数据库
- 非关系型数据库

## 关系型数据库

关系型数据库是建立在关系模型基础上的数据库，借助于集合代数等数学概念和方法来处理数据库中的数据。简单说，关系型数据库是由多张能互相连接的表组成的数据库。

**优点**

1. 都是使用表结构，格式一致，易于维护。
2. 使用通用的 SQL 语言操作，使用方便，可用于复杂查询。
3. 数据存储在磁盘中，安全。

**缺点**

1. 读写性能比较差，不能满足海量数据的高效率读写。
2. 不节省空间。因为建立在关系模型上，就要遵循某些规则，比如数据中某字段值即使为空仍要分配空间。
3. 固定的表结构，灵活度较低。

常见的关系型数据库有 Oracle、DB2、PostgreSQL、Microsoft SQL Server、Microsoft Access 和 MySQL 等。

## 非关系型数据库

非关系型数据库又被称为 [NoSQL](https://c.biancheng.net/nosql/)（Not Only SQL )，意为不仅仅是 SQL。通常指数据以对象的形式存储在数据库中，而对象之间的关系通过每个对象自身的属性来决定。

**优点**

1. 非关系型数据库存储数据的格式可以是 key-value 形式、文档形式、图片形式等。使用灵活，应用场景广泛，而关系型数据库则只支持基础类型。
2. 速度快，效率高。 NoSQL 可以使用硬盘或者随机存储器作为载体，而关系型数据库只能使用硬盘。
3. 海量数据的维护和处理非常轻松。
4. 非关系型数据库具有扩展简单、高并发、高稳定性、成本低廉的优势。
5. 可以实现数据的分布式处理。

**缺点**

1. 非关系型数据库暂时不提供 SQL 支持，学习和使用成本较高。
2. 非关系数据库没有事务处理，没有保证数据的完整性和安全性。适合处理海量数据，但是不一定安全。
3. 功能没有关系型数据库完善。

常见的非关系型数据库有 Neo4j、[MongoDB](https://c.biancheng.net/mongodb/)、[Redis](https://c.biancheng.net/redis/)、Memcached、MemcacheDB 和 [HBase](https://c.biancheng.net/hbase/) 等。

数据库系统主要有以下 3 个组成部分：

1. 数据库：用于存储数据的地方。
2. 数据库管理系统：用于管理数据库的软件。
3. 数据库应用程序：为了提高数据库系统的处理能力所使用的管理数据库库的软件补充。

## 数据库的组成

数据库（DataBase，DB）提供了一个存储空间来存储各种数据，可以将数据库视为一个存储数据的容器。一个数据库可能包含许多文件，一个数据库系统中通常包含许多数据库。

数据库管理系统（Database Management System，DBMS）是用户创建、管理和维护数据库时所使用的软件，位于用户和操作系统之间，对数据库进行统一管理。DBMS 能定义数据存储结构，提供数据的操作机制，维护数据库的安全性、完整性和可靠性。

虽然已经有了 DBMS，但是在很多情况下，DBMS 无法满足对数据管理的要求。

数据库应用程序（DataBase Application）的使用可以满足对数据管理的更高要求，还可以使数据管理过程更加直观和友好。数据库应用程序负责与 DBMS 进行通信、访问和管理 DBMS 中存储的数据，允许用户插入、修改、删除数据库中的数据。

下面再简单介绍一下 DBMS 提供的一些功能，主要包括以下几个方面。

**数据定义功能**

DBMS 提供数据定义语言（Data Definition Language，DDL），用户通过它可以方便地对数据库中的数据对象进行定义。

**数据操纵功能**

DBMS 还提供数据操纵语言（Data Manipulation Language，DML），用户可以使用 DML 操作数据，实现对数据库的基本操作，如查询、插入、删除和修改等。

**数据库的运行管理**

数据库在建立、运用和维护时由数据库管理系统统一管理、统一控制，以保证数据的安全性、完整性、多用户对数据的并发使用及发生故障后的系统恢复。例如：

- 数据的完整性检查功能保证用户输入的数据应满足相应的约束条件；
- 数据库的安全保护功能保证只有赋予权限的用户才能访问数据库中的数据；
- 数据库的并发控制功能使多个用户可以在同一时刻并发地访问数据库的数据；
- 数据库系统的故障恢复功能使数据库运行出现故障时可以进行数据库恢复，以保证数据库可靠地运行。

**提供方便、有效地存取数据库信息的接口和工具**

编程人员可通过编程语言与数据库之间的接口进行数据库应用程序的开发。数据库管理员（Database Administrator，DBA）可通过提供的工具对数据库进行管理。

> 数据库管理员是维护和管理数据库的专门人员。

**数据库的建立和维护功能**

数据库功能包括数据库初始数据的输入、转换功能，数据库的转储、恢复功能，数据库的重组织功能和性能监控、分析功能等。这些功能通常由一些使用程序来完成。

# MYSQL安装



# MYSQL数据库操作

对数据库进行查询和修改操作的语言叫做 SQL（Structured Query Language，结构化查询语言）。SQL 语言是目前广泛使用的关系数据库标准语言，是各种数据库交互方式的基础。

SQL 包含以下 4 部分：

**数据定义语言（Data Definition Language，DDL）**

用来创建或删除数据库以及表等对象，主要包含以下几种命令：

- DROP：删除数据库和表等对象
- CREATE：创建数据库和表等对象
- ALTER：修改数据库和表等对象的结构

**数据操作语言（Data Manipulation Language，DML）**

用来变更表中的记录，主要包含以下几种命令：

- SELECT：查询表中的数据
- INSERT：向表中插入新数据
- UPDATE：更新表中的数据
- DELETE：删除表中的数据

**数据查询语言（Data Query Language，DQL）**

用来查询表中的记录，主要包含 SELECT 命令，来查询表中的数据。

**数据控制语言（Data Control Language，DCL）**

用来确认或者取消对数据库中的数据进行的变更。除此之外，还可以对数据库中的用户设定权限。主要包含以下几种命令：

- GRANT：赋予用户操作权限
- REVOKE：取消用户的操作权限
- COMMIT：确认对数据库中的数据进行的变更
- ROLLBACK：取消对数据库中的数据进行的变更

## 书写格式

> 对 SQL 本身的关键字进行大写，而对表或者列的名称使用小写，这样可以提高代码的可阅读性和可维护性

**语句以;结尾**

SQL是逐条执行，一句SQL代表一个操作

**语句不分区大小写**

- 关键字大写
- 数据库名、表名和列名等小写

但数据是区分大小写的

**常数的书写方式固定**

在 SQL 语句中直接书写的字符串、日期或者数字等称为常数。常数的书写方式如下所示：

- SQL 语句中含有字符串的时候，需要像 'abc' 这样，使用英文单引号`'`将字符串括起来，用来标识这是一个字符串。
- SQL 语句中含有日期的时候，同样需要使用英文单引号将其括起来。日期的格式有很多种（'26 Jan 2010' 或者'10/01/26' 等），本教程统一使用 '2020-01-26' 这种`'年-月-日'`的格式。
- 在 SQL 语句中书写数字的时候，不需要使用任何符号标识，直接写成 1000 这样的数字即可。

**单词之间需要用空格或换行分割**

不能使用全角空格（中文空格）作为单词的分隔符，否则会发生错误，出现无法预期的结果。

SQL 语句中的标点符号必须都是英文状态下的，即半角字。

## 查看数据库

**查看所有数据库**

```sql
SHOW DATABASES [LIKE '数据库名']
```

语法说明如下：

- LIKE 从句是可选项，用于匹配指定的数据库名称。LIKE 从句可以部分匹配，也可以完全匹配。
- 数据库名由单引号`' '`包围。

```sql
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.00 sec)
```

**创建并查看数据库**

```sql
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.00 sec)

mysql> CREATE DATABASE test_db;
Query OK, 1 row affected (0.00 sec)

mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| test_db            |
+--------------------+
5 rows in set (0.00 sec)
```

**使用LIKE**

先创建三个数据库，名字分别为 test_db、db_test、db_test_db

```sql
mysql> create database db_test;
Query OK, 1 row affected (0.00 sec)
mysql> CREATE DATABASE db_test_db;
Query OK, 1 row affected (0.00 sec)
```

1. 完全匹配

```sql
mysql> SHOW DATABASES LIKE 'test_db';
+--------------------+
| Database (test_db) |
+--------------------+
| test_db            |
+--------------------+
1 row in set (0.01 sec)
```

2. 包含匹配

```sql
mysql> SHOW DATABASES LIKE '%test%';
+-------------------+
| Database (%test%) |
+-------------------+
| db_test           |
| db_test_db        |
| test_db           |
+-------------------+
3 rows in set (0.00 sec)
```

3. 开头匹配

```sql
mysql> SHOW DATABASES LIKE 'db%';
+----------------+
| Database (db%) |
+----------------+
| db_test        |
| db_test_db     |
+----------------+
2 rows in set (0.00 sec)
```

4. 结尾匹配

```sql
mysql> SHOW DATABASES LIKE '%db';
+----------------+
| Database (%db) |
+----------------+
| db_test_db     |
| test_db        |
+----------------+
2 rows in set (0.00 sec)
```

## 创建数据库

```sql
CREATE DATABASE [IF NOT EXISTS] <数据库名>
[[DEFAULT] CHARACTER SET <字符集名>] 
[[DEFAULT] COLLATE <校对规则名>];
```

`[ ]`中的内容是可选的。语法说明如下：

- <数据库名>：创建数据库的名称。MySQL 的数据存储区将以目录方式表示 MySQL 数据库，因此数据库名称必须符合操作系统的文件夹命名规则，不能以数字开头，尽量要有实际意义。注意在 MySQL 中不区分大小写。
- IF NOT EXISTS：在创建数据库之前进行判断，只有该数据库目前尚不存在时才能执行操作。此选项可以用来避免数据库已经存在而重复创建的错误。
- [DEFAULT] CHARACTER SET：指定数据库的字符集。指定字符集的目的是为了避免在数据库中存储的数据出现乱码的情况。如果在创建数据库时不指定字符集，那么就使用系统的默认字符集。
- [DEFAULT] COLLATE：指定字符集的默认校对规则。

>MySQL 的字符集（CHARACTER）和校对规则（COLLATION）是两个不同的概念。字符集是用来定义 MySQL 存储字符串的方式，校对规则定义了比较字符串的方式。

**创建数据库**

```sql
mysql> CREATE DATABASE test_db;
Query OK, 1 row affected (0.12 sec);
```

1 row affected”表示操作只影响了数据库中一行的记录

**指定字符集与校验规则**

```sql
mysql> CREATE DATABASE test_db_char
    -> DEFAULT CHARACTER SET utf8
    -> DEFAULT COLLATE utf8_general_ci;
Query OK, 1 row affected, 2 warnings (0.01 sec)
```

使用`SHOW CREATE DATABASE`可以查看test_db_char数据库的定义声明

![3f67fdaed35acf828009b1ee7823b100](https://gitee.com/qiqibaba43/image/raw/master/202311021624553.png)

## 修改数据库

在 MySQL 数据库中只能对数据库使用的字符集和校对规则进行修改，数据库的这些特性都储存在 db.opt 文件中。

```sql
ALTER DATABASE [数据库名] { 
[ DEFAULT ] CHARACTER SET <字符集名> |
[ DEFAULT ] COLLATE <校对规则名>}
```

语法说明如下：

- ALTER DATABASE 用于更改数据库的全局特性。
- 使用 ALTER DATABASE 需要获得数据库 ALTER 权限。
- 数据库名称可以忽略，此时语句对应于默认数据库。
- CHARACTER SET 子句用于更改默认的数据库字符集。

查看数据库`test_db`数据库的声明属性

![89f71f7e959d6b71681f85349143eed1](https://gitee.com/qiqibaba43/image/raw/master/202311021636767.png)

数据库 test_db 的指定字符集修改为` gb2312`，默认校对规则修改为 `gb2312_unicode_ci`

![53615f243984a975a3a154fce67ae3fa](https://gitee.com/qiqibaba43/image/raw/master/202311021643822.png)

## 删除数据库

 ```sql
 DROP DATABASE [ IF EXISTS ] <数据库名>
 ```

语法说明如下：

- <数据库名>：指定要删除的数据库名。
- IF EXISTS：用于防止当数据库不存在时发生错误。
- DROP DATABASE：删除数据库中的所有表格并同时删除数据库。使用此语句时要非常小心，以免错误删除。如果要使用 DROP DATABASE，需要获得数据库 DROP 权限。

```sql
mysql> DROP DATABASE test_db_char;
Query OK, 0 rows affected (0.01 sec)
```

## 选择数据库

当用 CREATE DATABASE 语句创建数据库之后，该数据库不会自动成为当前数据库，需要用 USE 来指定当前数据库。其语法格式为： 

```sql
    USE <数据库名>
```

将test_db设置为默认数据库

```sql
mysql> USE test_db;
Database changed
```

## MYSQL注释

**单行注释**

- 单行注释可以使用#注释符，#注释符后直接加注释内容。格式如下：

```sql
# 注释内容
```

```sql
mysql> # 使用db_test数据库
mysql> USE db_test;
Database changed
```

- 单行注释可以使用--注释符，--注释符后需要加一个空格，注释才能生效。格式如下： 

```sql
-- 注释内容
```

```sql
mysql> -- 使用db_test_db数据库
mysql> USE db_test_db;
Database changed
```

**多行注释**

多行注释使用/* */注释符。/*用于注释内容的开头，*/用于注释内容的结尾。多行注释格式如下： 

```sql
 /*
  第一行注释内容
  第二行注释内容
*/
```

```sql
mysql> /*sdaih
   /*> da
   /*> */USE test_db;
Database changed
```

## MYSQL大小写规范

![6d253eb407e5a9a6257ee823246f685b](https://gitee.com/qiqibaba43/image/raw/master/202311030853235.png)



# MSYSQL数据类型

数据类型包括：整数类型，浮点数类型和定点数类型，日期和时间类型，字符串类型，二进制类型

## 整数类型类型

|   类型    | 字节数 |
| :-------: | :----: |
|  TINTINT  |   1    |
| SMALLINT  |   2    |
| MEDIUMINT |   3    |
|    INT    |   4    |
|  BINGINT  |   8    |

## 小数类型

浮点类型有两种，分别是单精度浮点数（FLOAT）和双精度浮点数（DOUBLE）；定点类型只有一种，就是 DECIMAL。

浮点类型和定点类型都可以用(M, D)来表示，其中M称为精度，表示总共的位数；D称为标度，表示小数的位数。

浮点数类型的取值范围为 M（1～255）和 D（1～30，且不能大于 M-2），分别表示显示宽度和小数位数。M 和 D 在 FLOAT 和DOUBLE 中是可选的，FLOAT 和 DOUBLE 类型将被保存为硬件所支持的最大精度。DECIMAL 的默认 D 值为 0、M 值为 10。

|     类型     | 字节数 |
| :----------: | :----: |
|    FLOAT     |   4    |
|    DOUBLE    |   8    |
| DECIMAL(M,D) |  M+2   |

在 MySQL 中，定点数以<font color='red'>字符串</font>形式存储，在对精度要求比较高的时候，使用 DECIMAL 的类型比较好

## 日期时间类型

| 类型      | 格式                | 范围                                              | 字节数 |
| --------- | ------------------- | ------------------------------------------------- | ------ |
| YEAR      | YYYY                | 1901 ~ 2155                                       | 1      |
| TIME      | HH:MM:SS            | -838:59:59 ~ 838:59:59                            | 3      |
| DATE      | YYYY-MM-DD          | 1000-01-01 ~ 9999-12-3                            | 3      |
| DATETIME  | YYYY-MM-DD HH:MM:SS | 1000-01-01 00:00:00 ~ 9999-12-31 23:59:59         | 8      |
| TIMESTAMP | YYYY-MM-DD HH:MM:SS | 1980-01-01 00:00:01 UTC ~ 2040-01-19 03:14:07 UTC | 4      |

utc指世界标准时间

**YEAR类型**

- 以 4 位字符串或者 4 位数字格式表示的 YEAR，范围为 '1901'～'2155'。输入格式为 'YYYY' 或者 YYYY，例如，输入 '2010' 或 2010，插入数据库的值均为 2010。
- 以 2 位字符串格式表示的 YEAR，范围为 '00' 到 '99'。'00'～'69' 和 '70'～'99' 范围的值分别被转换为 2000～2069 和 1970～1999 范围的 YEAR 值。'0' 与 '00' 的作用相同。插入超过取值范围的值将被转换为 2000。
- 以 2 位数字表示的 YEAR，范围为 1～99。1～99 和 70～99 范围的值分别被转换为 2001～2069 和 1970～1999 范围的 YEAR 值。注意，在这里 0 值将被转换为 0000，而不是 2000。

**TIME类型**

小时部分如此大的原因是 TIME 类型不仅可以用于表示一天的时间（必须小于 24 小时），还可能是某个事件过去的时间或两个事件之间的时间间隔（可大于 24 小时，或者甚至为负）。

- 'D HH：MM：SS' 格式的字符串。还可以使用这些“非严格”的语法：'HH：MM：SS'、'HH：MM'、'D HH' 或 'SS'。这里的 D 表示日，可以取 0～34 之间的值。在插入数据库时，D 被转换为小时保存，格式为 “D*24+HH”。
- 'HHMMSS' 格式、没有间隔符的字符串或者 HHMMSS 格式的数值，假定是有意义的时间。例如，'101112' 被理解为'10：11：12'，但是 '106112' 是不合法的（它有一个没有意义的分钟部分），在存储时将变为 00：00：00。

**DATE类型**

- 以 'YYYY-MM-DD' 或者 'YYYYMMDD' 字符中格式表示的日期，取值范围为 '1000-01-01'～'9999-12-3'。例如，输入 '2015-12-31' 或者 '20151231'，插入数据库的日期为2015-12-31。
- 以 'YY-MM-DD' 或者 'YYMMDD' 字符串格式表示日期，在这里YY表示两位的年值。MySQL 解释两位年值的规则：'00～69' 范围的年值转换为 '2000~2069'，'70~99' 范围的年值转换为 '1970～1999'。例如，输入 '15-12-31'，插入数据库的日期为 2015-12-31；输入 '991231'，插入数据库的日期为 1999-12-31。
- 以 YYMMDD 数字格式表示的日期，与前面相似，00~69 范围的年值转换为 2000～2069，80～99 范围的年值转换为 1980～1999。例如，输入 151231，插入数据库的日期为 2015-12-31，输入 991231，插入数据库的日期为 1999-12-31。
- 使用 CURRENT_DATE 或者 NOW()，插入当前系统日期。

> 提示：MySQL 允许“不严格”语法：任何标点符号都可以用作日期部分之间的间隔符。例如，'98-11-31'、'98.11.31'、'98/11/31'和'98@11@31' 是等价的，这些值也可以正确地插入数据库。

## 字符串类型

- M表示指定长度
- L表示实际长度

| 类型名称   | 说明       | 字节数                   |
| ---------- | ---------- | ------------------------ |
| CHAR(M)    | 定长字符串 | M字节，1<=M<=255         |
| VARCHAR(M) | 变长字符串 | L+1字节，L<=M，1<=M<=255 |
| TINYTEXT   |            | L+1字节，L<=$2^8$        |
| TEXT       |            | L+2字节，L<=$2^{16}$     |
| MEDIUTEXT  |            | L+3字节，L<=$2^{24}$     |
| LONGTEXT   |            | L+4字节，L<=$2^{32}$     |
| ENUM       | 枚举       | 1或2字节                 |
| SET        | 集合       | 1，2，3，4或8个字节      |

一个 VARCHAR(10) 列能保存一个最大长度为 10 个字符的字符串，实际的存储需要字符串的长度 L 加上一个字节以记录字符串的长度。对于字符 “abcd”，L 是 4，而存储要求 5 个字节。

## 二进制类型

| 类型名称      | 说明             | 字节数                 |
| ------------- | ---------------- | ---------------------- |
| BIT(M)        | 位字段类型       | (M+7)/8 字节，1<=M<=64 |
| BINARY(M)     | 定长二进制字符串 | M 字节                 |
| VARBINARY(M)  | 变长二进制字符串 | M+1 字节               |
| YINYBLOB(M)   |                  | L+1 字节，在此，L<2^8  |
| BLOB(M)       |                  | L+2 字节，在此，L<2^16 |
| MEDIUMBLOB(M) |                  | L+3 字节，在此，L<2^24 |
| LONGBLOB(M)   |                  | L+4 字节，在此，L<2^32 |

# MYSQL存储引擎

在 MySQL 数据库，变量分为系统变量和用户自定义变量。系统变量以 @@ 开头，用户自定义变量以 @ 开头。

使用`SHOW ENGINES`查看当前系统的存储引擎

![f5f902a568c24fef5af02df36d434499](C:\Users\任侠\Documents\Tencent Files\2962298936\nt_qq\nt_data\Pic\2023-11\Ori\f5f902a568c24fef5af02df36d434499.png)

Support 列的值表示某种引擎是否能使用，`YES`表示可以使用，`NO`表示不能使用，`DEFAULT`表示该引擎为当前默认的存储引擎。

## InnoDB引擎

InnoDB是事务型数据库的首选引擎，支持事务安全表（ACID），其它存储引擎都是非事务安全表，支持行锁定和外键，MySQL5.5以后默认使用InnoDB存储引擎。

****

**ACID**

- 原子性（Atomicity）
  原子性是指事务是一个不可分割的工作单位，事务中的操作要么都发生，要么都不发生。
- 一致性（Consistency）
  事务前后数据的完整性必须保持一致。
- 隔离性（Isolation）
  事务的隔离性是多个用户并发访问数据库时，数据库为每一个用户开启的事务，不能被其他事务的操作数据所干扰，多个并发事务之间要相互隔离。
- 持久性（Durability）
  持久性是指一个事务一旦被提交，它对数据库中数据的改变就是永久性的，接下来即使数据库发生故障也不应该对其有任何影响。

****





## MyISAM引擎

MyISAM基于ISAM存储引擎，并对其进行扩展。它是在Web、数据仓储和其他应用环境下最常使用的存储引擎之一。MyISAM拥有较高的插入、查询速度，但不支持事务，不支持外键。





## 修改引擎

**查看默认引擎**

```sql
SHOW VARIABLES LIKE 'default_storage_engine%';
```

```sql
mysql> SHOW VARIABLES LIKE 'default_storage_engine%';
+------------------------+--------+
| Variable_name          | Value  |
+------------------------+--------+
| default_storage_engine | InnoDB |
+------------------------+--------+
1 row in set (0.01 sec)
```

**修改默认引擎**

```sql
SET default_storage_engine=< 存储引擎名 >
```

```sql
mysql> SET default_storage_engine=MyISAM;
Query OK, 0 rows affected (0.00 sec)

mysql> SHOW VARIABLES LIKE 'default_storage_engine%';
+------------------------+--------+
| Variable_name          | Value  |
+------------------------+--------+
| default_storage_engine | MyISAM |
+------------------------+--------+
1 row in set (0.00 sec)
```

<font color='red'>修改完默认引擎后重启Linux，默认引擎依旧是InnoDB</font>

# MYSQL数据表操作

## 创建数据表

```sql
CREATE TABLE <表名> ([表定义选项])[表选项][分区选项];
```

其中，`[表定义选项]`的格式为：

```sql
<列名1> <类型1> [,…] <列名n> <类型n>
```

CREATE TABLE 语句的主要语法及使用说明如下：

- CREATE TABLE：用于创建给定名称的表，必须拥有表CREATE的权限。
- <表名>：指定要创建表的名称，在 CREATE TABLE 之后给出，必须符合标识符命名规则。表名称被指定为 db_name.tbl_name，以便在特定的数据库中创建表。无论是否有当前数据库，都可以通过这种方式创建。在当前数据库中创建表时，可以省略 db-name。如果使用加引号的识别名，则应对数据库和表名称分别加引号。例如，'mydb'.'mytbl' 是合法的，但 'mydb.mytbl' 不合法。
- <表定义选项>：表创建定义，由列名（col_name）、列的定义（column_definition）以及可能的空值说明、完整性约束或表索引组成。
- 默认的情况是，表被创建到当前的数据库中。若表已存在、没有当前数据库或者数据库不存在，则会出现错误。

**创建数据表**

```sql
mysql> CREATE TABLE tb_tmp1
    -> (
    -> id INT(11),
    -> name VARCHAR(25),
    -> deptId INT(11),
    -> salary FLOAT
    -> );
Query OK, 0 rows affected, 2 warnings (0.01 sec)
```

**显示数据表**

```sql
mysql> SHOW TABLES;
+-------------------+
| Tables_in_test_db |
+-------------------+
| tb_tmp1           |
+-------------------+
1 row in set (0.00 sec)
```

## 修改数据表

```sql
ALTER TABLE <表名> [修改选项]
```

修改选项的语法格式如下：

```sql
{ ADD COLUMN <列名> <类型>
| CHANGE COLUMN <旧列名> <新列名> <新列类型>
| ALTER COLUMN <列名> { SET DEFAULT <默认值> | DROP DEFAULT }
| MODIFY COLUMN <列名> <类型>
| DROP COLUMN <列名>
| RENAME TO <新表名>
| CHARACTER SET <字符集名>
| COLLATE <校对规则名> }
```



## 修改/删除字段

**修改字段名称**

```sql
ALTER TABLE <表名> CHANGE <旧字段名> <新字段名> <新数据类型>;
```

其中：

- 旧字段名：指修改前的字段名；
- 新字段名：指修改后的字段名；
- 新数据类型：指修改后的数据类型，如果不需要修改字段的数据类型，可以将新数据类型设置成与原来一样，但数据类型不能为空。

```sql
mysql> ALTER TABLE tb_tmp1 CHANGE deptId deptId1 int(11);
Query OK, 0 rows affected, 1 warning (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 1

mysql> DESC tb_tmp1;
+---------+-------------+------+-----+---------+-------+
| Field   | Type        | Null | Key | Default | Extra |
+---------+-------------+------+-----+---------+-------+
| id      | int         | YES  |     | NULL    |       |
| name    | varchar(25) | YES  |     | NULL    |       |
| deptId1 | int         | YES  |     | NULL    |       |
| salary  | float       | YES  |     | NULL    |       |
+---------+-------------+------+-----+---------+-------+
4 rows in set (0.00 sec)
```

**修改数据类型**

```sql
ALTER TABLE <表名> MODIFY <字段名> <数据类型>
```

其中：

- 表名：指要修改数据类型的字段所在表的名称。
- 字段名：指需要修改的字段。
- 数据类型：指修改后字段的新数据类型。

```sql
mysql> ALTER TABLE tb_tmp1 MODIFY name VARCHAR(20);
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> DESC tb_tmp1;
+---------+-------------+------+-----+---------+-------+
| Field   | Type        | Null | Key | Default | Extra |
+---------+-------------+------+-----+---------+-------+
| id      | int         | YES  |     | NULL    |       |
| name    | varchar(20) | YES  |     | NULL    |       |
| deptId1 | int         | YES  |     | NULL    |       |
| salary  | float       | YES  |     | NULL    |       |
+---------+-------------+------+-----+---------+-------+
4 rows in set (0.00 sec)
```

**删除字段**

```sql
mysql> ALTER TABLE tb_tmp1 DROP deptId1;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> DESC tb_tmp1;
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| id     | int         | YES  |     | NULL    |       |
| name   | varchar(20) | YES  |     | NULL    |       |
| salary | float       | YES  |     | NULL    |       |
+--------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)
```

## 删除数据表

```sql
DROP TABLE [IF EXISTS] 表名1 [ ,表名2, 表名3 ...]
```

对语法格式的说明如下：

- 表名1, 表名2, 表名3 ...表示要被删除的数据表的名称。DROP TABLE 可以同时删除多个表，只要将表名依次写在后面，相互之间用逗号隔开即可。
- IF EXISTS 用于在删除数据表之前判断该表是否存在。如果不加 IF EXISTS，当数据表不存在时 MySQL 将提示错误，中断 SQL 语句的执行；加上 IF EXISTS 后，当数据表不存在时 SQL 语句可以顺利执行，但是会发出警告（warning）。

```sql
mysql> SHOW TABLES;
+-------------------+
| Tables_in_test_db |
+-------------------+
| tb_tmp1           |
| tb_tmp3           |
+-------------------+
2 rows in set (0.00 sec)

mysql> DROP TABLE tb_tmp3;
Query OK, 0 rows affected (0.01 sec)

mysql> SHOW TABLES;
+-------------------+
| Tables_in_test_db |
+-------------------+
| tb_tmp1           |
+-------------------+
1 row in set (0.00 sec)
```

## 删除被关联的主表





## 查看表结构

```sql
DESCRIBE <表名>;
```

或者简写：

```sql
DESC <表名>;
```

```sql
mysql> DESC tb_tmp1;
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| id     | int         | YES  |     | NULL    |       |
| name   | varchar(25) | YES  |     | NULL    |       |
| deptId | int         | YES  |     | NULL    |       |
| salary | float       | YES  |     | NULL    |       |
+--------+-------------+------+-----+---------+-------+
4 rows in set (0.01 sec)
```

其中，各个字段的含义如下：

- Null：表示该列是否可以存储 NULL 值。
- Key：表示该列是否已编制索引。PRI 表示该列是表主键的一部分，UNI 表示该列是 UNIQUE 索引的一部分，MUL 表示在列中某个给定值允许出现多次。
- Default：表示该列是否有默认值，如果有，值是多少。
- Extra：表示可以获取的与给定列有关的附加信息，如 AUTO_INCREMENT 等。

**SHOW CREATE TABLE**

以SQL语句的形式展示表结构

```sql
SHOW CREATE TABLE <表名>;
```

在 SHOW CREATE TABLE 语句的结尾处（分号前面）添加\g或者\G参数可以改变展示形式。

```sql
mysql> SHOW CREATE TABLE tb_tmp1 \g
+---------+--------------------------------------------------------------------------------------------+
| Table   | Create Table                                                                                                                                                                           |
+---------+--------------------------------------------------------------------------------------------+
| tb_tmp1 | CREATE TABLE `tb_tmp1` (
  `id` int DEFAULT NULL,
  `name` varchar(25) DEFAULT NULL,
  `deptId` int DEFAULT NULL,
  `salary` float DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=gb2312 |
+---------+--------------------------------------------------------------------------------------------+
1 row in set (0.00 sec)
```

```sql
mysql> SHOW CREATE TABLE tb_tmp1 \G
*************************** 1. row ***************************
       Table: tb_tmp1
Create Table: CREATE TABLE `tb_tmp1` (
  `id` int DEFAULT NULL,
  `name` varchar(25) DEFAULT NULL,
  `deptId` int DEFAULT NULL,
  `salary` float DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=gb2312
1 row in set (0.00 sec)

```

## 添加字段

```sql
ALTER TABLE <表名> ADD <新字段名><数据类型>[约束条件];
```

对语法格式的说明如下：                                       

- <表名> 为数据表的名字；
- <新字段名> 为所要添加的字段的名字；
- <数据类型> 为所要添加的字段能存储数据的数据类型；
- [约束条件] 是可选的，用来对添加的字段进行约束。

```sql
mysql> DESC tb_tmp1;
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| id     | int         | YES  |     | NULL    |       |
| name   | varchar(20) | YES  |     | NULL    |       |
| salary | float       | YES  |     | NULL    |       |
+--------+-------------+------+-----+---------+-------+
3 rows in set (0.01 sec)

mysql> ALTER TABLE tb_tmp1 ADD depyId int(11);
Query OK, 0 rows affected, 1 warning (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 1

mysql> DESC tb_tmp1;
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| id     | int         | YES  |     | NULL    |       |
| name   | varchar(20) | YES  |     | NULL    |       |
| salary | float       | YES  |     | NULL    |       |
| depyId | int         | YES  |     | NULL    |       |
+--------+-------------+------+-----+---------+-------+
4 rows in set (0.01 sec)
```

一般添加的字段都默认在末尾

**在开头添加字段**

```sql
ALTER TABLE <表名> ADD <新字段名> <数据类型> [约束条件] FIRST;
```

**在中间添加字段**

```sql
ALTER TABLE <表名> ADD <新字段名> <数据类型> [约束条件] AFTER <已经存在的字段名>;
```

```sql
mysql> ALTER TABLE tb_tmp1 ADD age char AFTER name;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> DESC tb_tmp1;
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| id     | int         | YES  |     | NULL    |       |
| name   | varchar(20) | YES  |     | NULL    |       |
| age    | char(1)     | YES  |     | NULL    |       |
| salary | float       | YES  |     | NULL    |       |
| depyId | int         | YES  |     | NULL    |       |
+--------+-------------+------+-----+---------+-------+
5 rows in set (0.00 sec)
```

# MYSQL约束

## 约束概念

- 主键约束：主键是表的一个特殊字段，该字段能唯一标识该表中的每条信息。
- 外键约束：外键约束经常和主键约束一起使用，用来确保数据的一致性。
- 唯一约束：唯一约束与主键约束有一个相似的地方，就是它们都能够确保列的唯一性。与主键约束不同的是，唯一约束在一个表中可以有多个，并且设置唯一约束的列是允许有空值的，虽然只能有一个空值。
- 检查约束：检查约束是用来检查数据表中，字段值是否有效的一个手段。
- 非空约束：非空约束用来约束表中的字段不能为空。
- 默认值约束：默认值约束用来约束当数据表中某个字段不输入值时，自动为其添加一个已经设置好的值。

## MYSQL主键

主键（PRIMARY KEY）的完整称呼是“主键约束”，是 MySQL 中使用最为频繁的约束。

使用主键应注意以下几点：

- 每个表只能定义一个主键。
- 主键值必须唯一标识表中的每一行，且不能为 NULL，即表中不可能存在有相同主键值的两行数据。这是唯一性原则。
- 一个字段名只能在联合主键字段表中出现一次。
- 联合主键不能包含不必要的多余字段。当把联合主键的某一字段删除后，如果剩下的字段构成的主键仍然满足唯一性原则，那么这个联合主键是不正确的。这是最小化原则。

### 创建表时设置主键

**设置单字段主键**

```sql
 <字段名> <数据类型> PRIMARY KEY [默认值]
```

```sql
mysql> CREATE TABLE tb_tmp3
    -> (
    -> id INT(11) PRIMARY KEY,
    -> name VARCHAR(25)
    -> );
Query OK, 0 rows affected, 1 warning (0.01 sec)

mysql> DESC tb_tmp3;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int         | NO   | PRI | NULL    |       |
| name  | varchar(25) | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
2 rows in set (0.00 sec)
```

**定义完后指定**

```sql
[CONSTRAINT <约束名>] PRIMARY KEY [字段名]
```

```sql
mysql> CREATE TABLE tb_emp4
    -> (
    -> id INT(11),
    -> name VARCHAR(25),
    -> deptId INT(11),
    -> salary FLOAT,
    -> PRIMARY KEY(id)
    -> );
Query OK, 0 rows affected (0.37 sec)
mysql> DESC tb_emp4;
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| id     | int(11)     | NO   | PRI | NULL    |       |
| name   | varchar(25) | YES  |     | NULL    |       |
| deptId | int(11)     | YES  |     | NULL    |       |
| salary | float       | YES  |     | NULL    |       |
+--------+-------------+------+-----+---------+-------+
4 rows in set (0.14 sec)
```

**联合主键**

所谓的联合主键，就是这个主键是由一张表中多个字段组成的。

```sql
PRIMARY KEY [字段1，字段2，…,字段n]
```

```sql
mysql> CREATE TABLE tb_emp5
    -> (
    -> name VARCHAR(25),
    -> deptId INT(11),
    -> salary FLOAT,
    -> PRIMARY KEY(name,deptId)
    -> );
Query OK, 0 rows affected (0.37 sec)
mysql> DESC tb_emp5;
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| name   | varchar(25) | NO   | PRI | NULL    |       |
| deptId | int(11)     | NO   | PRI | NULL    |       |
| salary | float       | YES  |     | NULL    |       |
+--------+-------------+------+-----+---------+-------+
3 rows in set (0.14 sec)
```

### 修改表时添加主键

```sql
ALTER TABLE <数据表名> ADD PRIMARY KEY(<字段名>);
```

```sql
mysql> ALTER TABLE tb_emp2
    -> ADD PRIMARY KEY(id);
Query OK, 0 rows affected (0.94 sec)
Records: 0  Duplicates: 0  Warnings: 0
mysql> DESC tb_emp2;
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| id     | int(11)     | NO   | PRI | NULL    |       |
| name   | varchar(30) | YES  |     | NULL    |       |
| deptId | int(11)     | YES  |     | NULL    |       |
| salary | float       | YES  |     | NULL    |       |
+--------+-------------+------+-----+---------+-------+
4 rows in set (0.12 sec)
```

### 删除主键

```sql
ALTER TABLE <数据表名> DROP PRIMARY KEY;
```

```sql
mysql> ALTER TABLE tb_emp2
    -> DROP PRIMARY KEY;
Query OK, 0 rows affected (0.94 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

## 主键自增长

在 MySQL 中，当主键定义为自增长后，这个主键的值就不再需要用户输入数据了，而由数据库系统根据定义自动赋值。每增加一条记录，主键会自动以相同的步长进行增长。

通过给字段添加 AUTO_INCREMENT 属性来实现主键自增长。语法格式如下：

```sql 
字段名 数据类型 AUTO_INCREMENT
```

默认情况下，AUTO_INCREMENT 的初始值是 1，每新增一条记录，字段值自动加 1。
一个表中只能有一个字段使用 AUTO_INCREMENT 约束，且该字段必须有唯一索引，以避免序号重复（即为主键或主键的一部分）。
AUTO_INCREMENT 约束的字段必须具备 NOT NULL 属性。
AUTO_INCREMENT 约束的字段只能是整数类型（TINYINT、SMALLINT、INT、BIGINT 等）。
AUTO_INCREMENT 约束字段的最大值受该字段的数据类型约束，如果达到上限，AUTO_INCREMENT 就会失效。

```sql
mysql> CREATE TABLE test_student(
    -> id INT(4) PRIMARY KEY AUTO_INCREMENT,
    -> name VARCHAR(25) NOT NULL
    -> );
Query OK, 0 rows affected, 1 warning (0.02 sec)

mysql> INSERT INTO test_student(name) VALUES ('Java');
Query OK, 1 row affected (0.00 sec)
mysql> INSERT INTO test_student(name) VALUES ('MySQL');
Query OK, 1 row affected (0.01 sec)
mysql> INSERT INTO test_student(name) VALUES ('Python');
Query OK, 1 row affected (0.00 sec)

mysql> SELECT * FROM test_student;
+----+--------+
| id | name   |
+----+--------+
|  1 | Java   |
|  2 | MySQL  |
|  3 | Python |
+----+--------+
3 rows in set (0.00 sec)
```

**指定自增字段的初始值**

```sql
mysql> CREATE TABLE tb_student( id INT(4) PRIMARY KEY AUTO_INCREMENT, name VARCHAR(25) NOT NULL )AUTO_INCREMENT=100;
Query OK, 0 rows affected, 1 warning (0.01 sec)

mysql> SELECT * FROM test_student;
+----+--------+
| id | name   |
+----+--------+
|  1 | Java   |
|  2 | MySQL  |
|  3 | Python |
+----+--------+
```

## 外键约束

MySQL 外键约束（FOREIGN KEY）是表的一个特殊字段，经常与主键约束一起使用。对于两个具有关联关系的表而言，相关联字段中主键所在的表就是主表（父表），外键所在的表就是从表（子表）。

外键用来建立主表与从表的关联关系，为两个表的数据建立连接，约束两个表中数据的一致性和完整性。

主表删除某条记录时，从表中与之对应的记录也必须有相应的改变。一个表可以有一个或多个外键，外键可以为空值，若不为空值，则每一个外键的值必须等于主表中主键的某个值。

定义外键时，需要遵守下列规则：

- 主表必须已经存在于数据库中，或者是当前正在创建的表。如果是后一种情况，则主表与从表是同一个表，这样的表称为自参照表，这种结构称为自参照完整性。
- 必须为主表定义主键。
- 主键不能包含空值，但允许在外键中出现空值。也就是说，只要外键的每个非空值出现在指定的主键中，这个外键的内容就是正确的。
- 在主表的表名后面指定列名或列名的组合。这个列或列的组合必须是主表的主键或候选键。
- 外键中列的数目必须和主表的主键中列的数目相同。
- 外键中列的数据类型必须和主表主键中对应列的数据类型相同。

### 创建表时设置外键

在 CREATE TABLE 语句中，通过 FOREIGN KEY 关键字来指定外键，具体的语法格式如下：

```sql
 [CONSTRAINT <外键名>] FOREIGN KEY 字段名 [，字段名2，…]
REFERENCES <主表名> 主键列1 [，主键列2，…]
```



```sql
mysql> CREATE TABLE tb_dept1
    -> (
    -> id INT(11) PRIMARY KEY,
    -> name VARCHAR(22) NOT NULL,
    -> location VARCHAR(50)
    -> );
Query OK, 0 rows affected, 1 warning (0.01 sec)

mysql> CREATE TABLE tb_emp6
    -> (
    -> id INT(11) PRIMARY KEY,
    -> name VARCHAR(25),
    -> deptId INT(11),
    -> salary FLOAT,
    -> CONSTRAINT fk_emp_dept1
    -> FOREIGN KEY(deptId) REFERENCES tb_dept1(id)
    -> );
Query OK, 0 rows affected, 2 warnings (0.01 sec)

mysql> DESC tb_emp6;
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| id     | int         | NO   | PRI | NULL    |       |
| name   | varchar(25) | YES  |     | NULL    |       |
| deptId | int         | YES  | MUL | NULL    |       |
| salary | float       | YES  |     | NULL    |       |
+--------+-------------+------+-----+---------+-------+
4 rows in set (0.00 sec)
```

以上语句执行成功之后，在表 tb_emp6 上添加了名称为 fk_emp_dept1 的外键约束，外键名称为 deptId，其依赖于表 tb_dept1 的主键 id。

### 修改表时添加外键

```sql
ALTER TABLE <数据表名> ADD CONSTRAINT <外键名>
FOREIGN KEY(<列名>) REFERENCES <主表名> (<列名>);
```

```sql
mysql> ALTER TABLE tb_emp2
    -> ADD CONSTRAINT fk_tb_dept1
    -> FOREIGN KEY(deptId)
    -> REFERENCES tb_dept1(id);
Query OK, 0 rows affected (1.38 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> SHOW CREATE TABLE tb_emp2\G
*************************** 1. row ***************************
       Table: tb_emp2
Create Table: CREATE TABLE `tb_emp2` (
  `id` int(11) NOT NULL,
  `name` varchar(30) DEFAULT NULL,
  `deptId` int(11) DEFAULT NULL,
  `salary` float DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `fk_tb_dept1` (`deptId`),
  CONSTRAINT `fk_tb_dept1` FOREIGN KEY (`deptId`) REFERENCES `tb_dept1` (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=gb2312
1 row in set (0.12 sec)
```

### 删除外键约束

```sql
ALTER TABLE <表名> DROP FOREIGN KEY <外键约束名>;
```

删除数据表 tb_emp2 中的外键约束 fk_tb_dept1，SQL 语句和运行结果如下所示。

```sql
mysql> ALTER TABLE tb_emp2
    -> DROP FOREIGN KEY fk_tb_dept1;
Query OK, 0 rows affected (0.19 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> SHOW CREATE TABLE tb_emp2\G
*************************** 1. row ***************************
       Table: tb_emp2
Create Table: CREATE TABLE `tb_emp2` (
  `id` int(11) NOT NULL,
  `name` varchar(30) DEFAULT NULL,
  `deptId` int(11) DEFAULT NULL,
  `salary` float DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `fk_tb_dept1` (`deptId`)
) ENGINE=InnoDB DEFAULT CHARSET=gb2312
1 row in set (0.00 sec)
```

## 唯一约束

MySQL 唯一约束（Unique Key）是指所有记录中字段的值不能重复出现。例如，为 id 字段加上唯一性约束后，每条记录的 id 值都是唯一的，不能出现重复的情况。如果其中一条记录的 id 值为‘0001’，那么该表中就不能出现另一条记录的 id 值也为‘0001’。

唯一约束与主键约束相似的是它们都可以确保列的唯一性。不同的是，唯一约束在一个表中可有多个，并且设置唯一约束的列允许有空值，但是只能有一个空值。而主键约束在一个表中只能有一个，且不允许有空值。比如，在用户信息表中，为了避免表中用户名重名，可以把用户名设置为唯一约束。

### 创建表时设置约束

在定义完列之后直接使用 UNIQUE 关键字指定唯一约束，语法格式如下：

```sql
<字段名> <数据类型> UNIQUE
```

```sql
mysql> CREATE TABLE tb_dept2
    -> (
    -> id INT(11) PRIMARY KEY,
    -> name VARCHAR(22) UNIQUE,
    -> location VARCHAR(50)
    -> );
Query OK, 0 rows affected, 1 warning (0.01 sec)

mysql> DESC tb_dept2;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| id       | int         | NO   | PRI | NULL    |       |
| name     | varchar(22) | YES  | UNI | NULL    |       |
| location | varchar(50) | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)
```

### 修改时添加唯一约束

```sql
ALTER TABLE <数据表名> ADD CONSTRAINT <唯一约束名> UNIQUUE (<列名字>);
```

```sql
mysql> ALTER TABLE tb_dept1 
    -> ADD CONSTRAINT unique_name UNIQUE(name);
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> DESC tb_dept1;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| id       | int         | NO   | PRI | NULL    |       |
| name     | varchar(22) | NO   | UNI | NULL    |       |
| location | varchar(50) | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)
```

## 检查约束

### 创建表时检查约束

```sql
CHECK (<检查约束>)
```

在 test_db 数据库中创建 tb_emp7 数据表，要求 salary 字段值大于 0 且小于 10000，SQL 语句和运行结果如下所示

```sql
mysql> CREATE TABLE tb_emp7
    -> (
    -> id INT(11) PRIMARY KEY,
    -> name VARCHAR(25),
    -> deptId INT(11),
    -> salary FLOAT,
    -> CHECK(salary>0 AND salary<100),
    -> FOREIGN KEY(deptId) REFERENCES tb_dept1(id)
    -> );
Query OK, 0 rows affected, 2 warnings (0.01 sec)
```

### 修改时添加检查约束

```sql
ALTER TABLE tb_emp7 ADD CONSTRAINT <检查约束名> CHECK(<检查约束>)
```

```sql
mysql> ALTER TABLE tb_emp7
    -> ADD CONSTRAINT check_id
    -> CHECK(id>0);
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

### 删除检查约束

```sql
ALTER TABLE <数据表名> DROP CONSTRAINT <检查约束名>;
```

```sql
mysql> ALTER TABLE tb_emp7
    -> DROP CONSTRAINT check_id;
Query OK, 0 rows affected (0.00 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

## 默认值

### 创建表时设置默认值

```sql
<字段名><数据类型> DEFAULT <默认值>;
```

```sql
mysql> CREATE TABLE tb_dept3
    -> (
    -> id INT(11) PRIMARY KEY,
    -> name VARCHAR(22),
    -> location VARCHAR(50) DEFAULT 'Beijing'
    -> );
Query OK, 0 rows affected, 1 warning (0.02 sec)

mysql> DESC tb_dept3;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| id       | int         | NO   | PRI | NULL    |       |
| name     | varchar(22) | YES  |     | NULL    |       |
| location | varchar(50) | YES  |     | Beijing |       |
+----------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)
```

### 修改表时设置约束

```sql
 ALTER TABLE <数据表名>
CHANGE COLUMN <字段名> <数据类型> DEFAULT <默认值>;
```

```sql
mysql> ALTER TABLE tb_dept3 
    -> CHANGE COLUMN location
    -> location VARCHAR(50) DEFAULT 'Shanghai';
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> DESC tb_dept3;
+----------+-------------+------+-----+----------+-------+
| Field    | Type        | Null | Key | Default  | Extra |
+----------+-------------+------+-----+----------+-------+
| id       | int         | NO   | PRI | NULL     |       |
| name     | varchar(22) | YES  |     | NULL     |       |
| location | varchar(50) | YES  |     | Shanghai |       |
+----------+-------------+------+-----+----------+-------+
3 rows in set (0.00 sec)
```

### 删除默认约束

```\
ALTER TABLE <数据表名>
CHANGE COLUMN <字段名> <字段名> <数据类型> DEFAULT NULL;
```

```sql
mysql> ALTER TABLE tb_dept3
    -> CHANGE COLUMN location
    -> location VARCHAR(50) DEFAULT NULL;
Records: 0  Duplicates: 0  Warnings: 0
    
mysql> DESC tb_dept3;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| id       | int         | NO   | PRI | NULL    |       |
| name     | varchar(22) | YES  |     | NULL    |       |
| location | varchar(50) | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)

```

## 非空约束

MySQL 非空约束（NOT NULL）指字段的值不能为空。对于使用了非空约束的字段，如果用户在添加数据时没有指定值，数据库系统就会报错。可以通过 CREATE TABLE 或 ALTER TABLE 语句实现。在表中某个列的定义后加上关键字 NOT NULL 作为限定词，来约束该列的取值不能为空。

### 创建表设置非空约束

```sql
<字段名> <数据类型> NOT NULL;
```

```sql
mysql> CREATE TABLE tb_dept4
    -> (
    -> id INT(11) PRIMARY KEY,
    -> name VARCHAR(22) NOT NULL,
    -> location VARCHAR(50)
    -> );
Query OK, 0 rows affected, 1 warning (0.02 sec)

mysql> DESC tb_dept4;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| id       | int         | NO   | PRI | NULL    |       |
| name     | varchar(22) | NO   |     | NULL    |       |
| location | varchar(50) | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)
```

### 修改表时添加非空约束

```sql
ALTER TABLE <数据表名>
CHANGE COLUMN <字段名>
<字段名><数据类型> NOY NULL;
```

```sql
mysql> ALTER TABLE tb_dept4
    -> CHANGE COLUMN location 
    -> location VARCHAR(50) NOT NULL;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> DESC tb_dept4;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| id       | int         | NO   | PRI | NULL    |       |
| name     | varchar(22) | NO   |     | NULL    |       |
| location | varchar(50) | NO   |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)
```

### 删除非空约束

```sql
ALTER TABLE <数据表名>
CHANGE COLUMN <字段名><字段名><数据类型> NULL;
```

```sql
mysql> ALTER TABLE tb_dept4
    -> CHANGE COLUMN location 
    -> location VARCHAR(50) NULL;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> DESC tb_dept4;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| id       | int         | NO   | PRI | NULL    |       |
| name     | varchar(22) | NO   |     | NULL    |       |
| location | varchar(50) | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
3 rows in set (0.01 sec)
```

# 运算符与函数

## 算数运算符

```sql
mysql> CREATE TABLE temp(num INT);
Query OK, 0 rows affected (0.01 sec)

mysql> INSERT INTO temp VALUE (64);
Query OK, 1 row affected (0.01 sec)

mysql> SELECT num,num+10,num+0.5 FROM temp;
+------+--------+---------+
| num  | num+10 | num+0.5 |
+------+--------+---------+
|   64 |     74 |    64.5 |
+------+--------+---------+
1 row in set (0.00 sec)



mysql> SELECT num,num*2,num/2,num/3,num/0 FROM temp;
+------+-------+---------+---------+-------+
| num  | num*2 | num/2   | num/3   | num/0 |
+------+-------+---------+---------+-------+
|   64 |   128 | 32.0000 | 21.3333 |  NULL |
+------+-------+---------+---------+-------+
1 row in set, 1 warning (0.01 sec)

```

## 逻辑运算符

| 运算符    | 作用 |
| --------- | ---- |
| NOT或者！ | 非   |
| AND或者&& | 与   |
| OR和\|\|  | 或   |
| XOR       | 异或 |

NOT和!都是逻辑非运算符，返回和操作数相反的结果，具体语法规则为：

- 当操作数为 0（假）时，返回值为 1；
- 当操作数为非零值时，返回值为 0；
- 当操作数为 NULL 时，返回值为 NULL。

 AND 和 && 都是逻辑与运算符，具体语法规则为：

- 当所有操作数都为非零值并且不为 NULL 时，返回值为 1；
- 当一个或多个操作数为 0 时，返回值为 0；
- 操作数中有任何一个为 NULL 时，返回值为 NULL。

OR 和 || 都是逻辑或运算符，具体语法规则为：

- 当两个操作数都为非 NULL 值时，如果有任意一个操作数为非零值，则返回值为 1，否则结果为 0；
- 当有一个操作数为 NULL 时，如果另一个操作数为非零值，则返回值为 1，否则结果为NULL；
- 假如两个操作数均为 NULL 时，则返回值为 NULL。

XOR 表示逻辑异或，具体语法规则为：

- 当任意一个操作数为 NULL 时，返回值为 NULL；
- 对于非 NULL 的操作数，如果两个操作数都是非 0 值或者都是 0 值，则返回值为 0；
- 如果一个为0值，另一个为非 0 值，返回值为 1。

## 比较运算符

= 运算符用来比较两边的操作数是否相等，相等的话返回 1，不相等的话返回 0。具体的语法规则如下：

- 若有一个或两个操作数为 NULL，则比较运算的结果为 NULL。
- 若两个操作数都是字符串，则按照字符串进行比较。
- 若两个操作数均为整数，则按照整数进行比较。
- 若一个操作数为字符串，另一个操作数为数字，则 MySQL 可以自动将字符串转换为数字。

<=> 操作符和 = 操作符类似，不过 <=> 可以用来判断 NULL 值，具体语法规则为：

- 当两个操作数均为 NULL 时，其返回值为 1 而不为 NULL；
- 而当一个操作数为 NULL 时，其返回值为 0 而不为 NULL。

与 = 的作用相反，<> 和 != 用于判断数字、字符串、表达式是否不相等。

- 如果两侧操作数不相等，返回值为 1，否则返回值为 0；
- 如果两侧操作数有一个是 NULL，那么返回值也是 NULL。

<= 是小于等于运算符，用来判断左边的操作数是否小于或者等于右边的操作数。

- 如果小于或者等于，返回值为 1，否则返回值为 0；
- 如果两侧操作数有一个是 NULL，那么返回值也是 NULL。

IS NULL 或 ISNULL 运算符用来检测一个值是否为 NULL，如果为 NULL，返回值为 1，否则返回值为 0。ISNULL 可以认为是 IS NULL 的简写，去掉了一个空格而已，两者的作用和用法都是完全相同的。

IS NOT NULL 运算符用来检测一个值是否为非 NULL，如果是非 NULL，返回值为 1，否则返回值为 0。

```sql
mysql> SELECT NULL IS NULL，ISNULL(NULL)，ISNULL(10)，10 IS NOT NULL;
+--------------+--------------+------------+----------------+
| NULL IS NULL | ISNULL(NULL) | ISNULL(10) | 10 IS NOT NULL |
+--------------+--------------+------------+----------------+
|            1 |            1 |          0 |              1 |
+--------------+--------------+------------+----------------+
1 row in set (0.01 sec)
```

BETWEEN AND 运算符用来判断表达式的值是否位于两个数之间，或者说是否位于某个范围内，它的语法格式如下：

```
expr BETWEEN min AND max
```

expr 表示要判断的表达式，min 表示最小值，max 表示最大值。如果 expr 大于等于 min 并且小于等于 max，那么返回值为 1，否则返回值为 0。

## 位运算

| 运算符 | 说明   | 格式 |
| ------ | ------ | ---- |
| \|     | 位或   | a\|b |
| &      | 位与   | a&b  |
| ^      | 位异或 | a^b  |
| ~      | 位取反 | ~a   |
| <<     | 位左移 | a<<b |
| >>     | 位右移 | a>>b |

# MySQL查询

插入数据

```sql
INSERT INTO TABLE () VALUES ();
```

## 查询语句

    SELECT
    {* | <字段列名>}
    [
    FROM <表 1>, <表 2>…
    [WHERE <表达式>
    [GROUP BY <group by definition>
    [HAVING <expression> [{<operator> <expression>}…]]
    [ORDER BY <order by definition>]
    [LIMIT[<offset>,] <row count>]
    ]

其中，各条子句的含义如下：

- `{*|<字段列名>}`包含星号通配符的字段列表，表示所要查询字段的名称。
- `<表 1>，<表 2>…`，表 1 和表 2 表示查询数据的来源，可以是单个或多个。
- `WHERE <表达式>`是可选项，如果选择该项，将限定查询数据必须满足该查询条件。
- `GROUP BY< 字段 >`，该子句告诉 MySQL 如何显示查询出来的数据，并按照指定的字段分组。
- `[ORDER BY< 字段 >]`，该子句告诉 MySQL 按什么样的顺序显示查询出来的数据，可以进行的排序有升序（ASC）和降序（DESC），默认情况下是升序。
- `[LIMIT[<offset>，]<row count>]`，该子句告诉 MySQL 每次显示查询出来的数据条数。

### 查询所有字段

查询所有字段是指查询表中所有字段的数据。MySQL 提供了以下 2 种方式查询表中的所有字段。

**使用“*”查询表的所有字段**
SELECT 可以使用“*”查找表中所有字段的数据，语法格式如下：

```
SELECT * FROM 表名;
```

使用“*”查询时，只能按照数据表中字段的顺序进行排列，不能改变字段的排列顺序。

```sql
mysql> INSERT INTO tb_emp1 (id,name,deptId) VALUES (1,"zhangs","xiaoshou");
Query OK, 1 row affected (0.01 sec)

mysql> INSERT INTO tb_emp1 (id,name,deptId) VALUES (2,"lis","qianduan");
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO tb_emp1 (id,name,deptId) VALUES (3,"wangw","houduan");
Query OK, 1 row affected (0.00 sec)

mysql> SELECT * FROM tb_emp1;
+----+--------+----------+
| id | name   | deptId   |
+----+--------+----------+
|  1 | zhangs | xiaoshou |
|  2 | lis    | qianduan |
|  3 | wangw  | houduan  |
+----+--------+----------+
3 rows in set (0.00 sec)
```

### 查询指定字段

```sql
SELECT < 列名 > FROM < 表名 >;
```

```sql
mysql> SELECT name FROM tb_emp1;
+--------+
| name   |
+--------+
| zhangs |
| lis    |
| wangw  |
+--------+
3 rows in set (0.00 sec)

mysql> SELECT name,id,deptId FROM tb_emp1;
+--------+----+----------+
| name   | id | deptId   |
+--------+----+----------+
| zhangs |  1 | xiaoshou |
| lis    |  2 | qianduan |
| wangw  |  3 | houduan  |
+--------+----+----------+
3 rows in set (0.00 sec)
```

## 过滤重复数据

```sql
SELECT DISTINCT <字段名> FROM <表名>;
```

使用 DISTINCT 关键字时需要注意以下几点：

- DISTINCT 关键字只能在 SELECT 语句中使用。
- 在对一个或多个字段去重时，DISTINCT 关键字必须在所有字段的最前面。
- 如果 DISTINCT 关键字后有多个字段，则会对多个字段进行组合去重，也就是说，只有多个字段组合起来完全是一样的情况下才会被去重。

```sql
mysql> SELECT * FROM stu_info;
+----+----------+------+-------+
| id | name     | age  | stuno |
+----+----------+------+-------+
|  1 | zhangsan |   18 |    23 |
|  2 | lisi     |   19 |    24 |
|  3 | wangwu   |   18 |    25 |
|  4 | zhaoliu  |   18 |    26 |
|  5 | zhangsan |   18 |    27 |
|  6 | wangwu   |   20 |    28 |
+----+----------+------+-------+
6 rows in set (0.01 sec)

mysql> SELECT DISTINCT age FROM stu_info;
+------+
| age  |
+------+
|   18 |
|   19 |
|   20 |
+------+
3 rows in set (0.01 sec)

mysql> SELECT DISTINCT name,age FROM stu_info;
+----------+------+
| name     | age  |
+----------+------+
| zhangsan |   18 |
| lisi     |   19 |
| wangwu   |   18 |
| zhaoliu  |   18 |
| wangwu   |   20 |
+----------+------+
5 rows in set (0.00 sec)

mysql> SELECT DISTINCT * FROM stu_info;
+----+----------+------+-------+
| id | name     | age  | stuno |
+----+----------+------+-------+
|  1 | zhangsan |   18 |    23 |
|  2 | lisi     |   19 |    24 |
|  3 | wangwu   |   18 |    25 |
|  4 | zhaoliu  |   18 |    26 |
|  5 | zhangsan |   18 |    27 |
|  6 | wangwu   |   20 |    28 |
+----+----------+------+-------+
6 rows in set (0.00 sec)
```

DISTINCT 只能返回它的目标字段，而无法返回其它字段，所以在实际情况中，我们经常使用 DISTINCT 关键字来返回不重复字段的条数。

```sql
mysql> SELECT COUNT(DISTINCT name,age) FROM stu_info;
+--------------------------+
| COUNT(DISTINCT name,age) |
+--------------------------+
|                        5 |
+--------------------------+
1 row in set (0.00 sec)
```

## 设置别名

**为表指定别名**

```sql
<表名> [AS] <别名>
```

其中各子句的含义如下：

- <表名>：数据库中存储的数据表的名称。
- <别名>：查询时指定的表的新名称。
- AS关键字可以省略，省略后需要将表名和别名用空格隔开。

注意：表的别名不能与该数据库的其它表同名。字段的别名不能与该表的其它字段同名。在条件表达式中不能使用字段的别名。

下面为 stu_info 表指定别名 stu

```sql
mysql> SELECT stu.age,stu.name FROM stu_info AS stu;
+------+----------+
| age  | name     |
+------+----------+
|   18 | zhangsan |
|   19 | lisi     |
|   18 | wangwu   |
|   18 | zhaoliu  |
|   18 | zhangsan |
|   20 | wangwu   |
+------+----------+
6 rows in set (0.00 sec)

```

**为字段指定别名**

```
 <字段名> [AS] <别名>其中，各子句的语法含义如下：
```

- <字段名>：为数据表中字段定义的名称。
- <字段别名>：字段新的名称。
- AS关键字可以省略，省略后需要将字段名和别名用空格隔开。

为 name 指定别名 student_name，为 age 指定别名 student_age

```sql
mysql> SELECT name AS stu_name,age AS stu_age FROM stu_info;
+----------+---------+
| stu_name | stu_age |
+----------+---------+
| zhangsan |      18 |
| lisi     |      19 |
| wangwu   |      18 |
| zhaoliu  |      18 |
| zhangsan |      18 |
| wangwu   |      20 |
+----------+---------+
6 rows in set (0.00 sec)
```

## 限制结果的条数

**指定初始位置**

```sql
LIMIT 初始位置,记录数
```

**不指定初始位置**

```sql
LIMIT 记录数
```

**OFFSET**

```sql
LIMIT 记录数 OFFSET 初始位置
```

## 排序

ORDER BY 关键字主要用来将查询结果中的数据按照一定的顺序进行排序。其语法格式如下：

```sql
ORDER BY <字段名> [ASC|DESC]
```

语法说明如下。

- 字段名：表示需要排序的字段名称，多个字段时用逗号隔开。
- ASC|DESC：`ASC`表示字段按升序排序；`DESC`表示字段按降序排序。其中`ASC`为默认值。

**单字段排序**

```sql
mysql> SELECT * FROM stu_info ORDER BY age;
+----+----------+------+-------+
| id | name     | age  | stuno |
+----+----------+------+-------+
|  1 | zhangsan |   18 |    23 |
|  3 | wangwu   |   18 |    25 |
|  4 | zhaoliu  |   18 |    26 |
|  5 | zhangsan |   18 |    27 |
|  2 | lisi     |   19 |    24 |
|  6 | wangwu   |   20 |    28 |
+----+----------+------+-------+
6 rows in set (0.00 sec)
```

**多字段排序**

```sql
mysql> SELECT * FROM stu_info ORDER BY name,age;
+----+----------+------+-------+
| id | name     | age  | stuno |
+----+----------+------+-------+
|  2 | lisi     |   19 |    24 |
|  3 | wangwu   |   18 |    25 |
|  6 | wangwu   |   20 |    28 |
|  1 | zhangsan |   18 |    23 |
|  5 | zhangsan |   18 |    27 |
|  4 | zhaoliu  |   18 |    26 |
+----+----------+------+-------+
6 rows in set (0.00 sec)
```

在对多个字段进行排序时，排序的第一个字段必须有相同的值，才会对第二个字段进行排序。如果第一个字段数据中所有的值都是唯一的，MySQL 将不再对第二个字段进行排序。

**指定升序，降序**

```sql
mysql> SELECT * FROM stu_info ORDER BY name DESC;
+----+----------+------+-------+
| id | name     | age  | stuno |
+----+----------+------+-------+
|  4 | zhaoliu  |   18 |    26 |
|  1 | zhangsan |   18 |    23 |
|  5 | zhangsan |   18 |    27 |
|  3 | wangwu   |   18 |    25 |
|  6 | wangwu   |   20 |    28 |
|  2 | lisi     |   19 |    24 |
+----+----------+------+-------+
6 rows in set (0.00 sec)
```

## 条件查询

使用 WHERE 关键字的语法格式如下：

```sql
WHERE 查询条件
```

查询条件可以是：

- 带比较运算符和逻辑运算符的查询条件
- 带 BETWEEN AND 关键字的查询条件
- 带 IS NULL 关键字的查询条件
- 带 IN 关键字的查询条件
- 带 LIKE 关键字的查询条件

**单一条件查询语句**

```sql
mysql> SELECT * FROM stu_info 
    -> WHERE age=18;
+----+----------+------+-------+
| id | name     | age  | stuno |
+----+----------+------+-------+
|  1 | zhangsan |   18 |    23 |
|  3 | wangwu   |   18 |    25 |
|  4 | zhaoliu  |   18 |    26 |
|  5 | zhangsan |   18 |    27 |
+----+----------+------+-------+
4 rows in set (0.01 sec)
```

**多条件查询语句**

```sql
mysql> SELECT * FROM stu_info WHERE stuno>25 AND age<20;
+----+----------+------+-------+
| id | name     | age  | stuno |
+----+----------+------+-------+
|  4 | zhaoliu  |   18 |    26 |
|  5 | zhangsan |   18 |    27 |
+----+----------+------+-------+
2 rows in set (0.00 sec)
```

## 模糊查询

在 MySQL 中，LIKE 关键字主要用于搜索匹配字段中的指定内容。其语法格式如下：

```sql
[NOT] LIKE '字符串'
```

其中：

- NOT ：可选参数，字段中的内容与指定的字符串不匹配时满足条件。
- 字符串：指定用来匹配的字符串。“字符串”可以是一个很完整的字符串，也可以包含通配符。

LIKE 关键字支持百分号“%”和下划线“_”通配符。

**%**

“%”是 MySQL 中最常用的通配符，它能代表任何长度的字符串，字符串的长度可以为 0。例如，`a%b`表示以字母 a 开头，以字母 b 结尾的任意长度的字符串。该字符串可以代表 ab、acb、accb、accrb 等字符串。

```sql
mysql> SELECT * FROM stu_info WHERE name LIKE 'z%n';
+----+----------+------+-------+
| id | name     | age  | stuno |
+----+----------+------+-------+
|  1 | zhangsan |   18 |    23 |
|  5 | zhangsan |   18 |    27 |
+----+----------+------+-------+
2 rows in set (0.00 sec)

mysql> SELECT * FROM stu_info WHERE name LIKE '%a%';
+----+----------+------+-------+
| id | name     | age  | stuno |
+----+----------+------+-------+
|  1 | zhangsan |   18 |    23 |
|  3 | wangwu   |   18 |    25 |
|  4 | zhaoliu  |   18 |    26 |
|  5 | zhangsan |   18 |    27 |
|  6 | wangwu   |   20 |    28 |
+----+----------+------+-------+
5 rows in set (0.00 sec)
```

```sql
NOT LIKE ''
```

表示字符串不匹配时满足条件

```sql
mysql> SELECT * FROM stu_info WHERE name NOT LIKE 'z%';
+----+--------+------+-------+
| id | name   | age  | stuno |
+----+--------+------+-------+
|  2 | lisi   |   19 |    24 |
|  3 | wangwu |   18 |    25 |
|  6 | wangwu |   20 |    28 |
+----+--------+------+-------+
3 rows in set (0.00 sec)
```

**_**

“_”只能代表单个字符，字符的长度不能为 0。例如，`a_b`可以代表 acb、adb、aub 等字符串。

```sql
mysql> SELECT * FROM stu_info WHERE name LIKE 'z______';
+----+---------+------+-------+
| id | name    | age  | stuno |
+----+---------+------+-------+
|  4 | zhaoliu |   18 |    26 |
+----+---------+------+-------+
1 row in set (0.00 sec)
```

### 区分大小写

默认情况下，LIKE 关键字匹配字符的时候是不区分大小写的。如果需要区分大小写，可以加入 BINARY 关键字。

```sql
mysql> SELECT * FROM stu_info WHERE name LIKE 'Z%';
+----+----------+------+-------+
| id | name     | age  | stuno |
+----+----------+------+-------+
|  1 | zhangsan |   18 |    23 |
|  4 | zhaoliu  |   18 |    26 |
|  5 | zhangsan |   18 |    27 |
+----+----------+------+-------+
3 rows in set (0.00 sec)

mysql> SELECT * FROM stu_info WHERE name LIKE BINARY 'Z%';
Empty set, 1 warning (0.00 sec)
```

## 范围查询

使用 BETWEEN AND 的基本语法格式如下：

```sql
[NOT] BETWEEN 取值1 AND 取值2
```

其中：

- NOT：可选参数，表示指定范围之外的值。如果字段值不满足指定范围内的值，则这些记录被返回。
- 取值1：表示范围的起始值。
- 取值2：表示范围的终止值。

```sql
mysql> SELECT * FROM stu_info WHERE stuno BETWEEN 25 AND 27;
+----+----------+------+-------+
| id | name     | age  | stuno |
+----+----------+------+-------+
|  3 | wangwu   |   18 |    25 |
|  4 | zhaoliu  |   18 |    26 |
|  5 | zhangsan |   18 |    27 |
+----+----------+------+-------+
3 rows in set (0.00 sec)
```

## 分组查询



## 过滤查询





## 交叉查询





## 过滤分组





## 交叉连接





## 内连接





## 外连接



## 子查询



## 正则查询



# MySQL数据

INSERT VALUES 的语法格式为：

```sql
INSERT INTO <表名> [ <列名1> [ , … <列名n>] ]
VALUES (值1) [… , (值n) ];
```

语法说明如下。

- `<表名>`：指定被操作的表名。
- `<列名>`：指定需要插入数据的列名。若向表中的所有列插入数据，则全部的列名均可以省略，直接采用 INSERT<表名>VALUES(…) 即可。
- `VALUES` 或 `VALUE` 子句：该子句包含要插入的数据清单。数据清单中数据的顺序要和列的顺序相对应。

语法格式为：

```sql
INSERT INTO <表名>
SET <列名1> = <值1>,
    <列名2> = <值2>,
    …
```

此语句用于直接给表中的某些列指定对应的列值，即要插入的数据的列名在 SET 子句中指定，col_name 为指定的列名，等号后面为指定的数据，而对于未指定的列，列值会指定为该列的默认值。

## 修改数据

使用 UPDATE 语句修改单个表，语法格式为：

```sql
UPDATE <表名> SET 字段 1=值 1 [,字段 2=值 2… ] [WHERE 子句 ]
[ORDER BY 子句] [LIMIT 子句]
```

语法说明如下：

- `<表名>`：用于指定要更新的表名称。
- `SET` 子句：用于指定表中要修改的列名及其列值。其中，每个指定的列值可以是表达式，也可以是该列对应的默认值。如果指定的是默认值，可用关键字 DEFAULT 表示列值。
- `WHERE` 子句：可选项。用于限定表中要修改的行。若不指定，则修改表中所有的行。
- `ORDER BY` 子句：可选项。用于限定表中的行被修改的次序。
- `LIMIT` 子句：可选项。用于限定被修改的行数。

```sql
mysql> SELECT * FROM tb_courses;
+----+----------+-------+------------------+
| id | name     | grade | info             |
+----+----------+-------+------------------+
|  1 | Networdk |     3 | Computer Network |
+----+----------+-------+------------------+
1 row in set (0.00 sec)
mysql> UPDATE tb_courses
    -> SET grade=4;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> SELECT * FROM tb_courses;
+----+----------+-------+------------------+
| id | name     | grade | info             |
+----+----------+-------+------------------+
|  1 | Networdk |     4 | Computer Network |
+----+----------+-------+------------------+
1 row in set (0.00 sec)

```

**根据条件修改表中数据**

```sql
mysql> UPDATE tb_courses SET name='DB',grade=3.5
    -> WHERE id=1;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> SELECT * FROM tb_courses;
+----+------+-------+------------------+
| id | name | grade | info             |
+----+------+-------+------------------+
|  1 | DB   |   3.5 | Computer Network |
+----+------+-------+------------------+
1 row in set (0.00 sec)
```

## 删除数据

使用 DELETE 语句从单个表中删除数据，语法格式为：

```sql
DELETE FROM <表名> [WHERE 子句] [ORDER BY 子句] [LIMIT 子句]
```

语法说明如下：

- `<表名>`：指定要删除数据的表名。
- `ORDER BY` 子句：可选项。表示删除时，表中各行将按照子句中指定的顺序进行删除。
- `WHERE` 子句：可选项。表示为删除操作限定删除条件，若省略该子句，则代表删除该表中的所有行。
- `LIMIT` 子句：可选项。用于告知服务器在控制命令被返回到客户端前被删除行的最大值。

```sql
mysql> DELETE FROM tb_courses;
Query OK, 1 row affected (0.00 sec)

mysql> SELECT * FROM tb_courses;
Empty set (0.00 sec)
```

**TRUNCATE 和 DELETE 的区别**

从逻辑上说，TRUNCATE 语句与 DELETE 语句作用相同，但是在某些情况下，两者在使用上有所区别。

- DELETE 是 DML 类型的语句；TRUNCATE 是 DDL 类型的语句。它们都用来清空表中的数据。
- DELETE 是逐行一条一条删除记录的；TRUNCATE 则是直接删除原来的表，再重新创建一个一模一样的新表，而不是逐行删除表中的数据，执行数据比 DELETE 快。因此需要删除表中全部的数据行时，尽量使用 TRUNCATE 语句， 可以缩短执行时间。
- DELETE 删除数据后，配合事件回滚可以找回数据；TRUNCATE 不支持事务的回滚，数据删除后无法找回。
- DELETE 删除数据后，系统不会重新设置自增字段的计数器；TRUNCATE 清空表记录后，系统会重新设置自增字段的计数器。
- DELETE 的使用范围更广，因为它可以通过 WHERE 子句指定条件来删除部分数据；而 TRUNCATE 不支持 WHERE 子句，只能删除整体。
- DELETE 会返回删除数据的行数，但是 TRUNCATE 只会返回 0，没有任何意义。

# 视图与索引

MySQL 视图（View）是一种虚拟存在的表，同真实表一样，视图也由列和行构成，但视图并不实际存在于数据库中。行和列的数据来自于定义视图的查询中所使用的表，并且还是在使用视图时动态生成的。

视图并不同于数据表，它们的区别在于以下几点：

- 视图不是数据库中真实的表，而是一张虚拟表，其结构和数据是建立在对数据中真实表的查询基础上的。
- 存储在数据库中的查询操作 SQL 语句定义了视图的内容，列数据和行数据来自于视图查询所引用的实际表，引用视图时动态生成这些数据。
- 视图没有实际的物理记录，不是以数据集的形式存储在数据库中的，它所对应的数据实际上是存储在视图所引用的真实表中的。
- 视图是数据的窗口，而表是内容。表是实际数据的存放单位，而视图只是以不同的显示方式展示数据，其数据来源还是实际表。
- 视图是查看数据表的一种方法，可以查询数据表中某些字段构成的数据，只是一些 SQL 语句的集合。从安全的角度来看，视图的数据安全性更高，使用视图的用户不接触数据表，不知道表结构。
- 视图的建立和删除只影响视图本身，不影响对应的基本表。

## 创建视图

```sql
CREATE VIEW <视图名> AS <SELECT语句>
```

语法说明如下。

- `<视图名>`：指定视图的名称。该名称在数据库中必须是唯一的，不能与其他表或视图同名。
- `<SELECT语句>`：指定创建视图的 SELECT 语句，可用于查询多个基础表或源视图。

对于创建视图中的 SELECT 语句的指定存在以下限制：

- 用户除了拥有 CREATE VIEW 权限外，还具有操作中涉及的基础表和其他视图的相关权限。
- SELECT 语句不能引用系统或用户变量。
- SELECT 语句不能包含 FROM 子句中的子查询。
- SELECT 语句不能引用预处理语句参数。

**单表**

```sql
mysql> SELECT * FROM stu_info;
+----+----------+------+-------+
| id | name     | age  | stuno |
+----+----------+------+-------+
|  1 | zhangsan |   18 |    23 |
|  2 | lisi     |   19 |    24 |
|  4 | zhaoliu  |   18 |    26 |
|  5 | zhangsan |   18 |    27 |
|  6 | wangwu   |   20 |    28 |
+----+----------+------+-------+
5 rows in set (0.01 sec)

mysql> CREATE VIEW view
    -> AS SELECT id,name FROM stu_info;
Query OK, 0 rows affected (0.00 sec)

mysql> SELECT * FRom view;
+----+----------+
| id | name     |
+----+----------+
|  1 | zhangsan |
|  2 | lisi     |
|  4 | zhaoliu  |
|  5 | zhangsan |
|  6 | wangwu   |
+----+----------+
5 rows in set (0.00 sec)
```

**多表**







## 查询视图

```sql
DESC 视图名;
```

```sql
mysql> DESC view;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int         | NO   |     | 0       |       |
| name  | varchar(25) | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
2 rows in set (0.00 sec)
```

```sql
SHOW CREATE VIEW 视图名;
```

```sql
mysql> SHOW CREATE VIEW view\G;
*************************** 1. row ***************************
                View: view
         Create View: CREATE ALGORITHM=UNDEFINED DEFINER=`root`@`localhost` SQL SECURITY DEFINER VIEW `view` AS select `stu_info`.`id` AS `id`,`stu_info`.`name` AS `name` from `stu_info`
character_set_client: utf8mb4
collation_connection: utf8mb4_0900_ai_ci
1 row in set (0.00 sec)
```

## 修改视图

```sql
ALTER VIEW <视图名> AS <SELECT语句>
```

视图是一个虚拟表，实际的数据来自于基本表，所以通过插入、修改和删除操作更新视图中的数据，实质上是在更新视图所引用的基本表的数据。

视图包含以下结构中的任何一种，它就是不可更新的：

- 聚合函数 SUM()、MIN()、MAX()、COUNT() 等。
- DISTINCT 关键字。
- GROUP BY 子句。
- HAVING 子句。
- UNION 或 UNION ALL 运算符。
- 位于选择列表中的子查询。
- FROM 子句中的不可更新视图或包含多个表。
- WHERE 子句中的子查询，引用 FROM 子句中的表。
- ALGORITHM 选项为 TEMPTABLE（使用临时表总会使视图成为不可更新的）的时候。

## 删除视图

```sql
DROP VIEW <视图名1> [ , <视图名2> …]
```

## 创建索引

**CREATE INDEX**

索引就是根据表中的一列或若干列按照一定顺序建立的列值与记录行之间的对应关系表，实质上是一张描述索引列的列值与原表中记录行之间一 一对应关系的有序表。

```sql
CREATE <索引名> ON <表名> (<列名> [<长度>] [ ASC | DESC])
```

语法说明如下：

- `<索引名>`：指定索引名。一个表可以创建多个索引，但每个索引在该表中的名称是唯一的。
- `<表名>`：指定要创建索引的表名。
- `<列名>`：指定要创建索引的列名。通常可以考虑将查询语句中在 JOIN 子句和 WHERE 子句里经常出现的列作为索引列。
- `<长度>`：可选项。指定使用列前的 length 个字符来创建索引。使用列的一部分创建索引有利于减小索引文件的大小，节省索引列所占的空间。在某些情况下，只能对列的前缀进行索引。索引列的长度有一个最大上限 255 个字节（MyISAM 和 InnoDB 表的最大上限为 1000 个字节），如果索引列的长度超过了这个上限，就只能用列的前缀进行索引。另外，BLOB 或 TEXT 类型的列也必须使用前缀索引。
- `ASC|DESC`：可选项。`ASC`指定索引按照升序来排列，`DESC`指定索引按照降序来排列，默认为`ASC`。

**CREATE TABLE**

索引也可以在创建表（CREATE TABLE）的同时创建。在 CREATE TABLE 语句中添加以下语句。语法格式：

```sql
CONSTRAINT PRIMARY KEY [索引类型] (<列名>,…)
```

在 CREATE TABLE 语句中添加此语句，表示在创建新表的同时创建该表的主键。

语法格式：

```sql
KEY | INDEX [<索引名>] [<索引类型>] (<列名>,…)
```

在 CREATE TABLE 语句中添加此语句，表示在创建新表的同时创建该表的索引。

语法格式：

```sql
UNIQUE [ INDEX | KEY] [<索引名>] [<索引类型>] (<列名>,…)
```

在 CREATE TABLE 语句中添加此语句，表示在创建新表的同时创建该表的唯一性索引。

语法格式：

```sql
FOREIGN KEY <索引名> <列名>
```

在 CREATE TABLE 语句中添加此语句，表示在创建新表的同时创建该表的外键。

在使用 CREATE TABLE 语句定义列选项的时候，可以通过直接在某个列定义后面添加 PRIMARY KEY 的方式创建主键。而当主键是由多个列组成的多列索引时，则不能使用这种方法，只能用在语句的最后加上一个 PRIMARY KRY(<列名>，…) 子句的方式来实现。

**ALTER TABLE**

语法格式：

```sql
ADD INDEX [<索引名>] [<索引类型>] (<列名>,…)
```

在 ALTER TABLE 语句中添加此语法成分，表示在修改表的同时为该表添加索引。

语法格式：

ADD PRIMARY KEY [<索引类型>] (<列名>,…)

在 ALTER TABLE 语句中添加此语法成分，表示在修改表的同时为该表添加主键。

语法格式：

```sql
ADD UNIQUE [ INDEX | KEY] [<索引名>] [<索引类型>] (<列名>,…)
```

在 ALTER TABLE 语句中添加此语法成分，表示在修改表的同时为该表添加唯一性索引。

语法格式：

```sql
ADD FOREIGN KEY [<索引名>] (<列名>,…)
```

在 ALTER TABLE 语句中添加此语法成分，表示在修改表的同时为该表添加外键。







# 事务

## 特性

数据库的**事务（Transaction）**是一种机制、一个操作序列，包含了一组数据库操作命令。事务把所有的命令作为一个整体一起向系统提交或撤销操作请求，即这一组数据库命令要么都执行，要么都不执行，因此事务是一个不可分割的工作逻辑单元。

在数据库系统上执行并发操作时，事务是作为最小的控制单元来使用的，特别适用于多用户同时操作的数据库系统。例如，航空公司的订票系统、银行、保险公司以及证券交易系统等。

事务具有 4 个特性，即原子性（Atomicity）、一致性（Consistency）、隔离性（Isolation）和持久性（Durability），这 4 个特性通常简称为 ACID。

### 原子性

事务是一个完整的操作。事务的各元素是不可分的（原子的）。事务中的所有元素必须作为一个整体提交或回滚。如果事务中的任何元素失败，则整个事务将失败。

以银行转账事务为例，如果该事务提交了，则这两个账户的数据将会更新。如果由于某种原因，事务在成功更新这两个账户之前终止了，则不会更新这两个账户的余额，并且会撤销对任何账户余额的修改，事务不能部分提交。

### 一致性

当事务完成时，数据必须处于一致状态。也就是说，在事务开始之前，数据库中存储的数据处于一致状态。在正在进行的事务中. 数据可能处于不一致的状态，如数据可能有部分被修改。然而，当事务成功完成时，数据必须再次回到已知的一致状态。通过事务对数据所做的修改不能损坏数据，或者说事务不能使数据存储处于不稳定的状态。

以银行转账事务事务为例。在事务开始之前，所有账户余额的总额处于一致状态。在事务进行的过程中，一个账户余额减少了，而另一个账户余额尚未修改。因此，所有账户余额的总额处于不一致状态。事务完成以后，账户余额的总额再次恢复到一致状态。

### 隔离性

对数据进行修改的所有并发事务是彼此隔离的，这表明事务必须是独立的，它不应以任何方式依赖于或影响其他事务。修改数据的事务可以在另一个使用相同数据的事务开始之前访问这些数据，或者在另一个使用相同数据的事务结束之后访问这些数据。

另外，当事务修改数据时，如果任何其他进程正在同时使用相同的数据，则直到该事务成功提交之后，对数据的修改才能生效。张三和李四之间的转账与王五和赵二之间的转账，永远是相互独立的。

### 持久性

事务的持久性指不管系统是否发生了故障，事务处理的结果都是永久的。

一个事务成功完成之后，它对数据库所作的改变是永久性的，即使系统出现故障也是如此。也就是说，一旦事务被提交，事务对数据所做的任何变动都会被永久地保留在数据库中。

事务的 ACID 原则保证了一个事务或者成功提交，或者失败回滚，二者必居其一。因此，它对事务的修改具有可恢复性。即当事务失败时，它对数据的修改都会恢复到该事务执行前的状态。

## 语法与流程

为了维护 MySQL 服务器，经常需要在 MySQL 数据库中进行日志操作：

- UNDO 日志：复制事务执行前的数据，用于在事务发生异常时回滚数据。
- REDO 日志：记录在事务执行中，每条对数据进行更新的操作，当事务提交时，该内容将被刷新到磁盘。

SQL 使用下列语句来管理事务。

**开始事务**

```sql
BEGIN;
```

**提交事务**

MySQL 使用下面的语句来提交事务：

```sql
COMMIT;
```

将事务中所有对数据库的更新都写到磁盘上的物理数据库中，事务正常结束。

**回滚事务**

```sql
ROLLBACK;
```

在事务运行的过程中发生了某种故障，事务不能继续执行，系统将事务中对数据库的所有已完成的操作全部撤销，回滚到事务开始时的状态。
