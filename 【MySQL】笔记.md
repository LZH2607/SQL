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

```mysql
SHOW DATABASES;
```



#### 创建

```mysql
CREATE DATABASE 数据库名;
```

```mysql
CREATE DATABASE
IF NOT EXISTS 数据库名;
```

例如：

```mysql
CREATE DATABASE db;
```

```mysql
CREATE DATABASE
IF NOT EXISTS db;
```



#### 删除

```mysql
DROP DATABASE 数据库名;
```

```mysql
DROP DATABASE
IF EXISTS 数据库名;
```

例如：

```mysql
DROP DATABASE db;
```

```mysql
DROP DATABASE
IF EXISTS db;
```



#### 使用数据库

```mysql
USE 数据库名;
```

例如：

```mysql
USE db;
```



#### 查看当前使用的数据库

```mysql
SELECT
	DATABASE ();
```



### 二、操作表

#### 查询

```mysql
SHOW TABLES;
```



#### 创建

```mysql
CREATE TABLE 表名 (
	字段名1 数据类型1,
	字段名2 数据类型2,
	···
);
```

例如：

```mysql
CREATE TABLE user (
	id INT,
	username VARCHAR (20),
	password VARCHAR (60)
);
```



#### 查看结构

```mysql
DESC 表名;
```

例如：

```mysql
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

```mysql
DROP TABLE 表名;
```

```mysql
DROP TABLE
IF EXISTS 表名;
```

例如：

```mysql
DROP TABLE user;
```

```mysql
DROP TABLE
IF EXISTS user;
```



#### 修改表名

```mysql
ALTER TABLE 表名 RENAME TO 新表名;
```

例如：

```mysql
ALTER TABLE user RENAME TO tb_user;
```



#### 添加一列

```mysql
ALTER TABLE 表名 ADD 列名 数据类型;
```

例如：

```mysql
ALTER TABLE user ADD gender char(1);
```



#### 删除一列

```mysql
ALTER TABLE 表名 DROP 列名;
```

例如：

```mysql
ALTER TABLE user DROP gender;
```



#### 修改列的数据类型

```mysql
ALTER TABLE 表名 MODIFY 列名 新数据类型;
```

例如：

```mysql
ALTER TABLE user MODIFY username VARCHAR (30);
```



#### 修改列名和数据类型

```mysql
ALTER TABLE 表名 CHANGE 列名 新列名 新数据类型;
```

例如：

```mysql
ALTER TABLE user CHANGE password pwd VARCHAR (50);
```



## DML

### 一、添加

#### 给指定列添加一条数据

```mysql
INSERT INTO 表名 (列名1, 列名2, ···)
VALUES
	(值1, 值2, ···);
```

例如：

```mysql
INSERT INTO user (id, username)
VALUES
	(1, "Tom");
```



#### 给全部列添加一条数据

```mysql
INSERT INTO 表名
VALUES
	(值1, 值2, ···);
```

例如：

```mysql
INSERT INTO user
VALUES
	(1, "Tom", "123");
```



#### 给指定列添加多条数据

```mysql
INSERT INTO 表名 (列名1, 列名2, ···)
VALUES
	(值1, 值2, ···),
	(值1, 值2, ···),
	···;
```

例如：

```mysql
INSERT INTO user (id, username)
VALUES
	(1, "Tom"),
	(2, "Jack");
```



#### 给全部列添加多条数据

```mysql
INSERT INTO 表名
VALUES
	(值1, 值2, ···),
	(值1, 值2, ···),
	···;
```

例如：

```mysql
INSERT INTO user
VALUES
	(1, "Tome", "123"),
	(2, "Jack", "456");
```



### 二、修改

#### 修改表中部分数据

```mysql
UPDATE 表名
SET 列名1 = 值1,
 列名2 = 值2,
 ···
WHERE
	条件;
```

例如：

```mysql
UPDATE user
SET username = "Jenny",
 password = "abc"
WHERE
	id = 1;
