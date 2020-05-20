MySQL

# 语法格式

```mysql
mysqli_function(value,value,...);
```

# 数据库

> 基本的几种语法

```mysql
mysqli_connect($connect);
mysqli_query($connect,"SQL 语句");
mysqli_fetch_array();
mysqli_fetch_assoc()
mysqli_close();
```

**注意：**MySQL命令终止符为分号 **;** 

**注意：** **->** 是换行符标识，不要复制.

## mysql连接

### 命令行

```mysql
mysql -u root (-p)
```

> 退出 mysql> 命令提示窗口可以使用 exit 命令

```
mysql> exit;
Bye
```

### php脚本

PHP 提供了 mysqli_connect() 函数来连接数据库

该函数有 6 个参数，在成功链接到 MySQL 后返回连接标识，失败返回 FALSE 。

```mysql
mysqli_connect(host,username,password,dbname,port,socket);
```

| 参数       | 描述                                        |
| :--------- | :------------------------------------------ |
| *host*     | 可选。规定主机名或 IP 地址。                |
| *username* | 可选。规定 MySQL 用户名。                   |
| *password* | 可选。规定 MySQL 密码。                     |
| *dbname*   | 可选。规定默认使用的数据库。                |
| *port*     | 可选。规定尝试连接到 MySQL 服务器的端口号。 |
| *socket*   | 可选。规定 socket 或要使用的已命名 pipe。   |

使用 PHP 的 mysqli_close() 函数来断开与 MySQL 数据库的链接

该函数只有一个参数为 mysqli_connect() 函数创建连接成功后返回的 MySQL 连接标识符

```mysql
bool mysqli_close ( mysqli $link )
```

### 连接 MySQL 服务器

```php
<?php
    $dbhost = 'localhost';  // mysql服务器主机地址
    $dbuser = 'root';            // mysql用户名
    $conn = mysqli_connect($dbhost, $dbuser);
    if(! $conn )
    {
        die('Could not connect: ' . mysqli_error());
    }
    echo '数据库连接成功！';
    mysqli_close($conn);
?>
```

## mysql创建

> 使用 **create** 命令创建数据库

### 命令行

```mysql
mysql> create DATABASE WordPress;
```

### 使用 PHP脚本 创建数据库

```mysql
mysqli_query(connection,query,resultmode);
```

| 参数         | 描述                                                         |
| :----------- | :----------------------------------------------------------- |
| *connection* | 必需。规定要使用的 MySQL 连接。                              |
| *query*      | 必需，规定查询字符串。                                       |
| *resultmode* | 可选。一个常量。可以是下列值中的任意一个：MYSQLI_USE_RESULT（如果需要检索大量数据，请使用这个）MYSQLI_STORE_RESULT（默认） |

### 实例

```php
<?php
    $dbhost = 'localhost';  // mysql服务器主机地址
    $dbuser = 'root';            // mysql用户名
    $conn = mysqli_connect($dbhost, $dbuser);
    if(! $conn )
    {
      die('连接错误: ' . mysqli_error($conn));
    }
    echo '连接成功<br />';
    $sql = 'CREATE DATABASE XXXX';
    $retval = mysqli_query($conn,$sql );
    if(! $retval )
    {
        die('创建数据库失败: ' . mysqli_error($conn));
    }
    echo "数据库创建成功\n";
    mysqli_close($conn);
?>
```

## 删除数据库

### 命令行

```mysql
mysql> drop database XXXXX;
```

使用 mysql **mysqladmin** 命令在终端来执行删除命令

```mysql
mysqladmin -u root -p drop XXXX
```

### php

PHP使用 mysqli_query 函数来创建或者删除 MySQL 数据库。

该函数有两个参数，在执行成功时返回 TRUE，否则返回 FALSE

```php
<?php
    $dbhost = 'localhost:3306';  // mysql服务器主机地址
    $dbuser = 'root';            // mysql用户名
    $conn = mysqli_connect($dbhost, $dbuser);
    if(! $conn )
    {
        die('连接失败: ' . mysqli_error($conn));
    }
    echo '连接成功<br/>';
    $sql = 'DROP DATABASE XXX';
    $retval = mysqli_query( $conn, $sql );
    if(! $retval )
    {
        die('删除数据库失败: ' . mysqli_error($conn));
    }
    echo "数据库 删除成功\n";
    mysqli_close($conn);
    ?>
```



注意：** 在使用PHP脚本删除数据库时，不会出现确认是否删除信息，会直接删除指定数据库，所以你在删除数据库时要特别小心

## 选择数据库

### 命令提示窗口中选择

```mysql
mysql> use xxx;
Database changed
```

执行以上命令后，你就已经成功选择了XXX数据库，在后续的操作中都会在 RUNOOB 数据库中执行。

**注意:**所有的数据库名，表名，表字段都是区分大小写的。所以你在使用SQL命令时需要输入正确的名称。

### 使用PHP脚本选择MySQL数据库

PHP 提供了函数 mysqli_select_db 来选取一个数据库。函数在执行成功后返回 TRUE ，否则返回 FALSE

```mysql
mysqli_select_db(connection,dbname);
```

| 参数         | 描述                            |
| :----------- | :------------------------------ |
| *connection* | 必需。规定要使用的 MySQL 连接。 |
| *dbname*     | 必需，规定要使用的默认数据库。  |

### demo

```
<?php
    $dbhost = 'localhost:3306';  // mysql服务器主机地址
    $dbuser = 'root';            // mysql用户名
    $dbpass = '123456';          // mysql用户名密码
    $conn = mysqli_connect($dbhost, $dbuser, $dbpass);
    if(! $conn )
    {
        die('连接失败: ' . mysqli_error($conn));
    }
    echo '连接成功';
    mysqli_select_db($conn, 'XXX' );
    mysqli_close($conn);
?>
```

## 查看数据库

### 命令行

```mysql
show databases;
#查看所有数据库
show create database XXX;
#查看某一数据库
```



### php

```php
$sql='SHOW DATABASES';
$sql2="show create database XXX";
mysqli_query($conn,$sql);
```

## 修改数据库

只允许修改数据库的选项,不能修改名称

### 命令行

```mysql
alter database 库名 charset utf8mb4;
alter database 库名 charset utf8mb4 collate gbk_chinese_ci;
```

### php脚本

```php
$sql='alter database 库名 charset utf8mb4';
$sql2='alter database 库名 charset utf8mb4 collate gbk_chinese_ci';
mysqli_query($conn,$sql);
```



# 数据类型

### 数值类型

MySQL支持所有标准SQL数值数据类型。

这些类型包括严格数值数据类型(INTEGER、SMALLINT、DECIMAL和NUMERIC)，以及近似数值数据类型(FLOAT、REAL和DOUBLE PRECISION)。

关键字INT是INTEGER的同义词，关键字DEC是DECIMAL的同义词。

BIT数据类型保存位字段值，并且支持MyISAM、MEMORY、InnoDB和BDB表。

作为SQL标准的扩展，MySQL也支持整数类型TINYINT、MEDIUMINT和BIGINT。下面的表显示了需要的每个整数类型的存储和范围

