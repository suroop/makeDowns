## isset() 函数

**isset()** 函数用于检测变量是否已设置并且非 NULL。

如果一次传入多个参数，那么 isset() 只有在全部参数都被设置时返回 TRUE，计算过程从左至右，中途遇到没有设置的变量时就会立即停止

如果指定变量存在且不为 NULL，则返回 TRUE，否则返回 FALSE

## date() 函数

### 语法

```PHP
string date ( string $format [, int $timestamp ] )
```

| format      | 必需。规定时间戳的格式。                   |
| ----------- | ------------------------------------------ |
| `timestamp` | 可选。规定时间戳。默认是当前的日期和时间。 |

###  格式化日期

```PHP

<?php
echo date("Y/m/d") . "<br>";
echo date("Y.m.d") . "<br>";
echo date("Y-m-d");
?>
```

| *日*                 | ---                                                          | ---                                                          |
| -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| *d*                  | 月份中的第几天，有前导零的 2 位数字                          | *01* 到 *31*                                                 |
| *D*                  | 星期中的第几天，文本表示，3 个字母                           | *Mon* 到 *Sun*                                               |
| *j*                  | 月份中的第几天，没有前导零                                   | *1* 到 *31*                                                  |
| *l*（"L"的小写字母） | 星期几，完整的文本格式                                       | *Sunday* 到 *Saturday*                                       |
| *N*                  | ISO-8601 格式数字表示的星期中的第几天（PHP 5.1.0 新加）      | *1*（表示星期一）到 *7*（表示星期天）                        |
| *S*                  | 每月天数后面的英文后缀，2 个字符                             | *st*，*nd*，*rd* 或者 *th*。可以和 *j* 一起用                |
| *w*                  | 星期中的第几天，数字表示                                     | *0*（表示星期天）到 *6*（表示星期六）                        |
| *z*                  | 年份中的第几天                                               | *0* 到 *365*                                                 |
| *星期*               | ---                                                          |                                                              |
| *W*                  | ISO-8601 格式年份中的第几周，每周从星期一开始（PHP 4.1.0 新加的） | 例如：*42*（当年的第 42 周）                                 |
| *月*                 |                                                              |                                                              |
| *F*                  | 月份，完整的文本格式，例如 January 或者 March                | *January* 到 *December*                                      |
| *m*                  | 数字表示的月份，有前导零                                     | *01* 到 *12*                                                 |
| *M*                  | 三个字母缩写表示的月份                                       | *Jan* 到 *Dec*                                               |
| *n*                  | 数字表示的月份，没有前导零                                   | *1* 到 *12*                                                  |
| *t*                  | 给定月份所应有的天数                                         | *28* 到 *31*                                                 |
| *年*                 | ---                                                          | ---                                                          |
| *L*                  | 是否为闰年                                                   | 如果是闰年为 *1*，否则为 *0*                                 |
| *o*                  | ISO-8601 格式年份数字。这和 *Y* 的值相同，只除了如果 ISO 的星期数（*W*）属于前一年或下一年，则用那一年。（PHP 5.1.0 新加） | Examples: *1999* or *2003*                                   |
| *Y*                  | 4 位数字完整表示的年份                                       | 例如：*1999* 或 *2003*                                       |
| *y*                  | 2 位数字表示的年份                                           | 例如：*99* 或 *03*                                           |
| *时间*               | ---                                                          | ---                                                          |
| *a*                  | 小写的上午和下午值                                           | *am* 或 *pm*                                                 |
| *A*                  | 大写的上午和下午值                                           | *AM* 或 *PM*                                                 |
| *B*                  | Swatch Internet 标准时                                       | *000* 到 *999*                                               |
| *g*                  | 小时，12 小时格式，没有前导零                                | *1* 到 *12*                                                  |
| *G*                  | 小时，24 小时格式，没有前导零                                | *0* 到 *23*                                                  |
| *h*                  | 小时，12 小时格式，有前导零                                  | *01* 到 *12*                                                 |
| *H*                  | 小时，24 小时格式，有前导零                                  | *00* 到 *23*                                                 |
| *i*                  | 有前导零的分钟数                                             | *00* 到 *59*>                                                |
| *s*                  | 秒数，有前导零                                               | *00* 到 *59*>                                                |
| *u*                  | 毫秒 （PHP 5.2.2 新加）。需要注意的是 **date()** 函数总是返回 *000000* 因为它只接受 integer 参数， 而 DateTime::format() 才支持毫秒。 | 示例: *654321*                                               |
| *时区*               | ---                                                          | ---                                                          |
| *e*                  | 时区标识（PHP 5.1.0 新加）                                   | 例如：*UTC*，*GMT*，*Atlantic/Azores*                        |
| *I*                  | 是否为夏令时                                                 | 如果是夏令时为 *1*，否则为 *0*                               |
| *O*                  | 与格林威治时间相差的小时数                                   | 例如：*+0200*                                                |
| *P*                  | 与格林威治时间（GMT）的差别，小时和分钟之间有冒号分隔（PHP 5.1.3 新加） | 例如：*+02:00*                                               |
| *T*                  | 本机所在的时区                                               | 例如：*EST*，*MDT*（【译者注】在 Windows 下为完整文本格式，例如"Eastern Standard Time"，中文版会显示"中国标准时间"）。 |
| *Z*                  | 时差偏移量的秒数。UTC 西边的时区偏移量总是负的，UTC 东边的时区偏移量总是正的。 | *-43200* 到 *43200*                                          |
| *完整的日期／时间*   | ---                                                          | ---                                                          |
| *c*                  | ISO 8601 格式的日期（PHP 5 新加）                            | 2004-02-12T15:19:21+00:00                                    |
| *r*                  | RFC 822 格式的日期                                           | 例如：*Thu, 21 Dec 2000 16:01:07 +0200*                      |
| *U*                  | 从 Unix 纪元（January 1 1970 00:00:00 GMT）开始至今的秒数    | 参见 time()                                                  |

