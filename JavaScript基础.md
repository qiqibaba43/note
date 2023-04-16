[TOC]




# 1.语言特点

## 解释型

代码不需要手动编译，而是通过解释器一边编译一边执行。浏览器都集成了JS解释器。Node.JS也是JS引擎，使得JS可以直接在计算机中运行

## 函数式编程

可以向其他类型的值一样赋值给任意变量，也可以作为参数传递给其他函数

## 单线程

降低了JS代码的复杂度，在某些场景下使得JS性能变差，JS提供了异步编程方式，提高了代码的运行速度

## 面向对象

将相关功能统一封装到一个对象中，无需考虑实现细节

## 扩展ES

ECMScript定义最基本的语法。DOM，BOM可以通过JS操作网页和浏览器。NodeJS的fs模块直接操作计算机系统中的各种文件



****



# 2.Hello World

JS代码需要写在script中

`<scrpit>`

`alert("Hello World!")`//网页弹出警告框

`console.log('Hello World')`//控制台中输出

`document.write('Hello World')`//在网页中输出

`</script>`

- 可以直接编写在html的script中

- 也可以编写在一个外部XXX.js文件中，然后引入网页

`<script src="文件路径"></script>`

- 也可以写在指定的属性中

  `<button onclick="alert('hello world')">点击</button>`

  `<a href="javascript:alert(alert(hello));">点击</a>`



****



# 3.基本语法

声明变量 `let a; a=10;`     `var a;a='hello'；`

变量没有具体而理性，可以随意修改字面量

声明定义变量的时候，先在内存中查找是否有变量值，如果没有，则开辟一内存区域储存值；否则，就直接将内存值的地址赋值给变量

const声明常量，锁定的是地址值。

标识符命名：驼峰命名法  maxLength

类名命名：大驼峰命名法  MaxLength

常量命名：全部大写   MAXLENTH



****



# 4.数据类型

不同数据类型之间不可以运算，console.log(typeof a)会在控制台输出a的数据类型

## 1.数值&大整数

当数值超过一定范围后会显示近似值。Infinity是一个特殊的数值表示无穷。NaN表示非法的数值

二进制：0b    八进制：0o      十六进制：0x    

****

BigInt用来表示一些比较大的整数。数字范围以内存能表示的最大值。大整数以n结尾

## 2.字符串

​	用单引号或者双引号括起来，特殊符号需要用转义字符\表示。\n表示	换行 。let a=‘123’  let b=‘abc${a}’

​	b的值就是abc123

## 3.布尔值，空值，未定义，符号

​	布尔值 boolean有true和false两种值

​	空值 null，用typeof检查null的类型时，会返回object

​	未定义 undefined 当声明了一个变量却没有赋值的时候，值就是	undefined

​	符号 symbol 创建一个唯一的标识 `let a=Symbol()`

****

## 数据类型之间的转化

- 转字符串

  toString()与String()     String()可以将null和undefined转为字符串，而toString()不可以

  `a=a.toString(a)`       `a=String(a)`

- 转数值

  `a=Number(a)`

  如果字符串转数值不合法时候，结果是NaN

  如果是空串，转化为0;true转1，false转0

  null转0;undef转NaN

​		`a=parseInt(a)`  ***解析时，从左向右读取有效的整数，非法字符后面全部舍去***

​		`a=parseFloat(a)`转成浮点型

- 转布尔值

  0和NaN转false  其他都转true

  空串转false   其他都转true

  `a=" "  `空格也转true

  null和undefined转false

  

****

​				a??=100  当a的值为null或者undefined的时候，a赋值为100

​				a=a**2  表示a的二次方

****

- ==相等运算符比较的时候，两者类型不同，会先转化为相同类型（通常是数值）再比较

​				特例***null==undefined 返回true***

​				***NaN==NaN 返回false***

​				NaN不与任何值相等

- ===全等运算符**不会进行类型的自动转化**

- let声明的变量具有块作用域，在代码块外无法访问，而var不具有块作用域

- prompt用于获取用户输入的内容

  `let num=prompt("输入一个数")`

****

## 4.对象

创建对象 `let obj=new Object()`
给对象添加属性`obj.name="jone"`
删除对象属性`delete obj.name`
删除对象不存在的属性时，会返回`undefined`
属性名可以是任何值，当报错的时候，可以用中括号括起来，然后用引号引起来`obj[3a$%^]`

****



# 5.函数

函数也是一个对象，具有其他对象所有的功能，可以存储代码，调用代码

语法：`funtion 函数名(){代码块}`

调用函数：`函数名（）`

## 1.定义方式

- 函数声明：`function 函数声明([参数]){代码块}`