MySQL支持多种类型，大致可以分为三类：数值、日期/时间和字符串(字符)类型

| 类型         | 大小                                     | 范围（有符号）                                               | 范围（无符号）                                               | 用途            |
| :----------- | :--------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :-------------- |
| TINYINT      | 1 byte                                   | (-128，127)                                                  | (0，255)                                                     | 小整数值        |
| SMALLINT     | 2 bytes                                  | (-32 768，32 767)                                            | (0，65 535)                                                  | 大整数值        |
| MEDIUMINT    | 3 bytes                                  | (-8 388 608，8 388 607)                                      | (0，16 777 215)                                              | 大整数值        |
| INT或INTEGER | 4 bytes                                  | (-2 147 483 648，2 147 483 647)                              | (0，4 294 967 295)                                           | 大整数值        |
| BIGINT       | 8 bytes                                  | (-9,223,372,036,854,775,808，9 223 372 036 854 775 807)      | (0，18 446 744 073 709 551 615)                              | 极大整数值      |
| FLOAT        | 4 bytes                                  | (-3.402 823 466 E+38，-1.175 494 351 E-38)，0，(1.175 494 351 E-38，3.402 823 466 351 E+38) | 0，(1.175 494 351 E-38，3.402 823 466 E+38)                  | 单精度 浮点数值 |
| DOUBLE       | 8 bytes                                  | (-1.797 693 134 862 315 7 E+308，-2.225 073 858 507 201 4 E-308)，0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) | 0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) | 双精度 浮点数值 |
| DECIMAL      | 对DECIMAL(M,D) ，如果M>D，为M+2否则为D+2 | 依赖于M和D的值                                               | 依赖于M和D的值                                               | 小数值          |

### 日期和时间类型

表示时间值的日期和时间类型为DATETIME、DATE、TIMESTAMP、TIME和YEAR。

每个时间类型有一个有效值范围和一个"零"值，当指定不合法的MySQL不能表示的值时使用"零"值

| 类型      | 大小 ( bytes) | 范围                                                         | 格式                | 用途                     |
| :-------- | :------------ | :----------------------------------------------------------- | :------------------ | :----------------------- |
| DATE      | 3             | 1000-01-01/9999-12-31                                        | YYYY-MM-DD          | 日期值                   |
| TIME      | 3             | '-838:59:59'/'838:59:59'                                     | HH:MM:SS            | 时间值或持续时间         |
| YEAR      | 1             | 1901/2155                                                    | YYYY                | 年份值                   |
| DATETIME  | 8             | 1000-01-01 00:00:00/9999-12-31 23:59:59                      | YYYY-MM-DD HH:MM:SS | 混合日期和时间值         |
| TIMESTAMP | 4             | 1970-01-01 00:00:00/2038结束时间是第 **2147483647** 秒，北京时间 **2038-1-19 11:14:07**，格林尼治时间 2038年1月19日 凌晨 03:14:07 | YYYYMMDD HHMMSS     | 混合日期和时间值，时间戳 |

### 字符串类型

字符串类型指CHAR、VARCHAR、BINARY、VARBINARY、BLOB、TEXT、ENUM和SET

| CHAR       | 0-255 bytes           | 定长字符串                      |
| ---------- | --------------------- | ------------------------------- |
| CHAR       | 0-255 bytes           | 定长字符串                      |
| VARCHAR    | 0-65535 bytes         | 变长字符串                      |
| TINYBLOB   | 0-255 bytes           | 不超过 255 个字符的二进制字符串 |
| TINYTEXT   | 0-255 bytes           | 短文本字符串                    |
| BLOB       | 0-65 535 bytes        | 二进制形式的长文本数据          |
| TEXT       | 0-65 535 bytes        | 长文本数据                      |
| MEDIUMBLOB | 0-16 777 215 bytes    | 二进制形式的中等长度文本数据    |
| MEDIUMTEXT | 0-16 777 215 bytes    | 中等长度文本数据                |
| LONGBLOB   | 0-4 294 967 295 bytes | 二进制形式的极大文本数据        |
| LONGTEXT   | 0-4 294 967 295 bytes | 极大文本数据                    |

**注意**：char(n) 和 varchar(n) 中括号中 n 代表字符的个数，并不代表字节个数，比如 CHAR(30) 就可以存储 30 个字符。

CHAR 和 VARCHAR 类型类似，但它们保存和检索的方式不同。它们的最大长度和是否尾部空格被保留等方面也不同。在存储或检索过程中不进行大小写转换。

BINARY 和 VARBINARY 类似于 CHAR 和 VARCHAR，不同的是它们包含二进制字符串而不要非二进制字符串。也就是说，它们包含字节字符串而不是字符字符串。这说明它们没有字符集，并且排序和比较基于列值字节的数值值。

BLOB 是一个二进制大对象，可以容纳可变数量的数据。有 4 种 BLOB 类型：TINYBLOB、BLOB、MEDIUMBLOB 和 LONGBLOB。它们区别在于可容纳存储范围不同。

有 4 种 TEXT 类型：TINYTEXT、TEXT、MEDIUMTEXT 和 LONGTEXT。对应的这 4 种 BLOB 类型，可存储的最大长度不同，可根据实际情况选择。

**UTF－8**：一个汉字＝3个字节

-  （1）**char**:  char 不用多说了，它是定长格式的，但是长度范围是 0~255. 当你想要储存一个长度不足 255 的字符时，Mysql 会用空格来填充剩下的字符。因此在读取数据时，char 类型的数据要进行处理，把后面的空格去除。
-  （2）**varchar**:  关于 varchar，有的说最大长度是 255，也有的说是 65535，查阅很多资料后发现是这样的：varchar 类型在 5.0.3 以下的版本中的最大长度限制为 255，而在 5.0.3 及以上的版本中，varchar 数据类型的长度支持到了 65535，也就是说可以存放 65532 个字节（注意是字节而不是字符！！！）的数据（起始位和结束位占去了3个字节），也就是说，在 5.0.3 以下版本中需要使用固定的 TEXT 或 BLOB 格式存放的数据可以在高版本中使用可变长的 varchar 来存放，这样就能有效的减少数据库文件的大小。
-  （3）**text**: 与 char 和 varchar 不同的是，text 不可以有默认值，其最大长度是 2 的 16 次方-1

**总结起来，有几点：**

-  经常变化的字段用 varchar
-  知道固定长度的用 char
-  尽量用 varchar
-  超过 255 字符的只能用 varchar 或者 text
-  能用 varchar 的地方不用 text

# 数据表

## MySQL 创建数据表

> 创建MySQL数据表需要以下信息：

- 表名
- 表字段名
- 定义每个表字段

### 语法

```mysql
CREATE TABLE table_name (column_name column_type);
```

### 命令提示符

