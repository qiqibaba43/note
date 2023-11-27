# 连接

国内镜像代理

```bash
go env -w GOPROXY=https://mirrors.aliyun.com/goproxy/,direct
```

开启数据库

```mysql
mysql -u root -p
#用root身份打开mysql
#用户名root 密码@Wgw20030305
CREATE DATABASE gorm
#创建数据库gorm
```

安装gorm

```bash
go get gorm.io/driver/mysql
go get gorm.io/gorm
```

连接mysql

```go
package main

import (
	"fmt"
	"gorm.io/driver/mysql"
	"gorm.io/gorm"
)

var DB *gorm.DB

func init() {
	username := "root"         //用户名
	password := "@Wgw20030305" //密码
	host := "127.0.0.1"        //IP
	port := 3306               //端口号
	Dbname := "gorm"           //数据库名
	timeout := "10s"           //超时

	//root:root@tcp(127.0.0.1:3306)/gorm?
	dsn := fmt.Sprintf("%s:%s@tcp(%s:%d)/%s?charset=utf8mb4&parseTime=True&loc=Local&timeout=%s", username, password, host, port, Dbname, timeout)
	//连接MySQL，获得DB实例
	db, err := gorm.Open(mysql.Open(dsn))
	if err != nil {
		panic("连接数据库失败，error=" + err.Error())
	}
	//连接成功
	//fmt.Println(db)
	DB = db
}

func main() {
	fmt.Println(DB)
}
```

为了保证数据的一致性，gorm默认是在事务中执行读写操作。如果没有需要，可以在初始化时禁用，以提升性能

```go
db,err:=gorm.Open(mysql.sqlite.Open("gorm.db"),&gorm.Config{
    SkipDefaultTransaction:True,
})
```

一般采用蛇形命名法，表名用复数，字段名用单数

```go
type Student struct {
	ID   uint
	Name string
	Age  int
}
var DB *gorm.DB
func main(){
    DB.AutoMigrate(&Student{})
}
```

在数据库中就会显示出表单students

```mysql
mysql> show tables;
+----------------+
| Tables_in_gorm |
+----------------+
| students       |
+----------------+
1 row in set (0.00 sec)

mysql> show create table students\G;
*********************** 1. row *************************
       Table: students
Create Table: CREATE TABLE `students` (
  `id` bigint unsigned NOT NULL AUTO_INCREMENT,
  `name` longtext,
  `age` bigint DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci
1 row in set (0.00 sec)
```

显示日志

默认只打印错误和慢SQL

更换日志等级

```go
var mysqlLogger=logger.Default.LogMode(logger.Info)

db, err := gorm.Open(mysql.Open(dsn), &gorm.Config{
		SkipDefaultTransaction: true,
		Logger: mysqlLogger,
	})
```

# 模型定义

小写的属性是不会生成字段的

`AutoMigrate`的逻辑只新增，不修改，不删除

```go
type Student struct{
	ID unit
    Name string
    Age int
}
```

变为

```go
type Student struct{
	ID unit
    Name string
    Age int
    Email *string
}
```

数据库中会新增字段email

再变为

```go
type Student struct{
	ID unit
    Name1 string
    Age int
    Email *string
}
```

数据库中会新增字段name1，且name依旧存在

修改字段的大小

```go
type Student struct {
	ID    uint    `gorm:"size:10"`
	Name1 string  `gorm:"size:16"`
	Age   int     `gorm:"size:3"`
	Email *string `gorm:"size:128"`
}
```

```go
2023/11/20 19:49:28 /home/renxia/桌面/gorm/connect.go:50
[16.696ms] [rows:0] ALTER TABLE `students` MODIFY COLUMN `name1` varchar(16)

2023/11/20 19:49:28 /home/renxia/桌面/gorm/connect.go:50
[15.536ms] [rows:0] ALTER TABLE `students` MODIFY COLUMN `age` tinyint

2023/11/20 19:49:28 /home/renxia/桌面/gorm/connect.go:50
[15.661ms] [rows:0] ALTER TABLE `students` MODIFY COLUMN `email` varchar(128)
```

## 字段标签

声明 model 时，tag 是可选的，GORM 支持以下 tag： tag 名大小写不敏感，但建议使用 camelCase 风格

多个tag之间用分号间隔

```go
type Student struct{
    Name *string `gorm:"size:16;column:Name1"`
}
```



| 标签           | 作用         |
| -------------- | ------------ |
| type           | 字段类型     |
| size           | 字段大小     |
| column         | 自定义列名   |
| primaryKey     | 主键         |
| default        | 设置默认值   |
| not null       | 不能为空     |
| embedded       | 嵌套字段     |
| embeddedPrefix | 嵌套字段前缀 |
| comment        | 注释         |

# CURD

## 创建