- 函数表达式： `const 函数名=function([参数]){代码块}`

- 箭头函数：`const 函数名=([参数])=>{代码块}`

  函数表达式和箭头函数都可以写成***匿名函数***的形式

  `function(){}`            `()=>{}`

## 2.参数

### 1.形参与实参

- 当实参多余形参，多余的实参省略
- 当实参小于形参，缺少的用undefined补全

### 2.对象实参

- 修改变量只会影响当前变量

- 如果有其他的变量指向该对象，那么所有指向该对象的变量都会受影响

- 对象可以作为实参传递，传递实参的时候，传递的是对象中存储的值

- ***函数每次调用都会创建新的默认值***

****

```js
function fun(a={name:"唐僧"}){
	console.log(a.name)
	a.name="悟空"
	console.log(a.name)
}
fun()
fun()
```

  输出：唐僧 悟空 唐僧 悟空  

****

```js
let obj={name:"唐僧"}
function fun(a=obj){
	console.log(a.name)
	a.name="悟空"
	console.log(a.name)
}
fun()
fun()
```

  输出：唐僧 悟空 悟空 悟空  

***因为是对同一个对象操作的，所以会对obj的字面量进行修改***

****

### 3.函数参数

```js
function(a){
	console.log(a)
}
fun(()=>console("我是一个箭头函数"))
```

输出：我是一个箭头函数

## 3.函数返回值

箭头函数的返回值可以直接写在箭头后面

`const sum=(a,b)=>a+b`

如果在箭头函数后面设置对象的字面量作为返回值的时候，对面的字面量必须用( )括起来，防止与代码块的{  }混淆

`const fun()=>({name:"任侠"})`

## 4.对象的方法

```
let obj={}
obj.sum=function(a+b){
	console.log(a+b)
}
```

调用obj的sum函数：`obj.sum(1,2)`

## 5.window对象

window对象表示浏览器的窗口，可以对浏览器窗口进行操作，除此以外，window对象存储JS中的内置对象和浏览器的宿主对象

向window对象中添加的属性，方法会自动变成***全局变量***

当window对象中变量和let声明变量同名时，会优先使用全局变量

## 6.提升

为了更加合理的使用内存存储变量

- 变量的提升

使用***var***声明的变量，会在所有代码执行前被***声明***

```
console.log(a)
var a=10
```

输出：undefined           因为a只是被申明，还没有被赋值，当执行完`console.log(a)`后才执行赋值操作`a=10`

相当于：

```js
var a
console.log(a)
a=10
```

****

- 函数的提升

只有以function开头声明的函数才会提升 `function fun(){}`会提升；而`var fun=function(){}`不会提升

***let声明也会提升，但在赋值前禁止访问***

## 7.立即执行函数

当使用var声明变量的时候，因为var没有局部变量，所以名称相同的变量会相互干扰。可以通过函数来限制var的作用域范围

```js
(function(){
    var a=10
    console.log(a)
})()；
```

使用立即执行函数可以用来创建一个一次性的函数作用域

在使用立即执行函数的时候，最好在后面加分号；整体加括号，防止函数被提升

## 8.this函数

- 以方法形式调用，返回当前调用方法的对象
- 以函数形式调用，返回的是window

***箭头函数没有自己的this，它的this有外层的作用域决定，与箭头函数的调用方法无关***

# 6.面向对象

```js
//类名一般用大驼峰命名法
class Person{
    name
    age
    static height=178  //静态属性只能通过类访问
	getName(){
        console.log(this.name)
    }
}
//创建对象
const peron=new Person()
console.log(Person.height)
person.getName()
```

检查对象是否由某个类创建

`person instanceof Person`

## 1.构造函数

```js
class Person{
    name
    age
    constructor(name,age){
        console.log("构造函数被调用了")
        this.name=name
        this.age=age
    }
}
const person=new Person("唐僧"，18)
```

`this.name`表示当前创建对象的name属性

## 2.封装

属性使用#开头具有私有属性，私有属性只能在类内部访问

```js
class Person{
    #name="唐僧"
    getName(){
        return this.#name
    }  
    setName(name){
        this.#name=name
    }
}
const p1=new Person()
console.log(getName())
p1.setName("沙僧")
```

其他写法：

```js
class Person{
    #name
    get name(){
        retrun this.#name
    }
}
const p1=new Person()
console.log(p1.name)
```

## 3.继承

使用关键字extents

子类通过使用同名方法重写父类

***构造函数的重写，必须要写`super()`用来调用父类的构造函数***