```mysql
mysql> use XXXX;
Database changed
mysql> CREATE TABLE userinfo(
   id INT NOT NULL AUTO_INCREMENT,
   name CHAR(10) NOT NULL,
   password CHAR(18) NOT NULL,
   birthday DATE,
   PRIMARY KEY ( id )
   )ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

- 如果你不想字段为 **NULL** 可以设置字段的属性为 **NOT NULL**， 在操作数据库时如果输入该字段的数据为**NULL** ，就会报错。
- AUTO_INCREMENT定义列为自增的属性，一般用于主键，数值会自动加1。
- PRIMARY KEY关键字用于定义列为主键。 您可以使用多列来定义主键，列间以逗号分隔。
- ENGINE 设置存储引擎，CHARSET 设置编码

### PHP脚本创建数据表

使用 PHP 的 **mysqli_query()** 函数来创建已存在数据库的数据表。

该函数有两个参数，在执行成功时返回 TRUE，否则返回 FALSE

```php
<?php
$dbhost = 'localhost:3306';  // mysql服务器主机地址
$dbuser = 'root';            // mysql用户名
$dbpass = '123456';          // mysql用户名密码
$conn = mysqli_connect($dbhost, $dbuser, $dbpass);
if(! $conn )
{
    die('连接失败: ' . mysqli_error($conn));
}
echo '连接成功<br />';
$sql = "CREATE TABLE xxx_tbl(".
       "xxx_id INT NOT NULL AUTO_INCREMENT,".
       "xxx_title VARCHAR(100) NOT NULL,".
       "xxx_author VARCHAR(40) NOT NULL,".
       "submission_date DATE,".
       "PRIMARY KEY ( xxx_id )".
       ")ENGINE=InnoDB DEFAULT CHARSET=utf8;";
mysqli_select_db( $conn, 'XXXX' );
$retval = mysqli_query( $conn, $sql );
if(! $retval )
{
    die('数据表创建失败: ' . mysqli_error($conn));
}
echo "数据表创建成功\n";
mysqli_close($conn);
?>
```

### MySQL 字段属性应该尽量设置为 NOT NULL

除非你有一个很特别的原因去使用 NULL 值，你应该总是让你的字段保持 NOT NULL。这看起来好像有点争议，请往下看。

**1、**首先，我们要搞清楚空值 **""** 和 **NULL** 的概念：

-  1）空值是不占用空间的
-  2）MySQL中的NULL其实是占用空间的

所谓的 NULL 就是什么都没有，连 **\0** 都没有，**\0** 在字符串中是结束符，但是在物理内存是占空间的，等于一个字节，而 NULL 就是连这一个字节都没有。

**2、**其次，在数据库里是严格区分的，任何数跟 NULL 进行运算都是 NULL, 判断值是否等于 NULL，不能简单用 =，而要用 IS NULL关键字。

**3、**数据库的字段 col1 设为 NOT NULL, 仅仅说明该字段不能为 NULL, 也就是说只有在:

```
INSERT INTO table1(col1) VALUES(NULL);
```

这种情况下数据库会报错，而:

```
INSERT INTO table1(col1) VALUES('');
```

不会报错。

（如果字段是自增ID，第一句不会报错，这不能说明是可以为NULL,而是 数据库系统会根据ID设的缺省值填充，或者如果是自增字段就自动加一等缺省操作。）

**4、**含有空值的列很难进行查询优化，而且对表索引时不会存储 NULL 值的，所以如果索引的字段可以为 NULL，索引的效率会下降很多。因为它们使得索引、索引的统计信息以及比较运算更加复杂。你应该用 0、一个特殊的值或者一个空串代替空值。

**5、**联表查询的时候，例如 LEFT JOIN table2，若没有记录，则查找出的 table2 字段都是 null。假如 table2 有些字段本身可以是 null，那么除非把 table2 中 not null 的字段查出来，否则就难以区分到底是没有关联记录还是其他情况。

## MySQL 删除数据表

### 语法

```mysql
DROP TABLE table_name ;
```

### 命令提示窗口

```mysql
mysql> use XXXX;
Database changed
mysql> DROP TABLE xxx_tbl
```

### PHP脚本删除数据表

```
mysqli_query(connection,query,resultmode);
```

```php
<?php
    $dbhost = 'localhost:3306';  // mysql服务器主机地址
    $dbuser = 'root';            // mysql用户名
    $dbpass = '123456';          // mysql用户名密码
    $conn = mysqli_connect($dbhost, $dbuser, $dbpass);
    if(! $conn )
    {
      die('连接失败: ' . mysqli_error($conn));
    }
    echo '连接成功<br />';
    $sql = "DROP TABLE xxx_tbl";
    mysqli_select_db( $conn, 'XXXX' );
    $retval = mysqli_query( $conn, $sql );
    if(! $retval )
    {
      die('数据表删除失败: ' . mysqli_error($conn));
    }
    echo "数据表删除成功\n";
    mysqli_close($conn);
?>
```

## MySQL 更改数据表

更改数据表的表名和选项

### 命令行

```mysql
alter table xxx to xxxx;
#更改表名
alter table xxx charset utf8bm4;
#更改表选项
```

### php

```php
$sql='alter table xxx rename to xxxx';

$sql='alter table xxx charset utf8bm4';

mysqli_query($conn,$sql);
```

## MySQL 显示数据表

### 命令行

```mysql
show tables;
#所有
show create table xxxx;
#某一个
desc 表名
#查看表的信息
```

### php

```php
$sql='show tables';
$sql2='show create table xxxx';
$sql3='desc 表名';
mysqli_query($conn,$sql);
```

## MySQL 插入数据

MySQL 表中使用 **INSERT INTO** SQL语句来插入数据

### 命令提示窗口插入数据

如果数据是完全对应字段名的会,可以省略(field);

```mysql
INSERT INTO table_name ( field1, field2,...fieldN )
                       VALUES
                       ( value1, value2,...valueN );
```

如果数据是字符型，必须使用单引号或者双引号，如："value"

### 使用PHP脚本插入数据

```mysql
mysqli_query(connection,query,resultmode);
```

对于含有中文的数据插入，需要添加 语句

```php
 mysqli_query($conn , "set names utf8");
```



```php
<?php
    $dbhost = 'localhost:3306';  // mysql服务器主机地址
    $dbuser = 'root';            // mysql用户名
    $dbpass = '123456';          // mysql用户名密码
    $conn = mysqli_connect($dbhost, $dbuser, $dbpass);
    if(! $conn )
    {
      die('连接失败: ' . mysqli_error($conn));
    }
    echo '连接成功<br />';
    // 设置编码，防止中文乱码
    mysqli_query($conn , "set names utf8");

    $XXX_title = '学习 Python';
    $XXX_author = 'RUNOOB.COM';
    $submission_date = '2016-03-06';

    $sql = "INSERT INTO runoob_tbl ".
            "(runoob_title,runoob_author, submission_date) ".
            "VALUES ".
            "('$runoob_title','$runoob_author','$submission_date')";
    mysqli_select_db( $conn, 'XXXX' );
    $retval = mysqli_query( $conn, $sql );
    if(! $retval )
    {
      die('无法插入数据: ' . mysqli_error($conn));
    }
    echo "数据插入成功\n";
    mysqli_close($conn);
