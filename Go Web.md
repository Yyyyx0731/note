





## Web 应用的工作原理

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307271618954.png" alt="image-20230727161844809" style="zoom: 45%;" />

























# 搭建服务器







## 使用默认多路复用器

### 使用处理器函数处理请求

```go
package main

import (
	"fmt"
	"net/http"
)

//创建处理器函数
func handler(w http.ResponseWriter,r *http.Request){
	fmt.Fprintln(w,"hello world!!",r.URL.Path)
}

func main() {
	//设置访问的路由
	http.HandleFunc("/",handler) // 当url中的路径为/(根目录)时，服务器调用 handler 函数

	//设置监听的端口
	http.ListenAndServe(":8080",nil)//处理器参数为 nil，那么服务器将使用默认的多路复用器 DefaultServeMux
	//也可以通过调用 NewServeMux 函数创建一个多路复用器
}
```

打开浏览器：输入以下网址：http://localhost:8080/hi  （8080端口号后可不输入其他内容，页面则只显示hello world!!）

效果：<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307271719141.png" alt="image-20230727171900092" style="zoom:50%;" />

- 往 http.ResponseWriter 写入什么内容，浏览器的网页源码就是什么内容；

   http.Request 里面封装了浏览器发过来的请求（包含路径、浏览器类型等等）。

- *http.Request.URL.Path 可以把访问的地址打印出来。

- 设置监听端口时，如果网络地址参数（第一个参数）为空字符串，那么服务器使用默认端口进行网络连接

  -  http：80
  - https：443

  处理器参数为 nil（第二个参数），那么服务器将使用默认的多路复用器 DefaultServeMux。也可以通过调用 NewServeMux 函数创建一个多路复用器





### 使用处理器处理请求

http.Hanlder( "" , 处理器 )  		 要实现server

```go
package main

import (
	"fmt"
	"net/http"
)

type MyHandler struct{}

func (m *MyHandler) ServeHTTP(w http.ResponseWriter,r *http.Request){
	fmt.Fprintln(w,"自己创建的处理器处理请求...")
}

func main() {
	myHandler := MyHandler{}
	http.Handle("/myHandler",&myHandler)

	http.ListenAndServe(":8080",nil)

}
```

- 结构体需要实现了 handler 接口( 有ServeHTTP方法 )，方法的参数类型必须是 http.ResponseWriter 和 *http.Request，就是一个处理器。



#### 通过 server 结构对服务器进行更详细的配置

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307272044008.png" alt="image-20230727204248451" style="zoom: 62%;" />

```go
package main

import (
	"fmt"
	"net/http"
	"time"
)

type MyHandler struct{}

func (m *MyHandler) ServeHTTP(w http.ResponseWriter,r *http.Request){
	fmt.Fprintln(w,"通过详细配置处理器处理请求...")
}

func main() {
	myHandler := MyHandler{}

	//创建 server 结构，并配置字段
	server := http.Server{
		Addr:":8080",
		ReadTimeout: 2*time.Second,
		Handler: &myHandler,
	}
	server.ListenAndServe()

}
```







### 使用处理器处理请求

http . HandlerFunc( "" , 处理器函数 )

```go
	//映射地址 处理器函数
	//去首页
	http.HandleFunc("/main", controller.GetPageBooksByPrice)
	//去登录
	http.HandleFunc("/login",controller.Login)
```









## 自己创建多路复用器

```go
package main

import (
	"fmt"
	"net/http"
)

func handler(w http.ResponseWriter,r *http.Request){
	fmt.Fprintln(w,"自己创建的多路复用器...")
}

func main() {
	mux:=http.NewServeMux()
	mux.HandleFunc("/myMux",handler)
	http.ListenAndServe(":8080",mux)
}
```



























# HTTP 协议

- **超文本传输协议。**

  **详细规定了浏览器和万维网服务器之间相互通信的规则。**

- 客户端与服务端相互通信时传输的内容 称为 **报文**。

  - 客户端发给服务器端的叫 *请求报文*。
  - 服务器发给客户端的叫 *响应报文*。