```js
class Animal{
    name
    constructor(name){
        this.name=name
    }
    say(){
        console.log("动物在叫")
    }
}
class Dog extents Animal{
    age
    constructor(name,age){
        super(name)
        this.age=age
    }
    say(){
        super.say()
        //调用父类的同名方法
        console.log("汪汪汪")
    }
}
```

## 4.对象的内存结构

- 属性存储在对象自身：

  直接通过对象添加的属性 

  构造器中x=y添加的属性

- 原型对象`prototype`

  对象中的一个属性`__proto__`存储原型对象

***优先查找对象自身的属性，然后才查找原型对象***

****

## 5.原型

添加到原型对象中的方法：

- 在类中通过`方法名（）{}`添加的方法
- 主动向原型中添加的属性或方法

`console.log(对象名.__proto__)`

`console.log(Object.getPrototypeOf(对象名))`获得原型对象的内容

原型对象中的内容：1.构造函数  2.对象的属性和方法

原型可能也有原型，对象越复杂，原型越多。最后是`null`

***原型相当于一个公共区域，类实例化的每一个对象都可以访问，节约空间***

***JS通过原型实现继承，子类的原型相当于父类的实例***

## 6.原型的修改

```js
class Person{
    
}
const p1=new Person()
p1.__proto__say=()=>{}
//通过类的实例修改原型
p1.__protp=new Dog()
//给对象的原型直接赋一个新的原型值，不会影响其他实例
Person.prototype.say=()=>{}
//通过类的prototype属性修改原型
```

## 7.instanceof与hasOwn

instanceof检查对象的原型链上是否有该类  `console.log(子类 instanceof 父类)`

hasOwn通过实例对象对用，检查对象自身含有某个属性   `Object.hasOwn(对象，属性名)`

in检查属性是否存在，不论是在对象自身还是原型中 `console.log(属性名 in 对象)`

## 8.new

```js
function myNew () {
	//创建一个新对象
	var obj = new Object ();
	//取出参数中的第一个参数，获得构造函数
	var constructor = Array.prototype.shift.call(arguments);
	//连接原型，新对象可以访问原型中的属性
	obj._proto_ = constructor.prototype;
	// 执行构造函数，即绑定 this，并且为这个新对象添加属性
	var result = constructor.apply(obj,arguments);
	return typeof result === "object" ? result :obj ;
}
```

# 7.数组

不存在的元素返回`undefined	`，可以不连续定义数组

## 1.遍历

`for(变量 of 数组)`

`for(变量 in 数组)`

## 2.常见方法

- `at()`

  根据索引值获取元素，索引可以是负数。-1表示倒数第一个元素，以此类推

- `concat()`

  将两个数组拼接到一起

- `indexOf()`

  获取元素在数组中第一次出现的下标

- `join()`

  将所有元素拼接到一起，默认使用逗号隔开

  ```js
  arr.join("")//中间没有链连接符号
  ```

- `slice()`

  截取数组的一部分 前闭后开

  只有一个值，从该下表开始到最后

  空值，对数组进行***浅拷贝***
  
- `structuredClone(数组)`

  常用于深拷贝


****

```js
const arr2=arr1
//直接使用赋值语句，两个数组实际上是指向同一对象的
const arr2=arr1.scile()
//将arr1所有元素都切到arr2，是创建了一个新的数组，两者是不同的对象
```

****

- `push(元素)`

  向数组末尾添加元素，返回数组的长度

- `pop()`

  删除并返回数组的最后一个元素

- `unshift()`

  向元素开头添加元素，返回数组的长度

- `shift()`

  删除并返回数组第一个元素

- `splice()`

  参数分别是：删除的起始位置，删除的个数，要插入的元素

  返回被删除的元素

- `reverse()`

  反转数组


****

## 3.深拷贝与浅拷贝

浅拷贝只复制指向某个对象的指针，而不复制对象本身，新旧对象还是共享同一块内存

浅拷贝是按位拷贝对象，它会创建一个新对象，这个对象有着原始对象属性值的一份精确拷贝
如果属性是基本类型，拷贝的就是基本类型的值；如果属性是内存地址（引用类型），拷贝的就是内存地址 ，因此如果其中一个对象改变了这个地址，就会影响到另一个对象

****

深拷贝会另外创造一个一模一样的对象，新对象跟原对象不共享内存，修改新对象不会改到原对象，是“值”而不是“引用”（不是分支）

拷贝第一层级的对象属性或数组元素
递归拷贝所有层级的对象属性和数组元素
深拷贝会拷贝所有的属性,并拷贝属性指向的动态分配的内存。当对象和它所引用的对象一起拷贝时即发生深拷贝。深拷贝相比于浅拷贝速度较慢并且花销较大

## 4.复制