?
```



# 查询选项

## MySQL 查询数据 

- 查询语句中你可以使用一个或者多个表，表之间使用逗号(,)分割，并使用WHERE语句来设定查询条件。
- SELECT 命令可以读取一条或者多条记录。
- 你可以使用星号（*）来代替其他字段，SELECT语句会返回表的所有字段数据

```
select * from xxx_tbl;
```

- 你可以使用 WHERE 语句来包含任何条件。
- 你可以使用 LIMIT 属性来设定返回的记录数。
- 你可以通过OFFSET指定SELECT语句开始查询的数据偏移量。默认情况下偏移量为0。

### 通过命令提示符获取数据

```
    SELECT column_name,column_name
    FROM table_name
    [WHERE Clause]
    [LIMIT N][ OFFSET M]
```

### PHP脚本来获取数据

使用 PHP 函数的 **mysqli_query()** 及 **SQL SELECT** 命令来获取数据。

该函数用于执行 SQL 命令，然后通过 PHP 函数 **mysqli_fetch_array()** 来使用或输出所有查询的数据。

**mysqli_fetch_array()** 函数从结果集中取得一行作为关联数组，或数字数组，或二者兼有 返回根据从结果集取得的行生成的数组，如果没有更多行则返回 false。

以下实例为从数据表 runoob_tbl 中读取所有记录

```php
<?php
    $dbhost = 'localhost:3306';  // mysql服务器主机地址
    $dbuser = 'root';            // mysql用户名
    $dbpass = '123456';          // mysql用户名密码
    $conn = mysqli_connect($dbhost, $dbuser, $dbpass);
    if(! $conn )
    {
        die('连接失败: ' . mysqli_error($conn));
    }
    // 设置编码，防止中文乱码
    mysqli_query($conn , "set names utf8");

    $sql = 'SELECT xxx_id, xxx_title, 
            xxx_author
            FROM xxx_tbl';

    mysqli_select_db( $conn, 'XXX );
    $retval = mysqli_query( $conn, $sql );
    while($row = mysqli_fetch_array($retval, MYSQLI_ASSOC))
    {
        echo "<p>{$row['xxx_id']}</p> ".
             "<p>{$row['xxx_title']} </p> ".
             "<p>{$row['xxx_author']} </p> ".
             "<br>"
    }
    mysqli_close($conn);
?>
```

使用 PHP 函数的 **mysqli_query()** 及 **SQL SELECT** 命令来获取数据。

该函数用于执行 SQL 命令，然后通过 PHP 函数 **mysqli_fetch_array()** 来使用或输出所有查询的数据。

**mysqli_fetch_array()** 函数从结果集中取得一行作为关联数组，或数字数组，或二者兼有 返回根据从结果集取得的行生成的数组，如果没有更多行则返回 false。

以上实例中，读取的每行记录赋值给变量 $row，然后再打印出每个值。

**注意：**记住如果你需要在字符串中使用变量，请将变量置于花括号。

在上面的例子中，PHP mysqli_fetch_array() 函数第二个参数为 **MYSQLI_ASSOC**， 设置该参数查询结果返回关联数组，你可以使用字段名称来作为数组的索引。

PHP 提供了另外一个函数 **mysqli_fetch_assoc()**, 该函数从结果集中取得一行作为关联数组。 返回根据从结果集取得的行生成的关联数组，如果没有更多行，则返回 false。

## MySQL 别名

使用as 关键字或直接省略

### 命令行

```mysql
select xxx as xx from table1;
```

### 去重查询

> 不去重查询

```mysql
select xxx from tablexxx;
select all xxxx from tablexxx; 
```

> 去重查询

```mysql
select distinct * from tablexxx;
```

重复的数据会被去除

## 数据源

```mysql
select * from table1,table2;
```

```mysql
select * from table1 as t1;
```

```mysql
select * from (select * from table2) as t2;
#此时必须要起别名,否则会报错
```



## TOP

> TOP 子句用于规定要返回的记录的数目。

现在，我们希望从上面的 "Persons" 表中选取头两条记录

```mysql
SELECT TOP 2 * FROM Persons
```

"Persons" 表中选取 50% 的记录

```mysql
SELECT TOP 50 PERCENT * FROM Persons
```



## IN

> IN 操作符允许我们在 WHERE 子句中规定多个值(用于枚举型)

Persons 表:

| Id   | LastName | FirstName | Address        | City     |
| :--- | :------- | :-------- | :------------- | :------- |
| 1    | Adams    | John      | Oxford Street  | London   |
| 2    | Bush     | George    | Fifth Avenue   | New York |
| 3    | Carter   | Thomas    | Changan Street | Beijing  |

```mysql
SELECT * FROM Persons
WHERE LastName IN ('Adams','Carter')
```

结果表:

| Id   | LastName | FirstName | Address        | City    |
| :--- | :------- | :-------- | :------------- | :------ |
| 1    | Adams    | John      | Oxford Street  | London  |
| 3    | Carter   | Thomas    | Changan Street | Beijing |

## BETWEEN

> 操作符 BETWEEN ... AND 会选取两个值之间的数据范围。这些值可以是数值、文本或者日期。

```mysql
SELECT * FROM Persons
WHERE id
BETWEEN 2 AND 15
```



> 显示范围之外的人，请使用 NOT 操作符

```mysql
SELECT * FROM Persons
WHERE id
NOT BETWEEN 1 AND 7
```



## SELECT INTO 语句

SELECT INTO 语句从一个表中选取数据，然后把数据插入另一个表中。

SELECT INTO 语句常用于创建表的备份复件或者用于对记录进行存档。

```mysql
SELECT *
INTO table_backup
FROM table;
```



```mysql
SELECT *
INTO table_backup IN athoner_database
FROM table
```

## CHECK 约束

CHECK 约束用于限制列中的值的范围。

如果对单个列定义 CHECK 约束，那么该列只允许特定的值。

如果对一个表定义 CHECK 约束，那么此约束会在特定的列中对值进行限制

```mysql
CREATE TABLE Persons
(
Id_P int NOT NULL,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255),
CHECK (Id_P>0)
)
```

> 添加check约束

```mysql
ALTER TABLE Persons
ADD CHECK (Id_P>0)
```



如果需要命名 CHECK 约束，以及为多个列定义 CHECK 约束

```mysql
CREATE TABLE Persons
(
Id_P int NOT NULL,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255),
CONSTRAINT chk_Person CHECK (Id_P>0 AND City='Sandnes')
)
```

> 撤销check

```mysql
ALTER TABLE Persons
DROP CHECK chk_Person
```

## INDEX

**CREATE INDEX 语句用于在表中创建索引。**

**在不读取整个表的情况下，索引使数据库应用程序可以更快地查找数据**

在表中创建索引，以便更加快速高效地查询数据。

用户无法看到索引，它们只能被用来加速搜索/查询。

**注释：**更新一个包含索引的表需要比更新一个没有索引的表更多的时间，这是由于索引本身也需要更新。因此，理想的做法是仅仅在常常被搜索的列（以及表）上面创建索引。

> CREATE INDEX 语法

```mysql
CREATE INDEX index_name
ON table_name (column_name)
```

> CREATE UNIQUE INDEX 语法

```mysql
CREATE UNIQUE INDEX index_name
ON table_name (column_name);
```

> 实例

```mysql
CREATE INDEX PersonIndex
ON Person (LastName) ;
```

```mysql
CREATE INDEX PersonIndex
ON Person (LastName DESC) ;
```

```mysql
CREATE INDEX PersonIndex
ON Person (LastName, FirstName);
```

如果指定字段是字符串，需要指定长度，建议长度与定义字段时的长度一致，字段类型如果不是字符串，可以不填写长度部分

> 显示索引

```mysql
show index from 表名;
```

> 删除索引

```mysql
drop index 索引名称 on 数据表
```



## MySQL WHERE 子句

- 查询语句中你可以使用一个或者多个表，表之间使用逗号**,** 分割，并使用WHERE语句来设定查询条件。
- 你可以在 WHERE 子句中指定任何条件。
- 你可以使用 AND 或者 OR 指定一个或多个条件。
- WHERE 子句也可以运用于 SQL 的 DELETE 或者 UPDATE 命令。
- WHERE 子句类似于程序语言中的 if 条件，根据 MySQL 表中的字段值来读取指定的数据

```mysql
SELECT field1, field2,...fieldN FROM table_name1, table_name2...
[WHERE condition1 [AND [OR]] condition2.....
```

### 命令行

```mysql
SELECT * from xxxx_tbl WHERE author='xxx';
```

使用了 **WHERE BINARY** 关键字，是区分大小写的

### php脚本

```php
$sql_search_where='SELECT * from table1 WHERE author="surp"';
$retval_searchresult=mysqli_query($conn,$sql_search_where);
```

使用 PHP 函数的 mysqli_query() 及相同的 SQL SELECT 带上 WHERE 子句的命令来获取数据。

该函数用于执行 SQL 命令，然后通过 PHP 函数 mysqli_fetch_array() 来输出所有查询的数据

**where：**数据库中常用的是where关键字，用于在初始表中筛选查询。它是一个约束声明，用于约束数据，在返回结果集之前起作用。

**group by:**对select查询出来的结果集按照某个字段或者表达式进行分组，获得一组组的集合，然后从每组中取出一个指定字段或者表达式的值。

**having：**用于对where和group by查询出来的分组经行过滤，查出满足条件的分组结果。它是一个过滤声明，是在查询返回结果集以后对查询结果进行的过滤操作。

**执行顺序**

select –>where –> group by–> having–>order by

## MySQL UPDATE 更新

### 命令行

```
UPDATE table_name SET field1=new-value1, field2=new-value2
[WHERE Clause]
```

### php脚本

```php
$sql_update='UPDATE table1 SET submission_date="2020-4-12" WHERE author="liuneng"';
        $retval_update=mysqli_query($conn,$sql_update);
```



## MySQL DELETE 语句

- 如果没有指定 WHERE 子句，MySQL 表中的所有记录将被删除。
- 你可以在 WHERE 子句中指定任何条件
- 您可以在单个表中一次性删除记录。

### 从命令行中删除数据

```php
mysql> use XXXX;
mysql> DELETE FROM xxx_tbl WHERE xxx_id=3;
```

### php脚本

```php
$sql_delete='DELETE FROM table1 WHERE id=4';
        $retval_delete=mysqli_query($conn,$sql_delete);
        if(!$retval_delete){
            echo "删除数据失败";
        }
        else{
            echo "删除数据成功";
        }
```

### delete，drop，truncate 

-  1、delete 和 truncate 仅仅删除表数据，drop 连表数据和表结构一起删除，打个比方，delete 是单杀，truncate 是团灭，drop 是把电脑摔了。
-  2、delete 是 DML 语句，操作完以后如果没有不想提交事务还可以回滚，truncate 和 drop 是 DDL 语句，操作完马上生效，不能回滚，打个比方，delete 是发微信说分手，后悔还可以撤回，truncate 和 drop 是直接扇耳光说滚，不能反悔。
-  3、执行的速度上，**drop>truncate>delete**，打个比方，drop 是神舟火箭，truncate 是和谐号动车，delete 是自行车。

## MySQL LIKE 子句

我们知道在 MySQL 中使用 SQL SELECT 命令来读取数据， 同时我们可以在 SELECT 语句中使用 WHERE 子句来获取指定的记录。

WHERE 子句中可以使用等号 **=** 来设定获取数据的条件，如 "xxx = 'XXXX'"。

但是有时候我们需要获取 XXXX 字段含有 "COM" 字符的所有记录，这时我们就需要在 WHERE 子句中使用 SQL LIKE 子句。

SQL LIKE 子句中使用百分号 **%**字符来表示任意字符，类似于UNIX或正则表达式中的星号 *****。

如果没有使用百分号 **%**, LIKE 子句与等号 **=** 的效果是一样的。

### 语法

```mysql
SELECT field1, field2,...fieldN 
FROM table_name
WHERE field1 LIKE condition1 [AND [OR]] filed2 = 'somevalue'
```

### 命令行

```
SELECT * from XXX_tbl  WHERE xxxx_author LIKE '%COM';
```



- 你可以在 WHERE 子句中指定任何条件。
- 你可以在 WHERE 子句中使用LIKE子句。
- 你可以使用LIKE子句代替等号 **=**。
- LIKE 通常与 **%** 一同使用，类似于一个元字符的搜索。
- 你可以使用 AND 或者 OR 指定一个或多个条件。
- 你可以在 DELETE 或 UPDATE 命令中使用 WHERE...LIKE 子句来指定条件。

### php脚本

```php
$sql_search_like='SELECT * from table1 WHERE author LIKE "su%"';
```

### like 匹配/模糊匹配，会与 **%** 和 **_** 结合使用

```
'%a'     //以a结尾的数据
'a%'     //以a开头的数据
'%a%'    //含有a的数据
'_a_'    //三位且中间字母是a的
'_a'     //两位且结尾字母是a的
'a_'     //两位且开头字母是a的
```

在 where like 的条件查询中，SQL 提供了四种匹配方式。

1. **%**：表示任意 0 个或多个字符。可匹配任意类型和长度的字符，有些情况下若是中文，请使用两个百分号（%%）表示。
2. **_**：表示任意单个字符。匹配单个任意字符，它常用来限制表达式的字符长度语句。
3. **[]**：表示括号内所列字符中的一个（类似正则表达式）。指定一个字符、字符串或范围，要求所匹配对象为它们中的任一个。
4. **[^]** ：表示不在括号所列之内的单个字符。其取值和 [] 相同，但它要求所匹配对象为指定字符以外的任一个字符。
5. 查询内容包含通配符时,由于通配符的缘故，导致我们查询特殊字符 “%”、“_”、“[” 的语句无法正常实现，而把特殊字符用 “[ ]” 括起便可正常查询

## MySQL UNION 操作符

### 语法

```
SELECT expression1, expression2, ... expression_n
FROM tables
[WHERE conditions]
UNION [ALL | DISTINCT]
SELECT expression1, expression2, ... expression_n
FROM tables
[WHERE conditions];
```

- **expression1, expression2, ... expression_n**: 要检索的列。
- **tables:** 要检索的数据表。
- **WHERE conditions:** 可选， 检索条件。
- **DISTINCT:** 可选，删除结果集中重复的数据。默认情况下 UNION 操作符已经删除了重复数据，所以 DISTINCT 修饰符对结果没啥影响。
- **ALL:** 可选，返回所有结果集，包含重复数据。

```mysql
SELECT xxxx FROM table1
WHERE xxx
UNION
SELECT xxxx FROM table2
WHERE xxxx
ORDER BY country;#对结果排序
```



**UNION 语句**：用于将不同表中相同列中查询的数据展示出来；（不包括重复数据）

**UNION ALL 语句**：用于将不同表中相同列中查询的数据展示出来；（包括重复数据）

## MySQL 排序

### 语法

以下是 SQL SELECT 语句使用 ORDER BY 子句将查询数据排序后再返回数据

```
SELECT field1, field2,...fieldN FROM table_name1, table_name2...
ORDER BY field1 [ASC [DESC][默认 ASC]], [field2...] [ASC [DESC][默认 ASC]]
```

- 你可以使用任何字段来作为排序的条件，从而返回排序后的查询结果。
- 你可以设定多个字段来排序。
- 你可以使用 ASC 或 DESC 关键字来设置查询结果是按升序或降序排列。 默认情况下，它是按升序排列。
- 你可以添加 WHERE...LIKE 子句来设置条件。

### 在命令提示符中使用

```mysql
SELECT * from xxx ORDER BY XXX ASC;
SELECT * from xxx ORDER BY XXX DESC;
```

### 在 PHP 脚本中使用 ORDER BY 子句

```php
$sql = 'SELECT id, title, 
        author, submission_date
        FROM XXX_tbl
        ORDER BY  submission_date ASC';
$retval = mysqli_query( $conn, $sql );
```

## MySQL GROUP BY 语句

### GROUP BY 语法

```mysql
SELECT column_name, function(column_name)
FROM table_name
WHERE column_name operator value
GROUP BY column_name;
```

分组的目的是为了统计

一般要使用到一些函数,count(*),

支持多次分组 group by xxx,xxxx

#### 回溯统计

**`with rollup`**

```mysql
SELECT column_name, function(column_name)
FROM table_name
WHERE column_name operator value
GROUP BY column_name
WITH ROLLUP;
```

未使用with rollup

```mysql
count(*) | class | sex    |
+----------+-------+--------+
|        1 | 4     | female |
|        1 | 3     | female |
|        1 | 3     | male   |
|        3 | 2     | male   |
|        1 | 1     | female |
|        1 | 1     | male
```

使用了withrollup

```
count(*) | class | sex    |
+----------+-------+--------+
|        1 | 4     | female |
|        1 | 4     | NULL   |
|        1 | 3     | female |
|        1 | 3     | male   |
|        2 | 3     | NULL   |
|        3 | 2     | male   |
|        3 | 2     | NULL   |
|        1 | 1     | female |
|        1 | 1     | male   |
|        2 | 1     | NULL   |
|        8 | NULL  | NULL
```

## MySQL having

having 语句用于分组语句,在一定程度上与where 相似,

having能做where 几乎所有能做的事,但是where不一定

having在内存中读取(速度慢),且有一点的限制条件

where在磁盘中读取(速度快),几乎不受条件限制

```
select count(*) as c,class,sex from table3 group by class DESC,sex having c<2;
```

## MySQL ORDER BY

+ 可以使用字段
+ 使用排序方式排序

```mysql
select * from table3 ORDER BY class DESC;
```

```mysql
select * from table3 ORDER BY class DESC,id;
```

> 当对子查询使用order by时,需要加上limit关键字

## MySQL limit

> 作用

+ limit可以有效减小服务器的压力与传输压力
+ 实现分页数据

> 方式

+ limit x (从0开始,一共x条)
+ limit x,y(从x+1,到x+y),

```
select * from table3 ORDER BY class DESC;
```

### 限制删除数量

```mysql
delete from tablexxx where xxxx limit xxx;
```

### 限制更新

```mysql
update tablexxx set xxx=xxxx where xxxxx limit xxxxx;
```

## MySQL 清空数据

```mysql
truncate tablexxx;
```

比`delete`删除更彻底,

> 本质是先删除表,再创建表
>
> 能够让表回到原始状态(比如自增长)

## MySQL JOIN连接

在 SELECT, UPDATE 和 DELETE 语句中使用 Mysql 的 JOIN 来联合多表查询

- **INNER JOIN（内连接,或等值连接）**：**可以省略 INNER 使用 JOIN**,获取两个表中字段匹配关系的记录。
- **LEFT JOIN（左连接）：**获取左表所有记录，即使右表没有对应匹配的记录。
- **RIGHT JOIN（右连接）：** 与 LEFT JOIN 相反，用于获取右表所有记录，即使左表没有对应匹配的记录。

### INNER JOIN

```
TABLE_A  A  INNER JOIN TABLE_B B ON A.KEY = B.KEY
```

### LEFT JOIN

```
TABLE_A  A LEFT JOIN TABLE_B B ON A.KEY = B.KEY
```

### RIGHT JOIN

```
TABLE_A A RIGHT TABLE_B B ON  A.KEY = B.KEY
```

### OUTER JOIN(外连接)

```
TABLE_A A FULL 

OUTER JOIN TABLE_B B ON A.KEY = B.KEY
```

### LEFT JOIN EXCLUDING INNER JOIN(左连接 - 内连接)

```
TABLE_A A

LEFT JOIN TABLE_B ON A.KEY = B.KEY WHERE B.KEY IS NULL 
```

### LEFT JOIN EXCLUDING INNER JOIN(左连接 - 内连接)

```
TABLE_A A

RIGHT JOIN TABLE_B B ON A.KEY = B.KEY WHERE A.KEY IS NULL
```

### OUTER JOIN EXCLUDING INNER JOIN (外连接 - 内连接)

```mysql
TABLE_A

FULL OUTER JOIN TABLE_B B ON A.KEY = B.KEY WHERE A.KEY IS NULL OR B.KEY IS NULL
```

### 自然连接

```mysql
select t1.* t2.xxx from table1 t1 natural join table2 t2;
```

自动搜索相同字段,将同名字段合成为一个字段

> 要求字段设计规范

### using

```mysql
select t1.* t2.xxx from table1 t1 left join table2 t2 using(id)
```

using()可以用多个字段作为条件

### php脚本

```
mysqli_query();
```

## 子查询



## MySQL NULL 值处理

- **IS NULL:** 当列的值是 NULL,此运算符返回 true。
- **IS NOT NULL:** 当列的值不为 NULL, 运算符返回 true。
- **<=>:** 比较操作符（不同于 = 运算符），当比较的的两个值相等或者都为 NULL 时返回 true。

### 命令行

```mysql
SELECT * FROM tbl WHERE XXX IS NULL;
SELECT * FROM tbl WHERE XXX IS NOT NULL;
```

### php脚本

```php
if( isset($count ))
{
   $sql = "SELECT author, count
           FROM  test_tbl
           WHERE count = $count";
}
else
{
   $sql = "SELECT author, count
           FROM  tbl
           WHERE count IS NULL";
}
$retval = mysqli_query( $conn, $sql );
```

## MySQL 正则表达式

MySQL 同样也支持其他正则表达式的匹配， MySQL中使用 REGEXP 操作符来进行正则表达式匹配。

| 模式       | 描述                                                         |
| :--------- | :----------------------------------------------------------- |
| ^          | 匹配输入字符串的开始位置。如果设置了 RegExp 对象的 Multiline 属性，^ 也匹配 '\n' 或 '\r' 之后的位置。 |
| $          | 匹配输入字符串的结束位置。如果设置了RegExp 对象的 Multiline 属性，$ 也匹配 '\n' 或 '\r' 之前的位置。 |
| .          | 匹配除 "\n" 之外的任何单个字符。要匹配包括 '\n' 在内的任何字符，请使用象 '[.\n]' 的模式。 |
| [...]      | 字符集合。匹配所包含的任意一个字符。例如， '[abc]' 可以匹配 "plain" 中的 'a'。 |
| [^...]     | 负值字符集合。匹配未包含的任意字符。例如， '[^abc]' 可以匹配 "plain" 中的'p'。 |
| p1\|p2\|p3 | 匹配 p1 或 p2 或 p3。例如，'z\|food' 能匹配 "z" 或 "food"。'(z\|f)ood' 则匹配 "zood" 或 "food"。 |
| *          | 匹配前面的子表达式零次或多次。例如，zo* 能匹配 "z" 以及 "zoo"。* 等价于{0,}。 |
| +          | 匹配前面的子表达式一次或多次。例如，'zo+' 能匹配 "zo" 以及 "zoo"，但不能匹配 "z"。+ 等价于 {1,}。 |
| {n}        | n 是一个非负整数。匹配确定的 n 次。例如，'o{2}' 不能匹配 "Bob" 中的 'o'，但是能匹配 "food" 中的两个 o。 |
| {n,m}      | m 和 n 均为非负整数，其中n <= m。最少匹配 n 次且最多匹配 m 次。 |

### 命令行

```mysql
#查找name字段中以'fu'为开头的所有数据
mysql> SELECT name FROM person_tbl WHERE name REGEXP '^fu';
#查找name字段中以'ck'为结尾的所有数据
mysql> SELECT name FROM person_tbl WHERE name REGEXP 'ck$';
```

## MySQL视图

> 语法

```mysql
create view 视图名(列名1, 列名2, ...) as select 语句;
```

> 显示视图

```mysql
show tables/views;
```



```MySQL
show create view 视图名;
```

> 删除视图

```mysql
drop view 视图名;
```

## MySQL 预处理

>##### 编译过程：

1. 预处理
   预编译一次，可以多次执行。用来解决一条SQL多次执行的问题
2. 编译
   编译最慢。有词法分析、语法分析、简单逻辑分析。
3. 汇编
4. 链接



> 语法

```mysql
prepare 预处理名字 from 'SQL语句';#必须是单引号
prepare stmt from 'select * from stu where stuno=?';#?是占位符
```

> 变量

```mysql
set @sex='男';
```

> 执行

```mysql
execute 预处理名 ;#无变量时
execute 预处理名 using @sex, @addr ;#需要变量时
```





# 子查询

## 标量子查询

## 列子查询

## 行子查询

## 表子查询

## exist子查询

## 比较查询



# 数据字段

## 添加字段

[column]和[position]为可选项

[position]可以是`in first`或者是`after 字段名`,默认是插在最后一行

### 命令行

```mysql
alter table XXX add [column] 字段名 字段类型 [posiotion]
```

### php脚本

```php
$sql='alter table XXX add [column] 字段名 字段类型 [position]';
mysqli_query($conn,$sql);
```

## 修改字段

#### change

一般用来修改字段名

```mysql
alter table xxx change 旧字段名 新字段名 字段类型
```

```php
$sql='alter table xxx change 旧字段名 新字段名 字段类型';
mysqli_query($conn,$sql);
```



#### modify

一般用来修改字段类型,属性,位置

```mysql
alter table xxx modify 字段名 字段类型 [属性] [位置]
```

```
$sql='alter table xxx modify 字段名 字段类型 [属性] [位置]';
mysqli_query($conn,$sql);
```



## 删除字段

### 命令行

```mysql
alter table 表名 drop 字段名
```

### php脚本

```php
$sql='alter table 表名 drop 字段名';
mysqli_query($conn,$sql);
```

# 数据属性

## NULL

```mysql
create table table1(
	id char(10) NOT NULL,
	name char(10) NOT NULL,
	age int NULL;
)
```

标记了NULL的属性的字段,可以为空,

标记了NOT NULL的属性的字段,必须填写,

## default

```mysql
create table table2(
	name char(10) NOT NULL ,
	age int NOT NULL DEFAULT 0
)
```

标记了DEFAULT的属性的字段,可以为空,如果为空,则会自动填充上dafault的值

DEFAULT 可以为NULL,当DEFAULT不为NULL时,相当于设置了NOT NULL

## 主键

```
create table table3(
	id varchar(10) ,
	identify char(18) NOT NULL, 
	PRIMARY KEY ( id )
);
```

​	主键用于索引,具有唯一性,不能重复,并且不能为NULL



## 外键

FOREIGN KEY 约束用于预防破坏表之间连接的动作。

FOREIGN KEY 约束也能防止非法数据插入外键列，因为它必须是它指向的那个表中的值之一

```mysql
CREATE TABLE Orders
(
Id_O int NOT NULL,
OrderNo int NOT NULL,
Id_P int,
PRIMARY KEY (Id_O),
[constraint  Id_P ]FOREIGN KEY (Id_P) REFERENCES Persons(Id_P)#refreshces
)
```

> 添加外键

```mysql
ALTER TABLE Orders ADD FOREIGN KEY (Id_P) REFERENCES Persons(Id_P)
```



> 撤销外键

```mysql
ALTER TABLE Orders DROP FOREIGN KEY fk_PerOrders
```



## 唯一键

> 创建方式

1、直接在表字段之后增加唯一键标识符：unique[key]

2、在所有的字段之后使用unique key（字段列表）;

3、在创建完表之后也可以用增加唯一键 .alter table 表名 add unique key（字段列表）；

> 唯一键效果

**在不为空的情况下，不允许重复**

在查看表创建语句的时候，会看到与主键不同的一点，多出一个“名字”

> 删除唯一键

一个表中允许存在多个唯一键：

删除基本语法：alter table 表名 drop index 唯一键名字；

index代表索引，唯一键是索引的一种（提升查询效率）

> 修改唯一键

先删除后增加

> 复合唯一键

唯一键与主键一样，可以使用多个字段来共同保存唯一性。

一般主键都是单一字段（逻辑字段），而其它需要唯一性的内容都是由唯一键来处理。

## AUTO_INCREMENT

默认地，AUTO_INCREMENT 的开始值是 1，每条新记录递增 1。

> SQL 语法

要让 AUTO_INCREMENT 序列以其他的值起始

并且下一个值为该值加+1

```mysql
ALTER TABLE Persons AUTO_INCREMENT=100
```

MS SQL 执行 auto-increment 任务

```mysql
CREATE TABLE Persons
(
P_Id int PRIMARY KEY AUTO_INCREMENT,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255)
)
```



## COMMENT

为字段添加描述

# 数据新增

## 插入多条数据

```
INSERT INTO table_name  (field1, field2,...fieldN)  VALUES  (valueA1,valueA2,...valueAN),(valueB1,valueB2,...valueBN),(valueC1,valueC2,...valueCN)......;
```

## 蠕虫复制

> copy 数据从一个表到另一个表

```mysql
INSERT INTO 表名 [字段列表] SELECT 字段列表 FROM 表名
```

表结构一致

+ 字段数量匹配

+ 字段类型匹配

> 指数增长

```mysql
INSERT INTO 这张表 SELECT * FROM 这张表
```



## 主键冲突

由于一张表只能有一个主键,当拷贝数据时,可能会出现两个主键的问题

## 忽略新数据

```mysql
INSERT IGNORE INTO tablexxx values (xxxxx);
```

如果冲突,则忽略插入的数据.

## 更新部分数据

```mysql
INSERT INTO tablexxx values (xxxxxx) ON DUPLICATE KEY UPDATE XXXX="xxxx";
```

主键不冲突,则新增,

主键不冲突,则更新,

适用于字段较多

## 全部替换

```mysql
REPLACE INTO tablexxx values ();
```

先检查一遍是否冲突,在插入,如果冲突则先删除,后新增,

适用于字段较少的

# MySQL 事务

事务是必须满足4个条件（ACID）：：原子性（**A**tomicity，或称不可分割性）、一致性（**C**onsistency）、隔离性（**I**solation，又称独立性）、持久性（**D**urability）。

- **原子性：**一个事务（transaction）中的所有操作，要么全部完成，要么全部不完成，不会结束在中间某个环节。事务在执行过程中发生错误，会被回滚（Rollback）到事务开始前的状态，就像这个事务从来没有执行过一样。
- **一致性：**在事务开始之前和事务结束以后，数据库的完整性没有被破坏。这表示写入的资料必须完全符合所有的预设规则，这包含资料的精确度、串联性以及后续数据库可以自发性地完成预定的工作。
- **隔离性：**数据库允许多个并发事务同时对其数据进行读写和修改的能力，隔离性可以防止多个事务并发执行时由于交叉执行而导致数据的不一致。事务隔离分为不同级别，包括读未提交（Read uncommitted）、读提交（read committed）、可重复读（repeatable read）和串行化（Serializable）。
- **持久性：**事务处理结束后，对数据的修改就是永久的，即便系统故障也不会丢失。

### 事务控制语句

- BEGIN 或 START TRANSACTION 显式地开启一个事务；
- COMMIT 也可以使用 COMMIT WORK，不过二者是等价的。COMMIT 会提交事务，并使已对数据库进行的所有修改成为永久性的；
- ROLLBACK 也可以使用 ROLLBACK WORK，不过二者是等价的。回滚会结束用户的事务，并撤销正在进行的所有未提交的修改；
- SAVEPOINT identifier，SAVEPOINT 允许在事务中创建一个保存点，一个事务中可以有多个 SAVEPOINT；
- RELEASE SAVEPOINT identifier 删除一个事务的保存点，当没有指定的保存点时，执行该语句会抛出一个异常；
- ROLLBACK TO identifier 把事务回滚到标记点；
- SET TRANSACTION 用来设置事务的隔离级别。InnoDB 存储引擎提供事务的隔离级别有READ UNCOMMITTED、READ COMMITTED、REPEATABLE READ 和 SERIALIZABLE。

### 事务处理方法

1、用 BEGIN, ROLLBACK, COMMIT来实现

- **BEGIN** 开始一个事务
- **ROLLBACK** 事务回滚
- **COMMIT** 事务确认

2、直接用 SET 来改变 MySQL 的自动提交模式:

- **SET AUTOCOMMIT=0** 禁止自动提交
- **SET AUTOCOMMIT=1** 开启自动提交

```mysql
begin;
#一段代码
SAVEPOINT sp1;
rollback;# 回滚
#一段代码
rollback to sp1;
#一段代码
RELEASE SAVEPOINT sp1;
#commit
```

# 数据管理

## 数据导出

> 语法

```mysql
select *|字段 into outfile 'xxxx.xx' from xxtable;
```

> 选项

+ FIELDS TERMINATED BY  'value' 设置字段之间的分隔符可以为单个或多个字符，默认情况下为制表符“\t”。
+ FIELDS   ENCLOSED   BY   'value'   设置字段的包围字符，只能为单个字符，如果使用了OPTIONALLY  则只包括  CHAR  和  VARCHAR  等字符数据字段
+ FIELDS   ESCAPED   BY   'value'   设置如何写入或读取特殊字符，只能为单个字符，即设置转义字符，默认值为“\”。    
+ LINES   STARTING   BY   'value'    设置每行数据开头的字符，可以为单个或多个字符，默认情况下不使用任何字符。

+ LINES   TERMINATED   BY   'value'   设置每行数据结尾的字符，可以为单个或多个字符，默认值为“\n”。

> demo

```mysql

