#### 一、数据库基本操作

##### 1、数据库操作

```mysql
##查询所有数据库
show databases
##查询指定数据库
show create database db_name;
##创建数据库
create database db_name
##删除数据库
drop database db_name
##使用数据库
use db_name
```

##### 2、数据表操作

```mysql
create table table_name(
	field_name, field_type [列级别约束条件][默认值],
	field_name, field_type [列级别约束条件][默认值],
	field_name, field_type [列级别约束条件][默认值]
	...
	[表级别约束条件]
)
##demo
use spring_test;
## 创建数据库模板
create table t_employee (
	ID int(11) NOT NULL AUTO_INCREMENT COMMENT '员工编号',
	NAME varchar(20) DEFAULT NULL COMMENT '员工姓名',
	DEPART_NAME int(11) DEFAULT NULL COMMENT '部门编号',
	SALARY float DEFAULT NULL COMMENT '员工工资',
	PRIMARY KEY (`ID`)
) ENGINE=InnoDB AUTO_INCREMENT = 9 DEFAULT CHARSET=UTF8;

##查看表结构
DESCRIBE table_name;
  ##查看详细表结构，获取sql语句, 参数\G使结果更加整齐
	SHOW CREATE TABLE tablename\G;
## 修改表
 ## 修改表名
 	ALTER TABLE old_table_name RENAME new_table_name;
 ## 修改表结构
 	ALTER TABLE table_name MODIFY field_name field_type;
 ## 修改字段名
 	ALTER TABLE table_name CHANGE old_field_name new_field_name new_field_type;
 ## 添加字段 FIRST表示添加到表第一个字段，AFTER field_name 表示添加到field_name字段后面
 	ALTER TABLE table_name ADD new_field_name new_field_type [constraint] [FIRST|AFTER]
 ## 删除表字段
 	ALTER TABLE table_name DROP field_name;
 ## 删除表外键约束
 	ALTER TABLE table_name DROP FOREIGN KEY foreign_constraint_name;
## 删除表
  ## 删除未关联的表
	DROP TABLE table_name
  ## 删除关联的表
  	ALTER TABLE child_table_name DROP FOREIGN KEY foreign_constraint_name;
  	DROP TABLE parent_table_name
```



##### 3、表约束

​	（1）主键约束

```
field_name field_type PRIMARY KEY
```

​	（2）外键约束

```
FOREIGN KEY field_name REFERENCES 外键表(field_name)
```

​	（3）非空约束	

```
field_name field_type NOT NULL
```

​	（4）唯一性约束	

```
field_name field_type UNIQUE
```

​	（5）默认约束

```
filed_name field_type DEFAULT 默认值
```

​	（6）主键自增

​		AUTO_INCREMENT, 约束字段必须为主键，字段类型为任何整数类型`(TINYINT、SMALLINT、INT、BIGINT)`

##### 4、数据类型和运算符

​	（1）整数类型

​		![image-20200409113503003](C:\Users\18856\AppData\Roaming\Typora\typora-user-images\image-20200409113503003.png)

![image-20200409113536250](C:\Users\18856\AppData\Roaming\Typora\typora-user-images\image-20200409113536250.png)

​	（2）浮点类型和定点数类型

​			![image-20200409113714990](C:\Users\18856\AppData\Roaming\Typora\typora-user-images\image-20200409113714990.png)

​	

​	（3）日期和时间类型

​	![image-20200409113834835](C:\Users\18856\AppData\Roaming\Typora\typora-user-images\image-20200409113834835.png)

​	（4）字符串类型

![image-20200409133003412](C:\Users\18856\AppData\Roaming\Typora\typora-user-images\image-20200409133003412.png)

​	<img src="C:\Users\18856\AppData\Roaming\Typora\typora-user-images\image-20200409133222205.png" alt="image-20200409133222205" style="zoom:80%;" />



（5）

（6）二进制数据类型

