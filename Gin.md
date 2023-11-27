***需要在gomod下使用***

```bash
go mod init 模块名
```

引入Gin框架

```go
import "github.com/gin-gonic/gin"
```

下载Gin

```bash
go get -u github.com/gin-gonic/gin
```

使用`postman`作为后端收发数据

# 响应

## Hello World

```go
package main

import (
	"github.com/gin-gonic/gin"
	"net/http"
)

func main() {
	router := gin.Default()
	//创建一个默认路由
    
	router.GET("/index", func(c *gin.Context) {
        //绑定路规则和路由函数，访问/index的路由
        
		c.String(http.StatusOK, "Hello World!")
        //http.StatusOK的默认值为200
        //当访问127.0.0.1:8080时会显示404 no found
        //访问127.0.0.1:8080/index会显示Hello World
	})

	router.Run(":8080")
}
```

两种启动方式

```go
router.Run(":8080")
http.ListenAndServer(":8080",router)
```

- 返回字符串

  ```go
  router.GET("/index", func(c *gin.Context) {
  		c.String(http.StatusOK, "Hello World!")
  	})
  ```

- 返回JSON

  ```go
  type UserInfo struct {
  	UserName string `json:"user_Name"`
  	Age      int    `json:"age"`
      Password string `json:"-"`
      //`json名称`，在浏览器中会显示出来
      //如果用`json:"-"`则不会显示
  }
  user := UserInfo{"aw", 20，"123456"}
  c.JSON(http.StatusOK, user)
  ```

  也可以使用json相应map

  ```go
  userMap := map[string]string{
      "user_name":"aw",
      "age":"20",
  }
  c.JSON(http.StatusOK,userMap)
  ```

  直接相应json

  ```go
  c.JSON(http.StatusOK,gin.H{"user_name":"aw","age":"23"})
  ```

- 返回xml

  ```go
  c.XML(http.StatusOK,gin.H{"user_name":"aw","age":"23"})
  ```

- 返回yaml

  ```go
  c.YAML(http.StatusOK,gin.H{"user_name":"aw","age":"23","data":gin.H{"user_name":"ax"}})
  ```


## 响应html

需要创建一个`templates`模板文件夹，里面创建`html`文件

```go
//响应函数
c.HTML(http.StatusOK,"index.html",gin.H{"username":"aw"})
//通过gin.H{}向前端传递数据
```

```html
//html
<body>
    <p>{{.username}}<p>
    //使用{{.json名}}获取从后端传递的数据
</body>    
```

## 响应文件

静态文件一般存放在`static`目录下

```go
router.StaticFile("static", "static/12.jpg")
	//第一个参数网站路径，第二个参数本地资源路径
	//在goland不存在相对文件路径，只有相对项目的路径
```

## 重定向

```go
//重定向
router.GET("/baidu", func(c *gin.Context) {
	c.Redirect(301, "https://www.baidu.com")
	//301为永久重定向
})
router.GET("/now", func(c *gin.Context) {
	c.Redirect(302, "https://lixianla.com/")
	//302为临时重定向
})
```

# 请求

```go
package main

import (
	"fmt"
	"github.com/gin-gonic/gin"
)

func _query(c *gin.Context) {
	//user := c.Query("user")
	//fmt.Println(user)

	fmt.Println(c.GetQuery("user"))
    //网址中user存在则返回user对应的值和true
    //不存在则返回false
}

func main() {
	router := gin.Default()
	router.GET("/query", _query)
	router.Run(":8080")
}
```

网址输入`127.0.0.1:8080/query?user=renxia`

***只有网址中存在user=，不管后面有没有值对应，都算true***

## 动态参数

```go
router.GET("/param/:user",func (c *gin.Context) {
	fmt.Println(c.Param("user"))
} )
```

***必须要加冒号***

## 表单参数

```go
router.POST("/form",func(c *gin.Context) {
	fmt.Println(c.PostForm("name"))
})

router.POST("/form",func(c *gin.Context) {
	fmt.Println(c.DefaultPostForm("name","aw"))
})
//设置默认值
```

**使用POST方法**

## 原始参数

```go
router.POST("/raw", func (c *gin.Context) {
	body, _ := c.GetRawData()
    
    //获取请求头，在postman的Headers中
	contentType := c.GetHeader("Content-Type")
	fmt.Println(contentType)
	fmt.Println(string(body))
})
```