mysql> SELECT  *  FROM   test_db.person   INTO   OUTFILE   "G:/person1.txt"
    ->   FIELDS
    ->     TERMINATED BY ','
    ->     ENCLOSED BY '\"'
    ->     ESCAPED BY '\''
    ->   LINES
    ->     TERMINATED BY '\r\n';
```



## 数据导入

> 语法

```mysql
LOAD DATA INFILE xxxx INTO TABLE tablename [OPTIONS] [IGNORE number LINES];
```

> 选项

+ FIELDS    TERMINATED    BY    'value'       设置字段之间分隔符，单个或多个字符，默认为'\t'　
+ FIELDS     [OPTIONALLY]    ENCLOSEED   BY    'value'     设置字段包围分隔符，单个字符　　
+ FIELDS     ESCAPED    BY    'value'          如何写入或读取特殊字符，单个字符　
+ LINES    STARTING   BY     'value'           每行数据开头的字符，单个或多个　　
+ LINES    TERMINATED    BY    'value'      每行数据结尾的字符，单个或多个

> demo

```mysql
mysql> LOAD  DATA  INFILE  'G:\fruits.txt' INTO  TABLE test_db.fruits
    -> FIELDS
    ->  TERMINATED BY ','
    -> ENCLOSED BY '\"'
    -> ESCAPED BY '\''
    ->  LINES
    -> TERMINATED BY '\r\n';
```