## 会话方式

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307272125042.png" alt="image-20230727212514580" style="zoom:50%;" />







## 报文

### 格式

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307272127747.png" alt="image-20230727212756660" style="zoom:50%;" />



### 请求报文

#### 格式

请求行和请求头组成首部。

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307272129529.png" alt="image-20230727212916477" style="zoom:50%;" />

- ***Get请求没有请求体。***POST才有。



### 响应报文

#### 格式

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307272137448.png" alt="image-20230727213553990" style="zoom:50%;" />









## 响应状态码

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307272138839.png" alt="image-20230727213816749" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307272139193.png" alt="image-20230727213903129" style="zoom:50%;" />



### 常见的状态码

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307272141622.png" alt="image-20230727214023835" style="zoom:50%;" />

































# 操作数据库

database/sql包



1 . <img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307272145290.png" alt="image-20230727214528225" style="zoom:50%;" />

2 . 定义两个全局变量

```go
var (
	DB *sql.DB
	err error
)
```

3 . 创建 init 函数

​	 <img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307272148163.png" alt="image-20230727214816075" style="zoom:50%;" />

​       <img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307272151837.png" alt="image-20230727215136603" style="zoom:50%;" />

- ​			sql.open( ) 不会校验账号密码是否正确

  ​			db.Ping( ) 尝试与数据库建立连接（校验dsn是否正确）





## 增

```go

func addClient(n string,p string) {
	sqlStr:="insert into client(name,password) values(?,?)"
    
	_,err:=db.Exec(sqlStr,n,pp)
	if err!=nil {
		fmt.Println(err)
	}
    
}
```





## 删

```go

func deleteClient(n string)  {
	sqlStr := `delete from client  where name = ?`
    
	_, err := db.Exec(sqlStr, n)
	if err != nil {
		fmt.Println("delete:", err)
		return
	}
    
}
```





## 改

```go

func modifyName(n string)  {
	selStr := "update client set name = ? where name = ? "
    
	_, err := db.Exec(selStr, n,name)
	if err != nil {
		fmt.Println("exec err:",err)
		return
	}

}
```





## 查

### 单行查询

```go

func Query(name string,password string,db *sql.DB){
	sqlStr:="select password from client where name =?;"
    
	var c string=""
	err:=db.QueryRow(sqlStr,name).Scan(&c)
	if err != nil {
		fmt.Println("query:",err)
	}
	
}
```



### 多行查询

```go
//GetOrderItemsByOrderID 根据订单号获取该订单的所有订单项
func GetOrderItemsByOrderID(orderID string) ([]*model.OrderItem, error) {
	//写sql语句
	sql := "select id,count,amount,title,author,price,img_path,order_id from order_items where order_id = ?"
	//执行
	rows, err := utils.Db.Query(sql, orderID)
	if err != nil {
		return nil, err
	}
	var orderItems []*model.OrderItem
	for rows.Next() {
		orderItem := &model.OrderItem{}
		rows.Scan(&orderItem.OrderItemID, &orderItem.Count, &orderItem.Amount, &orderItem.Title, &orderItem.Author, &orderItem.Price, &orderItem.ImgPath, &orderItem.OrderID)
		//添加到切片中
		orderItems = append(orderItems, orderItem)
	}
	return orderItems, nil
}
```























# 单元测试

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307280005515.png" alt="image-20230728000437968" style="zoom: 40%;" />

​					     <img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307280007507.png" alt="image-20230728000719475" style="zoom:50%;" />

































# 处理请求





## 获取请求URL(请求行中的信息)

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307281532491.png" alt="image-20230728153208387" style="zoom:50%;" />

​	<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307281531271.png" alt="image-20230728153131022" style="zoom:40%;" />

例：

```go
package main

import (
	"fmt"
	"net/http"
)

//创建处理器函数
func handler1(w http.ResponseWriter,r *http.Request){
	fmt.Fprintln(w,"地址：",r.URL.Path)
	fmt.Fprintln(w,"请求地址后的查询字符串：：",r.URL.RawQuery)
}

func main() {
	http.HandleFunc("/ttttttttest",handler1)
	http.ListenAndServe(":8080",nil)
}

```