- `const obj1=Object.assign({},obj)`

  没有的属性会补全，同名属性会覆盖

# 8.高阶函数

## 回调函数（callback）

将一个函数作为参数传递，就将这个函数成为回调函数

## 1.高阶函数

一个函数的参数或者返回值是函数，则这个函数就成为高阶函数

作用：向另一个函数的内部动态传递代码

```js
function filter(arr,cb){
    for(int i=0;i<arr.length;i++){
        if(cb(arr[i])){
            newArr.push(arr[i])
        }
    }
    return newArr
}
function fn(a){
    return a.age>18
}
let result=filter(arr,fn(a))
let result=filter(arr,a=>a.age>18)
```

动态生成一个新的函数

```js
function somefn(){
    return "hello"
}
function outer(cb){
    const result=cb()
	return result
}
let ans=outer(somefn)
```

## 2.闭包

```js
function outer(){
    let num=0
    return ()=>{
        num++
        coonsole.log(num)
    }
}
const fn=outer()
```

闭包就是能访问到外部函数作用域中变量的函数

构成闭包的条件

- 函数的嵌套
- 内部函数要引用外部函数中的变量
- 内部函数作为外部函数的返回值返回

****

函数作用域在函创建的时候就确定，***与调用的位置无关***

```js
let a=1
function f1(){
	cnsole.log(a)
}
function f2(){
    let a=2
    f1()
}
f2()
输出 2
```

****

## 3.闭包的生命周期

闭包在外部函数调用时产生，外部函数灭磁带哦用都会产生一个全新的闭包***其中的内部变量都是相互独立的***

内部函数被垃圾回收，闭包才会消失

## 4.高阶函数的应用

- `sort()`

​			对数组进行排序，***默认按照Unicode编码进行排序***

​		`arr.sort((a,b)=>a-b)`升序排列

​		`arr.srot((a,b)=>b-a)`降序排列

- `forEach()`

  用于遍历数组

  需要一个回调函数作为参数传递，数组有多少个元素，回调函数就会调用几次

  回调函数的三个参数：element 遍历时的当前元素  index 当前元素的下表 array 当前遍历的数组

- `filter()`

  将数组中符合条件的元素保存到一个新的数组中，然后返回

  需要一个回调函数作为参数，每个元素都会调用回调函数，根据返回值添加

  `let result=arr.filter(elemrnt=>elemrnt>5)`

- `map()`

  与`filter()`类似，生成一个新的数组

  `result=arr.map(element=>"li"+element+"li")`

- `reduce()`

  需要一个回调函数作为参数 ，数组的第一个元素为a，第二个元素为b，return的值作为第二次调用的a，然后第三个元素作为b

  ```js
  result=arr.reduce((a,b)=>{
      console.log(a,b)
      return a+b
  })
  ```

  也可以指定第二个参数作为初始值，第一次调用的a为初始值，b为第一个元素

## 5.可变参数

函数的隐含参数 arguments，也是一个类数组对象（伪数组）

arguments用来存储函数的实参，无论是否定义形参

***类数组不能使用数组的方法***

```js
function sum(){
    let result=0
    for(let num of arguments){
        result+=num
    }
    return result
}
实现任意个数字的相加
```

在定义函数时，将函数的参数指定为可变参数，可以接受任意数量的实参，并将他们储存到一个数组中返回

```javascript
function fn(...args){
    console.log(args)
}
```

可变参数可以与普通参数一起使用，必须将可变参数写到最后0

## 6.call与apply

函数不仅可以通过 `函数 （）` 这种方法调用，也可以通过函数的`call（）`方法和`apply()`方法来调用函数

***call和apply的第一个参数，指定函数的this对象。***

**call的实参直接写在this对象的后面**`fn.call(obj,"hello","world")`

***apply的实参需要通过一个数组传递***

`fn.apply(obj,["hello","world"])`

## 7.bind

用于创建一个新的函数，与原函数的功能一样，指定this对象，并且锁死，***无法修改***。

也可以绑定参数

```js
function fn(){}
let obj={name:"任侠"}
const fn()={obj，10}
//第一个参数绑定为10
```

***箭头函数没有自身的this，由作用域决定，call、apply和bind不能修改***

***箭头函数也没有arguments***

****

# 9.内建对象

## 1.数组的解构

变量多，没有对应的默认为undefined

变量少，多余的实参直接舍弃

```js
let [a,b,c,d]=[1,2,3]
//a=1,b=2,c=3,d=undefined
//可以给变量指定一个默认值
let [a,b,c,d=4]
```

可以使用`...n`获取多余的元素存储在数组中

****

快速交换两个变量值