Postman中Body发送数据

- form-data格式

  ```go
  ----------------------------698739750918599348687518
  Content-Disposition: form-data; name="name"
  
  abc
  ----------------------------698739750918599348687518
  Content-Disposition: form-data; name="age"
  
  20
  ----------------------------698739750918599348687518--
  ```

- x-www-form-urlencoded格式

  ```go
  name=abc&age=20
  ```

- raw格式

  ```json
  {
      "name":"abc",
      "age":"20"
  }
  ```

# 四大请求

`GET`	`POST`	`PUT`	`DELETE`

RESTful风格指网络应用编程中资源定位于资源操作的风格

- GET：从服务器取资源
- POST：在服务器新建资源
- PUT：在服务器更新资源（客户端提供完整资源数据）
- PATCH：在服务器更新资源（客户端提供需要修改的资源数数据）
- DELETE：从服务器删除资源

```go
package main

import (
	"fmt"
	"github.com/gin-gonic/gin"
	"github.com/goccy/go-json"
	"net/http"
)

type ArticleModel struct {
	Title   string `json:"title"`
	Content string `json:"content"`
}

type Response struct {
	Code int    `json:"code"`
	Data any    `json:"data"`
	Msg  string `json:"msg"`
}

func _bindJson(c *gin.Context, obj any) (err error) {
	body, _ := c.GetRawData()
	contentType := c.GetHeader("Content-Type")
	switch contentType {
	case "application/json":
		err = json.Unmarshal(body, obj)
		if err != nil {
			fmt.Println(err.Error())
			return err
		}
	}
	return nil
}

// 文章列表页面
func _getList(c *gin.Context) {

	articleList := []ArticleModel{
		{"Go语言入门", "asdasds"},
		{"Python语言入门", "asd"},
	}

	c.JSON(http.StatusOK, Response{0, articleList, "成功"})
}

// 文章详细页面
func _getDetail(c *gin.Context) {
	//获取param中的id
	fmt.Println(c.Param("id"))
	article := ArticleModel{
		"Go语言入门", "asd",
	}
	c.JSON(http.StatusOK, Response{0, article, "成功"})
}

// 创建文章
func _create(c *gin.Context) {
	//接收前端传递来的json数据
	var article ArticleModel

	err := _bindJson(c, &article)
	if err != nil {
		fmt.Println(err)
		return
	}

	c.JSON(http.StatusOK, Response{0, article, "成功"})
}

// 编辑文章
func _update(c *gin.Context) {
	fmt.Println(c.Param("id"))
	var article ArticleModel

	err := _bindJson(c, &article)
	if err != nil {
		fmt.Println(err)
		return
	}
	c.JSON(http.StatusOK, Response{0, article, "修改成功"})
}
func _delete(c *gin.Context) {
	fmt.Println(c.Param("id"))

	c.JSON(http.StatusOK, Response{0, map[string]string{}, "删除成功"})
}
func main() {
	router := gin.Default()
	router.GET("/articles", _getList)       //列表
	router.GET("/articles/:id", _getDetail) //详情
	router.POST("/articles", _create)       //创建
	router.PUT("/articles/:id", _update)    //更新
	router.DELETE("/articles/:id", _delete) //删除
	router.Run(":8080")
}
```

# 请求头

```go
package main

import (
	"fmt"
	"github.com/gin-gonic/gin"
	"net/http"
)

func main() {
	router := gin.Default()

	router.GET("/", func(c *gin.Context) {
		fmt.Println(c.GetHeader("User-Agent"))
		//首字母不区分大小写，但单词与单词之间使用"-"分割
        
		fmt.Println(c.Request.Header["User-Agent"])
        //可以获取多个key对应的value
		c.JSON(http.StatusOK, gin.H{"msg": "成功"})
	})
    
    //爬虫和普通用户区别对待
	router.GET("/index", func(c *gin.Context) {
		userAgent := c.GetHeader("User-Agent")
		//使用正则匹配
		//字符串的包含匹配
		if strings.Contains(userAgent, "python") {
			c.JSON(0, gin.H{"data": "爬虫数据"})
			return
		}
		c.JSON(0, gin.H{"data": "用户数据"})
	})

	router.Run(":8080")
}
```