效果：<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307281550176.png" alt="image-20230728155009139" style="zoom:50%;" />









## 获取请求头

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307281608624.png" alt="image-20230728160810542" style="zoom:50%;" />

```go
package main

import (
	"fmt"
	"net/http"
)

//创建处理器函数
func handler1(w http.ResponseWriter,r *http.Request){
	fmt.Fprintln(w,"请求头中的所有信息：",r.Header)
	fmt.Fprintln(w,"请求头中Accept-Encoding的信息：",r.Header["Accept-Encoding"])
	fmt.Fprintln(w,"请求头中Accept-Encoding的属性值：",r.Header.Get("Accept-Encoding"))
}

func main() {
	http.HandleFunc("/test",handler1)
	http.ListenAndServe(":8080",nil)
}

```

结果：<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307281619759.png" alt="image-20230728161952704" style="zoom:50%;" />









## 获取请求体

***Get请求没有请求体。***

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307281645205.png" alt="image-20230728164403105" style="zoom:40%;" />

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307281646807.png" alt="image-20230728164603705" style="zoom:40%;" />

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307281646551.png" alt="image-20230728164651486" style="zoom:40%;" />



例：

```go
package main

import (
	"fmt"
	"net/http"
)

func handler2(w http.ResponseWriter,r *http.Request){
	//获取请求体中内容的长度
	length:=r.ContentLength

	body := make([]byte,length)
	r.Body.Read(body)
	fmt.Fprintln(w,"请求体中的内容：",string(body))
}

func main() {
	http.HandleFunc("/",handler2)
	http.ListenAndServe(":8080",nil)
}

```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
</head>
<body>
    <form action="http://localhost:8080" method="post">  // 两文件通过此标签连接
        用户名：<input type="text" name="name"><br>
        <input type="submit" value="提交">
    </form>
</body>
</html>
```

效果：<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307281658016.png" alt="image-20230728165846972" style="zoom:50%;" />

​			<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307281700663.png" alt="image-20230728170047622" style="zoom:50%;" />









## 获取请求参数



### Form 字段

1. 类型是 url.Values ，Form 是解析好的表单数据，包括 URL 字段的 query 参数和 POST 或 PUT 的表单数据。

   <img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307281849233.png" alt="image-20230728184939143" style="zoom:50%;" />

2. Form 字段只有在调用 Requst 的 ParseForm 方法后才有效。

   <img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307281850987.png" alt="image-20230728185000923" style="zoom:50%;" />



例：

```go
package main

import (
	"fmt"
	"net/http"
)

func handler2(w http.ResponseWriter,r *http.Request){
	//解析表单，在调用 r.Form 前必须执行改操作
	r.ParseForm()

	//获取请求参数
	fmt.Fprintln(w,"请求参数有：",r.Form)

}

func main() {
	http.HandleFunc("/",handler2)
	http.ListenAndServe(":8080",nil)
}

```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
</head>
<body>
    <form action="http://localhost:8080" method="post">  // 两文件通过此标签连接
        用户名：<input type="text" name="name"><br>
        <input type="submit" value="提交">
    </form>
</body>
</html>
```

效果：<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307281923874.png" alt="image-20230728192341810" style="zoom:50%;" />

​			<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307281923931.png" alt="image-20230728192328883" style="zoom:50%;" />



### FormValue 和 PostFormValue

可以快速获取某一请求参数。

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307282049973.png" alt="image-20230728204959896" style="zoom:75%;" />

- FormValue：URL中的请求参数（get和post请求都可以）
- PostFormValue：Form表单中的请求参数（只能获取post请求的值）













## 给客户端响应

使用 http.ResponseWriter 给用户响应。

### 响应一个字符串

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307282129552.png" alt="image-20230728211603277" style="zoom:40%;" />

### 响应一个页面

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307282129029.png" alt="image-20230728212505655" style="zoom:40%;" />