```js
[a,b]=[b,a]
等号左边是要解构赋值的变量，等号右边相当于新建了一个数组，将b，a两个字面量赋给数组
```

## 2.对象的解构

```js
let obj={name:"任侠",age:18}
let {name,age}=obj
//在变量声明的同时进行解构
let {name:a,age:b}=obj
给name，age起别名，那么a="任侠"，b=18
```

## 3.对象的序列化

JS中的对象使用都是存储在计算机的内存中，序列化指将对象转化为一个可以存储的格式

在JS中序列化通常指将一个对象转化为字符串

作用：***通过字符串进行读写操作，使得JS对象可以在不同的语言之间传递,编写配置文件***

使用工具类 （静态方法）`JSON(JavaScript Object  Notation)`,转换后的字符串称为JSON字符串

将对象转字符串`const str=JSON.stringify(obj)`

将字符串转对象`const obj=JSON.parse(str)`

***两个对象是不同的对象，相当于对原对象的深拷贝***

### JSON的手动编写

- JSON对象  `[]`

  `JSON.pares('["hello",true]')`

- JSON数组  `{}`

  `JSON.pares('{"name":"任侠","age":18}')`

***外边必须使用单引号引起来，而属性名必须使用双引号引起来***

可以使用的***属性值***：数字，字符串（用单引号引起来），布尔值，数组，空值，对象

## 4.Map

用于存储键值对解构的数据`(key-value)`

与object的区别：object中的属性名只能是字符串或者符号，map中key可以是任何数据类型

- `set(key，value)` 插入键值对

- `get(key)` 获取key对应的value

- `delete(key)` 删除key对应的键值对
- `has(key)`  检查是否有key对应的键值对

`const arr=Array.from(map)   const arr=[...map]`将map转成一个二维数组

`const map=new Map([["name","renxai"],["age",18]，[{},()=>{}]])`通过二维数组构建一个map

```javascript
遍历map
for(const entry of map){
    const [key,value]=entry
    console.log(key,value)
}
```
## 5.Set

功能与数组类似，但只能存储不同的元素

- `has()`
- `add()`
- `delete()`
- `size()`

set与map的本质一样，但key与value都一样

## 6.Math

map是一个工具类，***不能通过new创建一个对象***

- `Math.floor()`          向下取整
- `Math.ceil()`             向上取整
- `Math.round()`           四舍五入
- `Math.trunc()`           舍去小数

`Math.random()` 返回一个0到1之间的伪随机数，***包括0不包括1***

## 7.Date

`let date=new Date()`创建当前时间的对象

也可以在Date（）的构造函数中传递一个表示时间的字符串`date=new Date("2023-2-13T20:00:00")`

也可以`date=new Date(2023,01,13)`表示2023年2越13日

`date=new Date(2023)`表示时间戳2023毫秒的***格林威治时间***，然后再转化为中国标准时间

- `getFullYear()`返回四位数的年份
- `getMonth（）`返回月份的下标。返回值的范围是0到11。返回值为5，表示六月

- `getDate()`返回日期
- `geyDay()`返回值的范围0到6。返回0表示周日

- `getTime()`获取到时间戳。1970年1月1日0时0分0秒到当前时间的毫秒

日期的格式化：

- `toLoctionDateString()`显示日期

- `toLoctionTimeString()`显示时间

- `toLoctionString()`           显示日期和时间

  可选参数：

  第一个参数：描述语言和地区的字符串“zh-CN”中文中国    “zh-HK”中文香港    “en-US”英文美国

  第二个参数：显示日期和时间的格式的对象   `{dataStyle:"full",timeStyle:"full"}`     full，long,medium,short 

​			十二小时制	`{hour12:true}`

## 8.包装类

通过`new String()`创建一个String类型的对象***不能使用***

包装类一共有5个`String,Number,Boolean,BigInt,Symbol`

***通过包装类将一个原始值包装为对应的对象，当我们给一个原始值调用方法或属性的时候，JS解释器会自动将该原始值包装为对应的对象，然后给该对象添加方法或属性***

```javascript
let str="hello"
str.name="哈哈"
console.log(str.name)
```

***第一个给str添加name属性时创建的对象与第二次读取str的name属性时创建的对象不一样，所以会输出undefined***

## 9.字符串

字符串本质是一个数组，***是不可变类型***

- `charAt() `      返回下标对应的元素
- `concat()`      拼接
- `includes()`第一个参数 查找的字符串  第二个参数  查找的起始位置
- `split()`        第一个参数  分割的字符
- `toLowerCase()`  转小写
- `toUperCase()`     转大写
- `trim()`                      去除字符串前后空格
- `trimStart()`         去除开始的空格
- `trimEnd() `               去除结束的空格

