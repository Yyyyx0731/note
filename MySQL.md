

# 相关概念



<img src="C:\Users\黄\AppData\Roaming\Typora\typora-user-images\image-20230724203542466.png" alt="image-20230724203542466" style="zoom:50%;" />































# SQL





## 通用语法

<img src="C:\Users\黄\AppData\Roaming\Typora\typora-user-images\image-20230724205229660.png" alt="image-20230724205229660" style="zoom:50%;" />















## 分类

<img src="C:\Users\黄\AppData\Roaming\Typora\typora-user-images\image-20230724205434859.png" alt="image-20230724205434859" style="zoom:50%;" />















## DDL



- <font color='cornflowerblue'>方括号中的内容可以省略。</font>

<img src="C:\Users\黄\AppData\Roaming\Typora\typora-user-images\image-20230724210032886.png" alt="image-20230724210032886" style="zoom:50%;" />







### 表操作



#### 创建

<img src="C:\Users\黄\AppData\Roaming\Typora\typora-user-images\image-20230724211207932.png" alt="image-20230724211207932" style="zoom:50%;" />

- 变长字符串：<font color='orange'>**varchar ( n )** </font>，n是能够存储的<font color='orange'>最大长度</font>，超出会报错。
- 定长字符串：<font color='cornflowerblue'>**char ( n )**</font> ，n是<font color='cornflowerblue'>定长</font>，如果实际储存长度小于n，也占用 n 个字符的空间，其他空间用空格占位。

补：<img src="C:\Users\黄\AppData\Roaming\Typora\typora-user-images\image-20230724213121534.png" alt="image-20230724213121534" style="zoom:50%;" />





#### 查询

##### 查询当前数据库所以表

##### 查询表=结构

##### 查询指定的建表语句

![image-20230724210721791](C:\Users\黄\AppData\Roaming\Typora\typora-user-images\image-20230724210721791.png)





#### 修改

##### 添加字段

<img src="C:\Users\黄\AppData\Roaming\Typora\typora-user-images\image-20230724213405637.png" alt="image-20230724213405637" style="zoom:50%;" />



##### 修改字段

###### 修改数据类型

<img src="C:\Users\黄\AppData\Roaming\Typora\typora-user-images\image-20230724213710257.png" alt="image-20230724213710257" style="zoom:50%;" />

###### 修改字段名和字段类型

<img src="C:\Users\黄\AppData\Roaming\Typora\typora-user-images\image-20230724213731652.png" alt="image-20230724213731652" style="zoom:50%;" />



##### 修改表名

![image-20230724214100757](C:\Users\黄\AppData\Roaming\Typora\typora-user-images\image-20230724214100757.png)



##### 删除字段

<img src="C:\Users\黄\AppData\Roaming\Typora\typora-user-images\image-20230724214020632.png" alt="image-20230724214020632" style="zoom:50%;" />



##### 删除表

###### 删除表

![image-20230724214216025](C:\Users\黄\AppData\Roaming\Typora\typora-user-images\image-20230724214216025.png)

###### 删除并重新创建指定表

![image-20230724214317477](C:\Users\黄\AppData\Roaming\Typora\typora-user-images\image-20230724214317477.png)

<img src="C:\Users\黄\AppData\Roaming\Typora\typora-user-images\image-20230724214355685.png" alt="image-20230724214355685" style="zoom:50%;" />











## DML

<img src="C:\Users\黄\AppData\Roaming\Typora\typora-user-images\image-20230724215146110.png" alt="image-20230724215146110" style="zoom:50%;" />



### 添加数据

<img src="C:\Users\黄\AppData\Roaming\Typora\typora-user-images\image-20230724214938909.png" alt="image-20230724214938909" style="zoom:50%;" />





### 修改数据

<img src="C:\Users\黄\AppData\Roaming\Typora\typora-user-images\image-20230724215009999.png" alt="image-20230724215009999" style="zoom:50%;" />





### 删除数据

<img src="C:\Users\黄\AppData\Roaming\Typora\typora-user-images\image-20230724215035677.png" alt="image-20230724215035677" style="zoom:50%;" />











## DQL









## DCL

































































