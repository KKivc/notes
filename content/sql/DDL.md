---
title: DDL
source: feishu
space: SQL
---

DDL
数据库操作
查询
查询所有数据库
show databases;
查询当前数据库
Select database();
创建
create database [if not exists] 数据库名 [default charset 字符集] [collate 排序规则];
删除
drop database [if exists] 数据库名;
使用
Use 数据库名;
表操作（表头）
查询
查询当前数据库所有表
show tables;
 查询表结构
desc 表名;
查询指定表的建表语句
show create table 表名;  
创建

create table 表名(
    字段1 字段1类型[comment ‘字段1注释’],
    字段2 字段2类型，
    ...
    字段n 字段n类型
)[comment ‘表注释’]; 

//字段用逗号隔开，最后一个字段不用逗号
修改
添加字段
alter table 表名 add 字段名 类型(长度) [comment 注释];
修改数据类型
alter table 表名 modify 字段名 新数据类型(长度);
修改字段名和字段类型
alter table 表名 change 旧字段名 新字段名 类型(长度);
删除
删除字段
alter table 表名 drop 字段名;
修改表名
alter table 表名 rename to 新表名;
删除表
drop table [if exists] 表名;
删除指定表，并重新创建改表
truncate table 表名;
数值类型

age tinyint unsigned
score decimal(4,1)     100.0
字符串类型
char              0-255 bytes             定长字符串         char(10)  最大存储长度10个字符   即使使用一个字符也会占用10个字符的空间，未占用空间空格补位
varchar          0-65535 bytes          变长字符串     varchar(10)    使用一个字符就占用一个字符空间，会根据所存储的内容计算当前所占用的空间，对比char性能较差
tinyblob         0-255 bytes             不超过255个字符的二进制数据
tinytext          0-255 bytes             短文本字符串
blob              0-65535 bytes          二进制形式的长文本数据
text               0-65535 bytes          长文本数据
mediumblob    0-16777215 bytes     二进制形式的中等长度文本数据
mediumtext    0-16777215 bytes     中等长度文本数据
longblob         0-4294967295 bytes   二进制形式的极大文本数据
longtext           0-4294967295 bytes   极大文本数据
gender char(1)           username varchar(50)
日期类型

birthday date