## 包含文件

在 `PHP` 中，您可以在服务器执行 `PHP` 文件之前在该文件中插入一个文件的内容。

include 和 require 语句用于在执行流中插入写在其他文件中的有用的代码

**include 和 require 除了处理错误的方式不同之外，在其他方面都是相同的：**

- require 生成一个致命错误（E_COMPILE_ERROR），在错误发生后脚本会停止执行。
- include 生成一个警告（E_WARNING），在错误发生后脚本会继续执行

假设您有一个标准的页头文件，名为 `"header.php"`。如需在页面中引用这个页头文件，请使用 include/require

```php+HTML
//header.php
$color='red';
$car='BMW';
echo '<a href="/">主页</a>
<a href="/html">HTML 教程</a>
<a href="/php">PHP 教程</a>';
```



```php+HTML
//body.php
<html>
<head>
<meta charset="utf-8">
</head>
<body>

<?php include 'header.php';
    echo "I have a $color $car"; // I have a red BMW
    ?>
<h1>欢迎来到我的主页!</h1>
<p>一些文本。</p>

</body>
</html>
```



## 文件处理

### 打开文件

`fopen()` 函数用于在 `PHP` 中打开文件

```php+HTML
<html>
<body>

<?php
$file=fopen("filename","r");
?>

</body>
</html>
```

文件可能通过下列模式来打开

| 模式 | 描述                                                         |
| :--- | :----------------------------------------------------------- |
| r    | 只读。在文件的开头开始。                                     |
| r+   | 读/写。在文件的开头开始。                                    |
| w    | 只写。打开并清空文件的内容；如果文件不存在，则创建新文件。   |
| w+   | 读/写。打开并清空文件的内容；如果文件不存在，则创建新文件。  |
| a    | 追加。打开并向文件末尾进行写操作，如果文件不存在，则创建新文件。 |
| a+   | 读/追加。通过向文件末尾写内容，来保持文件内容。              |
| x    | 只写。创建新文件。如果文件已存在，则返回 FALSE 和一个错误。  |
| x+   | 读/写。创建新文件。如果文件已存在，则返回 FALSE 和一个错误。 |

这样处理打开文件比较好

```php
<?php
$file=fopen("welcome.txt","r") or exit("Unable to open file!");
?>
```



### 关闭文件

在打开文件之后需要关闭文件

```php
<?php
$file = fopen("test.txt","r");

//执行一些代码

fclose($file);
?>
```



### 检测文件末尾

`feof() `函数检测是否已到达文件末尾`（EOF)`

+ 在 w 、a 和 x 模式下，您无法读取打开的文件

```php
if (feof($file)) echo "文件结尾";//return true
```



### 逐行读取文件

`fgets()` 函数用于从文件中逐行读取文件。

**注释：**在调用该函数之后，文件指针会移动到下一行

