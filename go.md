# 1.安装GoLang

## 1.1环境变量

在环境变量中设置

- GOROOT：源码所在的路径
- GOPATH：开发项目GO项目的默认路径
- PATH：源码路径下的bin文件

文件夹的格式

- Goworkspace
  - src
    - go_code
      - project_01
        - main
          - Hello.go
        - package
        - go.mod

配置mod依赖：

`go mod init 项目/main`

## 1.2运行程序

`go build`编译程序生成`exe`文件

`go run 项目名` 直接运行`go`文件，类似于执行脚本文件

:star:常用快捷键

`Ctrl+Alt+L`：格式化代码

`Ctrl+/`：单行注释

`Ctrl+Shift+/`：多行注释

`Ctrl+J`：快速生成代码片段

`Ctrl+X`：删除当前光标所在行

`Ctrl+D`：复制当前光标所在行

`Alt+回车`：自动导包

****

## 实现输入输出

```go
package main

import(
	"fmt" //输出包
    "flag"//输入包
)

func main(){
    var x = flag.Int("y",0,"代输入数据")
    //定义命令行参数x
    //第一个参数：在命令行输入 --y可以将=后面的数字传入x中
    //第二个参数：x的默认值
    //第三个参数：对x的描述
    flag.Parse()
    //调用flag包中的解析函数
    fmt.Println(*x)
    //调用fmt包中的打印函数
}
```



****

# 2.基础语法

## 2.1基本类型

- bool
- string
- int,int8,int16,int32,int64
- uint,uint8,uint16,uint32,uint64,uintptr
- byte（uint8别名）
- rune（int32别名，表示一个Unicode码）
- float32，float64
- complex64，complex128

## 2.2声明变量

声明变量的格式：`var name type`

var 是声明变量关键字，name是变量名，type是变量类型

:star:所有的内存在Go中都是经过初始化的

批量声明变量：

```
var {
	a int
	b bool
	c []float32
	d func() bool
	e struct {
		x int
	}
}
```

简短声明：`i:=0`

注意点：

- 定义变量，同时显式初始化
- 不能提供数据类型
- 只能用于函数内部

多重赋值：

```go
var a,b int = 100, 200
b, a=a, b
//a与b互换
```

## 2.3匿名变量

在编码过程中，可能会遇到没有名称的变量、类型或方法。虽然这不是必须的，但有时候这样做可以极大地增强代码的灵活性，这些变量被统称为匿名变量。

匿名变量使用一个下划线`_`表示。任何类型都可以赋值给它，但任何赋给这个标识符的值都将被抛弃，因此这些值不能在后续的代码中使用，也不可以使用这个标识符作为变量对其它变量进行赋值或运算。使用匿名变量时，只需要在变量声明的地方使用下画线替换即可

```go
func GetData() (int, int) {
    return 100, 200
}
func main(){
    a, _ := GetData()
    _, b := GetData()
    fmt.Println(a, b)
}
//a=100 b=200
```

:star:<font color='red'>匿名变量不会占用内存，不会分配内存空间</font>

## 2.4复数型

- complex128表示64位实数和虚数

- complex64表示32位实数和虚数

声明复数格式：`var name complex128 = complex(x,y)`

x为实部，y为虚部

## 2.5字符串型

Go语言中字符串占用1至4个字节。不仅减少了内存和硬盘空间占用，同时也不用像其它语言那样需要对使用 UTF-8 字符集的文本进行编码和解码

定义多行字符串，使用反引号

```
const str = `a
b
c
`

fmt.Println(str)
```

***在反引号中间的内容不会被转义***

## 2.6字符型

Go语言的字符有两种：

- uint8类型，又叫byte型，表示ASCII码的一个字符
- rune类型，表示一个UTF-8字符。等价于int32

在书写Unicode字符时，需要在16进制数前加前缀`\u`或者`\U`

使用到4字节，使用前缀`\u`。使用到8字节，使用前缀`\U`

****

Unicode 统一了所有字符的编码，是一个 Character Set，也就是字符集，字符集只是给所有的字符一个唯一编号，但是却没有规定如何存储。