# 10.正则表达式

正则表达式用于创建一共规则。检查一个字符串是否符合规则或者将字符串中符合规则的内容提取出来

## 1.创建表达式

`let reg=new RegExp("a","i")`创建一个正则表示式的对象

第一个参数  正则表达式        第二个参数  匹配模式

也可以通过字面量创建正则表达式 `reg=/a/i`

## 2.基本语法

在正则表达式中大部分字符都可以直接写

- `[] `       		  表示字符集                   `[a-z]`表示任意的小写字母
- `[^a-z]`      表示除了a到z的所有字符
- `.`                   ***表示除换行符以外的字符***

- `\w`                表示字母，下划线和数字
- `\W`                表示除了字母，下划线和数字
- `\d`                表示数字
- `\D`                表示除了数字

特殊字符

- `^ `                     匹配开头的字符
- `$`                     匹配结尾的字符
- `| `                     表示或

限定词 （只对前面的***一个字符***生效）

- `{n}`                 正好n个                         `ab{3}` 表示b匹配了3次
- `{n,}`              至少n个
- `{n,m}`           最少n个最多m个
- `*`                      匹配零个或多个          `/zo*`表示匹配z，zo，zoo等
- `+`                      匹配一个或多个          `/zo+`表示匹配zo，zoo等
- `?`                      匹配零个或一共           `/z(oo)?`表示匹配z，zoo

匹配模式

- `i`                      忽略大小写
- `g`                      全局匹配（默认情况下是只匹配一个）

## 3.常用方法

- `test() `        检查是否符合正则表达式，符合返回true
- `exec()`        返回一个数组，元素是符合正则表达式的字符串

## 4.字符串的正则方法

- `split()`     根据正则表达式对字符串进行拆分

`let result=str.split(/a[bd]c/)`      表示以abc或者adc进行拆分

- `search()`   根据正则表达式获取字符串
- `replace()`根据正则表达式替换对应的字符串

`str.replace(/a[bd]c/g,123)`       将所有的abc和adc替换成123     

- `match()`     与`search()`类似，但会一次性返回所有符合正则的字符串。而`search()`会一个一个返回
- `macthAll()`返回一个迭代器



# 11.DOM（文档对象模型）

浏览器提供一个document对象，他是一个全局变量可以直接使用

## 1.hello world

```javascript
<button id="btn">点我一下</button>
const btn=document.geyElementById("btn")
btn.innerText="Click Me"
```
## 2.节点
### 1.文档节点

document对象的原型链：

`HTMLDocument->Document->Node->EventTarget->Object.prototype->null`

- 凡是在原型链上存在的对现象的属性和方法都可以通过Document去调用

部分属性：

- `document.documentElement`               html跟元素
- `document.head`                                      head元素
- `document.title`                                    title元素
- `document.body`                                      body元素
- `document.links`                                    获取网页内所有的超链接

### 2.元素节点

根据document获取已有的节点元素：

- `document.getElementsById()`根据id获取一个元素节点对象
- `document.getElementsByClassName()`根据class的属性值获取有***一组***元素节点的对象。返回值是一个***类数组对象***。该对象是一个实时更新的集合，当网页内容变化时，类数组对象也会立即变化

- `document.getElementsByTagName()`根据标签名获取节点元素对象。与`getElementsByClassName()`类似。`document.getElementsByTagName(*)`获取到页面所有元素节点

- `document.getElementsByName()`根据name获取一组元素节点，主要用于表单项
- `document.querySelectorAll()`根据选择器查询元素，返回的是类数组，不会更新。`document.querySelector()`只会返回一个

通过document创建元素节点：

`document.creatElement()`根据参数名创建元素节点对象，***没有插入到网页内***

div元素节点的原型链：

`div->HTMLDivElement->HTMLElement->Element->Node->EventTarget->Object.prototype->null`

通过元素系欸但那对象获取其他节点：

- `element.childNodes()`获取当前元素的所有***子节点***，包括空白的子节点，文本节点
- `element.children()`获取当前元素的子元素

- `element.firstElementChild()`获取当前第一个子元素
- `elemnet.lastElementChild()`获取当前元素最后一个子元素
- `element.nextElementSibling()`获取当前元素的下一个兄弟节点
- `element.previousElementSibling()`获取当前元素的前一个兄弟元素

- `element.parentElement()`获取当前元素的父元素

### 3.文本节点

在DOM中，网页中所有的文本内容都是文本节点