```go
//插入单个数据
s1 := Student{
    Name:   "aw",
	Age:    20,
	Gender: true,
	Email:  &email,
}

DB.Create(&s1)

//批量插入
var studentList []student
for i:=0;i<10;i++{
    studentList.append(studentList,Student{
		Name:   fmt.Sprintf("aw%d", i+1),
		Age:    21 + i,
		Gender: i%2 == 1,
		Email:  &email,
    })
}

DB.Create(studentList)
```

## 查询

```go
var student Student
	DB.Session(&gorm.Session{
		Logger: mysqlLogger,
	})
DB.Take(&student) //默认查找第一个
fmt.Println(student)

//查找第一个和最后一个
student = Student{}
DB.First(&student)
fmt.Println(student)
student = Student{}
DB.Last(&student)
fmt.Println(student)

//根据主键查询
student = Student{}
DB.Take(&student, 4)
fmt.Println(student)

//根据字段名查询
student = Student{}
DB.Take(&student, "name=?", "aw9") //"?"作为占位符，将操作全部转义，可以有效防止SQL注入
fmt.Println(student)
```

`First` and `Last` 方法会按主键排序找到第一条记录和最后一条记录 (分别)。 只有在目标` struct `是指针或者通过 `db.Model()` 指定 `model `时，该方法才有效。 此外，如果相关 `model `没有定义主键，那么将按` model` 的第一个字段进行排序。

> SQL注入即是指web应用程序对用户输入数据的合法性没有判断或过滤不严，攻击者可以在web应用程序中事先定义好的查询语句的结尾后，添加额外的SQL语句，在管理员不知情的情况下实现非法操作，以此来实现欺骗数据库服务器执行非授权的任意查询，从而进一步得到相应的数据信息。

- 参数用户可控 —— 即用户能够控制数据的输入
- 我们构造的参数可带入数据库执行 —— 原本要执行的代码，拼接了用户的输入

### 批量查询

```go
//全部查询
DB.Find(&studentList)
fmt.Println(studentList)

count := DB.Find(&studentList).RowsAffected  //返回查询的记录条数
err := DB.Find(&studentList).Error  //查询是否失败
fmt.Println(count, err)


for _, student := range studentList {
	data, _ := json.Marshal(student)
	fmt.Println(string(data))
}

//使用切片
var studentList []Student
DB.Find(&studentList, []int{4, 7, 9})
fmt.Println(studentList)

DB.Find(&studentList, "name in (?)", []string{"aw4", "aw8"})
DB.Where("name in (?)", []string{"aw74", "aw8"}).Find(&studentList)
//两种写法
fmt.Println(studentList)
```

## 更新

`save`是一个组合函数。如果保存值不包含主键，则将执行 Create，否则将执行 Update（包含所有字段）

```go
var student Student
DB.Take(&student, 10)
student.Name = "qiqibaba"
DB.Save(&student)
fmt.Println(student)

DB.Save(&Student{ID: 30, Name: "qiqibaba", Gender: true, Age: 0, Email: nil})   //两者是等效的

//使用seleect可以只对某个字段进行修改，不管其他字段是否改过
var student Student
DB.Take(&student, 20)
student.Name = "qiqibaba"
student.Age = 30
DB.Select("name").Save(&student)
fmt.Println(student)

//批量更新单个字段
var studentList   []student
DB.Find(&studentList, []int{10, 11, 12}).Update("gender", false)

//批量更新多个字段
var studentList []Student
DB.Find(&studentList, []int{10, 11, 12}).Updates(Student{Name: "aw0", Age: 100, Gender: false, Email: nil})
```

## 删除

```go
//删除
DB.Delete(&student)

//条件删除
DB.Where("name=?", "aw40").Delete(&student)
DB.Delete(&Student{},1)
DB.Delete(student,1)
DB.Delete(&student,1)
```

# HOOK

在创建，查询，更新，删除等操作之前之后调用的函数

```go
func (user *Student) BeforeCreate(tx *gorm.DB) (err error) {
	email := "wgw20030305@163.com"
	user.Email = &email
	return nil
}
```

**创建对象**

```go
// 开始事务
BeforeSave
BeforeCreate
// 关联前的 save
// 插入记录至 db
// 关联后的 save
AfterCreate
AfterSave
// 提交或回滚事务
```

**更新对象**

```go
// 开始事务
BeforeSave
BeforeUpdate
// 关联前的 save
// 更新 db
// 关联后的 save
AfterUpdate
AfterSave
// 提交或回滚事务
```

**删除对象**

```go
// 开始事务
BeforeDelete
// 删除 db 中的数据
AfterDelete
// 提交或回滚事务
```

**查询对象**

```go
// 从 db 中加载数据
// Preloading (eager loading)
AfterFind
```