```



#### 修改表中所有数据

```mysql
UPDATE 表名
SET 列名1 = 值1,
 列名2 = 值2,
 ···;
```

例如：

```mysql
UPDATE user
SET password = NULL;
```



### 三、删除

#### 删除表中部分数据

```mysql
DELETE
FROM
	表名
WHERE
	条件;
```

例如：

```mysql
DELETE
FROM
	USER
WHERE
	id = 2;
```



#### 删除表中所有数据

```mysql
DELETE
FROM
	表名;
```

例如：

```mysql
DELETE
FROM
	USER;
```



## DQL

基础查询：SELECT
条件查询：WHERE
分组查询：GROUP BY
排序查询：ORDER BY
分页查询：LIMIT



### 基础查询

#### 查询表中所有数据的部分字段

```mysql
SELECT
	字段名1,
	字段名2,
	···
FROM
	表名;
```

例如：

```mysql
SELECT
	name,
	age
FROM
	stu;
```



#### 查询表中所有数据的部分字段并去重

```mysql
SELECT DISTINCT
	字段名1,
	字段名2,
	···
FROM
	表名;
```

例如：

```mysql
SELECT DISTINCT
	age
FROM
	stu;
```



#### 查询表中所有数据的部分字段并修改字段名

```mysql
SELECT DISTINCT
	字段名1 AS 新字段名1,
	字段名2 AS 新字段名2,
	···
FROM
	表名;
```

```mysql
SELECT DISTINCT
	字段名1 新字段名1,
	字段名2 新字段名2,
	···
FROM
	表名;
```

例如：

```mysql
SELECT
	name,
	math AS 数学成绩,
	english AS 英语成绩
FROM
	stu;
```

```mysql
SELECT
	name,
	math 数学成绩,
	english 英语成绩
FROM
	stu;
```



#### 查询表中所有数据的全部字段

```mysql
SELECT
	*
FROM
	表名;
```

例如：

```mysql
SELECT
	*
FROM
	stu;
```



### 条件查询

|        符号         |                        功能                        |
| :-----------------: | :------------------------------------------------: |
|          =          |                        等于                        |
|      != 或 <>       |                       不等于                       |
|          >          |                        大于                        |
|         >=          |                      大于等于                      |
|          <          |                        小于                        |
|         <=          |                      小于等于                      |
| BETWEEN ··· AND ··· |                在···和···之间（含）                |
|      AND 或 &&      |                         且                         |
|     OR 或 \|\|      |                         或                         |
|      NOT 或 !       |                         非                         |
|      IN (···)       |                     在···之内                      |
|       IS NULL       |                       是NULL                       |
|     IS NOT NULL     |                      不是NULL                      |
|        LIKE         | 模糊查询<br />_：单个任意字符<br />%：多个任意字符 |

例如：

```mysql
SELECT
	*
FROM
	stu
WHERE
	age = 18;
```

```mysql
SELECT
	*
FROM
	stu
WHERE
	age != 18;
```

```mysql
SELECT
	*
FROM
	stu
WHERE
	age >= 20
AND age <= 30;
```

```mysql
SELECT
	*
FROM
	stu
WHERE
	age BETWEEN 20
AND 30;
```

```mysql
SELECT
	*
FROM
	stu
WHERE
	hire_date >= '1998-09-01'
AND hire_date <= '1999-09-01';
```

```mysql
SELECT
	*
FROM
	stu
WHERE
	hire_date BETWEEN '1998-09-01'
AND '1999-09-01';
```

```mysql
SELECT
	*
FROM
	stu
WHERE
	age = 18
OR age = 20
OR age = 22;
```

```mysql
SELECT
	*
FROM
	stu
WHERE
	age IN (18, 20, 22);
```

```mysql
SELECT
	*
FROM
	stu
WHERE
	english IS NULL;
```

```mysql
SELECT
	*
FROM
	stu
WHERE
	english IS NOT NULL;
```

```mysql
SELECT
	*
FROM
	stu
