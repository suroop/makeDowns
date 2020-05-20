# JSON

## JSON简介

> 概念

JSON: **J**ava**S**cript **O**bject **N**otation(JavaScript 对象表示法)

JSON 是存储和交换文本信息的语法。类似 XML



> 特点

JSON 语法是轻量级的文本数据交换格式

JSON 独立于语言：JSON 使用 Javascript语法来描述数据对象，但是 JSON 仍然独立于语言和平台。JSON 解析器和 JSON 库支持许多不同的编程语言。 目前非常多的动态（PHP，JSP，.NET）编程语言都支持JSON

JSON 具有自我描述性，更易理解



> 实例

```json
{
    "sites": [ 
    { "name":"google" , "url":"www.google.com" }, 
    { "name":"baidu" , "url":"www.baidu.com" }
    ]
}
```

这个 sites 对象是包含 2个站点记录（对象）的数组



> 区别

+ 与XML相同
  + JSON 是纯文本
  + JSON 具有"自我描述性"（人类可读）
  + JSON 具有层级结构（值中存在值）
  + JSON 可通过 JavaScript 进行解析
  + JSON 数据可使用 AJAX 进行传输
+ 与XML不同
  + 没有结束标签
  + 更短
  + 能够使用内建的 JavaScript eval() 方法进行解析
  + 使用数组
  + 不使用保留字



> 优点

JSON 比 XML 更小、更快，更易解析

+ 使用XML
  + 读取 XML 文档
  + 使用 XML DOM 来循环遍历文档
  + 读取值并存储在变量中
+ 使用JSON
  + 读取 JSON 字符串
  + 用eval()处理JSON 字符串

## JSON语法

> 语法

JSON 语法是 JavaScript 对象表示语法的子集

+ 数据在名称/值对中
+ 数据由逗号分隔
+ 大括号保存对象
+ 中括号保存数组



> 书写格式

JSON 数据的书写格式是：名称/值对

名称/值对包括字段名称（在双引号中），后面写一个冒号，然后是值

```
"name":"张三"
```

等价于jS的

```
name="张三"
```



> JSON数字

JSON 数字可以是整型或者浮点型

```
{"num":15}
```



> JSON字符串

JSON字符串可以双引号或单引号包裹

```
{"name":"张三"}
```



> JSON值

JSON 值可以是

- 数字（整数或浮点数）
- 字符串（在双引号中）
- 逻辑值（true 或 false）
- 数组（在中括号中）
- 对象（在大括号中）
- null

> JSON对象

JSON 对象在大括号（{}）中书写

对象可以包含多个名称/值对

```
{name:"张三","age":35,"sex":"male"}
```

等价于JS的

```
name="张三"
age=35
sex="male"
```



> JSON数组

JSON 数组在中括号中书写

数组可包含多个对象

```json
{
"sites": [
	{ "name":"google" , "url":"www.google.com" }, 
	{ "name":"微博" , "url":"www.weibo.com" }
]
}
```

> JOSN null

JSON 可以设置 null 值

```josn
{"thing":null}
```



> JSON文件

- JSON 文件的文件类型是 ".json"
- JSON 文本的 MIME 类型是 "application/json"

## JSON & XML

JSON 和 XML 都用于接收 web 服务端的数据

JSON 和 XML在写法上有所不同

> JSON

```json
{
    "sites": [ 
    { "name":"google" , "url":"www.google.com" }, 
    { "name":"weibo" , "url":"www.weibo.com" }
    ]
}
```



> XML

```xml
<sites>
  <site>
    <name>google</name> <url>www.google.com</url>
  </site>
  <site>
    <name>weibo</name> <url>www.weibo.com</url>
  </site>
</sites>
```



> 共同点

- SON 和 XML 数据都是 "自我描述" ，都易于理解。
- JSON 和 XML 数据都是有层次的结构
- JSON 和 XML 数据可以被大多数编程语言使用



> 不同点

- JSON 不需要结束标签
- JSON 更加简短
- JSON 读写速度更快
- JSON 可以使用数组
- XML 需要使用 XML 解析器来解析，JSON 可以使用标准的 JavaScript 函数来解析



