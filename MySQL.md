

# 相关概念



<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307250005133.png" alt="image-20230724203542466" style="zoom:50%;" />































# SQL





## 通用语法

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307250005040.png" alt="image-20230724205229660" style="zoom:50%;" />















## 分类

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307250008287.png" alt="image-20230724205434859" style="zoom:50%;" />















## DDL



- <font color='cornflowerblue'>方括号中的内容可以省略。</font>

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307250008969.png" alt="image-20230724210032886" style="zoom:50%;" />







### 表操作



#### 创建

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307250008676.png" alt="image-20230724211207932" style="zoom:50%;" />

- 变长字符串：<font color='orange'>**varchar ( n )** </font>，n是能够存储的<font color='orange'>最大长度</font>，超出会报错。
- 定长字符串：<font color='cornflowerblue'>**char ( n )**</font> ，n是<font color='cornflowerblue'>定长</font>，如果实际储存长度小于n，也占用 n 个字符的空间，其他空间用空格占位。

补：<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307250009240.png" alt="image-20230724213121534" style="zoom:50%;" />





#### 查询

##### 查询当前数据库所以表

##### 查询表=结构

##### 查询指定的建表语句

![image-20230724210721791](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307250010620.png)





#### 修改

##### 添加字段

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307250010005.png" alt="image-20230724213405637" style="zoom:50%;" />



##### 修改字段

###### 修改数据类型

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307250010958.png" alt="image-20230724213710257" style="zoom:50%;" />

###### 修改字段名和字段类型

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307250010914.png" alt="image-20230724213731652" style="zoom:50%;" />



##### 修改表名

![image-20230724214100757](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307250011978.png)



##### 删除字段

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307250010788.png" alt="image-20230724214020632" style="zoom:50%;" />



##### 删除表

###### 删除表

![image-20230724214216025](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307250011691.png)

###### 删除并重新创建指定表

![image-20230724214317477](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307250010923.png)

<img src="C:\Users\黄\AppData\Roaming\Typora\typora-user-images\image-20230724214355685.png" alt="image-20230724214355685" style="zoom:50%;" />











## DML

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307250013311.png" alt="image-20230724215146110" style="zoom:50%;" />



### 添加数据

![image-20230725110254022](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307251105682.png)



### 修改数据

![image-20230725111758138](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307251118550.png)

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307251118380.png" alt="image-20230725111845323" style="zoom: 45%;" />



### 删除数据

![image-20230725112109202](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307251121239.png)

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307251124027.png" alt="image-20230725112335477" style="zoom:45%;" />

​		 用 alter  table 是删除整个字段，而不是值。











## DQL

数据查询语言，用来查询数据库中表的记录。



### 语法

![image-20230725115511490](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307251155613.png)





### 基本查询

![](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307251208683.png)





### 条件查询

![image-20230725172641921](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307251727390.png)

例：<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307251746854.png" alt="image-20230725174511628" style="zoom: 60%;" />





### 分组查询

#### 聚合函数

![image-20230725175804399](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307251758498.png)

注：null 不参与聚合函数的运算。

例：<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307251800634.png" alt="image-20230725180046590" style="zoom:60%;" />



#### 分组查询

![](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307251831420.png)

例：![image-20230725183941425](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307251839511.png)

![image-20230725184544421](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307251845492.png)





### 排序查询

![image-20230725193635867](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307251936941.png)



- **<font color='orange'>第一个字段值相同时，再根据第二个字段排序。</font>**





### 分页查询

![image-20230725195048911](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307251951769.png)

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307251953373.png" alt="image-20230725195309287" style="zoom:50%;" />





### 案例

![image-20230725204112877](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252041964.png)





### 执行顺序

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252043271.png" alt="image-20230725204315189" style="zoom: 40%;" /><img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252043910.png" alt="image-20230725204346826" style="zoom:40%;" />















## DCL

管理数据库用户，控制数据库的访问权限。



![](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252052109.png)

例：<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252104696.png" alt="image-20230725210447636" style="zoom:60%;" />

​		% 表示可在任意主机访问；

​		localhost 只能在当前主机访问。









### 权限控制

![image-20230725210652737](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252106822.png)

​		

![image-20230725210753524](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252107612.png)





























## 函数



是指一段可以直接被另一段程序调用的程序或代码。



### 字符串函数

![](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252119120.png)

例：![image-20230725212129382](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252121424.png)





### 数值函数

![image-20230725212400597](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252124729.png)

例：<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252125954.png" alt="image-20230725212558903" style="zoom:50%;" />





### 日期函数

![image-20230725212938159](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252129679.png)

- dateAdd 中加的时间间隔可以是年、月、日 ... ...，取决于后面的类型 type。

  例：<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252132789.png" alt="image-20230725213202739" style="zoom:50%;" />





### 流程函数

![image-20230725213517226](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252135334.png)

例：<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252137793.png" alt="image-20230725213733707" style="zoom:50%;" />

​		注意：<font color='orange'>**空字符串不是 null** </font>！！

例：![image-20230725213955930](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252140373.png)





























## 约束

![image-20230725214309551](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252143681.png)

可以在创建/修改表时添加约束。







### 外键约束

外键用来让两张表之间的数据建立连接，从而保证数据的一致性和完整性。

![image-20230725214544145](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252145285.png)



#### 添加外键

![image-20230725214631357](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252146441.png)



#### 删除外键

![image-20230725214718799](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252147840.png)



#### 删除/更新行为

![image-20230725214819410](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252148503.png)































## 多表查询



#### 多表关系

![image-20230725215045838](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252150920.png)

##### 一对多（多对一）

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252152892.png" alt="image-20230725215208828" style="zoom:50%;" />



##### 多对多

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252152374.png" alt="image-20230725215227306" style="zoom:50%;" />



##### 一对一

![image-20230725215525148](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252155225.png)





#### 内连接









#### 外连接









#### 自连接











#### 子查询

























