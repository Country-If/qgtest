# 数据库笔记--SQL语法

## 数据库操作

### 链接数据库

`mysql -u root -p`

### 退出数据库

`exit / quit / ctrl+d`

​	sql语句最后需要有分号结尾(退出数据库可不用分号)

### 显示数据库版本

`select version();`

### 显示时间

`select now();`

### 查看所有数据库

`show databases;`

### 创建数据库，编码设为utf8

`create database 数据库名 charset=utf8；`

### 查看创建数据库的语句

`show create database 数据库名;`

### 查看当前使用的数据库

`select database();`

### 使用数据库

`use 数据库名;`

### 删除数据库

`drop database 数据库名;`

## 数据表操作

### 查看当前数据库中所有表

`show tables;`

### 创建表

`create talbe 数据表名字(字段 类型 约束, 字段 类型 约束, ......)`

eg：(可分行写)

`create table library(`

​	`id int primary key not null auto_increment, `

​	`title varchar(30),`

​	` publisher varchar(30)` 

`);`

##### 	--常用数据类型

​	整数：int, bit

​	小数：decimal(5,2) //表示存五位数，小数占两位

​	字符串：varchar, char

​	日期时间：date, time, datetime

​	枚举类型：enum (枚举类型可用下标代替元素，下标从1开始)

##### 	--约束：

​	auto_increment 表示自动增长

​	not null 表示不能为空

​	primary key 表示主键

​	default 表示默认值

### 查看表的创建语句

`show create table 数据表名`

### 查看表结构

`desc 数据表名;`

### 修改表(alter table)

#### --添加字段(列)

`alter table 数据表名 add 字段名 类型及约束;`

#### --修改字段：不重命名

`alter table 数据表名 modify 字段名 类型及约束;`

#### --修改字段：重命名

`alter table 数据表名 change 原字段名 新字段名 类型及约束;`

#### --删除字段

`alter table 数据表名 drop 字段名;`

#### --删除表

`drop table 数据表名;`

### *数据表中的增删改查(curd)

######    curd的解释：创建(create) 、更新(update) 、读取(read) 、删除(delete)

#### 增加(insert into)

#### --全列插入

`insert into  数据表名 values(......);`

​	values 内的数值需与字段相对应

​	主键字段可用 0 / null / default 来占位

#### --部分插入

`insert into 数据表名 (列1, 列2, ...) values (值1, 值2, ...);`

#### --多行插入

​	values 用逗号隔开，全列插入和部分插入都一样

eg: (以全列插入为例)

`insert into 数据表名 values(...), (...), ... ;`

#### 删除(delete)

#### --物理删除

`delete from 数据表名 where 条件;`

​	无条件则删除整个数据表中所有的数据

#### --逻辑删除(假删)

​	先增加一个字段(字段名：is_delete) (类型：bit ) (默认值：0)表示该信息是否已经不再使用

`alter table 数据表名 add is_delete bit default 0;`

​	将要删除的数据默认值改为1

`update 数据表名 set is_delete=1 where 条件;`

#### 修改(update)

`update 数据表名 set 列1=值1, 列2=值2, ... where 条件;`

#### 查询(select)

#### --查询所有数据

`select * from 数据表名;`

#### --指定条件查询

`select * from 数据表名 where 条件;`

#### --查询指定列

`select 列1, 列2, ... from 数据表名;`

​	可使用 as 为列或表指定别名，增加可读性

`select 列1 as 别名, ... from 数据表名;`

​	字段顺序可调整，先列出来则排在前

### 补充

#### 基础语句

select 查询

insert 插入

update 更新

delete 删除

from 从哪个表

where 查询条件 不同条件可用and / or连接

join 表连接

order by 排序