> 优势

XML 比 JSON 更难解析。

JSON 可以直接使用现有的 JavaScript 对象解析。

针对 AJAX 应用，JSON 比 XML 数据加载更快，而且更简单

+ 使用 XML
  + 获取 XML 文档
  + 使用 XML DOM 迭代循环文档
  + 接数据解析出来复制给变量

+ 使用 JSON
  + 获取 JSON 字符串
  + JSON.Parse 解析 JSON 字符串



## JSON对象

> 实例

```json
{"name":"张三","age":15}
```



> 使用

JSON 对象使用在大括号({})中书写。

对象可以包含多个 **key/value（键/值）**对。

key 必须是字符串，value 可以是合法的 JSON 数据类型（字符串, 数字, 对象, 数组, 布尔值或 null）。

key 和 value 中使用冒号(:)分割。

每个 key/value 对使用逗号(,)分割



> 访问对象值

+ 使用点号（.）来访问对象的值

```js
var Person={"name":"张三","age":15};
var name=Person.name;
```

+ 使用中括号（[]）来访问对象的值

```js
var Person={"name":"张三","age":15};
var name=Person["name"];
```



> 循环对象

使用for in 循环对象的属性

```js
var Person={"name":"张三","age":15};
for (property in Person){
    document.getElementById("title").innerHTML +=property;
    //document.getElementById("title").innerHTML +=Person[property];
}
```



> 镶嵌对象

```js
var Persons={
	"刘能":{
		"age":35
	},
	"张三":{
		"age":30
	}
}
```

使用点号(.)或者中括号([])来访问嵌套的 JSON 对象

```js
var Persons={
	"刘能":{
		"age":35
	},
	"张三":{
		"age":30
	}
}
console.log(Person."刘能".age);
console.log(Person."张三".["age"]);
```



> 修改值

+ 使用点号(.)来修改 JSON 对象的值

```js
var Person={"name":"张三","age":15};
Person.name="刘能";
```



+ 使用中括号([])来修改 JSON 对象的值

```js
var Person={"name":"张三","age":15};
Person.["name"]="刘能";
```



> 删除属性

使用 **delete** 关键字来删除 JSON 对象的属性

```js
var Person={"name":"张三","age":15};
delete Person.name;
delete Person["age"]
```



## JSON数组



> 实例

```json
{"website":["Google","Baidu","Bing"]}
```

.

> 使用

JSON 数组在中括号中书写。

JSON 中数组值必须是合法的 JSON 数据类型（字符串, 数字, 对象, 数组, 布尔值或 null）

数组值可以是以上的 JSON 数据类型，也可以是 JavaScript 的表达式，包括函数，日期，及 *undefined*



> 访问

使用索引值来访问数组

```js
var obj={"website":["Google","Baidu","Bing"]};
x=obj.website[0]
```



> 循环数组

使用 for-in 来访问数组

```js
var obj={"website":["Google","Baidu","Bing"]};
for (x in obj){
    console.log(obj.website[x]);
}
```



使用for循环来访问数组

```js
var obj={"website":["Google","Baidu","Bing"]};
for (let i=0;i<obj.website.length;i++){
    console.log(obj.website[i]);
}
```



> 嵌套对象的数组

```js
var Obj = {
    "name":"网站",
    "num":2,
    "sites": [
        { "name":"Google", "info":[ "Android", "Google 搜索", "Google 翻译" ] },
        { "name":"Taobao", "info":[ "淘宝", "网购" ] }
    ]
}
```



> 修改数组值

使用索引值来修改数组值

```js
var obj={"website":["google","Baidu","Bing"]};
obj.website[1]="Google";
```



> 删除数组元素

使用 **delete** 关键字来删除数组元素

数组的大小不变

```js
var obj={"website":["Google","Baidu","Bing"]};
delete obj.website[2]
```

**note**:delete 运算符并不是彻底删除元素，而是删除它的值，但仍会保留空间

运算符 delete 只是将该值置为 undefined，而不会影响数组长度