# bind绑定参数

bind可以将前端传递来的参数与`结构体`进行`参数绑定`,以及参数校验

需要在结构体上加入`Tag`          `json`	`form`	`url`	`xml`	`yaml`

## Must Bind

以Bind开头的方法，如：`BindJSON``BindQuery``BindUri`

在校验失败后后修改状态码

## Should Bind

可以绑定`json``query``param``yaml``xml`

不会修改状态码

### ShouldBindJSON

绑定Json参数

```go
router.POST("/", func(c *gin.Context) {
	var userInfo UserInfo
	err := c.ShouldBindJSON(&userInfo)
	if err != nil {
		c.JSON(http.StatusOK, gin.H{"msg": "错误"})
		return
	}
	c.JSON(http.StatusOK, userInfo)
})
```

### shouldBindQuery

绑定请求，需要在结构体中使用form标签

```go
type UserInfo struct{
    Name string `json:"name" form:"name"`
    Age  int    `json:"name" form:"age"`
}
```

```go
router.POST("/query", func(c *gin.Context) {
	var userInfo UserInfo
	err := c.ShouldBindQuery(&userInfo)
	if err != nil {
		c.JSON(http.StatusOK, gin.H{"msg": "错误"})
		return
	}
	c.JSON(http.StatusOK, userInfo)
})
```

# 验证器

## 常用验证器

**对于字符串**

- required：必填字段，不能没有，也不能为空

  ```go
  Name string `json:"name" binding:"required"`
  ```

- min：最小长度   max：最大长度

  ```go
  Password   string `json:"password" binding:"min=6,max=12"`
  ```

- len：长度

  ```go
  Password string`json:"password" binding:"len=6"`
  ```

**对于数字**

- eq：等于
- ne：不等于
- gt：大于
- gte：大于等于
- lt：小于
- lte：小于等于

**对于同级字段**

- eqfield：等于其他字段的值

  ```go
  Password   string `json:"password" binding:"min=6,max=12"`
  RePassword string ` json:"rePassword" binding:"eqfield=Password"`
  ```

- nefield：不等于其他字段的值

**忽略字段**

```go
binding="-"
```

## 内置验证器

```go
//枚举类型
oneof=red green

//字符串类型
contains=aw  //包含aw的字符串
excludes     //不包含
startswith   //字符串前缀
endswith     //字符串后缀

//数组类型
dive

//网络验证
ip        binding:"ip"
ipv4
ipv6
uri
url

//日期验证
```

## 自定义错误消息





# 文件

## 上传文件

`form-data`直接以文件流的形式传输

目录需要提前创建好

**SaveUploadedFile**

```go
router.POST("/upload", func(c *gin.Context) {
	file, err := c.FormFile("Myfile")
	if err != nil {
		fmt.Println("上传文件出错")
		c.JSON(http.StatusOK, gin.H{"msg": "上传错误"})
		return
	}
	fmt.Println(file.Size)
	fmt.Println(file.Filename)
	c.SaveUploadedFile(file, "./uploads/2.md")
    //第一个参数对应的是postman中的key
    //第二个参数为保存文件的路径的文件
	c.JSON(http.StatusOK, gin.H{"msg": "上传成功"})
})
```

**Open**读取文件内容

```go
router.POST("/upload", func(c *gin.Context) {
	file, err := c.FormFile("Myfile")
	if err != nil {
		fmt.Println("上传文件出错")
		c.JSON(http.StatusOK, gin.H{"msg": "上传错误"})
		return
	}
    fileRead, _ := file.Open()
	data, _ := io.ReadAll(fileRead)

	fmt.Println(string(data))
	fmt.Println(file.Size)
	fmt.Println(file.Filename)
	c.JSON(http.StatusOK, gin.H{"msg": "上传成功"})
})
```

通过Open读取文件内容，然后创建一个文件，将读取到的内容复制下来实现保存功能

```go
readerFile, _ := file.Open()
writerFile, _ := os.Create("./uploads/2.txt")
defer writerFile.Close()
n, _ := io.Copy(writerFile, readerFile)
fmt.Println(n)
```

***多个文件上传***