```php
<?php
$file = fopen("welcome.txt", "r") or exit("无法打开文件!");
// 读取文件每一行，直到文件结尾
while(!feof($file))
{
    echo fgets($file). "<br>";
}
fclose($file);
?>
```



### 逐字符读取文件

`fgetc() `函数用于从文件中逐字符地读取文件。

**注释：**在调用该函数之后，文件指针会移动到下一个字符

```php
<?php
$file=fopen("welcome.txt","r") or exit("无法打开文件!");
while (!feof($file))
{
    echo fgetc($file);
}
fclose($file);
?>
```



## 文件上传

- 标签的 **`enctype `**属性规定了在提交表单时要使用哪种内容类型。在表单需要二进制数据时，比如文件内容，请使用**` "multipart/form-data"`**。

- 标签的 **type="file"** 属性规定了应该把输入作为文件来处理。举例来说，当在浏览器中预览时，会看到输入框旁边有一个浏览按钮

- 通过使用 PHP 的全局数组 $_FILES，你可以从客户计算机向远程服务器上传文件。

  第一个参数是表单的 input name，第二个下标可以是 "name"、"type"、"size"、"tmp_name" 或 "error"。如下所示：

  + $_FILES\["file"]["name"] - 上传文件的名称
  + $_FILES\["file"]["type"] - 上传文件的类型
  + $_FILES\["file"]["size"] - 上传文件的大小，以字节计
  + $_FILES\["file"]["tmp_name"] - 存储在服务器的文件的临时副本的名称
  + $_FILES\["file"]["error"] - 由文件上传导致的错误代码

### 创建上传脚本

```php
<?php
if ($_FILES["file"]["error"] > 0)
{
    echo "错误：" . $_FILES["file"]["error"] . "<br>";
}
else
{
    echo "上传文件名: " . $_FILES["file"]["name"] . "<br>";
    echo "文件类型: " . $_FILES["file"]["type"] . "<br>";
    echo "文件大小: " . ($_FILES["file"]["size"] / 1024) . " kB<br>";
    echo "文件临时存储的位置: " . $_FILES["file"]["tmp_name"];
}
?>
```



### 上传限制

```php
<?php
// 允许上传的图片后缀
$allowedExts = array("gif", "jpeg", "jpg", "png");
$temp = explode(".", $_FILES["file"]["name"]);
$extension = end($temp);        // 获取文件后缀名
if ((($_FILES["file"]["type"] == "image/gif")
|| ($_FILES["file"]["type"] == "image/jpeg")
|| ($_FILES["file"]["type"] == "image/jpg")
|| ($_FILES["file"]["type"] == "image/pjpeg")
|| ($_FILES["file"]["type"] == "image/x-png")
|| ($_FILES["file"]["type"] == "image/png"))
&& ($_FILES["file"]["size"] < 204800)    // 小于 200 kb
&& in_array($extension, $allowedExts))
{
    if ($_FILES["file"]["error"] > 0)
    {
        echo "错误：: " . $_FILES["file"]["error"] . "<br>";
    }
    else
    {
        echo "上传文件名: " . $_FILES["file"]["name"] . "<br>";
        echo "文件类型: " . $_FILES["file"]["type"] . "<br>";
        echo "文件大小: " . ($_FILES["file"]["size"] / 1024) . " kB<br>";
        echo "文件临时存储的位置: " . $_FILES["file"]["tmp_name"];
    }
}
else
{
    echo "非法的文件格式";
}
?>
```

### 保存被上传的文件

这个临时的副本文件会在脚本结束时消失。要保存被上传的文件，我们需要把它拷贝到另外的位置

## cookie

### 创建cookie

setcookie() 函数用于设置 cookie。

**语法**

```PHP
setcookie(name, value, expire, path, domain);
```

**注释：**setcookie() 函数必须位于 <html> 标签之前

```php+HTML
<?php
setcookie("user", "runoob", time()+3600);
?>

<html>
```

###  获取Cookie 的值

PHP 的 $_COOKIE 变量用于取回 cookie 的值

```PHP
<?php
// 输出 cookie 值
echo $_COOKIE["user"];

// 查看所有 cookie
print_r($_COOKIE);
?>
```

### 如何删除 Cookie

当删除 cookie 时，使过期日期变更为过去的时间点

```
<?php
// 设置 cookie 过期时间为过去 1 小时
setcookie("user", "", time()-3600);
?>
```



## session

对话

## email

### 参数

