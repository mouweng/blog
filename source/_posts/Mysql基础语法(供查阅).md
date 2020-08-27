---
title: Mysql基础语法(供查阅)
date: 2020-08-26 23:41:12
categories: 
           - mysql
tags:
           - mysql
           - 语法
---
## 一、数据库管理

![](https://img.shields.io/badge/dynamic/json?color=ff69b4&label=某翁萨达&query=%24.data.totalSubs&url=https%3A%2F%2Fapi.spencerwoo.com%2Fsubstats%2F%3Fsource%3Dbilibili%26queryKey%3D287263504&logo=Bilibili)![](https://img.shields.io/badge/dynamic/json?color=ee0000&label=某翁萨达&query=%24.data.totalSubs&url=https%3A%2F%2Fapi.spencerwoo.com%2Fsubstats%2F%3Fsource%3Dweibo%26queryKey%3D6226103853&logo=Sina%20Weibo)![](https://img.shields.io/badge/dynamic/json?color=success&label=mouweng&query=%24.data.totalSubs&url=https%3A%2F%2Fapi.spencerwoo.com%2Fsubstats%2F%3Fsource%3Dgithub%26queryKey%3Dmouweng&logo=GitHub)

# 启动数据库
## 启动数据库
### 启动数据库
#### 启动数据库
##### 启动数据库



```mysql
# mysql -h主机名  -u用户名 -p密码
mysql -hlocalhost -uroot -p
```

##### 退出数据库

```mysql
quit
exit
\q
```

##### create 创建数据库

```mysql
create database testDB;
```

##### show 查看所有数据库

```mysql
show databases;
```

##### alter 修改数据库

```mysql
alter database testDB character set utf8;
```

##### use 使用数据库

```mysql
#选择某个数据库
use testDB;
# 查看当前使用的数据库
select database();
```

##### drop 删除数据库

```mysql
drop database testDB;
```

## 二、表管理

##### create 创建表

```mysql
create table  T_PEOPLE (
  -> id int auto_increment primary key,
  -> name varchar(20) not null,
  -> age int not null,
  -> birthday datetime);
```

##### drop 删除表

```
drop table newtable;
```

##### show 显示表

```mysql
show tables;
```

##### desc 查看表结构

```mysql
desc T_PEOPLE;
```

alter 修改表结构（增、删、改）

```mysql
# 将表编码设置为utf8
alter table T_PEOPLE convert to character set utf8;
# insert 在表中添加列（字段）
alter table T_PEOPLE add star BOOL;
# alter 删除（列）字段
alter table T_PEOPLE DROP column star;
# 重命名表
rename table T_PEOPLE TO NEW_PEOPLE;
```

##### create 利用已有数据创建新表

```mysql
create table newTable select * from T_PEOPLE;
```

## 三、数据的操作及管理

##### 增加数据（增）

```mysql
insert into T_PEOPLE VALUES (null, 'yifan', 18, '1998-04-03');
```

##### 删除数据（删）

```mysql
delete from t_people where name  = 'yifan';
```

##### 修改数据（改）

```mysql
update t_people set name = 'ok' where id = 1 AND age = 22;
```

##### 查询数据（查）

```mysql
mysql> select * from t_people;
+----+---------+-----+---------------------+
| ID | NAME    | AGE | BIRTHDAY            |
+----+---------+-----+---------------------+
|  1 | ok      |  22 | 1992-05-22 00:00:00 |
|  3 | mouweng |  23 | 1998-01-01 00:00:00 |
|  4 | fanfan  |  24 | 1998-01-01 00:00:00 |
+----+---------+-----+---------------------+
3 rows in set (0.00 sec)
```

##### ORDER BY

默认是ASC，不用写出

```mysql
# 以age从小到大的顺序排序
mysql> select * from t_people order by age;
+----+---------+-----+---------------------+
| ID | NAME    | AGE | BIRTHDAY            |
+----+---------+-----+---------------------+
|  1 | ok      |  22 | 1992-05-22 00:00:00 |
|  3 | mouweng |  23 | 1998-01-01 00:00:00 |
|  4 | fanfan  |  24 | 1998-01-01 00:00:00 |
+----+---------+-----+---------------------+
3 rows in set (0.00 sec)

# 先以birthday从小到大，再以age从大到小
mysql> select * from t_people order by birthday,age DESC;
+----+---------+-----+---------------------+
| ID | NAME    | AGE | BIRTHDAY            |
+----+---------+-----+---------------------+
|  1 | ok      |  22 | 1992-05-22 00:00:00 |
|  4 | fanfan  |  24 | 1998-01-01 00:00:00 |
|  3 | mouweng |  23 | 1998-01-01 00:00:00 |
+----+---------+-----+---------------------+
3 rows in set (0.00 sec)

# 先以birthday从小到大，再以age从小到大
mysql> select * from t_people order by birthday,age ASC;
+----+---------+-----+---------------------+
| ID | NAME    | AGE | BIRTHDAY            |
+----+---------+-----+---------------------+
|  1 | ok      |  22 | 1992-05-22 00:00:00 |
|  3 | mouweng |  23 | 1998-01-01 00:00:00 |
|  4 | fanfan  |  24 | 1998-01-01 00:00:00 |
+----+---------+-----+---------------------+
3 rows in set (0.00 sec)
```

##### DISTINCT

```mysql
# 用于返回唯一的不同的值
mysql> select distinct birthday from t_people;
+---------------------+
| birthday            |
+---------------------+
| 1992-05-22 00:00:00 |
| 1998-01-01 00:00:00 |
+---------------------+
2 rows in set (0.01 sec)
```



## 四、高级拓展

##### Limit

```mysql
# 返回前2条记录
mysql> select * from t_people limit 2;
+----+---------+-----+---------------------+
| ID | NAME    | AGE | BIRTHDAY            |
+----+---------+-----+---------------------+
|  1 | ok      |  22 | 1992-05-22 00:00:00 |
|  3 | mouweng |  23 | 1998-01-01 00:00:00 |
+----+---------+-----+---------------------+
2 rows in set (0.00 sec)

# 返回第二条和第三条记录
mysql> select * from t_people limit 1,3;
+----+---------+-----+---------------------+
| ID | NAME    | AGE | BIRTHDAY            |
+----+---------+-----+---------------------+
|  3 | mouweng |  23 | 1998-01-01 00:00:00 |
|  4 | fanfan  |  24 | 1998-01-01 00:00:00 |
+----+---------+-----+---------------------+
2 rows in set (0.00 sec)
```

##### Like

> LIKE 操作符用于在 WHERE 子句中搜索列中的指定模式。通配符规则使用如下

| 通配符 | 描述               |
| :----- | :----------------- |
| %      | 替代一个或多个字符 |
| _      | 仅替代一个字符     |

```mysql
mysql> select * from t_people where name like '%w%';
+----+---------+-----+---------------------+
| ID | NAME    | AGE | BIRTHDAY            |
+----+---------+-----+---------------------+
|  3 | mouweng |  23 | 1998-01-01 00:00:00 |
+----+---------+-----+---------------------+
1 row in set (0.00 sec)

mysql> select * from t_people where name like 'm_uweng';
+----+---------+-----+---------------------+
| ID | NAME    | AGE | BIRTHDAY            |
+----+---------+-----+---------------------+
|  3 | mouweng |  23 | 1998-01-01 00:00:00 |
+----+---------+-----+---------------------+
1 row in set (0.00 sec)
```





in



between



as



join

Inner join

left join

right join

Full join





union





##### 数学函数



##### 聚合函数



##### Group by

