# XML基础

> 概念

XML 指可扩展标记语言（e**X**tensible **M**arkup **L**anguage）。

XML 被设计用来传输和存储数据

> 实例

```xml
<?xml version="1.0" encoding="UTF-8"?>
<note>
  <to>Tove</to>
  <from>faxxxing</from>
  <heading>call</heading>
  <body>hello XML!</body>
</note>
```

## 简介

> 概念

- XML 指可扩展标记语言（EXtensible Markup Language）。
- XML 是一种很像HTML的标记语言。
- XML 的设计宗旨是传输数据，而不是显示数据。
- XML 标签没有被预定义。您需要自行定义标签。
- XML 被设计为具有自我描述性。
- XML 是 W3C 的推荐标准

> HTML与XML区别

- XML 被设计用来传输和存储数据，其焦点是数据的内容。
- HTML 被设计用来显示数据，其焦点是数据的外观。

HTML 旨在显示信息，而 XML 旨在传输信息

> XML不做任何事

XML 被设计用来结构化、存储以及传输信息

```xml
<note>
<to>Tove</to>
<from>Jani</from>
<heading>Reminder</heading>
<body>Don't forget me this weekend!</body>
</note>
```

这条便签具有自我描述性。它包含了发送者和接受者的信息，同时拥有标题以及消息主体

## 用途

> 简化数据共享

XML 数据以纯文本格式进行存储，因此提供了一种独立于软件和硬件的数据存储方法。

这让创建不同应用程序可以共享的数据变得更加容易。

> 简化数据传输

由于可以通过各种不兼容的应用程序来读取数据，以 XML 交换数据降低了这种复杂性

> 简化平台变更

升级到新的系统（硬件或软件平台），总是非常费时的。必须转换大量的数据，不兼容的数据经常会丢失。

XML 数据以文本格式存储。这使得 XML 在不损失数据的情况下，更容易扩展或升级到新的操作系统、新的应用程序或新的浏览器

> 增强数据实用性

通过 XML，您的数据可供各种阅读设备使用（掌上计算机、语音设备、新闻阅读器等），还可以供盲人或其他残障人士使用

> 创建新的互联网语言

很多新的互联网语言是通过 XML 创建的。

这里有一些实例：

- XHTML
- 用于描述可用的 Web 服务 的 WSDL
- 作为手持设备的标记语言的 WAP 和 WML
- 用于新闻 feed 的 RSS 语言
- 描述资本和本体的 RDF 和 OWL
- 用于描述针针对 Web 的多媒体 的 SMIL

## 结构

> 概念

XML 文档形成了一种树结构，它从"根部"开始，然后扩展到"枝叶"。

> 实例

```xml
<?xml version="1.0" encoding="UTF-8"?>
<note>
<to>Tove</to>
<from>Jani</from>
<heading>Reminder</heading>
<body>Don't forget me this weekend!</body>
</note>
```

第一行是 XML 声明。它定义 XML 的版本（1.0）和所使用的编码（UTF-8 : 万国码, 可显示各种语言）。

> `<note>`

描述文档的**根元素**

> `</note>`

最后一行定义根元素的结尾

> XML的树结构

XML 文档必须包含**根元素**。该元素是所有其他元素的父元素。

XML 文档中的元素形成了一棵文档树。这棵树从根部开始，并扩展到树的最底端

所有的元素都可以有子元素

```xml
<root>
<child>
<subchild>.....</subchild>
</child>
</root>
```

## 语法

> 根元素

XML 必须包含根元素，它是所有其他元素的父元素,实例中 root 就是根元素

```xml
<root>
  <child>
    <subchild>.....</subchild>
  </child>
</root>
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<note>
  <to>Tove</to>
  <from>Jani</from>
  <heading>Reminder</heading>
  <body>Don't forget me this weekend!</body>
</note>
```

> 声明

XML 声明文件的可选部分，如果存在需要放在文档的第一行

```xml
<?xml version="1.0" encoding="utf-8"?>
```

> 闭合便签

在 HTML 中，某些元素不必有一个关闭标签

```html
<input type="text">
```

在 XML 中，省略关闭标签是非法的。所有元素都**必须**有关闭标签

```xml
<p>This is a paragraph.</p>
```

> 大小写敏感

XML 标签对大小写敏感。标签 <Letter> 与标签 <letter> 是不同的。

必须使用相同的大小写来编写打开标签和关闭标签

```xml
<Message>这是错误的</message>
<message>这是正确的</message>
```

> 嵌套

+ 没有正确嵌套的元素

  + ```xml
    b><i>This text is bold and italic</b></i>
    ```

+ 所有元素都**必须**彼此正确地嵌套

  + ```xml
    <b><i>This text is bold and italic</i></b>
    ```

> 属性值

与 HTML 类似，XML 元素也可拥有属性（名称/值的对）。

在 XML 中，XML 的属性值必须加引号