| 参数       | 描述                                                         |
| :--------- | :----------------------------------------------------------- |
| to         | 必需。规定 email 接收者。                                    |
| subject    | 必需。规定 email 的主题。**注释：**该参数不能包含任何新行字符。 |
| message    | 必需。定义要发送的消息。应使用 (\n) 来分隔各行。每行应该限制在 70 个字符内。 |
| headers    | 可选。规定附加的标题，比如 From。应当使用 (\r\n) 分隔附加的标题。 |
| parameters | 可选。对邮件发送程序规定额外的参数。                         |

### 封装

```PHP
<?php
$to = "someone@example.com";         // 邮件接收者
$subject = "参数邮件";                // 邮件标题
$message = "Hello! 这是邮件的内容。";  // 邮件正文
$from = "someonelse@example.com";   // 邮件发送者
$headers = "From:" . $from;         // 头部信息设置
mail($to,$subject,$message,$headers);
echo "邮件已发送";
?>
```

### email

```php+HTML
<html>
<head>
<meta charset="utf-8">
</head>
<body>
<form method='post' action='mailform.php'>
    Email: <input name='email' type='text'><br>
    Subject: <input name='subject' type='text'><br>
    Message:<br>
    <textarea name='message' rows='15' cols='40'>
    </textarea><br>
    <input type='submit'>
    </form>
<?php
if (isset($_REQUEST['email'])) { // 如果接收到邮箱参数则发送邮件
    // 发送邮件
    $email = $_REQUEST['email'] ;
    $subject = $_REQUEST['subject'] ;
    $message = $_REQUEST['message'] ;
    mail("someone@example.com", $subject,
    $message, "From:" . $email);
    echo "邮件发送成功";
} else { // 如果没有邮箱参数则显示表单
    echo "<form method='post' action='mailform.php'>
    Email: <input name='email' type='text'><br>
    Subject: <input name='subject' type='text'><br>
    Message:<br>
    <textarea name='message' rows='15' cols='40'>
    </textarea><br>
    <input type='submit'>
    </form>";
}
?>

</body>
</html>
```

以上代码存在的问题是，未经授权的用户可通过输入表单在邮件头部插入数据。

假如用户在表单中的输入框内加入如下文本到电子邮件中，会出现什么情况呢

+ `someone@example.com%0ACc:person2@example.com`
+ `%0ABcc:person3@example.com,person3@example.com`
+ `anotherperson4@example.com,person5@example.com`
+ `%0ABTo:person6@example.com`

与往常一样，mail() 函数把上面的文本放入邮件头部，那么现在头部有了额外的 Cc:和 To: 字段。当用户点击提交按钮时，这封 e-mail 会被发送到上面所有的地址

```php+HTML
<html>
<head>
<meta charset="utf-8">
</head>
<body>
<?php
    function spamcheck($field)
    {
        // filter_var() 过滤 e-mail
        // 使用 FILTER_SANITIZE_EMAIL
        $field=filter_var($field, FILTER_SANITIZE_EMAIL);

        //filter_var() 过滤 e-mail
        // 使用 FILTER_VALIDATE_EMAIL
        if(filter_var($field, FILTER_VALIDATE_EMAIL))
        {
            return TRUE;
        }
        else
        {
            return FALSE;
        }
    }

    if (isset($_REQUEST['email']))
    {
        // 如果接收到邮箱参数则发送邮件

        // 判断邮箱是否合法
        $mailcheck = spamcheck($_REQUEST['email']);
        if ($mailcheck==FALSE)
        {
            echo "非法输入";
        }
        else
        {    
            // 发送邮件
            $email = $_REQUEST['email'] ;
            $subject = $_REQUEST['subject'] ;
            $message = $_REQUEST['message'] ;
            mail("someone@example.com", "Subject: $subject",
            $message, "From: $email" );
            echo "Thank you for using our mail form";
        }
    }
    else
    { 
        // 如果没有邮箱参数则显示表单
        echo "<form method='post' action='mailform.php'>
        Email: <input name='email' type='text'><br>
        Subject: <input name='subject' type='text'><br>
        Message:<br>
        <textarea name='message' rows='15' cols='40'>
        </textarea><br>
        <input type='submit'>
        </form>";
    }
?>

</body>
</html>
```



## error(错误)

### die() 函数

基本的错误处理:"die()" 语句

```php
<?php
	$file=fopen("welcome.txt","r");
?>
```

如果文件不存在，会得到类似这样的错误：

