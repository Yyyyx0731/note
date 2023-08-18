

# 相关概念



<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307250005133.png" alt="image-20230724203542466" style="zoom:50%;" />

















# go下载驱动



**<font color='red'>go get -u github.com/go-sql-driver/mysql</font>**

























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
- double：

  - double类型，长度需大于等于小数点位数，若相等则整数部分必须为0

  - 假设长度为3，小数点位数为2，则整数位数为3-2=1。

  - **整数位数**超出限制会导致插入失败

  - **小数位数**超出限制将对超出位从后往前依次进行**五舍六入**

  - ```mysql
    //两位小数，一位整数
    CREATE TABLE test (
      column_double double(3,2)
    )
    ```

    


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

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252237835.png" alt="image-20230724214355685" style="zoom:50%;" />











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

   distinct 跟在select 后。



注：给表起了别名后，无法再用原表名限定字段。

​		<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307261629235.png" alt="image-20230726162949185" style="zoom:55%;" />





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







### 模糊查询

1. ​	"%" 百分号通配符: 表示任何字符出现任意次数 (可以是0次)。、
2. ​    "_" 下划线通配符:表示只能匹配单个字符,不能多也不能少,就是一个字符。当然，也可以like "陈"，数量不限。
3. ​    like操作符:LIKE作用是指示mysql后面的搜索模式是利用通配符而不是直接相等匹配进行比较；但如果like后面没出现通配符，则在SQL执行优化时将 like 默认为 “=”执行
   

-- 模糊匹配含有“网”字的数据

```sql
SELECT * from app_info where appName like '%网%';
```

-- 模糊匹配以“网”字结尾的数据

```sql
SELECT * from app_info where appName like '%网';
```

-- 模糊匹配以“网”字开头的数据

```sql
SELECT * from app_info where appName like '网%';
```

-- 模糊匹配含有“xxx网xxx车xxx”的数据,如："途途网约车司机端、网络约车平台"

```sql
SELECT * from app_info where appName like '%网%车%';
```







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





























# 函数



是指一段可以直接被另一段程序调用的程序或代码。



## 字符串函数

![](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252119120.png)

例：![image-20230725212129382](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252121424.png)





## 数值函数

![image-20230725212400597](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252124729.png)

例：<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252125954.png" alt="image-20230725212558903" style="zoom:50%;" />





## 日期函数

![image-20230725212938159](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252129679.png)

- dateAdd 中加的时间间隔可以是年、月、日 ... ...，取决于后面的类型 type。

  例：<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252132789.png" alt="image-20230725213202739" style="zoom:50%;" />





## 流程函数

![image-20230725213517226](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252135334.png)

例：<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252137793.png" alt="image-20230725213733707" style="zoom:50%;" />

​		注意：<font color='orange'>**空字符串不是 null** </font>！！

例：![image-20230725213955930](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252140373.png)

例：<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252235943.png" alt="image-20230725223344179" style="zoom:50%;" />

![image-20230725223258117](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252232178.png)



























# 约束

![image-20230725214309551](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252143681.png)

- 可以在创建/修改表时添加约束。

补：auto_increment ：键值自动增长

例：<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252309142.png" alt="image-20230725230945031" style="zoom:50%;" />





## 外键约束

外键用来让两张表之间的数据建立连接（建立外键关联），从而保证数据的一致性和完整性。

​	子表：有外键的表

​	父表：外键所关联的表

![image-20230725214544145](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252145285.png)



### 添加外键

![image-20230725214631357](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252146441.png)



### 删除外键

![image-20230725214718799](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252147840.png)



### 删除/更新行为

![image-20230725214819410](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252148503.png)





































# 多表查询





## 多表关系

![image-20230725215045838](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252150920.png)

### 一对多（多对一）

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252152892.png" alt="image-20230725215208828" style="zoom:45%;" />



### 多对多

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252152374.png" alt="image-20230725215227306" style="zoom:45%;" />

![image-20230726153149912](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307261533998.png)



### 一对一

经常用来做单表的拆分。

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307252155225.png" alt="image-20230725215525148" style="zoom:45%;" />

![](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307261550555.png)













## 多表查询概述

![image-20230726155624142](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307261556214.png)

例：<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307261603746.png" alt="image-20230726155920547" style="zoom:58%;" />











## 分类

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307261617557.png" alt="image-20230726161712502" style="zoom: 35%;" />



### 连接查询

#### 内连接

内连接查询的是两张表<font color='red'>交集的部分</font>。

on + 连接条件

where + 筛选条件

##### 隐式内连接

![image-20230726162047914](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307261625014.png)

##### 显示内连接

![image-20230726162125536](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307261625414.png)

例：<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307261913238.png" alt="image-20230726191338171" style="zoom:60%;" />





#### 外连接

注意：都包含交集部分。

##### 左外连接

![image-20230726163237616](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307261632672.png)

##### 右外连接

![image-20230726163253753](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307261632828.png)





#### 自连接

![image-20230726163721025](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307261637134.png)









### 联合查询

union ， union  all

对于 union 查询，就是把多次查询的结果合并起来，形成一个新的查询结果集。、

![image-20230726164902427](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307261650855.png)

- <font color='cornflowerblue'>**union all ：对查询结果之间合并**</font>
- **<font color='orange'>union ： 对查询结果合并后去重</font>**

- 使用条件：<font color='pink'>**所有查询语句返回的字段相同**</font>

  ​                   <img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307261701044.png" alt="image-20230726170143998" style="zoom:60%;" />









### 子查询

![image-20230726170521989](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307261705102.png)



#### 分类

##### 根据<font color='red'>子查询</font>返回的结果

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307261710467.png" alt="image-20230726170931967" style="zoom:50%;" />



##### 根据子查询位置

where后，from后，select后。









#### 标量子查询

子查询结果为单个值（返回的结果只有一行一列）。

例：查询销售部的所有员工信息（括号中自查询的结果为一行一列，是4）

​		<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307261723410.png" alt="image-20230726172325350" style="zoom:50%;" />





#### 列子查询

子查询结果为一列。

![image-20230726172621297](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307261727142.png)

例：![image-20230726175035149](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307261755059.png)





#### 行子查询

子查询结果为一行。

例：![image-20230726175918109](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307261759152.png)





#### 表子查询

子查询结果为多行多列。

![image-20230726181301396](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307261813454.png)

![image-20230726182407497](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307261827505.png)

![image-20230726181454630](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307261816787.png)







## 案例

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307262041998.png" alt="image-20230726203820072" style="zoom:50%;" />



































# 事务



<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307262119482.png" alt="image-20230726211615724" style="zoom:40%;" />

- MySQL中的事务是默认自动提交的。



## 操作

### 法一：关闭事务自动提交

![](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307262130873.png)

### 法二：显式地开启事务

![image-20230726213341087](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307262133189.png)









## 四大特性

![image-20230726213859829](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307262138922.png)

​															因为数据最终是储存在磁盘中的。



​	





## 并发事务问题

![image-20230726214619419](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307262146554.png)









## 事务的隔离级别

解决并发事务所带来的问题。



- **<font color='deyellow'>数据的隔离级别越高，数据越安全，但是性能越低</font>**。



- 会出现的问题：

![](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307262254427.png)



![image-20230726222340766](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307262223889.png)



















