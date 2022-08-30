# 【MySQL】笔记



[toc]



## 基本概念

数据库（Database，DB）

数据库管理系统（Database Management System，DBMS）：
	关系型数据库管理系统：Oracle、MySQL、SQL Server、······
	非关系型数据库管理系统：MongoDB，Redis、······

结构化查询语言（Structured Query Language，SQL）

[MySQL Product Archives](https://downloads.mysql.com/archives/community/)

MySQL：
	数据库：文件夹
	数据表：文件（表文件）
	数据：文件（数据文件）

SQL：
	单行/多行书写
	以分号结尾

MySQL：
	不区分大小写
	建议关键字大写

注释：
	单行注释：
		通用：-- 注释
		MySQL特有：# 注释、#注释
	多行注释：
		/\* 注释 \*/、/\*注释\*/

SQL分类：
	DDL：对数据库、表进行操作
	DML：对表进行增、删、改
	DQL：对表进行查询
	DCL：对数据库进行权限控制



启动MySQL服务：

```
net stat mysql
```

连接数据库：

```
mysql -u用户名 -p密码
```

例如：

```
mysql -uroot -p1234
```



## DDL

### 一、操作数据库

#### 查询

```
SHOW DATABASES;
```



#### 创建

```
CREATE DATABASE 数据库名;
CREATE DATABASE IF NOT EXISTS 数据库名;
```

例如：

```
CREATE DATABASE db;
CREATE DATABASE IF NOT EXISTS db;
```



#### 删除

```
DROP DATABASE 数据库名;
DROP DATABASE IF EXISTS 数据库名;
```

例如：

```
DROP DATABASE db;
DROP DATABASE IF EXISTS db;
```



#### 使用数据库

```
USE 数据库名;
```

例如：

```
USE db;
```



#### 查看当前使用的数据库

```
SELECT DATABASE();
```



### 二、操作表

#### 查询

```
SHOW TABLES;
```



#### 创建

```
CREATE TABLE 表名 (
	字段名1 数据类型1,
	字段名2 数据类型2,
	···
	字段名n 数据类型n
)
```

例如：

```
CREATE TABLE user (
	id int,
	username varchar(20),
	password varchar(60)
)
```



#### 查看结构

```
DESC 表名;
```

例如：

```
DESC user;
```



#### 数据类型

MySQL的数据类型：
	数值类型：TINYINT、SMALLINT、MEDIUMINT、INT / INTEGER、BIGINT、FLOAT、DOUBLE、DECIMAL
	日期和时间类型：DATE、TIME、YEAR、DATETIME、TIMESTAMP
	字符串类型：CHAR、VARCHAR、TINYTEXT、TEXT、MEDIUMTEXT、LONGTEXT、TINYBLOB、BLOB、MEDIUMBLOB、LONGBLOB

数值类型：

|   数据类型    | 大小 / 字节 |
| :-----------: | :---------: |
|    TINYINT    |      1      |
|   SMALLINT    |      2      |
|   MEDIUMINT   |      3      |
| INT / INTEGER |      4      |
|    BIGINT     |      8      |
|     FLOAT     |      4      |
|    DOUBLE     |      8      |
|    DECIMAL    |             |

日期和时间类型：

| 数据类型  | 大小 / 字节 |        格式         |
| :-------: | :---------: | :-----------------: |
|   DATE    |      3      |     YYYY-MM-DD      |
|   TIME    |      3      |      HH:MM:SS       |
|   YEAR    |      1      |        YYYY         |
| DATETIME  |      8      | YYYY-MM-DD hh:mm:ss |
| TIMESTAMP |      4      |                     |

字符串类型：

|  数据类型  | 大小 / 字节  |
| :--------: | :----------: |
|    CHAR    |    0~255     |
|  VARCHAR   |   0~65535    |
|  TINYTEXT  |    0~255     |
|    TEXT    |   0~65535    |
| MEDIUMTEXT |  0~16777215  |
|  LONGTEXT  | 0~4294967295 |
|  TINYBLOB  |    0~255     |
|    BLOB    |   0~65535    |
| MEDIUMBLOB |  0~16777215  |
|  LONGBLOB  | 0~4294967295 |



#### 删除

```
DROP TABLE 表名;
DROP TABLE IF EXISTS 表名;
```

例如：

```
DROP TABLE user;
DROP TABLE IF EXISTS user;
```



#### 修改表名

```
ALTER TABLE 表名 RENAME TO 新表名;
```

例如：

```
ALTER TABLE user RENAME TO tb_user;
```



#### 添加一列

```
ALTER TABLE 表名 ADD 列名 数据类型;
```

例如：

```
ALTER TABLE user ADD gender char(1);
```



#### 删除一列

```
ALTER TABLE 表名 DROP 列名;
```

例如：

```
ALTER TABLE user DROP gender;
```



#### 修改列的数据类型

```
ALTER TABLE 表名 MODIFY 列名 新数据类型;
```

例如：

```
ALTER TABLE user MODIFY username varchar(30);
```



#### 修改列名和数据类型

```
ALTER TABLE 表名 CHANGE 列名 新列名 新数据类型;
```

例如：

```
ALTER TABLE user CHANGE password pwd varchar(50);
```