```
Warning: fopen(welcome.txt) [function.fopen]: failed to open stream:
No such file or directory in /www/runoob/test/test.php on line 2
```

使用die()做一些简单的处理

```php
<?php
if(!file_exists("welcome.txt"))
{
    die("文件不存在");
}
else
{
    $file=fopen("welcome.txt","r");
}
?>
```

如果文件不存在，会得到类似这样的错误消息

```
文件不存在
```

### 创建自定义错误处理器

创建一个自定义的错误处理器非常简单。创建了一个专用函数，可以在 PHP 中发生错误时调用该函数

#### 语法

```php
error_function(error_level,error_message,error_file,error_line,error_context)
```

| 参数          | 描述                                                         |
| :------------ | :----------------------------------------------------------- |
| error_level   | 必需。为用户定义的错误规定错误报告级别。必须是一个数字。参见下面的表格：错误报告级别。 |
| error_message | 必需。为用户定义的错误规定错误消息。                         |
| error_file    | 可选。规定错误发生的文件名。                                 |
| error_line    | 可选。规定错误发生的行号。                                   |
| error_context | 可选。规定一个数组，包含了当错误发生时在用的每个变量以及它们的值。 |

### 设置错误处理程序

PHP 的默认错误处理程序是内建的错误处理程序。我们打算把上面的函数改造为脚本运行期间的默认错误处理程序

**`set_error_handler `**— 设置用户自定义的错误处理函数

set_error_handler() 仅需要一个参数，可以添加第二个参数来规定错误级别

```php
    /*第一个参数接收错误等级,第二个接收错误发送的信息*/
function customError($errno,$errstr)
{
    echo "<b>Error:</b> [$errno] $errstr<br>";
    echo "脚本结束";
    die();
}
set_error_handler("customError");
```





#### 错误报告级别

| 值   | 常量                | 描述                                                         |
| :--- | :------------------ | :----------------------------------------------------------- |
| 2    | E_WARNING           | 非致命的 run-time 错误。不暂停脚本执行。                     |
| 8    | E_NOTICE            | run-time 通知。在脚本发现可能有错误时发生，但也可能在脚本正常运行时发生。 |
| 256  | E_USER_ERROR        | 致命的用户生成的错误。这类似于程序员使用 PHP 函数 trigger_error() 设置的 E_ERROR。 |
| 512  | E_USER_WARNING      | 非致命的用户生成的警告。这类似于程序员使用 PHP 函数 trigger_error() 设置的 E_WARNING。 |
| 1024 | E_USER_NOTICE       | 用户生成的通知。这类似于程序员使用 PHP 函数 trigger_error() 设置的 E_NOTICE。 |
| 4096 | E_RECOVERABLE_ERROR | 可捕获的致命错误。类似 E_ERROR，但可被用户定义的处理程序捕获。（参见 set_error_handler()） |
| 8191 | E_ALL               | 所有错误和警告。（在 PHP 5.4 中，E_STRICT 成为 E_ALL 的一部分） |



### 触发错误

在脚本中用户输入数据的位置，当用户的输入无效时触发错误是很有用的。在 PHP 中，这个任务由 trigger_error() 函数完成

```php
<?php
$test=2;
if ($test>1)
{
    trigger_error("变量值必须小于等于 1");
}
/*Notice: 变量值必须小于等于 1
  in /www/test/runoob.php on line 5*/
?>
```



### 错误记录

在默认的情况下，根据在 `php.ini` 中的 error_log 配置，PHP 向服务器的记录系统或文件发送错误记录。通过使用 `error_log()` 函数，您可以向指定的文件或远程目的地发送错误记录。

通过电子邮件向您自己发送错误消息，是一种获得指定错误的通知的好办法。

## Exception(异常)

异常用于在指定的错误发生时改变脚本的正常流程

类C++异常

### 异常的基本使用

使用Try、throw 和 catch语句

1. Try - 使用异常的函数应该位于 "try" 代码块内。如果没有触发异常，则代码将照常继续执行。但是如果异常被触发，会抛出一个异常。
2. Throw - 里规定如何触发异常。每一个 "throw" 必须对应至少一个 "catch"。
3. Catch - "catch" 代码块会捕获异常，并创建一个包含异常信息的对象。