这时，用什么规则存储 Unicode 字符就成了关键，可以规定，一个字符使用四个字节存储，也就是 32 位，这样就能涵盖现有 Unicode 包含的所有字符，这种编码方式叫做 UTF-32（UTF 是 UCS Transformation Format 的缩写）。UTF-32 的规则虽然简单，但是缺陷也很明显，假设使用 UTF-32 和 ASCII 分别对一个只有西文字母的文档编码，前者需要花费的空间是后者的四倍（ASCII 每个字符只需要一个字节存储）

****

## 2.7数据类型转换

:star:<font color='red'>Go语言中不存在隐式类型转换，所有变量类型转换必须显式声明</font>

只有相同底层类型的变量之间可以进行相互转换（将int16转换成int32）

- 将浮点数转换成整数时，直接截取整数部分
- 将int32转int16时，将前2个字节删去

## 2.8指针类型

:star:指针的两个核心概念：

- 类型指针：允许对这个指针类型的数据进行修改，传递数据可以直接使用指针，不需要拷贝数据。类型指针不能进行偏移和运算
- 切片：由指向起始元素的原始指针，元素数量和容量构成

指针没有被分配变量时，默认值为`nil`。指针通常缩写为`ptr`

也可以使用`new`创建指针变量

```
str := new(string)
*str = "Go学习"

fmt.Println(*str)
```

## 2.9生命周期

- 全局变量：生命周期和整个程序的运行周期一致
- 局部变量：生命周期时动态的，从创建变量的生命语句开始，到变量不再被引用为止
- 形式参数和函数返回值：都是局部变量，在函数被调用的时候创建，函数调用结束后被销毁

:star:堆与栈区别
堆与栈实际上是操作系统对进程占用的内存空间的两种管理方式，主要有如下几种区别：
（1）管理方式不同。栈由操作系统自动分配释放，无需我们手动控制；堆的申请和释放工作由程序员控制，容易产生内存泄漏；

（2）空间大小不同。每个进程拥有的栈大小要远远小于堆大小。理论上，进程可申请的堆大小为虚拟内存大小，进程栈的大小 64bits 的 Windows 默认 1MB，64bits 的 Linux 默认 10MB；

（3）生长方向不同。堆的生长方向向上，内存地址由低到高；栈的生长方向向下，内存地址由高到低。

（4）分配方式不同。堆都是动态分配的，没有静态分配的堆。栈有 2 种分配方式：静态分配和动态分配。静态分配是由操作系统完成的，比如局部变量的分配。动态分配由alloca()函数分配，但是栈的动态分配和堆是不同的，它的动态分配是由操作系统进行释放，无需我们手工实现。

（5）分配效率不同。栈由操作系统自动分配，会在硬件层级对栈提供支持：分配专门的寄存器存放栈的地址，压栈出栈都有专门的指令执行，这就决定了栈的效率比较高。堆则是由C/C++提供的库函数或运算符来完成申请与管理，实现机制较为复杂，频繁的内存申请容易产生内存碎片。显然，堆的效率比栈要低得多。

（6）存放内容不同。栈存放的内容，函数返回地址、相关参数、局部变量和寄存器内容等。当主函数调用另外一个函数的时候，要对当前函数执行断点进行保存，需要使用栈来实现，首先入栈的是主函数下一条语句的地址，即扩展指针寄存器的内容（EIP），然后是当前栈帧的底部地址，即扩展基址指针寄存器内容（EBP），再然后是被调函数的实参等，一般情况下是按照从右向左的顺序入栈，之后是被调函数的局部变量，注意静态变量是存放在数据段或者BSS段，是不入栈的。出栈的顺序正好相反，最终栈顶指向主函数下一条语句的地址，主程序又从该地址开始执行。堆，一般情况堆顶使用一个字节的空间来存放堆的大小，而堆中具体存放内容是由程序员来填充的。

## 2.10常量

所有的常量运算都在编译期完成，减少运行时间

`iota`常量生成器

常量类型声明可以使用`iota`常量生成器初始化。可用于生成一组规则相似的初始化常量。首行置0，下面每行依次加1

```go
const (
	Sunday Weekday = iota
    Monday
    Tuesday
    Wednesday
    Thursday
    Friday
    Saturday
)
```

无类型常量



# 3.流程控制

## 3.1分支结构