- `element.textConetnt`获取或修改元素中的文本内容。不考虑css的样式可以获取空格，换行，不可以获取标签
- `element.innerText`获取或修改元素中的文本内容，考虑css的样式，***触发网页的重排***，不可以获取空格，换行，标签。自动对标签进行转义，添加的标签会作为文本加入
- `element.innerHTML`获取或修改元素中的html代码，可以获取标签，空格，换行。可以直接向元素中添加html代码。***插入内容时，有被xss注入的风险***

### 4.属性节点（Attr）

- 属性名

  `元素.属性名`class属性需要用`className`读取***当读取一个布尔值的时候，会返回true或false***

- 方法
  - `getAttribute(属性名)`：读取属性
  - `setAttribute(属性名，属性值)`：修改属性
  - `removeAttribute()属性名`：删除属性

## 3.事件

为事件绑定响应函数（回调函数），完成与用户之间的交互

绑定响应函数：

- 直接在元素的属性中设置

  `<button>onclick="alert(你干嘛~)"</button>`

- 通过元素的指定属性设置回调函数

  新的绑定函数会覆盖旧的绑定函数
  
  ```javascript
  const btn=document.getElementById("btn")
  btn.onclick=function(){
      alter("欸呦~")
  }
  ```
  
- 通过元素`addEventListener()`方法绑定事件

  可以绑定多个绑定函数，依次执行

  `btn.addEventListener("click",function(){alter ("hello")})`

### 1.文档加载

JS代码在执行时，网页还没加载完毕，会出现无法获取DOM对象的情况

- 将代码编写到window.onload的回调函数中

  ***window.onload事件会在窗口中的内容加载完毕后才会触发***

```javascript
//window.onload事件会在窗口中的内容加载完毕后才会触发
window.onload=function(){
    
}
```

- 将代码编写达到`document`对象的`DOMContentLoaded`中

  `DOMContentLoaded事件会在文档中的内容加载完毕后才会触发`

```javascript
document.addElementListener("DOMContentLoaded",function(){
    
})
```

- 编写到外部的JS文件中，以`defer`的形式引入

  `<scrpit defer src=".scrpit.js"></script>`

### 2.元素操作

#### 1.添加元素

`creatElement()`		

参数：标签名			根据标签名创建一个节点

将节点添加到网页内`appendChild()`给一个子节点添加子节点

`appendChild()`只能固定添加到当前节点的末尾

:star:`insertAdjacentElement()`

参数：

- 第一个参数 “beforeend”（插入到结束标签之前）

  ​						“afterbegin”（插入到开始标签之后）

  ​						“beforebegin”（插入到当前元素的前面）

  ​						“afterend”（插入到当前元素的后面）

- 第二个参数      待插入的节点

添加网页元素   `insertAdjacentHTML()`

添加文本元素  `insertAdjacentText()`

#### 2.替换元素

`replaceWith()`		用参数代替

#### 3.删除元素

`remove()`			删除当前元素

****

`return false`取消默认行为，$\textcolor{red}{只能取消使用{xxx.function()这种绑定的事件中才适用}}$

也可以使用`href="javascript:;"`将超链接跳转停止

删除元素的父元素，可以使用`parentNode`获取父元素

在删除之前跳出弹窗，询问是否删除，可以使用`confirm(内容)`有确定和取消按钮，防止误删

```js
let flag=confirm("确认删除吗")
if(flag){
    tr.remove()
}
```

#### 4.节点复制

常规使用`appendChild()`，会将源节点，移动到目标节点的位置。不能做到复制的效果。使用`cloneNode()`，创建一个副本，返回一个新对象

***使用`cloneNode()`复制时，会复制所有属性，只会复制当前节点，而不会复制节点的子节点***

参数：true		表示对子节点进行复制。使用默认值false时，子节点不会复制

### 3.修改CSS样式

#### 1.修改

通过添加内联样式进行修改

```javascript
btn.onclick=function(){
    //元素.style.样式名=样式值
    box.style.width="400px"
}
```

$\textcolor{red}{如果样式名中有-符号，则需要将样式名修改为驼峰命名法}$，在JavaScript中，-号被会识别为两个属性相减。

例子：`background-color`需要修改成`backgroundColor`

当CSS样式设置`！important`的时候，JavaScript就不能修改了

#### 2.读取

- `元素名.style.样式名`

  某些元素可能没有设置内联样式，读取不到。设置的内联样式可能被`style`标签内重新设置的样式覆盖，读取不到真正的样式值

- `getComputedStyle()`

  返回一个对象，该对象会返回当前元素所有生效的样式

```javascript
const styleObj=getComputedStyle();
console.log(styleObj.width);
返回当前元素的宽度
```

同样的，样式名中含有“-”的时候，需要改成驼峰命名法

参数：

- 要获取样式的对象
- 要获取的伪元素