```php
<?php
    funciton check($num){
    if($num==0){
        throw new Exception("变量为1");
    }
}
try{
    check(0);
    // 如果抛出异常，以下文本不会输出
    echo '如果输出该内容，说明 $number 变量';
}
catch(Exception $e){
    echo "emmmm".$e->getMessage();
}
    ?>
```

遵循 "每个 throw 必须对应一个 catch" 的原则

1. 创建 checkNum() 函数。它检测数字。如果是，则抛出一个异常。
2. 在 "try" 代码块中调用 checkNum() 函数。
3. checkNum() 函数中的异常被抛出。
4. "catch" 代码块接收到该异常，并创建一个包含异常信息的对象 ($e)。
5. 通过从这个 exception 对象调用 $e->getMessage()，输出来自该异常的错误消息

### 创建一个自定义的 Exception 类

该类必须是 exception 类的一个扩展。

这个自定义的 myException 类继承了 PHP 的 exception 类的所有属性，可向其添加自定义的函数。

```php
<?php
    class myException extends Exception{
     $errorMsg = '错误行号 '.$this->getLine().' in '.$this->getFile()
        .': <b>'.$this->getMessage().'</b> 不是一个合法的 E-Mail 地址';
        return $errorMsg;
	}
    function check($email){
        if(xxxx){
            throw new myException($email); 
        }
    try{
        check("xxxxx");
    }    
    catch(myException $e){
        echo $this->errorMsg;
    }
    }
    ?>
```



这个新的类是旧的 exception 类的副本，外加 errorMessage。正因为它是旧类的副本，因此它从旧类继承了属性和方法，我们可以使用 exception 类的方法，比如 getLine()、getFile() 和 getMessage()

1. customException() 类是作为旧的 exception 类的一个扩展来创建的。这样它就继承了旧的 exception 类的所有属性和方法。
2. 创建 errorMessage() 函数。如果 e-mail 地址不合法，则该函数返回一条错误消息。
3. 把 $email 变量设置为不合法的 e-mail 地址字符串。
4. 执行 "try" 代码块，由于 e-mail 地址不合法，因此抛出一个异常。
5. "catch" 代码块捕获异常，并显示错误消息。

### 多个异常

可以使用多个 if..else 代码块，或一个 switch 代码块，或者嵌套多个异常。这些异常能够使用不同的 exception 类，并返回不同的错误消息

```php
<?php
    class myException extends Exception{
     $errorMsg = '错误行号 '.$this->getLine().' in '.$this->getFile()
        .': <b>'.$this->getMessage().'</b> 不是一个合法的 E-Mail 地址';
        return $errorMsg;
	}
    function check($email){
        if(xxxx){
            throw new myException($email); 
        }
        else if(xxx){
        	throw new Exception("{$email} is not a email");
        }
    }
    try{
        check("xxxxx");
    }
    catch(myException $e){
        echo $this->errorMsg;
    }
    catch(Exception $e){
    	echo $this->getmessage();
    }
    ?>
```

1. myException() 类是作为旧的 exception 类的一个扩展来创建的。这样它就继承了旧的 exception 类的所有属性和方法。
2. 创建 errorMessage。如果 e-mail 地址不合法，则该函数返回一个错误消息。
3. 把 $email 变量设置为一个字符串，该字符串是一个有效的 e-mail 地址，但包含字符串 "example"。
4. 执行 "try" 代码块，在第一个条件下，不会抛出异常。
5. 由于 e-mail 含有字符串 "example"，第二个条件会触发异常。
6. "catch" 代码块会捕获异常，并显示恰当的错误消息。

如果 myException 类抛出了异常，但没有捕获 myException，仅仅捕获了 base exception，则在base exception那里处理异常

### 设置顶层异常处理器

set_exception_handler() 函数可设置处理所有未捕获异常的用户定义函数

```php
<?php
function myException($exception)
{
    echo "<b>Exception:</b> " , $exception->getMessage();
}
 
set_exception_handler('myException');
 
throw new Exception('Uncaught Exception occurred');
?>
```



### 异常的规则

- 需要进行异常处理的代码应该放入 try 代码块内，以便捕获潜在的异常。
- 每个 try 或 throw 代码块必须至少拥有一个对应的 catch 代码块。
- 使用多个 catch 代码块可以捕获不同种类的异常。
- 可以在 try 代码块内的 catch 代码块中抛出（再次抛出）异常。

简而言之：如果抛出了异常，就必须捕获它。

## 过滤器

PHP 过滤器用于验证和过滤来自非安全来源的数据，比如用户的输入

### 什么是 PHP 过滤器