关键字 if 和 else 之后的左大括号`{`必须和关键字在同一行，如果你使用了 else if 结构，则前段代码块的右大括号`}`必须和 else if 关键字在同一行，这两条规则都是被编译器强制规定

```go
if condition {
    // do something
} else {
    // do something
}
```

## 3.2循环结构

***Go语言中只支持for关键字，不支持while与do while***

### for range

for range 可以遍历数组、切片、字符串、map 及通道（channel），for range 语法上类似于其它语言中的 foreach 语句

```go
for key, val := range coll {
    ...
}
```

- 数组，切片，字符串返回索引和值
- map返回键和值
- 通道只返回通道内的值

***对map遍历时，输出的键值对是无序的***

## 3.3switch

<font color="red">Go语言中，case与case之间不需要通过break语句跳出当前case代码块以避免执行到下一行</font>

每个`case`后可以对应多个待匹配的值

```go
var a = "mum"
switch a {
case "mum", "daddy":
    fmt.Println("family")
}
```

### fallthrough

在Go语言中 `case` 是一个独立的代码块，执行完毕后不会像C语言那样紧接着执行下一个` case`。为了兼容一些移植代码，加入了 `fallthrough` 关键字来实现

```go
var s = "hello"
switch {
case s == "hello":
    fmt.Println("hello")
    fallthrough
case s != "world":
    fmt.Println("world")
}
```

## 3.4goto

`goto`常用于跳出多层循环，而`break`只能跳出单层循环

`goto`语句通过标签进行代码之间的无条件跳转

```go
package main
import "fmt"
func main() {
    for x := 0; x < 10; x++ {
        for y := 0; y < 10; y++ {
            if y == 2 {
                // 跳转到标签
                goto breakHere
            }
        }
    }
    // 手动返回, 避免执行进入标签
    return
    // 标签
breakHere:
    fmt.Println("done")
}
```

# 4.容器

## 4.1数组

声明数组：`var 数组名 [元素数量] Type`

```go
var q [3]int = [3]int{1,2,3}

q :=[...]int {1,2,3}    
//省略号表示数组长度根据初始化值的个数计算
```

数组的长度是数组类型的一个组成部分，因此 [3]int 和 [4]int 是两种不同的数组类型，数组的长度必须是常量表达式，***因为数组的长度需要在编译阶段确定***

```go
纯文本复制
q := [3]int{1, 2, 3}q = [4]int{1, 2, 3, 4} // 编译错误：无法将 [4]int 赋给 [3]int
```

## 4.2多维数组

声明多维数组：`var 数组名 [元素数量1][元素数量2]...[元素数量n] Type`

```go
// 声明一个二维整型数组，两个维度的长度分别是 4 和 2
var array [4][2]int
// 使用数组字面量来声明并初始化一个二维整型数组
array = [4][2]int{{10, 11}, {20, 21}, {30, 31}, {40, 41}}
// 声明并初始化数组中索引为 1 和 3 的元素
array = [4][2]int{1: {20, 21}, 3: {40, 41}}
// 声明并初始化数组中指定的元素
array = [4][2]int{1: {0: 20}, 3: {1: 41}}
```

## 4.3切片

<font color="red">切片是对数组的一个连续片段的引用</font>

`slice [开始位置:结束位置]`

- sclie：表示目标切片对象
- 开始位置：对应目标切片对象的索引
- 结束位置：对应目标切片的结束索引   <font color="red">不包括在切片内</font>

各种表示方法：

- `a[0:0]`：清空切片
- `a[:]`：切片本身
- `a[:N]`：从开头到下表为N处
- `a[N:]`：从下表为N处到某位

### 直接创建切片

```go
var name []Type
```

### 动态的创建新的切片

```go
make([]Type,size,cap)
```

- Type：元素类型
- size：为该切片分配多少个元素
- cap：预分配的元素数量。<font color="red">提前分配空间，降低多次分配造成的性能问题。预分配不会影响当前使用空间</font>

### append()

为数组动态的添加元素

```go
var a []int
a = append(a,1,2,3)
a = append(a,[]int{1,2,3})
```

如果切片的容量不足，则会发生扩容

:star:1.18版本：

- 当前容量<256，倍增法
- 当前容量>256，按照1.25倍增加
- 初始容量为0，按照目标容量扩容