WHERE
	name LIKE "马%";
```

```mysql
SELECT
	*
FROM
	stu
WHERE
	name LIKE "_花%";
```

```mysql
SELECT
	*
FROM
	stu
WHERE
	name LIKE "%德%";
```



### 排序查询

```mysql
SELECT
	字段名1,
	字段名2,
	···
FROM
	表名
ORDER BY
	排序字段1 排序方式1,
	排序字段2 排序方式2,
	···;
```

排序方式：
	ASC：升序排列（默认）
	DESC：降序排列

例如：

```mysql
SELECT
	*
FROM
	stu
ORDER BY
	age ASC;
```

```mysql
SELECT
	*
FROM
	stu
ORDER BY
	math DESC,
	english ASC;
```



### 聚合函数

|  聚合函数   |   功能   |
| :---------: | :------: |
| count(列名) | 统计数量 |
|  max(列名)  |  最大值  |
|  min(列名)  |  最小值  |
|  sum(列名)  |   总和   |
|  avg(列名)  |  平均值  |

NULL不参与聚合函数的运算

例如：

```mysql
SELECT
	count(*) AS "总人数"
FROM
	stu;
```

```mysql
SELECT
	max(math)
FROM
	stu;
```



### 分组查询

```mysql
SELECT
	字段名1,
	字段名2,
	···
FROM
	表名
WHERE
	条件
GROUP BY
	分组字段名
HAVING
	条件;
```

执行顺序：HAVING ＜ 聚合函数 ＜ WHERE

例如：

```mysql
SELECT
	sex,
	avg(math),
	count(*)
FROM
	stu
GROUP BY
	sex;
```

```mysql
SELECT
	sex,
	avg(math) AS "数学平均分",
	count(*) AS "人数"
FROM
	stu
WHERE
	math > 70
GROUP BY
	sex;
```

```mysql
SELECT
	sex,
	avg(math),
	count(*)
FROM
	stu
WHERE
	math > 70
GROUP BY
	sex
HAVING
	count(*) > 2;
```



### 分页查询

```mysql
SELECT
	字段名1,
	字段名2,
	···
FROM
	表名
LIMIT 起始索引,
 查询条目数;
```

例如：

```mysql
SELECT
	*
FROM
	stu
LIMIT 0,
 3;
```

```mysql
SELECT
	*
FROM
	stu
LIMIT 3,
 3;
```



## 约束	

|   约束   |   关键字    |
| :------: | :---------: |
| 非空约束 |  NOT NULL   |
| 唯一约束 |   UNIQUE    |
| 主键约束 | PRIMARY KEY |
| 检查约束 |    CHECK    |
| 默认约束 |   DEFAULT   |
| 外键约束 | FOREIGN KEY |



### 创建表时添加约束

例如：

```mysql
CREATE TABLE emp (
	eid INT PRIMARY KEY auto_increment,
	ename VARCHAR (50) NOT NULL UNIQUE,
	join_date DATE NOT NULL,
	salary DOUBLE (7, 2) NOT NULL,
	bonus DOUBLE (7, 2) DEFAULT 0,
	dep_id INT,
	CONSTRAINT fk_emp_dep FOREIGN KEY (dep_id) REFERENCES dep (did)
);
```



### 创建表后添加约束

```mysql
-- 添加非空约束
ALTER TABLE 表名 MODIFY 字段名 数据类型 NOT NULL;
```

```mysql
-- 添加唯一约束
ALTER TABLE 表名 MODIFY 字段名 数据类型 UNIQUE;
```

```mysql
-- 添加主键约束
ALTER TABLE 表名 ADD PRIMARY KEY (字段名);
```

```mysql
-- 添加默认约束
ALTER TABLE 表名 ALTER 列名
SET DEFAULT 默认值;
```

```mysql
-- 添加外键约束
ALTER TABLE 表名 ADD CONSTRAINT 外键名 FOREIGN KEY (外键字段名) REFERENCES 主表名 (主表列名);
```



### 创建表后删除约束

```mysql
-- 删除非空约束
ALTER TABLE 表名 MODIFY 字段名 数据类型;
```

```mysql
-- 删除唯一约束
ALTER TABLE 表名 DROP INDEX 字段名;
```

```mysql
-- 删除主键约束
ALTER TABLE 表名 DROP PRIMARY KEY;
```

```mysql
-- 删除默认约束
ALTER TABLE 表名 ALTER 列名 DROP DEFAULT;
```

```mysql
-- 删除外键约束
ALTER TABLE 表名 DROP FOREIGN KEY 外键名;
```



## 多表查询

### 笛卡尔积

```mysql
SELECT
	字段名1,
	字段名2,
	···
