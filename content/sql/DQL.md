---
title: DQL
space: SQL
---



# 查询

## 查询多个字段

```sql
select 字段1,字段2,字段3,... from 表名;
select * from 表名;
```

## 查询且设置别名

### 表别名

`select * from 表名 as 别名;`

### 列别名

`select 字段1 [as 别名1], 字段2[as 别名2] ... from 表名;`

## 查询去除重复记录

`select distinct 字段名 from 表名;`

## 算术运算符

`select price +10 as new_price from product；`

- 多个列求和：`select name, chinese+english+math as total from stu;`

## 条件查询

`select 字段列表 from 表名 where 条件;`

### 条件

- not in ():不在范围内的；not：与之前相反

- 多条件不能用逗号隔开要用and，字段才可以用逗号

  - //like：'_'匹配一个字符        '%'任意个字符,可多个

  ```sql
  select * from stu where math in(80,90,92); #查询数学成绩是80/90/92的人
  select * from emp where name like '__';
  select * from emp where idcard like '%X';
  select * from emp where idcard is null;
  select * from emp where gender = '女' and age in(20,21,22,23);  #年龄为20、21、22、23的女性
  ```

  ### 聚合函数

  - max、min、avg平均值、sum==单列==求和、count计不为null行数

  ```sql
  
  select 聚合函数(字段列表) from 表名;
  select count(*) from emp;   #总人数
  select avg(age) from emp;  #平均年龄
  select sum(age) from emp where workaddress = '西安';
  ```

  ### 注意

  - null值不参与聚合函数的计数

  ### 分组查询

  - select后面只能跟==分组字段名和聚合函数==
  
  ```sql
  #语法
  select 分组字段名 from 表名 [where 条件] group by 分组字段名 [having 分组后过滤条件];
  
  select gender, count(*) from emp group by gender;    #统计男性、女性数量
  
  select ggender, avg(age) from emp group by gender;
  
  select workaddress, count(*) cnt from emp where age < 45 group by workaddress having cnt >= 3;    #年龄<45，员工数量>=3的工作地址 
  ```

  - where/having
  - where分组之前进行过滤，不参与分组；having分组之后对结果进行过滤
  - where不能对聚合函数进行判断，having可以
  
  ### 排序查询

  - order by后面的字段必须为数值类型/英文字符/日期
  
  ```sql
  select 字段列表 from 表名 order by 字段1 排序方式1，字段2 排序方式2;
  select * from emp order by age asc;
  select * from emp order by age, time desc;    //按照年龄升序排序，年龄相同按照入职时间降序排序
  ```
  
  #### 排序方式
  
  - asc 升序（默认）
  - desc 降序

  ### 分页查询

  - 分页查询在不同数据库有不同的体现，MySQL是limit
  
  - 显示前n条：`select 字段 from 表名 limit n；`
  - 起始索引=（查询页-1）*每页显示条数
  - 如果查询的是第一页数据，起始索引可以省略
  
  ```sql
  select 字段列表 from 表名 limit 起始索引，每页显示记录数；
  select * from emp limit 10;   #查询第一页数据，每页10条
  select * from emp limit 10, 10;    #查询第二页数据，每页10条
  ```
  

### 将查询值插入另一表中

`insert into product2 select  c_id ，count(*) from product1 group by c_id;`

## 编写顺序

- where>分组group by>having>排序order by >分页limit
- `select * from emp where gender ='男' and 20 <= age <=40  order by age, time limit 5;  ` #性别为男，年龄在20-40内的前5个员工，对查询结果升序、年龄相同按照入职时间升序