在切片的开始添加元素

```go
varr a = []int{1,2,3}
a = append([]int{0},a...)
```

### 复制

```go
copy(destSlice,srcSlice []T)int
```

将源切片	srcSlice	复制到目标切片`destSlice`。源目切片的类型必须完全一致。切片大小不一样，则会按照较小的处理。返回值为实际复制的元素个数

```go
slice1:=[]int {1,2,3,4,5}
slice2:=[]int {6,7,8}
copy(slice2,slice1)
copy(slice1,slice2)
```

### 删除

#### 从开头位置删除

- 直接移动数据指针

  ```go
  a = []int{1, 2, 3}
  a = a[1:] // 删除开头1个元素
  a = a[N:] // 删除开头N个元素
  ```

- 原地删除

  ```go
  a = []int{1, 2, 3}
  a = append(a[:0], a[1:]...) // 删除开头1个元素
  a = append(a[:0], a[N:]...) // 删除开头N个元素
  ```

- copy()删除

  ```go
  a = []int{1, 2, 3}
  a = a[:copy(a, a[1:])] // 删除开头1个元素
  //copy(a,a[1:])执行时，a已经发生变化
  a = a[:copy(a, a[N:])] // 删除开头N个元素
  ```

#### 从中间位置删除

```go
a = []int{1, 2, 3, ...}
a = append(a[:i], a[i+1:]...) // 删除中间1个元素
a = append(a[:i], a[i+N:]...) // 删除中间N个元素
a = a[:i+copy(a[i:], a[i+1:])] // 删除中间1个元素
a = a[:i+copy(a[i:], a[i+N:])] // 删除中间N个元素
```

#### 从尾部删除

```go
a = []int{1, 2, 3}
a = a[:len(a)-1] // 删除尾部1个元素
a = a[:len(a)-N] // 删除尾部N个元素
```

## 4.4map

```go
var mapname map[keytype] valuetype
```

- `mapname`为map的变量名
- `keytype`为键类型
- `valuetype`为键对应的值类型

<font color="red">map声明不会分配内存，初始化需要make，分配内存后才能赋值和使用</font>

```go
//声明map类型变量a
var a map[string]string
//make的两个参数
//1.变量的数据类型
//2.给变量分配的容量
a = make(map[string]string,10)
```

***key如果重复则会将value覆盖***

```go
//创建map的方法
//方法一
a := make(map[string]string,10)
a["no1"] = "北京"
a["no2"] = "南京"

//方法二
a := map[string]string{
    "no1" = "北京"，
    "no2" = "南京"
}
```

### 增删改查

```go
a := make(map[string]string,10)
a["no1"] = "北京"
a["no2"] = "南京"

//增加
a["no3"] = "天津"

//删除
delete(a,"no2")

//修改
a["no2"] = "上海"

//查找
val,findRes :=a["no1"]
if findRes {
    fmt.Println(val)
}else{
    fmt.Println("不存在")
}
```

### 遍历

```go
for k,v :=range scene{
    fmt.Println(k,v)
}

for _,v :=range scene{
    fmt.Println(v)
}
```

## 4.5list

初始化链表

```go
变量名 :=list.New()

var 变量名 list.List

```



# 5.函数

## 5.1函数声明

Go语言的函数属于一等公民

- 函数本身可以作为值进行传递
- 支持匿名函数和闭包
- 函数可以满足接口

Go语言中有三种类型的函数

- 函数
- 匿名函数或lambda函数
- 方法

Go语言函数声明的关键字`func`

```go
func 函数名(形式参数列表)(返回值列表){
    函数体
}
```

```go
func sum(x,y int)(z int){
    z = x + y
    return z
}
```

Go语言可以有多个返回值。常用最后一个返回参数返回可能出现的错误

```go
conn, err := connectToNetwork()
```

## 5.2匿名函数

### 定义函数

- 声明后调用

```go
func(data int){
    fmt.Println("Hello",data)
}(100)
```

- 被赋值

```go
f:=func(data int){
    fmt.Println("hello",data)
}

f(100)
```

### 作为回调函数