PHP 过滤器用于验证和过滤来自非安全来源的数据。

测试、验证和过滤用户输入或自定义数据是任何 Web 应用程序的重要组成部分。

PHP 的过滤器扩展的设计目的是使数据过滤更轻松快捷

### 为什么使用过滤器

通过使用过滤器，您能够确保应用程序获得正确的输入类型

#### 什么是外部数据

- 来自表单的输入数据
- Cookies
- Web services data
- 服务器变量
- 数据库查询结果

### 函数和过滤器

- filter_var() - 通过一个指定的过滤器来过滤单一的变量
- filter_var_array() - 通过相同的或不同的过滤器来过滤多个变量
- filter_input - 获取一个输入变量，并对它进行过滤
- filter_input_array - 获取多个输入变量，并通过相同的或不同的过滤器对它们进行过滤

### Validating 和 Sanitizing

Validating 过滤器：

- 用于验证用户输入
- 严格的格式规则（比如 URL 或 E-Mail 验证）
- 如果成功则返回预期的类型，如果失败则返回 FALSE

Sanitizing 过滤器：

- 用于允许或禁止字符串中指定的字符
- 无数据格式规则
- 始终返回字符串

### Filter函数

+ filter_has_var()先输入值,

+ filter_input()先输入类型

| 函数                                                         | 描述                                     | PHP  |
| :----------------------------------------------------------- | :--------------------------------------- | :--- |
| [filter_has_var()](https://www.runoob.com/php/func-filter-has-var.html) | 检查是否存在指定输入类型的变量。         | 5    |
| [filter_id()](https://www.runoob.com/php/func-filter-id.html) | 返回指定过滤器的 ID 号。                 | 5    |
| [filter_input()](https://www.runoob.com/php/func-filter-input.html) | 从脚本外部获取输入，并进行过滤。         | 5    |
| [filter_input_array()](https://www.runoob.com/php/func-filter-input-array.html) | 从脚本外部获取多项输入，并进行过滤。     | 5    |
| [filter_list()](https://www.runoob.com/php/func-filter-list.html) | 返回包含所有得到支持的过滤器的一个数组。 | 5    |
| [filter_var_array()](https://www.runoob.com/php/func-filter-var-array.html) | 获取多个变量，并进行过滤。               | 5    |
| [filter_var()](https://www.runoob.com/php/func-filter-var.html) | 获取一个变量，并进行过滤。               | 5    |

### 过滤器

| FILTER_CALLBACK                                              | 调用用户自定义函数来过滤数据。                               |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| FILTER_SANITIZE_STRING                                       | 去除标签，去除或编码特殊字符。                               |
| FILTER_SANITIZE_STRIPPED                                     | "string" 过滤器的别名。                                      |
| [FILTER_SANITIZE_ENCODED](https://www.runoob.com/php/filter-sanitize-encoded.html) | URL-encode 字符串，去除或编码特殊字符。                      |
| [FILTER_SANITIZE_SPECIAL_CHARS](https://www.runoob.com/php/filter-sanitize-special-chars.html) | HTML 转义字符 '"<>& 以及 ASCII 值小于 32 的字符。            |
| [FILTER_SANITIZE_EMAIL](https://www.runoob.com/php/filter-sanitize-email.html) | 删除所有字符，除了字母、数字以及 !#$%&'*+-/=?^_`{\|}~@.[]    |
| [FILTER_SANITIZE_URL](https://www.runoob.com/php/filter-sanitize-url.html) | 删除所有字符，除了字母、数字以及 $-_.+!*'(),{}\|\^~[]`<>#%";/?:@&= |
| [FILTER_SANITIZE_NUMBER_INT](https://www.runoob.com/php/filter-sanitize-number-int.html) | 删除所有字符，除了数字和 +-                                  |
| [FILTER_SANITIZE_NUMBER_FLOAT](https://www.runoob.com/php/filter-sanitize-number-float.html) | 删除所有字符，除了数字、+- 以及 .,eE                         |
| [FILTER_SANITIZE_MAGIC_QUOTES](https://www.runoob.com/php/filter-sanitize-magic-quotes.html) | 应用 addslashes()。                                          |
| [FILTER_UNSAFE_RAW](https://www.runoob.com/php/filter-unsafe-raw.html) | 不进行任何过滤，去除或编码特殊字符。                         |
| [FILTER_VALIDATE_INT](https://www.runoob.com/php/filter-validate-int.html) | 把值作为整数来验证。                                         |
| [FILTER_VALIDATE_BOOLEAN](https://www.runoob.com/php/filter-validate-boolean.html) | 把值作为布尔选项来验证。如果是 "1"、"true"、"on" 和 "yes"，则返回 TRUE。如果是 "0"、"false"、"off"、"no" 和 ""，则返回 FALSE。否则返回 NULL。 |
| [FILTER_VALIDATE_FLOAT](https://www.runoob.com/php/filter-validate-float.html) | 把值作为浮点数来验证。                                       |
| [FILTER_VALIDATE_REGEXP](https://www.runoob.com/php/filter-validate-regexp.html) | 根据 regexp（一种兼容 Perl 的正则表达式）来验证值。          |
| [FILTER_VALIDATE_URL](https://www.runoob.com/php/filter-validate-url.html) | 把值作为 URL 来验证。                                        |
| [FILTER_VALIDATE_EMAIL](https://www.runoob.com/php/filter-validate-email.html) | 把值作为 e-mail 地址来验证。                                 |
| [FILTER_VALIDATE_IP](https://www.runoob.com/php/filter-validate-ip.html) | 把值作为 IP 地址来验证，只限 IPv4 或 IPv6 或 不是来自私有或者保留的范围。 |

### 使用 Filter Callback

 通过使用 FILTER_CALLBACK 过滤器，可以调用自定义的函数，把它作为一个过滤器来使用。

可以创建自己的自定义函数，也可以使用已存在的 PHP 函数

```php
<?php
    function convertSpace($string)
    {
        return str_replace("_", ".", $string);
    }

    $string = "www_google_com!";

    echo filter_var($string, FILTER_CALLBACK,
    array("options"=>"convertSpace"));
?>
```



## 高级过滤器

### 检测一个数字是否在一个范围内

### 检测 IPv6 地址

### 检测 URL - 必须包含QUERY_STRING（查询字符串）

### 移除 ASCII 值大于 127 的字符

## `JSON`

### JSON 函数

| 函数            | 描述                                          |
| :-------------- | :-------------------------------------------- |
| json_encode     | 对变量进行 JSON 编码                          |
| json_decode     | 对 JSON 格式的字符串进行解码，转换为 PHP 变量 |
| json_last_error | 返回最后发生的错误                            |

### `josn_encode()`

```php
<?php
   $arr = array('a' => 1, 'b' => 2, 'c' => 3, 'd' => 4, 'e' => 5);
   echo json_encode($arr);
?>
    //{"a":1,"b":2,"c":3,"d":4,"e":5}
```

### `josn_decode()`

**参数**

- **json_string**: 待解码的 JSON 字符串，必须是 UTF-8 编码数据
- **assoc**: 当该参数为 TRUE 时，将返回数组，FALSE 时返回对象。
- **depth**: 整数类型的参数，它指定递归深度
- **options**: 二进制掩码，目前只支持 JSON_BIGINT_AS_STRING 。

```php
<?php
   $json = '{"a":1,"b":2,"c":3,"d":4,"e":5}';

   json_decode($json);
   json_decode($json, true);
/*
	{
    ["a"] => int(1)
    ["b"] => int(2)
    ["c"] => int(3)
    ["d"] => int(4)
    ["e"] => int(5)
	}
*/
/*
	["a"] => int(1)
    ["b"] => int(2)
    ["c"] => int(3)
    ["d"] => int(4)
    ["e"] => int(5)
*/
?>
```



#### 拓展

##### JSON 与 JS 对象的关系

JSON 是 JS 对象的字符串表示法，它使用文本表示一个 JS 对象的信息，本质是一个字符串

```javascript
var obj = {a: 'Hello', b: 'World'}; 
//这是一个对象，注意键名也是可以使用引号包裹的
var json ='{"a": "Hello", "b": "World"}'; 
//这是一个 JSON 字符串，本质是一个字符串
```

##### JSON 和 JS 对象互转

要实现从JSON字符串转换为JS对象，使用 JSON.parse() 方法

```javascript
var obj = JSON.parse('{"a": "Hello", "b": "World"}'); 
//结果是 {a: 'Hello', b: 'World'}
```

要实现从JS对象转换为JSON字符串，使用 JSON.stringify() 方法

```javascript
var json = JSON.stringify({a: 'Hello', b: 'World'}); 
//结果是 '{"a": "Hello", "b": "World"}'
```