### 响应 json 形式的数据

#### json

- JSON，全称是 JavaScript Object Notation，即 JavaScript对象标记法。
- JSON是一种轻量级（Light-Meight)、基于文本的(Text-Based)、可读的(Human-Readable)格式。
- JSON 的名称中虽然带有JavaScript，但这是指其语法规则是参考JavaScript对象的，而不是指只能用于JavaScript 语言。

##### 语法规则

- 数组（Array）用方括号(“`[]`”)表示。
- 对象（0bject）用大括号(“`{}`”)表示。
- 名称/值对(`name/value`）组合成数组和对象。
- 名称(`name`）置于**双引号**中，值（`value`）有**字符串、数值、布尔值、null、对象和数组**。
- 并列的数据之间用逗号(“`,`”）分隔

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307282154611.png" alt="image-20230728214923098" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307282128832.png" alt="image-20230728212838630" style="zoom:40%;" />

- 通过 content-type 设置响应头中内容的类型为 json。

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307282135530.png" alt="image-20230728213343324" style="zoom:40%;" />





### 让客户端重定向

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307282335874.png" alt="image-20230728233433376" style="zoom:40%;" />

































# 模板引擎-处理响应数据



<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307291832236.png" alt="image-20230729183217083" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307291834915.png" alt="image-20230729183452820" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307291839019.png" alt="image-20230729183926931" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307291847910.png" alt="image-20230729184718819" style="zoom:50%;" />



示例：

```go
package main

import (
	"html/template"
	"net/http"
)

//创建处理器函数
func testTemplate(w http.ResponseWriter,r *http.Request){
	//解析模板
	t,_ := template.ParseFiles("WebApp/hello.html")//注意此处的路径   未处理错误
	//执行
	t.Execute(w,"66666")
}

func main() {
	http.HandleFunc("/",testTemplate)
	http.ListenAndServe(":8080",nil)
}

```

```html
//hello.html文件内容

<!DOCTYPE html>
<html lang="ch">
<head>
    <meta charset="UTF-8">
    <title>模板</title>
</head>
<body>
  你好<br>
  后台传过来的数据：{{.}}
</body>
</html>
```

运行结果：<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307292356390.png" alt="image-20230729235654335" style="zoom:50%;" />

注意：**在goland里引入模板文件要写绝对路径**。



## 解析模板

- 后台传的数据可以有多个，但只显示第一个，其余传入的数据会被存在一个 map 中。
- 传的模板文件可以有多个，生成一个新模板 名字就是传入的文件名 ( 不含扩展名 )， 只返回第一个模板，其余传入的文件名会被存在一个 map 中。

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307300011129.png" alt="image-20230730001138011" style="zoom: 60%;" />

- 上述代码在解析模板时未处理错误，用下划线忽略了。可以使用 Must 来处理。


​		<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307300020300.png" alt="image-20230730002027179" style="zoom:65%;" />



## 执行模板

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307300025584.png" alt="image-20230730002509420" style="zoom:50%;" />



- 用过指定 不调用第一个模板：

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307300027871.png" alt="image-20230730002704782" style="zoom:50%;" />

​		 <img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307300028376.png" alt="image-20230730002825246" style="zoom:50%;" />





## 模板引擎的使用

一般三步走，定义、解析、渲染



- 定义模板文件

这个定义一个html文件即可，后缀名成可以设定为 tmpl 或者 tpl ，不过我们一般使用 tmpl 作为模板文件后缀。
模板文件解析



- 定义好了模板文件之后，可以使用下面的常用方法去解析模板文件，得到模板对象：


```go
func (t *Template) Parse(src string) (*Template, error)
func ParseFiles(filenames ...string) (*Template, error)
func ParseGlob(pattern string) (*Template, error)
```



- 模板渲染

```go
func (t *Template) Execute(wr io.Writer, data interface{}) error
func (t *Template) ExecuteTemplate(wr io.Writer, name string, data interface{}) error
```

​	<font color='cornflowerblue'>通过execute函数把数据放入到模板文件里面去</font>。



例：

```go
package main

import (
	"html/template"
	"net/http"
)

//创建处理器函数
func testTemplate(w http.ResponseWriter,r *http.Request){
	//解析模板
	t,_ := template.ParseFiles("WebApp/hello.html")//注意此处的路径
	//执行
	t.Execute(w,"66666")
}

func main() {
	http.HandleFunc("/",testTemplate)
	http.ListenAndServe(":8080",nil)
}

```







## 双层花括号

是<font color='red'>模板</font>语法。具体什么模板仅凭这点信息看不出来，因为现在很多模板引擎都是用的双大括号。

模板实际上就是在 HTML 结构的基础上，把上面要显示的内容的关键部分用这种特定的语法替换掉，在进行模板编译的时候，再<font color='red'>动态</font>根据实际内容来替换这些模板部分，以实现动态网站。

比如：我有一个 HTML 文件中有这么一段：

```text
<div id="username">用户名</div>
```

但是这样的话，每次打开这个 HTML，这里都显示的是“用户名”三个字。我希望通过其他编程语言来处理当前登录的用户，然后在这里显示当前登录的用户名。

那么，我通过其他编程语言，将用户名存在一个变量里面，比如就是 result，那么我就将 HTML 改写成这样：

```text
<div id="username">{{ result }}</div>
```




## 模板语法

模板语法都包含在 {{和}} 中间，其中 {{.}} 中的点表示当前对象。



1 . **<font color='orange'>{{.}}</font>** ，里面的这个点，就是传入的对象。例如：

```go
	name := "张三"
	err = t.Execute(w,name)
```

​			这样子， 括号里面的点就表示张三。可以直接放入到模板文件里面去动态的显示。

- 除了基本类型，还可以设置结构体，或者map。

结构体：

```go
u1 := User{
	Name:"小公主",
	Gender:"女",
	Age:16,
}
err = t.Execute(w,u1)
```
取数据的时候通过 .Name .Age .Gender 的形式进行读取数据即可。
<font color='cornflowerblue'>这个主意要首字母大写，因为结构体要对外开放权限。</font>

map：

```go
package main
import (
	"fmt"
	"html/template"
	"net/http"
)
type User struct {
	Name string
	Gender string
	Age int
}
func index(w http.ResponseWriter, r *http.Request)  {
	// 解析模板
	t, err := template.ParseFiles("Template_test/index.tmpl")
	if err != nil {
		fmt.Println("Parse template failed! err:",err)
		return
	}
	// 渲染模板
	u1 := User{
		Name:"小公主",
		Gender:"女",
		Age:16,
	}
	m1 := map[string]interface{}{
		"name":"小皇子",
		"gender":"男",
		"age" : 18,
	}
	err = t.Execute(w,map[string]interface{}{
		"u1":u1,
		"m1":m1,
	})
	if err != nil {
		fmt.Println("render template failed,err : ",err)
		return
	}
}
func main() {
	http.HandleFunc("/index",index)
	err := http.ListenAndServe(":9090",nil)
	if err != nil {
		fmt.Println("HTTP server start failed! err : ", err)
		return
	}
}
```

- 将一个map数据和一个结构体数据统一的放入到一个map里面，然后将这个全部的数据统一的返回给模板。

![在这里插入图片描述](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307312127960.png)

- 模板的引用要注意大小写。map里面的因为直接就是key/value的形式，所以不用首字母大写。

![image-20230731213006515](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307312130595.png)

### 条件判断语句

```go
{{if pipeline}} T1 {{end}}

{{if pipeline}} T1 {{else}} T0 {{end}}

{{if pipeline}} T1 {{else if pipeline}} T0 {{end}}
```



### range 循环遍历

- 这个就是将数据进行一个循环遍历输出的了，相当于for循环的样子
- Go的模板语法中使用range关键字进行遍历，有以下两种写法，其中pipeline的值必须是`数组`、`切片`、`字典`或者`通道`。

```go
	hobbyList := []string{
		"篮球",
		"足球",
		"双色球",
	}
```

- 我们将这个切片通过Execute函数传到模板上面去。
- 然后对这个切片进行遍历输出

![在这里插入图片描述](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307312148383.png)

- 这里我们声明两个变量，分别来接受这个切片的索引和内容

输出：<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307312148259.png" alt="image-20230731214741614" style="zoom:50%;" />



### $ 定义变量

路由的处理函数可以向模版传递数据（该数据我们称为参数），传递的数据在模版中以一个点（.）表示。除此之外，模版里还可以定义变量，<font color='red'>变量以美元符号（$）开头</font>。

```go
{{ range $key, $value := . }}
　<p>The key is {{ $key }} and the value is {{ $value }}</p>
{{ end }}
```











## 动作

{{ . }} 

点代表了传给M模板的数据。



### 条件动作

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308020922176.png" alt="image-20230802091857427" style="zoom:50%;" />

例：<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308020931228.png" alt="image-20230802092513195" style="zoom:50%;" />





### 迭代动作

相当于循环。

对象可以是数组、切片、映射、通道。

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308020933450.png" alt="image-20230802093324322" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308020934497.png" alt="image-20230802093413370" style="zoom:50%;" />



<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308020945111.png" alt="image-20230802094507028" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308021035193.png" alt="image-20230802094658148" style="zoom:50%;" />





### 设置动作

arg是要设置的新值。{{.}}读取新值。

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308021035792.png" alt="image-20230802103212496" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308021037300.png" alt="image-20230802103708232" style="zoom:50%;" />

- 如果 arg 是空字符串，相当于没有改。那么大括号{{.}}里还是传过来的值。


<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308021046099.png" alt="image-20230802103937904" style="zoom:50%;" />





### 包含动作

嵌套的模板，一个模板里包含另一个模板。

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308021047120.png" alt="image-20230802104757047" style="zoom:45%;" />

​							  格式二例：传入后台数据 <img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308021052169.png" alt="image-20230802105043980" style="zoom:45%;" />

​																			（传入的数据用 . 表示）

- <font color='cornflowerblue'>使用parseFiles解析模板文件时，需要将几个模板都传进去。</font>





### 定义动作

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308021056096.png" alt="image-20230802105617964" style="zoom:50%;" />

（点了其他超链接后，有不变的部分）

例：<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308021059800.png" alt="image-20230802105912618" style="zoom: 40%;" />

​	  <img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308021059663.png" alt="image-20230802105959600" style="zoom:40%;" />

​	<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308021101347.png" alt="image-20230802110109251" style="zoom:40%;" />

​	 <img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308021100265.png" alt="image-20230802110048164" style="zoom:40%;" />

​				<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308021103927.png" alt="image-20230802110308825" style="zoom:40%;" />

​					<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308021105647.png" alt="image-20230802110504566" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308021109184.png" alt="image-20230802110959067" style="zoom:40%;" />

​			  <img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308021111395.png" alt="image-20230802111124283" style="zoom:40%;" />

​			   <img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308021113833.png" alt="image-20230802111220700" style="zoom:40%;" />

​		 	 <img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308021113956.png" alt="image-20230802111313856" style="zoom:40%;" />

​			  <img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308021114938.png" alt="image-20230802111424350" style="zoom:40%;" />

​				<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308021115222.png" alt="image-20230802111539082" style="zoom:40%;" />

​			   <img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308021116689.png" alt="image-20230802111618605" style="zoom:40%;" />





### 块动作

如果定义动作里的3，在不同模板定义同名模板 if 的两种情况都不满足，即可通过块动作定义一个默认的模板。

这个动作允许用户定义一个模板并立即使用，相当于设置了一个默认的模板。

![image-20230802114313883](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308021143599.png)

- 例：<img src="C:/Users/%E9%BB%84/AppData/Roaming/Typora/typora-user-images/image-20230802113046006.png" alt="image-20230802113046006" style="zoom:40%;" />

​			 <img src="C:/Users/%E9%BB%84/AppData/Roaming/Typora/typora-user-images/image-20230802113136469.png" alt="image-20230802113136469" style="zoom:53%;" />

- 修改定义动作里的3例子的 if 语句：<img src="C:/Users/%E9%BB%84/AppData/Roaming/Typora/typora-user-images/image-20230802112510273.png" alt="image-20230802112510273" style="zoom:40%;" />

​			不满足 if 情况，执行 else 情况的语句，由于 else 中未解析content2，所以找不到hello里定义的content；所以执行块动作。





































# 处理静态文件



<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307311505814.png" alt="image-20230731150536653" style="zoom:50%;" />

返回一个处理器。

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307311527481.png" alt="image-20230731152702358" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202307311527469.png" alt="image-20230731152741368" style="zoom:50%;" />



































# 会话控制



让服务器知道哪些请求是哪些人发的。







## Cookie

- 服务器创建的，用来区分不同用户的一段信息。

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308031557944.png" alt="image-20230803155219070" style="zoom:50%;" />

- 是<font color='red'>保存在</font>浏览器（即在<font color='red'>客户端</font>）的。

- 是在服务器端创建的。

- 默认是会话级别的（打开到关闭浏览器算一次会话），有效时间是一次会话。

  [ 如果不设置有效时间，关闭浏览器就失效了，设置了关闭也不失效 ]

  <img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308031605154.png" alt="image-20230803160534930" style="zoom:50%;" />

- name 和 value 是每一个Cookie均必须有的部分。NAME是该Cookie的名称，VALUE是该Cookie的值。





### 运行原理

<img src="https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308031627277.png" alt="image-20230803162724158" style="zoom:50%;" />





### 创建cookie

```go
//setCookie 添加Cookie
func setCookie(w http.ResponseWriter, r *http.Request) {
    //创建Cookie
    cookie := http.Cookie{
        Name: "user",
        Value: "admin",
        HttpOnly: true,
    }
    //通过响应头，将Cookie发送给浏览器
    w.Header().Set("Set-Cookie", cookie.String())
}
```



![image-20230803163953344](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308031639573.png)



![image-20230803164528601](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308031645816.png)





### 获取cookie

- 每次发送请求通过请求头携带Cookie，所以我们可以<font color='orange'>通过Request结构的Header字段</font>获取所有Cookie。

![image-20230803165036780](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308031650905.png)



- 如果只获取一个Cookie，我们可以<font color='cornflowerblue'>通过Request结构的Cookie方法</font>快速获取

![image-20230803165136859](https://cdn.jsdelivr.net/gh/Yyyyx0731/blog@img/img/202308031651984.png)





### 用途及缺陷

- Cookie的用途

  - 广告推荐

  - 免登录

- Cookie的缺陷

  - Cookie是明文的，不安全（按F12能看见信息）

  - 不同的浏览器对Cookie的大小和数量有不同的限制

  - 每次发送请求携带过多的Cookie费流量

  - Cookie的Value字段是string类型，只能保存string类型的值













## Session



- 作用就是<font color='red'>在服务器端保存</font>一些用户的数据。

  然后传输给用户一个特殊的cookie，对应着服务器中的一个session；通过他可以获取到保存用户信息的session，进而可以知道是哪个用户在发送请求。





### 运行原理

1）第一次向服务器发送请求时创建Session，给它设置一个全球唯一的ID（可以通过UUID生成）

2）创建一个Cookie，将Cookie的Value设置为Session的ID值，并将Cookie发送给浏览器

3）以后再发送请求浏览器就会携带着该Cookie

4）服务器获取Cookie并根据它的Value值找到服务器中对应的Session，也就知道了请求是那个用户发的





### 创建

```go
//Session 结构
type Session struct {
	SessionID string
	UserName  string
	UserID    int//用作外键，关联user表
	Cart      *Cart
	OrderID   string
	Orders    []*Order
}


//创建一个Session
sess := &model.Session{
	SessionID: uuid,
	UserName:  user.Username,
	UserID:    user.ID,
}
```











































