```go
package main
import (
    "fmt"
)
// 遍历切片的每个元素, 通过给定函数进行元素访问
func visit(list []int, f func(int)) {
    for _, v := range list {
        f(v)
    }
}
func main() {
    // 使用匿名函数打印切片内容
    visit([]int{1, 2, 3, 4}, func(v int) {
        fmt.Println(v)
    })
}
```

## 5.3构造函数

在Go语言中没有构造函数，但有工厂函数

属性首字母大写，表示能被其他包访问

```go
type person struct{
    Name string
    age int
}

func NewPerson(name string,age int)*person{
    return &person{
        Name:name,
        age:age,
    }
}
```



## 5.4实现接口



## 5.5闭包

Go语言中闭包是引用了自由变量的函数，被引用的自由变量和函数一同存在，即使已经离开了自由变量的环境也不会被释放或者删除，在闭包中可以继续使用这个自由变量，因此，简单的说：

`函数 + 引用环境 = 闭包`

```go
// 准备一个字符串
str := "hello world"
// 创建一个匿名函数
foo := func() {
   
    // 匿名函数中访问str
    str = "hello dude"
}
// 调用匿名函数
foo()
```

## 5.6可变参数

```go
func myfunc(args ...int) {
    for _, arg := range args {
        fmt.Println(arg)
    }
}

//调用
//myfunc(2, 3, 4)
//myfunc(1, 3, 7, 13)
```

<font color='red'>Go语言中可以使用interface{}传递任意类型数据</font>

### 在多个可变参数函数中传递参数

***在传递可变参数遍历后面添加...***

## 5.7defer

延迟执行语句

## 5.8异常



## 5.9测试函数





# 6.包

## 6.1基本概念

***任何源代码文件必须数某个包，源码第一行有效代码必须是package packageName***

### 包的导入

```go
//单行导入
import "lab/test"

//多行导入
import (
	"database/sql/driver"
	"database/sql"
)
```

绝对路径：`GOPATH/src/xx   `

相对路径：`../xxx`

### 包的引用格式

- 标准格式引用

  ```go
  package main
  import "fmt"
  func main() {
      fmt.Println("C语言中文网")
  }
  ```

- 自定义别名引用

  ```go
  package main
  import F "fmt"
  func main() {
      F.Println("C语言中文网")
  }
  ```

- 省略引用

  ```go
  package main
  import . "fmt"
  func main() {
      //不需要加前缀 fmt.
      Println("C语言中文网")
  }
  ```

- 匿名引用



### init函数

包的初始化流程：