获取的元素样式值是带单位的，需要用`paseInt()`取整，去掉单位。参数元素样式值。将值再作为样式值传入的时候，***需要给其设置单位***

如：`parseInt(styleObj.width())+100+"px"`

#### 3.通过属性读取

- `元素.clientHeight()`获取元素内部的宽度（包括内容区和内边距）

- `元素.offsetHeight()`获取元素的可见框的大小（包括内容区，内边距和边框）
- `元素.scrollHeight()`获取元素滚动区域的大小
- `元素.offsetParent()`获取当前元素的定位父元素

- `元素.offsetTop()`获取元素相对于定位父元素的举例

### 4.通过class修改CSS

`box1.className="box2"`相当于将box1的属性名改为box2。使用`box1.className+=" box2"`将box2的样式应用到box1中

`元素.classList`是一个对象，对象中提供了当前元素的各种属性方法。`box1.classList.add("box2")`

`class.List`的方法:

- `classList.add()`                      添加类名
- `classList.remove()`	           删除类名			
- `classList.toggle()`               切换

切换——如果有box1的属性名，那就删除，如果没有的话，就添加

- `classList.replace()`              替换，用第二个参数的属性名替换第一个参数的属性名
- `classList.content()`               检查，检验当前元素是否含有该参数

## 4.事件对象

### 1.事件对象

事件对象，是事件被触发时由浏览器创建的一个对象。该对象封装了事件相关的各种信息。

在创建事件对象后，会将事件对象作为一个响应函数的参数传递，可以在事件的回调函数中定义一个形参接受事件对象

```javascript
box.addEventListener("mousemove",event=>{
    console.log(event);
    //打印事件详细信息     
    console.log(event.clientX,event.clientY);
    //打印鼠标所处位置的x轴，y轴
})
```

### 2.Event对象

常见的属性：

- `event.target`                触发事件的对象

****

:star:`event.target`与`this`的区别

`this`                   绑定事件的对象

事件的冒泡：当元素上的某个元素被触发后，祖先元素也会同时触发该事件。可以减少重复代码的书写。

$\textcolor{red}{事件的冒泡与位置无关，只与结构有关}$

取消冒泡：`event.stopPropagation()`在触发事件的事件对象回调函数中使用

当发生事件的冒泡后，this的对象会逐级向上传递，然后改变。然而event.target

****

- `event.currentTarget`             相当于`this`

- `event.preventDefault()`

  当给超链接设置点击响应函数，又不需要进行网页的跳转。可以，而`retrun false`只能取消`xxx.function(){}`这种形式的默认行为。`event.preventDefault`都适用

### 3.事件的委派

将本该绑定给多个元素的事件，可以利用冒泡，统一绑定给document，有效降低代码的复杂度

给现有的元素节点绑定事件，后再添加元素节点，不会绑定对应的事件。需要重复进行绑定操作

可以统一绑定在document中，再使用if条件语句进行判断，如果是符合要求的元素节点触发该事件，就执行该函数，否则不执行

### 4.事件的捕获

事件的传播分为三个阶段：

- 捕获阶段
- 目标阶段
- 冒泡阶段

事件的的捕获：事件从外向内的传导，当前元素触发事件后，会***从当前元素最大的祖先元素开始***，向目标元素，进行事件的捕获

默认情况下，事件不会在捕获阶段触发事件

如果希望在捕获阶段触发事件，可以将`addEvementListener`的第三个参数设置为true

```javascript
box.addEventListener("click",event=>{
    alter(“被执行”)
},true)
```

设置完后，事件的触发顺序就变成了最大的祖先元素开始到触发事件的元素

`eventPhase`可以查看事件触发的阶段

# 12.BOM（浏览器对象模型）

BOM提供了一组对象，通过对象可以完成对浏览器的各种操作

对象：

- Window —— 代表浏览器窗口（全局对象）
- Navigator —— 浏览器的对象（识别浏览器）
- Location —— 浏览器的地址栏信息
- History —— 浏览器的历史记录（控制浏览器的前进后退）
- Screen —— 屏幕的信息

BOM对象是作为window对象属性保存，所以可以直接在JS中访问这些对象

## 1.Navgate对象

## 2.History对象

## 3.Location对象

## 4.定时器

通过定时器，是的代码在指定时间后执行

`setTimeout()`设置定时器

第一个 参数：回调函数，指定时间后，需要执行的函数

第二个参数：间隔时间，单位毫秒

`clearTimeout()`关闭定时器   参数，定时器的变量名

`setInterval()`设置一个重复执行的定时器   语法与`setTimeout()`一样

`clearInterval()`关闭定时器