## JSON.parse()

>  介绍

JSON 通常用于与服务端交换数据。

在接收服务器数据时一般是字符串。

我们可以使用 JSON.parse() 方法将数据转换为 JavaScript 对象



> 语法

```
JOSN.parse(text [,reviver])
```

+ **参数说明：**
  + **text:**必需， 一个有效的 JSON 字符串。
  + **reviver:** 可选，一个转换结果的函数， 将为对象的每个成员调用此函数



> 实例

```json
{"name":"Google","url":"www.google.com"}
```

```js
var obj = JSON.parse('{"name":"Google","url":"www.google.com"}')
```



> 接收JSON数据

+ 使用 AJAX 从服务器请求 JSON 数据，并解析为 JavaScript 对象

```js
var xmlhttp = new XMLHttpRequest();
xmlhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
        myObj = JSON.parse(this.responseText);
        document.getElementById("demo").innerHTML = myObj.name;
    }
};
xmlhttp.open("GET", "demo.txt", true);
xmlhttp.send();
```

+ 使用 AJAX 从服务器请求 JSON 数据，并解析为 JavaScript 数组

```js
var xmlhttp = new XMLHttpRequest();
xmlhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
        myArr = JSON.parse(this.responseText);
        document.getElementById("demo").innerHTML = myArr[1];
    }
};
xmlhttp.open("GET", "demo_array.txt", true);
xmlhttp.send();
```



> 解析日期

JSON 不能存储 Date 对象

如果你需要存储 Date 对象，需要将其转换为字符串

之后再将字符串转换为 Date 对象

```js
var text = '{ "name":"Google", "initDate":"2013-12-14", "site":"www.google.com"}';
var obj = JSON.parse(text);
obj.initDate = new Date(obj.initDate);
```



> 解析函数

JSON 不允许包含函数，但你可以将函数作为字符串存储，之后再将字符串转换为函数

```js
var text = '{ "name":"Google", "alexa":"function () {return 1;}", }';
var obj = JSON.parse(text);
obj.alexa = eval("(" + obj.alexa + ")");
```

+ **eval()函数**
  + eval() 函数可计算某个字符串，并执行其中的的 JavaScript 代码

  + ```
    eval(string)
    ```

  + 参数必需:要计算的字符串，其中含有要计算的 JavaScript 表达式或要执行的语句

> 浏览器支持

- Firefox 3.5
- Internet Explorer 8
- Chrome
- Opera 10
- Safari 4



## JSON.stringify()

> 介绍

JSON 通常用于与服务端交换数据。

在向服务器发送数据时一般是字符串。

我们可以使用 JSON.stringify() 方法将 JavaScript 对象转换为字符串



> 语法

```
JSON.stringify(value[, replacer[, space]])
```



参数说明:

+ value:

  必需， 要转换的 JavaScript 值（通常为对象或数组）。

+ replacer:

  可选。用于转换结果的函数或数组。

  如果 replacer 为函数，则 JSON.stringify 将调用该函数，并传入每个成员的键和值。使用返回值而不是原始值。如果此函数返回 undefined，则排除成员。根对象的键是一个空字符串：""。

  如果 replacer 是一个数组，则仅转换该数组中具有键值的成员。成员的转换顺序与键在数组中的顺序一样。当 value 参数也为数组时，将忽略 replacer 数组。

+ space:

  可选，文本添加缩进、空格和换行符，如果 space 是一个数字，则返回值文本在每个级别缩进指定数目的空格，如果 space 大于 10，则文本缩进 10 个空格。space 也可以使用非数字，如：\t



>  转换

向服务器发送以下数据

```js
var obj = { "name":"google", "alexa":1, "site":"www.google.com"};
```

使用 JSON.stringify() 方法处理以上数据，将其转换为字符串

```js
var myJSON = JSON.stringify(obj);
```

myJSON 为字符串



> 浏览器支持

- Firefox 3.5
- Internet Explorer 8
- Chrome
- Opera 10
- Safari 4



## JSON使用

> 文本转换成对象





> 实例