```xml
<note date="12/11/2007">
<to>Tove</to>
<from>Jani</from>
</note>
```

> 实体字符

在 XML 中，一些字符拥有特殊的意义。

如果您把字符 "<" 放在 XML 元素中，会发生错误，这是因为解析器会把它当作新元素的开始

+  XML 错误

  + ```xml
    <message>if salary < 1000 then</message>
    ```

+ 实体引用

  + ```xml
    <message>if salary &lt; 1000 then</message>
    ```

| &lt ;   | <    | less than      |
| ------- | ---- | -------------- |
| &gt ;   | >    | greater than   |
| &amp ;  | &    | ampersand      |
| &apos ; | '    | apostrophe     |
| &quot ; | "    | quotation mark |

**note：**在 XML 中，只有字符 "<" 和 "&" 确实是非法的。大于号是合法的，但是用实体引用来代替它是一个好习惯

> 注释

在 XML 中编写注释的语法与 HTML 的语法很相似。

```xml
<!-- This is a comment -->
```

> 空格

HTML 会把多个连续的空格字符裁减（合并）为一个

在 XML 中，文档中的空格不会被删减

## 元素

> XML元素

XML 元素指的是从（且包括）开始标签直到（且包括）结束标签的部分

一个元素可以包含：

- 其他元素
- 文本
- 属性
- 或以上所有

```xml
<bookstore>
    <book category="CHILDREN">
        <title>Harry Potter</title>
        <author>J K. Rowling</author>
        <year>2005</year>
        <price>29.99</price>
    </book>
    <book category="WEB">
        <title>Learning XML</title>
        <author>Erik T. Ray</author>
        <year>2003</year>
        <price>39.95</price>
    </book>
</bookstore>
```

<bookstore> 和 <book> 都有 **元素内容**，因为他们包含其他元素

<book> 元素也有**属性**（category="CHILDREN"）

<author>、<year> 和 <price> 有**文本内容**，因为他们包含文本

> 命名规则

XML 元素必须遵循以下命名规则：

- 名称可以包含字母、数字以及其他的字符
- 名称不能以数字或者标点符号开始
- 名称不能以字母 xml（或者 XML、Xml 等等）开始
- 名称不能包含空格

可使用任何名称，没有保留的字词

## 属性

> 概念

XML元素具有属性，类似 HTML。

属性（Attribute）提供有关元素的额外信息

> 区别

在 HTML 中，属性提供有关元素的额外信息

```xtml
<a href="demo.html">
```

属性通常提供不属于数据组成部分的信息

> 引号

属性值必须被引号包围，不过单引号和双引号均可使用

```xml
<person sex="female">
<person sex='male'>
```

如果属性值本身包含双引号，您可以使用单引号

```xml
<name name='George "Shotgun" Ziegler'><name>
```

> 元素与属性

使用了 date 属性

```xml
<note date="10/01/2008">
<to>Tove</to>
<from>Jani</from>
<heading>Reminder</heading>
<body>Don't forget me this weekend!</body>
</note>
```

使用了 date 元素

```xml
<note>
<date>10/01/2008</date>
<to>Tove</to>
<from>Jani</from>
<heading>Reminder</heading>
<body>Don't forget me this weekend!</body>
</note>
```

属性难以阅读和维护。请尽量使用元素来描述数据.XML 中，您应该尽量避免使用属性

> '正确'的使用

向元素分配 ID 引用。这些 ID 索引可用于标识 XML 元素，它起作用的方式与 HTML 中 id 属性是一样的

```xml
<messages>
<note id="501">
<to>Tove</to>
<from>Jani</from>
<heading>Reminder</heading>
<body>Don't forget me this weekend!</body>
</note>
<note id="502">
<to>Jani</to>
<from>Tove</from>
<heading>Re: Reminder</heading>
<body>I will not</body>
</note>
</messages>
```

元数据（有关数据的数据）应当存储为属性，而数据本身应当存储为元素

## 验证

> 概念

通过 DTD 验证的XML是"合法"的 XML

> 良好的XML文档

"形式良好"的 XML 文档拥有正确的语法:

- XML 文档必须有一个根元素
- XML元素都必须有一个关闭标签
- XML 标签对大小写敏感
- XML 元素必须被正确的嵌套
- XML 属性值必须加引号

> 验证文档

合法的 XML 文档是"形式良好"的 XML 文档，也符合文档类型定义（DTD）的规则

```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<!DOCTYPE note SYSTEM "Note.dtd">
<note>
<to>Tove</to>
<from>Jani</from>
<heading>Reminder</heading>
<body>Don't forget me this weekend!</body>
</note>
```

DOCTYPE 声明是对外部 DTD 文件的引用

> DTD

DTD 的目的是定义 XML 文档的结构。它使用一系列合法的元素来定义文档结构