```go
router.POST("/uploads", func(c *gin.Context) {
	form, _ := c.MultipartForm()
	files, _ := form.File["upload[]"]
	for _, file := range files {
		c.SaveUploadedFile(file, "./uploads/"+file.Filename)
	}
	c.JSON(http.StatusOK, gin.H{"msg": fmt.Sprintln("成功上传 %d 个文件", len(files))})
})
```

## 下载文件

```go
router.GET("/download", func(c *gin.Context) {
    c.Header("Content-Type", "application/octet-stream")
    //唤醒浏览器的下载功能
    c.Header("Content-Disposition", "attachment;filename="+"name.png")
    //指定下载名称和格式
    c.File("./uploads/1.txt")
    //保存的文件路径
})
```

# 中间件和路由

## 单个中间件

```go
func main() {
	router := gin.Default()

	router.GET("/", func(c *gin.Context) {
		c.JSON(http.StatusOK, gin.H{"msg": "index"})
	}, func(c *gin.Context) {
		fmt.Println("1")
	}, func(c *gin.Context) {
		fmt.Println("2")
	}, func(c *gin.Context) {
		fmt.Println("3")
	})
	router.Run(":8080")
}
```

## 拦截中间响应

`GET（"/",func()）`第二个参数为一个切片，传入任意数量的函数

如果有多个单中间件，想要停止的话，可以在函数体内添加`c.Abort()`停止运行

```go
func m1(c *gin.Context) {
	fmt.Println("m1 in")
	c.Next()
	fmt.Println("m1 out")
}
func index(c *gin.Context) {
	fmt.Println("index in")
	c.Next()
	fmt.Println("index out")
}
func m2(c *gin.Context) {
	fmt.Println("m2 in")
	c.Next()
	fmt.Println("m2 out")
}

func main() {
	router := gin.Default()
	router.GET("/test", m1, index, m2)
	router.Run(":8080")
}
```

运行结果：

![df2c623db2e9020ff67584059ec5a2c3](https://gitee.com/qiqibaba43/image/raw/master/202310092032343.png)

`Next()`相当于将下面的内容先压入栈中，等到程序运行结束后，逐个弹出并运行

## 全局中间件

```go
func m1(c *gin.Context) {
	fmt.Println("m1 in")
	c.Next()
	fmt.Println("m1 out")
}
func main() {
	router := gin.Default()
    router.Use(m1)
	router.Run(":8080")
}
```

直接在主函数体内使用`Use()`函数

**传递数据**

```go
func m1(c *gin.Context) {
    c.Set("name":"aw")
}
func main(){
    router:=gin.Defult()
    router.GET("/",func(c *gin.Conetext){
        name,_:=c.Get("name")
        fmt.Println(name)
    })
    router.Run(":8080")
}
```

如果是传输的数据是结构体的话，接收数据的时候需要进行断言

# 路由分组

```go
func main() {
	router := gin.Default()

	r := router.Group("/api")

	r.GET("/test", func(c *gin.Context) {
		c.JSON(http.StatusOK, gin.H{"msg": "成功"})
	})
	router.Run(":8080")
}
```

只能通过`127.0.0.1:8080/api/test`访问网页，而不能通过`127.0.0.1:8080/test`

# 日志

- 记录用户操作，猜测用户行为
- 记录bug

## 内置日志系统

```go
func main() {
	file, _ := os.Create("gin.log")
    //创建文件gin.log，用于存放日志文件
	gin.DefaultWriter = io.MultiWriter(file, os.Stdout)
    //将日志写入gin.log于控制台中
	router := gin.Default()
	router.GET("/", func(c *gin.Context) {})
	router.Run(":8080")
}
```

## logrus

```go
logrus.SetLevel(logrus.DebugLevel)
//设置等级，低于当前等级不会打印
logrus.Error("错误")
logrus.Warnln("警告")
logrus.Infof("信息")
logrus.Debugf("debug")
logrus.Println("打印")
fmt.Println(logrus.GetLevel())
```

```go
log := logrus.WithField("app", "study").WithField("service", "logrus")
	//公共字段，每次运行都会输出
	//可以使用链式调用
	log = logrus.WithFields(logrus.Fields{
		"name": "aw",
		"ip":   "127.0.0.1",
	})
	//也可以使用Fields
	log.Errorf("你好")
```