FROM
	表名1,
	表名2,
	···;
```

例如：

```mysql
SELECT
	*
FROM
	emp,
	dep;
```



### 连接查询

#### 内连接

```mysql
-- 隐式内连接
SELECT
	字段名1,
	字段名2,
	···
FROM
	表名1,
	表名2,
	···
WHERE
	条件;
```

```mysql
-- 显示内连接
SELECT
	字段名1,
	字段名2,
	···
FROM
	表名1
INNER JOIN 表名2 ON 条件;
```

例如：

```mysql
-- 隐式内连接
SELECT
	*
FROM
	emp,
	dep
WHERE
	emp.dep_id = dep.did;
```

```mysql
-- 显式内连接
SELECT
	*
FROM
	emp
INNER JOIN dep ON emp.dep_id = dep.did;
```



#### 外连接

```mysql
-- 左外连接
SELECT
	字段名1,
	字段名2,
	···
FROM
	表名1
LEFT OUTER JOIN 表名2 ON 条件;
```

```mysql
-- 右外连接
SELECT
	字段名1,
	字段名2,
	···
FROM
	表名1
RIGHT OUTER JOIN 表名2 ON 条件;
```

例如：

```mysql
-- 左外连接
SELECT
	*
FROM
	emp
LEFT OUTER JOIN dep ON emp.dep_id = dep.did;
```

```mysql
-- 右外连接
SELECT
	*
FROM
	emp
RIGHT OUTER JOIN dep ON emp.dep_id = dep.did;
```



### 子查询

#### 单行单列

```mysql
SELECT
	字段名1,
	字段名2,
	···
FROM
	表名
WHERE
	字段名 = (子查询);

-- 使用=、!=、>、>=、<、<=等
```

例如：

```mysql
SELECT
	*
FROM
	emp
WHERE
	salary > (
		SELECT
			salary
		FROM
			emp
		WHERE
			ename = "猪八戒"
	);
```



#### 多行单列

```mysql
SELECT
	字段名1,
	字段名2,
	···
FROM
	表名
WHERE
	字段名 IN (子查询);
```

例如：

```mysql
SELECT
	*
FROM
	emp
WHERE
	dep_id IN (
		SELECT
			did
		FROM
			dep
		WHERE
			dname = "财务部"
		OR dname = "市场部"
	);
```



#### 多行多列

要作为虚拟表

```mysql
SELECT
	字段名1,
	字段名2,
	···
FROM
	(子查询)
WHERE
	条件;
```

例如：

```mysql
SELECT
	*
FROM
	(
		SELECT
			*
		FROM
			emp
		WHERE
			join_date > "2011-11-11"
	) t1,
	dep
WHERE
	t1.dep_id = dep.did;
```



## 事务（Transaction）

### 开启事务

```mysql
START TRANSACTION;
```

```mysql
BEGIN
;
```



### 提交事务

```mysql
COMMIT;
```



### 回滚事务

```mysql
ROLLBACK;
```



### 示例

```mysql
BEGIN
;

UPDATE account
SET money = money - 500
WHERE
	aname = "张三";

UPDATE account
SET money = money + 500
WHERE
	aname = "李四";

COMMIT;

ROLLBACK;
```



### 特征

事务：
	原子性
	一致性
	隔离性
	持久性