![](https://gitee.com/qiqibaba43/image/raw/master/202308211616462.png)

- 一个包可以有多个 init 函数，但并不能保证执行顺序
- 包不能出现环形引用的情况
- 包的重复引用是允许

## 6.2常用内置包

### fmt

fmt 包实现了格式化的标准输入输出，这与C语言中的 printf 和 scanf 类似。其中的 fmt.Printf() 和 fmt.Println() 是开发者使用最为频繁的函数。

格式化短语派生于C语言，一些短语（%- 序列）是这样使用：

- %v：默认格式的值。当打印结构时，加号（%+v）会增加字段名；
- %#v：Go样式的值表达；
- %T：带有类型的 Go 样式的值表达。

### io

这个包提供了原始的 I/O 操作界面。它主要的任务是对 os 包这样的原始的 I/O 进行封装，增加一些其他相关，使其具有抽象功能用在公共的接口上

### bufio

bufio 包通过对 io 包的封装，提供了数据缓冲功能，能够一定程度减少大块数据读写带来的开销。

### sync

sync 包实现多线程中锁机制以及其他同步互斥机制。

### flag

flag 包提供命令行参数的规则定义和传入参数解析的功能。绝大部分的命令行程序都需要用到这个包。

### net/http

net/http 包提供 HTTP 相关服务，主要包括 http 请求、响应和 URL 的解析，以及基本的 http 客户端和扩展的 http 服务。

通过 net/http 包，只需要数行代码，即可实现一个爬虫或者一个 Web 服务器，这在传统语言中是无法想象的。

### log

log 包主要用于在程序中输出日志。

log 包中提供了三类日志输出接口，Print、Fatal 和 Panic。

- Print 是普通输出；
- Fatal 是在执行完 Print 后，执行 os.Exit(1)；
- Panic 是在执行完 Print 后调用 panic() 方法。

## 6.3自定义包

- 如果项目的目录不在 GOPATH 环境变量中，则需要把项目移到 GOPATH 所在的目录中，或者将项目所在的目录设置到 GOPATH 环境变量中，否则无法完成编译；
- 使用 import 语句导入包时，使用的是包所属文件夹的名称；
- 包中的函数名第一个字母要大写，否则无法在外部调用；
- 自定义包的包名不必与其所在文件夹的名称保持一致，但为了便于维护，建议保持一致；
- 调用自定义包时使用 `包名 . 函数名` 的方式，如上例：demo.PrintStr()。

## 6.4import

如果我们想同时导入两个有着名字相同的包，例如 math/rand 包和 crypto/rand 包，那么导入声明必须至少为一个同名包指定一个新的包名以避免冲突。这叫做导入包的重命名。

```go
import (    
    "crypto/rand"  
     mrand "math/rand" // 将名称替换mrand避免冲突
)
```

## 6.5sync

sync包中提供了互斥锁`Mutex`和读写锁`RWMutex`用于处理并发过程中可能出现同时两个或多个写成读写同一个变量的情况

```go
func (m*Mutex) Lock()
func (m*Mutex) Unlock()
```

```go
package main
import (
    "fmt"
    "sync"
    "time"
)
func main() {
    var a = 0
    var lock sync.Mutex
    for i := 0; i < 1000; i++ {
        go func(idx int) {
            lock.Lock()
            defer lock.Unlock()
            a += 1
            fmt.Printf("goroutine %d, a=%d\n", idx, a)
        }(i)
    }
    // 等待 1s 结束主程序
    // 确保所有协程执行完
    time.Sleep(time.Second)
}
```



# 7.结构体

***Go语言中没有类的概念，也不支持继承等面向对象的概念***

Go语言的结构体与“类”都是符合结构体，但结构体的内嵌配合接口比面向对象具有更高的扩展性与灵活性

## 7.1结构体

### 定义

结构体的成员也成为字段，字段有以下特性：

- 字段拥有自己的类型和值
- 字段名唯一
- 字段的类型也可以是结构体，甚至是字段所在的结构体的类型

```go
type 类型名 struct{
    字段1 字段1类型
    字段2 字段2类型
}
```

### 实例化

```go
type Point struct {
    X int
    Y int
}
var p Point
p.X = 10
p.Y = 20
```



```go
type Player struct{
    Name string
    HealthPoint int
    MagicPoint int
}
tank := new(Player)
tank.Name = "Canon"
tank.HealthPoint = 300
```

在 C/C++ 语言中，使用 new 实例化类型后，访问其成员变量时必须使用`->`操作符。

在Go语言中，访问结构体指针的成员变量时可以继续使用`.`，这是因为Go语言为了方便开发者访问结构体指针的成员变量，使用了语法糖（Syntactic sugar）技术，将 ins.Name 形式转换(*ins).Name

### 赋值

- 键值对赋值

```go
ins := 结构体类型名{
    字段1: 字段1的值,
    字段2: 字段2的值,
    …
}
```

- 值赋值

```go
ins := 结构体类型名{
    字段1的值,
    字段2的值,
    …
}
```

使用这种格式初始化时，需要注意：

- 必须初始化结构体的所有字段
- 每一个初始值的填充顺序必须与字段在结构体中的声明顺序一致
- 键值对与值列表的初始化形式不能混用

****

匿名结构体

```go
ins := struct {
    // 匿名结构体字段定义
    字段1 字段类型1
    字段2 字段类型2
    …
}{
    // 字段值初始化
    初始化字段1: 字段1的值,
    初始化字段2: 字段2的值,
    …
}
```

****

## 7.2构造函数

### 重载

```go
type Cat struct {
    Color string
    Name  string
}
func NewCatByName(name string) *Cat {
    return &Cat{
        Name: name,
    }
}
func NewCatByColor(color string) *Cat {
    return &Cat{
        Color: color,
    }
}
```

### 父级构造调用

```go
type Cat struct {
    Color string
    Name  string
}
type BlackCat struct {
    Cat  // 嵌入Cat, 类似于派生
}
// “构造基类”
func NewCat(name string) *Cat {
    return &Cat{
        Name: name,
    }
}
// “构造子类”
func NewBlackCat(color string) *BlackCat {
    cat := &BlackCat{}
    cat.Color = color
    return cat
}
```

## 7.3方法与接收器

Go 方法是作用在接收器（receiver）上的一个函数，接收器是某种类型的变量，因此方法是一种特殊类型的函数

***接收器类型不能式接口类型，也不能式指针类型。但可以是其他允许类型的指针***

- 方法不允许重载，一个接收器不能有多个同名方法
- 但基于多个接收器，是具有重载的。多个同名方法可以在多个不同的接收器上存在

### 添加方法

```go
type Bag struct {
    items []int
}
//(b*Bag) 表示接收器，即 Insert 作用的对象实例
func (b *Bag) Insert(itemid int) {
    b.items = append(b.items, itemid)
}
func main() {
    b := new(Bag)
    b.Insert(1001)
}
```

### 接收器

```go
func (接收器变量 接收器类型) 方法名(参数列表) (返回参数) {
    函数体
}
```

- 接收器变量：使用接收器类型名的第一个小写字母。例如，Socket 类型的接收器变量应该命名为 s，Connector 类型的接收器变量应该命名为 c 等。
- 接收器类型：接收器类型和参数类似，可以是指针类型和非指针类型
- 方法名、参数列表、返回参数：格式与函数定义一致

### 指针类型与非指针类型

- 指针接收器：指针类型的接收器由一个结构体的指针组成，更接近于面向对象中的this，由于指针的特性，调用方法时，修改接收器指针的任意成员变量，在方法结束后，修改都是有效的

- 非指针接收器：Go语言会在代码运行时将接收器的值复制一份。在非指针接收器的方法中可以获取接收器的成员值，但修改后无效

## 7.4内嵌

```go
type innerS struct {
    in1 int
    in2 int
}
type outerS struct {
    b int
    c float32
    int // 类型内嵌
    innerS //结构体内嵌
}
func main() {
    outer := new(outerS)
    outer.b = 6
    outer.c = 7.5
    outer.int = 60
    outer.in1 = 5
    outer.in2 = 10

    // 使用结构体字面量
    outer2 := outerS{6, 7.5, 60, innerS{5, 10}}
}
```

<font color='red'>在一个结构体中对于每一种数据类型只能有一个匿名字段</font>

***内嵌的结构体可以直接访问其成员变量，如ins.a.b.c可以直接写成ins.c***

## 7.5IO





# 8.接口

Go 语言的接口设计是非侵入式的，接口编写者无须知道接口被哪些类型实现。而接口实现者只需知道实现的是什么样子的接口，但无须指明实现哪一个接口。编译器知道最终编译时使用哪个类型实现哪个接口，或者接口应该由谁来实现。

## 8.1定义

```go
type 接口类型名 interface{
    方法名1( 参数列表1 ) 返回值列表1
    方法名2( 参数列表2 ) 返回值列表2
    …
}
```

- 接口类型名：使用 type 将接口定义为自定义的类型名。Go语言的接口在命名时，一般会在单词后面添加 er
- 方法名：当方法名首字母大写时，且接口类型名首字母也是大写时，这个方法可以被接口所在的包之外的代码访问
- 参数列表、返回值列表：参数列表和返回值列表中的参数变量名可以被忽略

```go
type Writer interface {
    Write(p []byte) (n int, err error)
}
```

该接口可以调用 `Write()` 方法写入一个字节数组`()[]byte)`，返回值告知写入字节数`(n int)`和可能发生的错误`(err error)`

## 8.2实现接口

:star:![](https://gitee.com/qiqibaba43/image/raw/master/202308230938766.png)

- 方法签名完全一致
- 实现所有的接口

## 8.3类型断言

类型断言（Type Assertion）是一个使用在接口值上的操作，用于检查接口类型变量所持有的值是否实现了期望的接口或者具体的类型

```go
value, ok := x.(T)
```

其中，x 表示一个接口的类型，T 表示一个具体的类型（也可为接口类型）

该断言表达式会返回 x 的值（也就是 value）和一个布尔值（也就是 ok），可根据该布尔值判断 x 是否为 T 类型：

- 如果 T 是具体某个类型，类型断言会检查 x 的动态类型是否等于具体类型 T。如果检查成功，类型断言返回的结果是 x 的动态值，其类型是 T
- 如果 T 是接口类型，类型断言会检查 x 的动态类型是否满足 T。如果检查成功，x 的动态值不会被提取，返回值是一个类型为 T 的接口值
- 无论 T 是什么类型，如果 x 是 nil 接口值，类型断言都会失败

# 9.并发

## 9.1简述

- 进程/线程

进程是程序在操作系统中的一次执行过程，系统进行资源分配和调度的一个独立单位。

线程是进程的一个执行实体，是 CPU 调度和分派的基本单位，它是比进程更小的能独立运行的基本单位。

一个进程可以创建和撤销多个线程，同一个进程中的多个线程之间可以并发执行。

- 并发/并行

多线程程序在单核心的 cpu 上运行，称为并发；多线程程序在多核心的 cpu 上运行，称为并行。

并发与并行并不相同，并发主要由切换时间片来实现“同时”运行，并行则是直接利用多核实现多线程的运行，Go程序可以设置使用核心数，以发挥多核计算机的能力。

- 协程/线程

协程：独立的栈空间，共享堆空间，调度由用户自己控制，本质上有点类似于用户级线程，这些用户级线程的调度也是自己实现的。

线程：一个线程上可以跑多个协程，协程是轻量级的线程。

### goroutine

非常轻量级的实现，可在单个进程里执行成千上万的并发任务

使用`go`关键词可以创建goroutine

```go
//go 关键字放在方法调用前新建一个 goroutine 并执行方法体
go GetThingDone(param1, param2);
//新建一个匿名方法并执行
go func(param1, param2) {
}(val1, val2)
//直接新建一个 goroutine 并在 goroutine 中执行代码块
go {
    //do someting...
}
```

<font color='red'>当主线程结束时，不论协程是否结束，该程序都结束</font>

## 9.2并发通信











## 9.3chan

一个 channels 是一个通信机制，它可以让一个 goroutine 通过它给另一个 goroutine 发送值信息。每个 channel 都有一个特殊的类型，也就是 channels 可发送数据的类型。一个可以发送 int 类型数据的 channel 一般写为 chan int。

```go
var 通道变量 chan 通道类型
通道实例 := make(chan 数据类型，容量)
```

### 发送数据

```go
package main
func main() {
    // 创建一个整型通道
    ch := make(chan int)
    // 尝试将0通过通道发送
    ch <- 0
}\
```

### 接收数据

```go
//阻塞接收数据
data := <-ch

//非阻塞接收数据
data, ok := <-ch
```



## 9.4单向通道

```go
var 通道实例 chan<- 元素类型    // 只能写入数据的通道
var 通道实例 <-chan 元素类型    // 只能读取数据的通道
```

关闭channel

```go
close(ch)
```





## 9.5有缓冲通道

```go
通道实例 := make(chan 通道类型,缓冲大小)
```

#### 为什么Go语言对通道要限制长度而不提供无限长度的通道？

我们知道通道（channel）是在两个 goroutine 间通信的桥梁。使用 goroutine 的代码必然有一方提供数据，一方消费数据。当提供数据一方的数据供给速度大于消费方的数据处理速度时，如果通道不限制长度，那么内存将不断膨胀直到应用崩溃。因此，限制通道的长度有利于约束数据提供方的供给速度，供给数据量必须在消费方处理量+通道长度的范围内，才能正常地处理数据。

## 9.6超时机制

```go
select {
    case <-chan1:
    // 如果chan1成功读到数据，则进行该case处理语句
    case chan2 <- 1:
    // 如果成功向chan2写入数据，则进行该case处理语句
    default:
    // 如果上面都没有成功，则进入default处理流程
}
```

## 9.7CSP

```go
package main
import (
    "fmt"
)
func main() {
    done := make(chan int)
    go func() {
        fmt.Println("C语言中文网")
        <-done
    }()
    done <- 1
}
```

后台线程`<-done `接收操作完成之后，main 线程的`done <- 1 `发送操作才可能完成（从而退出 main、退出程序），而此时打印工作已经完成了

# 10.反射