```dtd
<!DOCTYPE note
[
<!ELEMENT note (to,from,heading,body)>
<!ELEMENT to (#PCDATA)>
<!ELEMENT from (#PCDATA)>
<!ELEMENT heading (#PCDATA)>
<!ELEMENT body (#PCDATA)>
]>
```

> Schema

一种基于 XML 的 DTD 代替者，它名为 XML Schema

```scheme
<xs:element name="note">

<xs:complexType>
<xs:sequence>
<xs:element name="to" type="xs:string"/>
<xs:element name="from" type="xs:string"/>
<xs:element name="heading" type="xs:string"/>
<xs:element name="body" type="xs:string"/>
</xs:sequence>
</xs:complexType>

</xs:element>
```

## 验证器

> 终止

XML 文档中的错误会终止您的 XML 应用程序。

W3C 的 XML 规范声明：如果 XML 文档存在错误，那么程序就不应当继续处理这个文档。理由是，XML 软件应当轻巧，快速，具有良好的兼容性。

如果使用 HTML，创建包含大量错误的文档是有可能的（比如您忘记了结束标签）。其中一个主要的原因是 HTML 浏览器相当臃肿，兼容性也很差，并且它们有自己的方式来确定当发现错误时文档应该显示为什么样子

**使用 XML 时，这种情况不应当存在**

> 根据DTD验证

只要把 DOCTYPE 声明（带有 DTD）添加到您的 XML 中 <xml> 元素

```xml
<?xml version="1.0" ?> 
<!DOCTYPE note [
  <!ELEMENT note (to,from,heading,body)>
  <!ELEMENT to      (#PCDATA)>
  <!ELEMENT from    (#PCDATA)>
  <!ELEMENT heading (#PCDATA)>
  <!ELEMENT body    (#PCDATA)>
]>
<note>
<to>Tove</to> 
<from>Jani</from> 
<heading>Reminder</heading> 
<message>Don't forget me this weekend!</message> 
</note>

```

## 查看

> 概念

在所有主流的浏览器中，均能够查看原始的 XML 文件。

不要指望 XML 文件会直接显示为 HTML 页面

> 标记

XML 文档将显示为代码颜色化的根以及子元素。

通过点击元素左侧的加号（+）或减号（ - ），可以展开或收起元素的结构。

要查看原始的 XML 源（不包括 + 和 - 符号），选择"查看页面源代码"或从浏览器菜单"查看源文件"。

> 本地查看

拖拽XML文件至浏览器

## CSS

通过使用 CSS（Cascading Style Sheets 层叠样式表），您可以添加显示信息到 XML 文档中

> 显示

把 XML 文件链接到 CSS 文件

```xml
<?xml-stylesheet type="text/css" href="style.css"?>
```

使用 CSS 格式化 XML 不是常用的方法

## XSLT

通过使用 XSLT，您可以把 XML 文档转换成 HTML 格式

> 使用XSLT显示XML

XSLT 是首选的 XML 样式表语言。

XSLT（eXtensible Stylesheet Language Transformations）远比 CSS 更加完善。

XSLT 是在浏览器显示 XML 文件之前，先把它转换为 HTML

# XML拓展

## XMLHttpRequest 对象

XMLHttpRequest 对象用于在后台与服务器交换数据。

XMLHttpRequest 对象是**开发者的梦想**：

- 在不重新加载页面的情况下更新网页
- 在页面已加载后从服务器请求数据
- 在页面已加载后从服务器接收数据
- 在后台向服务器发送数据

> 创建XMLHttpRequest对象

+ 创建 XMLHttpRequest 对象的语法

  + ```xml
    xmlhttp=new XMLHttpRequest();
    ```

+ 旧版本的Internet Explorer（IE5和IE6）中使用 ActiveX 对象

  + ```xml
    xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
    ```

## Parser

> 概念

所有现代浏览器都有内建的 XML 解析器。

XML 解析器把 XML 文档转换为 XML DOM 对象 - 可通过 JavaScript 操作的对象

> 创建XMLHttpRequest 对象

```js
if (window.XMLHttpRequest)
{// code for IE7+, Firefox, Chrome, Opera, Safari
xmlhttp=new XMLHttpRequest();
}
else
{// code for IE6, IE5
xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
}
```



> 解析XML文档

```JS
xmlhttp.open("GET","xxxx.xml",false);
xmlhttp.send();
xmlDoc=xmlhttp.responseXML;
```

> 解析XML字符串

```js
txt="<bookstore><book>";
txt=txt+"<title>Everyday Italian</title>";
txt=txt+"<author>Giada De Laurentiis</author>";
txt=txt+"<year>2005</year>";
txt=txt+"</book></bookstore>";

if (window.DOMParser)
{
parser=new DOMParser();
xmlDoc=parser.parseFromString(txt,"text/xml");
}
else // Internet Explorer
{
xmlDoc=new ActiveXObject("Microsoft.XMLDOM");
xmlDoc.async=false;
xmlDoc.loadXML(txt);
}
```

