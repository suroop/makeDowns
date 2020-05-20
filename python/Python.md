# Python

## 基础语法

> 标识符

- 第一个字符必须是字母表中字母或下划线 **_** 。
- 标识符的其他的部分由字母、数字和下划线组成。
- 标识符对大小写敏感。

> 保留字

```python
import keyword
keyword.kwlist
#即可查看所有保留字
```



> 注释

+ 单行注释以 **#** 开头

```python
# 一个注释跟mysql相同
```



+ 多行注释可以用多个 **#** 号，还有 **'''** 和 **"""**

```python
#注
#释
'''
注释
注释
'''
"""
也是注释
也是注释
"""
```





> 缩进

同一个代码块的语句必须包含相同的缩进空格数

```python
for i in range(1,100)
	if i<50:
        print(i)
    else:
        print("i>50")
```



> 多行语句

语句很长,可以使用反斜杠(\)来实现多行语句

```python
text="hello"+\
	"python"
```



在 [], {}, 或 () 中的多行语句，不需要使用反斜杠(\)

```python
text=['java','C++',
'python','javascript'
]
```



> input

执行下面的程序在按回车键后就会等待用户输入：

```python
input("这里是提示窗口,按下enter后执行")
```



> output

print 默认输出是换行的

```python
print("括号里的填要输出的内容")
```



如果要实现不换行需要在变量末尾加上 **end=""**：

```python
print("在这段话以后填上",end=" ")
```



> 同一行显示多条语句

同一行中使用多条语句，语句之间使用分号(;)分割

```python
num=0;str="hello python"
```

## 数据类型

Python 中的变量不需要声明。每个变量在使用前都必须赋值，变量赋值以后该变量才会被创建.

类似于JS、php等弱语言,它没有类型

```python
num1=45
str="hello python"
num2=45.5
```

> 标准数据类型

- Number（数字）
- String（字符串）
- List（列表）
- Tuple（元组）
- Set（集合）
- Dictionary（字典）

内置的 type() 函数可以用来查询变量所指的对象类型

### number

Python3 支持 **int、float、bool、complex（复数）**

```python
num1=45
type(num1)
#<class 'int'>
num2=45.5
type(num2)
#<class 'float'>
```

### String

Python中的字符串用单引号 **'** 或双引号 **"** 括起来，同时使用反斜杠 \\转义特殊字符

> 截取

变量[头下标:尾下标] 

note:-1表示最后一个字符,-2表示倒数第二个字符,以此类推



```python
str1="hello python"
str2=str1[0:4]
#hello
str3=str2[6:-1]
#python
```



加号 **+** 是字符串的连接符， 星号 ***** 表示复制当前字符串，与之结合的数字为复制的次数

### List

列表是写在方括号 **[]** 之间、用逗号分隔开的元素列表

类似于数组

```python
list=['hello',45,"python",56.5]
```

> 截取

```python
list=['hello',45,"python",56.5]
print(list[1:3])
print(list[2:3])
print(list[2:-1])
```

> 访问

```python
list=['hello',45,"python",56.5]
str1=list[0]
#hello
newlist=list[0:2]
#['hello',45,'python']
list
#'hello',45,"python",56.5
```

> 赋值

```python
list=['hello',45,"python",56.5]
list[2]="java"
list[0:2]=['php','mysql',65]
list=[]
```



### Tuple

元组（tuple）与列表类似，不同之处在于元组的元素不能修改

组写在小括号 **()** 里，元素之间用逗号隔开

```python
tuple=('hello',45,"python",56.5)
tuple[0]='java'#error
```

+ 元组可以访问,但是不可以被修改

### Set

集合（set）是由一个或数个形态各异的大小整体组成的，构成集合的事物或对象称作元素或是成员

可以使用大括号 **{ }** 或者 **set()** 函数创建集合

```python
member1={'Tom', 'Jim', 'Mary'}
member2={'Tom', 'Jack', 'Rose'}
```

> 集合运算

```python
member1={'Tom', 'Jim', 'Mary'}
member2={'Tom', 'Jack', 'Rose'}
print(member1)
print(member1 - member2)#差集
print(member1 | member2)#并集
print(member1 & member2)#交集
print(member1 ^ member2)#不同时存在的元素
```

### Dictionary

+ 字典（dictionary）是Python中另一个非常有用的内置数据类型

+ 列表是有序的对象集合，字典是无序的对象集合。两者之间的区别在于：字典当中的元素是通过键来存取的，而不是通过偏移存取

+ 字典用 **{ }** 标识，它是一个无序的 **键(key) : 值(value)** 的集合

+ 类似于 php关联数组

```python
dict={}#空的字典
dict={'name'='surp','age'='55','wage'='20000'}
dict[class]=2
dict[2]='number'
print(dict)#完整字典
print(dict[2])#输出键为 2 的值
print(dict[name])#输出键为 'name' 的值
print(dict.key())#输出所有键
print(dict.values())#输出所有值
```

### 数据类型转换

| 函数                                                         | 描述                                                |
| :----------------------------------------------------------- | :-------------------------------------------------- |
| [int(x [,base\])](https://www.runoob.com/python3/python-func-int.html) | 将x转换为一个整数                                   |
| [float(x)](https://www.runoob.com/python3/python-func-float.html) | 将x转换到一个浮点数                                 |
| [complex(real [,imag\])](https://www.runoob.com/python3/python-func-complex.html) | 创建一个复数                                        |
| [str(x)](https://www.runoob.com/python3/python-func-str.html) | 将对象 x 转换为字符串                               |
| [repr(x)](https://www.runoob.com/python3/python-func-repr.html) | 将对象 x 转换为表达式字符串                         |
| [eval(str)](https://www.runoob.com/python3/python-func-eval.html) | 用来计算在字符串中的有效Python表达式,并返回一个对象 |
| [tuple(s)](https://www.runoob.com/python3/python3-func-tuple.html) | 将序列 s 转换为一个元组                             |
| [list(s)](https://www.runoob.com/python3/python3-att-list-list.html) | 将序列 s 转换为一个列表                             |
| [set(s)](https://www.runoob.com/python3/python-func-set.html) | 转换为可变集合                                      |
| [dict(d)](https://www.runoob.com/python3/python-func-dict.html) | 创建一个字典。d 必须是一个 (key, value)元组序列。   |
| [frozenset(s)](https://www.runoob.com/python3/python-func-frozenset.html) | 转换为不可变集合                                    |
| [chr(x)](https://www.runoob.com/python3/python-func-chr.html) | 将一个整数转换为一个字符                            |
| [ord(x)](https://www.runoob.com/python3/python-func-ord.html) | 将一个字符转换为它的整数值                          |
| [hex(x)](https://www.runoob.com/python3/python-func-hex.html) | 将一个整数转换为一个十六进制字符串                  |
| [oct(x)](https://www.runoob.com/python3/python-func-oct.html) | 将一个整数转换为一个八进制字符串                    |

## 运算符

### 算术运算符

| 运算符 | 描述                                            |
| :----- | :---------------------------------------------- |
| +      | 加 - 两个对象相加                               |
| -      | 减 - 得到负数或是一个数减去另一个数             |
| *      | 乘 - 两个数相乘或是返回一个被重复若干次的字符串 |
| /      | 除 - x 除以 y                                   |
| %      | 取模 - 返回除法的余数                           |
| **     | 幂 - 返回x的y次幂                               |
| //     | 取整除 - 向下取接近商的整数                     |

### 比较运算符

| 运算符 | 描述                                                         |
| ------ | ------------------------------------------------------------ |
| ==     | 等于 - 比较对象是否相等                                      |
| !=     | 不等于 - 比较两个对象是否不相等                              |
| >      | 大于 - 返回x是否大于y                                        |
| <      | 小于 - 返回x是否小于y。所有比较运算符返回1表示真，返回0表示假 |
| >=     | 大于等于 - 返回x是否大于等于y。                              |
| <=     | 小于等于 - 返回x是否小于等于y。                              |

### 赋值运算符

| 运算符 | 描述             |
| ------ | ---------------- |
| =      | 简单的赋值运算符 |
| +=     | 加法赋值运算符   |
| -=     | 减法赋值运算符   |
| *=     | 乘法赋值运算符   |
| /=     | 除法赋值运算符   |
| %=     | 取模赋值运算符   |
| **=    | 幂赋值运算符     |
| //=    | 取整除赋值运算符 |

### 位运算符

| 运算符 | 描述                                                         |
| ------ | ------------------------------------------------------------ |
| &      | 按位与运算符：参与运算的两个值,如果两个相应位都为1,则该位的结果为1,否则为0 |
| \|     | 按位或运算符：只要对应的二个二进位有一个为1时，结果位就为1。 |
| ^      | 按位异或运算符：当两对应的二进位相异时，结果为1              |
| ~      | 按位取反运算符：对数据的每个二进制位取反,即把1变为0,把0变为1 |
| <<     | 左移动运算符：运算数的各二进位全部左移若干位，由"<<"右边的数指定移动的位数，高位丢弃，低位补0。 |
| >>     | 右移动运算符：把">>"左边的运算数的各二进位全部右移若干位，">>"右边的数指定移动的位数 |

### 逻辑运算符

| 运算符 | 逻辑表达式 |
| ------ | ---------- |
| and    | x and y    |
| or     | x or y     |
| not    | not x      |

### 成员运算符

测试实例中包含了一系列的成员，包括字符串，列表或元组

| 运算符 | 描述                                                    |
| ------ | ------------------------------------------------------- |
| in     | 如果在指定的序列中找到值返回 True，否则返回 False。     |
| not in | 如果在指定的序列中没有找到值返回 True，否则返回 False。 |

### 身份运算符

身份运算符用于比较两个对象的存储单元

| 运算符 | 描述                                        |
| ------ | ------------------------------------------- |
| is     | is 是判断两个标识符是不是引用自一个对象     |
| is not | is not 是判断两个标识符是不是引用自不同对象 |

### 运算符优先级

| 运算符                   | 描述                                                   |
| :----------------------- | :----------------------------------------------------- |
| **                       | 指数 (最高优先级)                                      |
| ~ + -                    | 按位翻转, 一元加号和减号 (最后两个的方法名为 +@ 和 -@) |
| * / % //                 | 乘，除，求余数和取整除                                 |
| + -                      | 加法减法                                               |
| >> <<                    | 右移，左移运算符                                       |
| &                        | 位 'AND'                                               |
| ^ \|                     | 位运算符                                               |
| <= < > >=                | 比较运算符                                             |
| == !=                    | 等于运算符                                             |
| = %= /= //= -= += *= **= | 赋值运算符                                             |
| is is not                | 身份运算符                                             |
| in not in                | 成员运算符                                             |
| not and or               | 逻辑运算符                                             |

## NUMBER

### 使用

> 创建

```python
var1 = 1
var2 = 10
```

> 删除

```python
del var
del var1 ,var2
```

> 使用十六进制和八进制

```python
number1 = 0xA0F # 十六进制

number2=0o37 # 八进制
```

### 数字类型转换

- **int(x)** 将x转换为一个整数。
- **float(x)** 将x转换到一个浮点数。
- **complex(x)** 将x转换到一个复数，实数部分为 x，虚数部分为 0。
- **complex(x, y)** 将 x 和 y 转换到一个复数，实数部分为 x，虚数部分为 y。x 和 y 是数字表达式

```python
a = 1.0
int(a)
#1
```

### 数学函数

| 函数                                                         | 返回值 ( 描述 )                                              |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [abs(x)](https://www.runoob.com/python3/python3-func-number-abs.html) | 返回数字的绝对值，如abs(-10) 返回 10                         |
| [ceil(x)](https://www.runoob.com/python3/python3-func-number-ceil.html) | 返回数字的上入整数，如math.ceil(4.1) 返回 5                  |
| cmp(x, y)                                                    | 如果 x < y 返回 -1, 如果 x == y 返回 0, 如果 x > y 返回 1。 **Python 3 已废弃，使用 (x>y)-(x。 |
| [exp(x)](https://www.runoob.com/python3/python3-func-number-exp.html) | 返回e的x次幂(ex),如math.exp(1) 返回2.718281828459045         |
| [fabs(x)](https://www.runoob.com/python3/python3-func-number-fabs.html) | 返回数字的绝对值，如math.fabs(-10) 返回10.0                  |
| [floor(x)](https://www.runoob.com/python3/python3-func-number-floor.html) | 返回数字的下舍整数，如math.floor(4.9)返回 4                  |
| [log(x)](https://www.runoob.com/python3/python3-func-number-log.html) | 如math.log(math.e)返回1.0,math.log(100,10)返回2.0            |
| [log10(x)](https://www.runoob.com/python3/python3-func-number-log10.html) | 返回以10为基数的x的对数，如math.log10(100)返回 2.0           |
| [max(x1, x2,...)](https://www.runoob.com/python3/python3-func-number-max.html) | 返回给定参数的最大值，参数可以为序列。                       |
| [min(x1, x2,...)](https://www.runoob.com/python3/python3-func-number-min.html) | 返回给定参数的最小值，参数可以为序列。                       |
| [modf(x)](https://www.runoob.com/python3/python3-func-number-modf.html) | 返回x的整数部分与小数部分，两部分的数值符号与x相同，整数部分以浮点型表示。 |
| [pow(x, y)](https://www.runoob.com/python3/python3-func-number-pow.html) | x**y 运算后的值。                                            |
| [round(x [,n\])](https://www.runoob.com/python3/python3-func-number-round.html) | 返回浮点数 x 的四舍五入值，如给出 n 值，则代表舍入到小数点后的位数。**其实准确的说是保留值将保留到离上一位更近的一端。** |
| [sqrt(x)](https://www.runoob.com/python3/python3-func-number-sqrt.html) | 返回数字x的平方根。                                          |

### 随机数函数

| 函数                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [choice(seq)](https://www.runoob.com/python3/python3-func-number-choice.html) | 从序列的元素中随机挑选一个元素，比如random.choice(range(10))，从0到9中随机挑选一个整数。 |
| [randrange ([start,\] stop [,step])](https://www.runoob.com/python3/python3-func-number-randrange.html) | 从指定范围内，按指定基数递增的集合中获取一个随机数，基数默认值为 1 |
| [random()](https://www.runoob.com/python3/python3-func-number-random.html) | 随机生成下一个实数，它在[0,1)范围内。                        |
| [seed([x\])](https://www.runoob.com/python3/python3-func-number-seed.html) | 改变随机数生成器的种子seed。如果你不了解其原理，你不必特别去设定seed，Python会帮你选择seed。 |
| [shuffle(lst)](https://www.runoob.com/python3/python3-func-number-shuffle.html) | 将序列的所有元素随机排序                                     |
| [uniform(x, y)](https://www.runoob.com/python3/python3-func-number-uniform.html) | 随机生成下一个实数，它在[x,y]范围内。                        |

### 三角函数

| 函数                                                         | 描述                                              |
| :----------------------------------------------------------- | :------------------------------------------------ |
| [acos(x)](https://www.runoob.com/python3/python3-func-number-acos.html) | 返回x的反余弦弧度值。                             |
| [asin(x)](https://www.runoob.com/python3/python3-func-number-asin.html) | 返回x的反正弦弧度值。                             |
| [atan(x)](https://www.runoob.com/python3/python3-func-number-atan.html) | 返回x的反正切弧度值。                             |
| [atan2(y, x)](https://www.runoob.com/python3/python3-func-number-atan2.html) | 返回给定的 X 及 Y 坐标值的反正切值。              |
| [cos(x)](https://www.runoob.com/python3/python3-func-number-cos.html) | 返回x的弧度的余弦值。                             |
| [hypot(x, y)](https://www.runoob.com/python3/python3-func-number-hypot.html) | 返回欧几里德范数 sqrt(x*x + y*y)。                |
| [sin(x)](https://www.runoob.com/python3/python3-func-number-sin.html) | 返回的x弧度的正弦值。                             |
| [tan(x)](https://www.runoob.com/python3/python3-func-number-tan.html) | 返回x弧度的正切值。                               |
| [degrees(x)](https://www.runoob.com/python3/python3-func-number-degrees.html) | 将弧度转换为角度,如degrees(math.pi/2) ， 返回90.0 |
| [radians(x)](https://www.runoob.com/python3/python3-func-number-radians.html) | 将角度转换为弧度                                  |

### 数学常量

| 常量 | 描述                                  |
| :--- | :------------------------------------ |
| pi   | 数学常量 pi（圆周率，一般以π来表示）  |
| e    | 数学常量 e，e即自然常数（自然常数）。 |



## STRING

### 使用

> 创建

可以使用引号( **'** 或 **"** )来创建字符串

```python
str='hello python'
```

> 访问

```python
str='hello python'
print (str)
print (str[1:5])
```

> 更新

```python
str='hello'
print(str+'python')
```

### 转义字符

| 转义字符    | 描述                                                         |
| :---------- | :----------------------------------------------------------- |
| \(在行尾时) | 续行符                                                       |
| \\          | 反斜杠符号                                                   |
| \'          | 单引号                                                       |
| \"          | 双引号                                                       |
| \a          | 响铃                                                         |
| \b          | 退格(Backspace)                                              |
| \000        | 空                                                           |
| \n          | 换行                                                         |
| \v          | 纵向制表符                                                   |
| \t          | 横向制表符                                                   |
| \r          | 回车                                                         |
| \f          | 换页                                                         |
| \oyy        | 八进制数，**yy** 代表的字符，例如：**\o12** 代表换行，其中 o 是字母，不是数字 0。 |
| \xyy        | 十六进制数，yy代表的字符，例如：\x0a代表换行                 |
| \other      | 其它的字符以普通格式输出                                     |

### 三引号

```python
str = """这是一个多行字符串的实例
多行字符串可以使用制表符
TAB ( \t )。
也可以使用换行符 [ \n ]。
"""
print(str)
```



## LIST

### 使用

> 创建

```python
list1 = ['Google','Firefox', 123, 9786532]
list2 = [1, 2, 3, 4, 5 ]
list3 = ["a", "b", "c", "d"]
```

> 访问

使用下标索引来访问列表中的值，同样你也可以使用方括号的形式截取字符

```python
print (list1[0])
print (list2[1:5])
```

> 更新

通过下标更新数据,或使用append()方法来添加列表项

```python
list = [1, 2, 3, 4, 5 ]
list[0]=555
list.append(56)
```

> 删除

使用 del 语句来删除列表的的元素

```python
list = [1, 2, 3, 4, 5 ]
del list[2]
```

### 嵌套列表

使用嵌套列表即在列表里创建其它列表

```python
a = ['a', 'b', 'c']
b = [1, 2, 3]
c= [a, n]
#[['a', 'b', 'c'], [1, 2, 3]]
```

### 函数

| 序号 | 函数                                                         |
| :--- | :----------------------------------------------------------- |
| 1    | [len(list)](https://www.runoob.com/python3/python3-att-list-len.html) 列表元素个数 |
| 2    | [max(list)](https://www.runoob.com/python3/python3-att-list-max.html) 返回列表元素最大值 |
| 3    | [min(list)](https://www.runoob.com/python3/python3-att-list-min.html) 返回列表元素最小值 |
| 4    | [list(seq)](https://www.runoob.com/python3/python3-att-list-list.html) 将元组转换为列表 |

### 方法

| 序号 | 方法                                                         |
| :--- | :----------------------------------------------------------- |
| 1    | [list.append(obj)](https://www.runoob.com/python3/python3-att-list-append.html) 在列表末尾添加新的对象 |
| 2    | [list.count(obj)](https://www.runoob.com/python3/python3-att-list-count.html) 统计某个元素在列表中出现的次数 |
| 3    | [list.extend(seq)](https://www.runoob.com/python3/python3-att-list-extend.html) 在列表末尾一次性追加另一个序列中的多个值（用新列表扩展原来的列表） |
| 4    | [list.index(obj)](https://www.runoob.com/python3/python3-att-list-index.html) 从列表中找出某个值第一个匹配项的索引位置 |
| 5    | [list.insert(index, obj)](https://www.runoob.com/python3/python3-att-list-insert.html) 将对象插入列表 |
| 6    | [list.pop([index=-1\])](https://www.runoob.com/python3/python3-att-list-pop.html) 移除列表中的一个元素（默认最后一个元素），并且返回该元素的值 |
| 7    | [list.remove(obj)](https://www.runoob.com/python3/python3-att-list-remove.html) 移除列表中某个值的第一个匹配项 |
| 8    | [list.reverse()](https://www.runoob.com/python3/python3-att-list-reverse.html) 反向列表中元素 |
| 9    | [list.sort( key=None, reverse=False)](https://www.runoob.com/python3/python3-att-list-sort.html) 对原列表进行排序 |
| 10   | [list.clear()](https://www.runoob.com/python3/python3-att-list-clear.html) 清空列表 |
| 11   | [list.copy()](https://www.runoob.com/python3/python3-att-list-copy.html) 复制列表 |

## TUPLE

元组与列表类似，不同之处在于元组的元素不能修改

元组使用小括号，列表使用方括号

### 使用

> 创建

```python
tup1 = (1, 2, 3, 4, 5 )
tup2 = "a", "b", "c", "d"   #  不需要括号也可以
tup1 = () #空元组
```

> 访问

下标索引来访问元组中的值

```python
print (tup1[0])
print (tup2[1:5])
```

> 更新

元组中的元素值是不允许修改的，但我们可以对元组进行连接组合

```python
tup1 = (1, 2, 3, 4, 5 )
tup2 = "a", "b", "c", "d"
tup3 = tup1 + tup2
print (tup3)
```

> 删除

元组中的元素值是不允许删除的，但我们可以使用del语句来删除整个元组

```python
tup = (1, 2, 3, 4, 5 )
del tup
```



> note

```python
元组中只包含一个元素时，需要在元素后面添加逗号，否则括号会被当作运算符使用
tup1 = (50)
type(tup1)     # 不加逗号，类型为整型
#<class 'int'>
 
tup1 = (50,)
type(tup1)     # 加上逗号，类型为元组
#<class 'tuple'>
```



## Dictionary

字典是另一种可变容器模型，且可存储任意类型对象。

字典的每个键值(key=>value)对用冒号(**:**)分割，每个对之间用逗号(**,**)分割，整个字典包括在花括号(**{})**中 

### 使用

> 创建

```
person={'name':'Alice','age':'115'}
```

+ 键必须是唯一的，但值则不必。

+ 值可以取任何数据类型，但键必须是不可变的，如字符串，数字或元组

> 访问

```python
person={'name':'Alice','age':'115'}
print(person['name'])
print(person['age'])
```

> 更新

```python
person={'name':'Alice','age':'115'}
person['age']='55'
```

> 删除

显示删除一个字典用del命令

```python
del person['name'] # 删除键 'Name'
person.clear()     # 清空字典
del person         # 删除字典
```

### 函数

| 序号 | 函数及描述                                                   |
| :--- | :----------------------------------------------------------- |
| 1    | len(dict) 计算字典元素个数，即键的总数。                     |
| 2    | str(dict) 输出字典，以可打印的字符串表示。                   |
| 3    | type(variable) 返回输入的变量类型，如果变量是字典就返回字典类型。 |

### 方法

| 序号 | 函数及描述                                                   |
| :--- | :----------------------------------------------------------- |
| 1    | [radiansdict.clear()](https://www.runoob.com/python3/python3-att-dictionary-clear.html) 删除字典内所有元素 |
| 2    | [radiansdict.copy()](https://www.runoob.com/python3/python3-att-dictionary-copy.html) 返回一个字典的浅复制 |
| 3    | [radiansdict.fromkeys()](https://www.runoob.com/python3/python3-att-dictionary-fromkeys.html) 创建一个新字典，以序列seq中元素做字典的键，val为字典所有键对应的初始值 |
| 4    | [radiansdict.get(key, default=None)](https://www.runoob.com/python3/python3-att-dictionary-get.html) 返回指定键的值，如果值不在字典中返回default值 |
| 5    | [key in dict](https://www.runoob.com/python3/python3-att-dictionary-in.html) 如果键在字典dict里返回true，否则返回false |
| 6    | [radiansdict.items()](https://www.runoob.com/python3/python3-att-dictionary-items.html) 以列表返回可遍历的(键, 值) 元组数组 |
| 7    | [radiansdict.keys()](https://www.runoob.com/python3/python3-att-dictionary-keys.html) 返回一个迭代器，可以使用 list() 来转换为列表 |
| 8    | [radiansdict.setdefault(key, default=None)](https://www.runoob.com/python3/python3-att-dictionary-setdefault.html) 和get()类似, 但如果键不存在于字典中，将会添加键并将值设为default |
| 9    | [radiansdict.update(dict2)](https://www.runoob.com/python3/python3-att-dictionary-update.html) 把字典dict2的键/值对更新到dict里 |
| 10   | [radiansdict.values()](https://www.runoob.com/python3/python3-att-dictionary-values.html) 返回一个迭代器，可以使用 list() 来转换为列表 |
| 11   | [pop(key[,default\])](https://www.runoob.com/python3/python3-att-dictionary-pop.html) 删除字典给定键 key 所对应的值，返回值为被删除的值。key值必须给出。 否则，返回default值。 |
| 12   | [popitem()](https://www.runoob.com/python3/python3-att-dictionary-popitem.html) 随机返回并删除字典中的最后一对键和值。 |

## SET

集合（set）是一个无序的不重复元素序列

可以使用大括号 **{ }** 或者 **set()** 函数创建集合

### 使用

> 创建

```python
person={'name','age','sex','money'}
Person=set('name','age','sex','money')

```



### 常用操作

> 添加

```python
person={'name','age','sex','money'}
person.add('tall')
```

> 移除

```python
person={'name','age','sex','money'}
person.remove('money')
```

> 计算个数

```python
person={'name','age','sex','money'}
len(person)#4
```

> 清空

```python
person={'name','age','sex','money'}
person.clear()
print(person)
#set()
```

> 判断元素

```python
'name' in person
# true
```

### 内置方法

| 方法                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [add()](https://www.runoob.com/python3/ref-set-add.html)     | 为集合添加元素                                               |
| [clear()](https://www.runoob.com/python3/ref-set-clear.html) | 移除集合中的所有元素                                         |
| [copy()](https://www.runoob.com/python3/ref-set-copy.html)   | 拷贝一个集合                                                 |
| [difference()](https://www.runoob.com/python3/ref-set-difference.html) | 返回多个集合的差集                                           |
| [difference_update()](https://www.runoob.com/python3/ref-set-difference_update.html) | 移除集合中的元素，该元素在指定的集合也存在。                 |
| [discard()](https://www.runoob.com/python3/ref-set-discard.html) | 删除集合中指定的元素                                         |
| [intersection()](https://www.runoob.com/python3/ref-set-intersection.html) | 返回集合的交集                                               |
| [intersection_update()](https://www.runoob.com/python3/ref-set-intersection_update.html) | 返回集合的交集。                                             |
| [isdisjoint()](https://www.runoob.com/python3/ref-set-isdisjoint.html) | 判断两个集合是否包含相同的元素，如果没有返回 True，否则返回 False。 |
| [issubset()](https://www.runoob.com/python3/ref-set-issubset.html) | 判断指定集合是否为该方法参数集合的子集。                     |
| [issuperset()](https://www.runoob.com/python3/ref-set-issuperset.html) | 判断该方法的参数集合是否为指定集合的子集                     |
| [pop()](https://www.runoob.com/python3/ref-set-pop.html)     | 随机移除元素                                                 |
| [remove()](https://www.runoob.com/python3/ref-set-remove.html) | 移除指定元素                                                 |
| [symmetric_difference()](https://www.runoob.com/python3/ref-set-symmetric_difference.html) | 返回两个集合中不重复的元素集合。                             |
| [symmetric_difference_update()](https://www.runoob.com/python3/ref-set-symmetric_difference_update.html) | 移除当前集合中在另外一个指定集合相同的元素，并将另外一个指定集合中不同的元素插入到当前集合中。 |
| [union()](https://www.runoob.com/python3/ref-set-union.html) | 返回两个集合的并集                                           |
| [update()](https://www.runoob.com/python3/ref-set-update.html) | 给集合添加元素                                               |

## 条件控制

### 基本使用

> 格式

```python
if condition_1:
    statement_block_1
elif condition_2:
    statement_block_2
else:
    statement_block_3
```

Python 中用 **elif** 代替了 **else if**

> note

- 1、每个条件后面要使用冒号 **:**，表示接下来是满足条件后要执行的语句块。
- 2、使用缩进来划分语句块，相同缩进数的语句在一起组成一个语句块。
- 3、在Python中没有switch – case语句

### if嵌套

```python
if 表达式1:
    语句
    if 表达式2:
        语句
    elif 表达式3:
        语句
    else:
        语句
elif 表达式4:
    语句
else:
    语句
```

## 循环控制

### 基本使用

> 语句

Python 中的循环语句有 for 和 while

> 格式

`while`

```python
while 判断条件(condition)：
    执行语句(statements)……
else:
    (statements)    
```

+ 在 Python 中没有 do..while 循环

`for`

```python
for <variable> in <sequence>:
    <statements>
else:
    <statements>
```

+ Python for循环可以遍历任何序列的项目，如一个列表或者一个字符串

> 无限循环

设置条件表达式永远不为 false 来实现无限循环

```python
a=1
while a==1
	print(a)
print(a+1)	
```

使用**CTRL+C** 来退出当前的无限循环

### range()

> 使用

遍历数字序列，可以使用内置range()函数。它会生成数列

```python
for i in range(5):
print(i)
# 0 1 2 3 4 
```

> 指定区间

```python
for i in range(5,9) :
    print(i)
# 5 6 7 8 9
```

> 指定增量

```python
for i in range(0, 10, 3) :
    print(i)
# 0 3 6 9
```

### 终止

#### **continue**

+ 被用来告诉 Python 跳过当前循环块中的剩余语句，然后继续进行下一轮循环

#### break

+ 可以跳出 for 和 while 的循环体。如果你从 for 或 while 循环中终止，任何对应的循环 else 块将不执行

#### pass

pass是空语句，是为了保持程序结构的完整性

pass 不做任何事情，一般用做占位语句

```python
while True:
	pass  
# 等待键盘中断 (Ctrl+C)
```

## 迭代器

+ 迭代是Python最强大的功能之一，是访问集合元素的一种方式。

+ 迭代器是一个可以记住遍历的位置的对象。
+ 迭代器对象从集合的第一个元素开始访问，直到所有的元素被访问完结束。迭代器只能往前不会后退

> 方法

+ **iter()**
+ **next()**

## 生成器

+ 在 Python 中，使用了 yield 的函数被称为生成器（generator）

+ 跟普通函数不同的是，生成器是一个返回迭代器的函数，只能用于迭代操作，更简单点理解生成器就是一个迭代器

+ 在调用生成器运行的过程中，每次遇到 yield 时函数会暂停并保存当前所有的运行信息，返回 yield 的值, 并在下一次执行 next() 方法时从当前位置继续运行。

  调用一个生成器函数，返回的是一个迭代器对象

## 函数

### 定义

- 函数代码块以 **def** 关键词开头，后接函数标识符名称和圆括号 **()**。
- 任何传入参数和自变量必须放在圆括号中间，圆括号之间可以用于定义参数。
- 函数的第一行语句可以选择性地使用文档字符串—用于存放函数说明。
- 函数内容以冒号起始，并且缩进。
- **return [表达式]** 结束函数，选择性地返回一个值给调用方。不带表达式的return相当于返回 None。

> 语法

Python 定义函数使用**def** 关键字

```
def 函数名（参数列表）:
    函数体
```

> 实例

```python
def hello() :
   print("Hello python!")
hello()
```

### 调用

定义一个函数：给了函数一个名称，指定了函数里包含的参数，和代码块结构

这个函数的基本结构完成以后，可以通过另一个函数调用执行

```python
def add(x,y)
	print(x+y)
add(3,5)#8
add("hello ","python")#hello python
add("number:",5)# number:5
```

### 参数传递

> 参数类型

- 必需参数
- 关键字参数
- 默认参数
- 不定长参数

> 必需参数

必需参数须以正确的顺序传入函数。调用时的数量必须和声明时的一样

> 关键字参数

关键字参数和函数调用关系紧密，函数调用使用关键字参数来确定传入的参数值。

使用关键字参数允许函数调用时参数的顺序与声明时不一致，因为 Python 解释器能够用参数名匹配参数值

> 默认参数

调用函数时，如果没有传递参数，则会使用默认参数。以下实例中如果没有传入 age 参数，则使用默认值

> 不定长参数

你可能需要一个函数能处理比当初声明时更多的参数。这些参数叫做不定长参数，和上述 2 种参数不同，声明时不会命名

### 匿名函数

python 使用 lambda 来创建匿名函数。

所谓匿名，意即不再使用 def 语句这样标准的形式定义一个函数

- ambda 只是一个表达式，函数体比 def 简单很多。
- lambda的主体是一个表达式，而不是一个代码块。仅仅能在lambda表达式中封装有限的逻辑进去。
- lambda 函数拥有自己的命名空间，且不能访问自己参数列表之外或全局命名空间里的参数。
- 虽然lambda函数看起来只能写一行，却不等同于C或C++的内联函数，后者的目的是调用小函数时不占用栈内存从而增加运行效率

### return 

## 数据结构

### 列表

> 列表的方法

| 方法              | 描述                                                         |
| :---------------- | :----------------------------------------------------------- |
| list.append(x)    | 把一个元素添加到列表的结尾，相当于 a[len(a):] = [x]。        |
| list.extend(L)    | 通过添加指定列表的所有元素来扩充列表，相当于 a[len(a):] = L。 |
| list.insert(i, x) | 在指定位置插入一个元素。第一个参数是准备插入到其前面的那个元素的索引，例如 a.insert(0, x) 会插入到整个列表之前，而 a.insert(len(a), x) 相当于 a.append(x) 。 |
| list.remove(x)    | 删除列表中值为 x 的第一个元素。如果没有这样的元素，就会返回一个错误。 |
| list.pop([i])     | 从列表的指定位置移除元素，并将其返回。如果没有指定索引，a.pop()返回最后一个元素。元素随即从列表中被移除。（方法中 i 两边的方括号表示这个参数是可选的，而不是要求你输入一对方括号，你会经常在 Python 库参考手册中遇到这样的标记。） |
| list.clear()      | 移除列表中的所有项，等于del a[:]。                           |
| list.index(x)     | 返回列表中第一个值为 x 的元素的索引。如果没有匹配的元素就会返回一个错误。 |
| list.count(x)     | 返回 x 在列表中出现的次数。                                  |
| list.sort()       | 对列表中的元素进行排序。                                     |
| list.reverse()    | 倒排列表中的元素。                                           |
| list.copy()       | 返回列表的浅复制，等于a[:]。                                 |

> note

类似 insert, remove 或 sort 等修改列表的方法没有返回值

> 列表当做堆栈使用

列表可以很方便的作为一个堆栈来使用，堆栈作为特定的数据结构，最先进入的元素最后一个被释放（后进先出）

```python
stack = [3, 4, 5]
stack.append(6)
stack.append(7)
stack
#[3, 4, 5, 6, 7]
stack.pop()
#7
stack
#[3, 4, 5, 6]
stack.pop()
#6
```

> 列表当做队列使用

列表当做队列用，只是在队列里第一加入的元素，第一个取出来

```python
queue = deque(["Eric", "John", "Michael"])
queue.append("Terry")           # Terry arrives
queue.append("Graham")          # Graham arrives
queue.popleft()                 # The first to arrive now leaves
#'Eric'
queue.popleft()                 # The second to arrive now leaves
#'John'
queue                           # Remaining queue in order of arrival
#deque(['Michael', 'Terry', 'Graham'])
```

> 嵌套列表

```python
matrix = [
			[1, 2, 3, 4],
			[5, 6, 7, 8],
			[9, 10, 11, 12],
		  ]
```

+ 法一

```python
[[row[i] for row in matrix] for i in range(4)]
#[[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]
```

+ 法二

```python
transposed = []
for i in range(4):
	transposed.append([row[i] for row in matrix])
```

+ 法三

```python
transposed = []
for i in range(4):# the following 3 lines implement the nested listcomp
	transposed_row = []
	for row in matrix:
		transposed_row.append(row[i])
	transposed.append(transposed_row)
```

> del

使用 del 语句可以从一个列表中依索引而不是值来删除一个元素。这与使用 pop() 返回一个值不同。可以用 del 语句从列表中删除一个切割，或清空整个列表

```python
a = [-1, 1, 66.25, 333, 333, 1234.5]
del a[0]
a
#[1, 66.25, 333, 333, 1234.5]
del a[2:4]
a
#[1, 66.25, 1234.5]
del a[:]
a
#[]
```

### 元组

```python
t = 12345, 54321, 'hello!'
t[0]
#12345
t
#(12345, 54321, 'hello!')
# Tuples may be nested:
u = t, (1, 2, 3, 4, 5)
u
#((12345, 54321, 'hello!'), (1, 2, 3, 4, 5))
```

元组在输出时总是有括号的，以便于正确表达嵌套结构。在输入时可能有或没有括号， 不过括号通常是必须的

### 集合

集合是一个无序不重复元素的集。基本功能包括关系测试和消除重复元素。

```python
basket = {'apple', 'orange', 'apple', 'pear', 'orange', 'banana'}
print(basket)                      # 删除重复的
#{'orange', 'banana', 'pear', 'apple'}
'orange' in basket                 # 检测成员
#True
'crabgrass' in basket
#False
```



### 字典

序列是以连续的整数为索引，与此不同的是，字典以关键字为索引，关键字可以是任意不可变类型，通常用字符串或数值。

理解字典的最佳方式是把它看做无序的键=>值对集合。在同一个字典之内，关键字必须是互不相同

```python
tel = {'jack': 4098, 'sape': 4139}
tel['guido'] = 4127
tel
#{'sape': 4139, 'guido': 4127, 'jack': 4098}
tel['jack']
#4098
del tel['sape']
tel['irv'] = 4127
tel
#{'guido': 4127, 'irv': 4127, 'jack': 4098}
list(tel.keys())
#['irv', 'guido', 'jack']
sorted(tel.keys())
#['guido', 'irv', 'jack']
'guido' in tel
#True
'jack' not in tel
#False
```

> 遍历

```python
knights = {'gallahad': 'the pure', 'robin': 'the brave'}
for k, v in knights.items():
	print(k, v)
#gallahad the pure
#robin the brave
```

在序列中遍历时，索引位置和对应值可以使用 enumerate() 函数同时得到

```python
for i, v in enumerate(['tic', 'tac', 'toe']):
	print(i, v)
'''
0 tic
1 tac
2 toe
'''
```

同时遍历两个或更多的序列，可以使用 zip() 组合

```python
questions = ['name', 'quest', 'favorite color']
answers = ['lancelot', 'the holy grail', 'blue']
for q, a in zip(questions, answers):
	 print('What is your {0}?  It is {1}.'.format(q, a))
'''
What is your name?  It is lancelot.
What is your quest?  It is the holy grail.
What is your favorite color?  It is blue.
'''
```

## 模块

### 基本

> 定义

 Python 提供了一个办法，把这些定义存放在文件中，为一些脚本或者交互式的解释器实例使用，这个文件被称为模块

> 实例

```Python
import sys
 
print('命令行参数如下:')
for i in sys.argv:
   print(i)
 
print('\n\nPython 路径为：', sys.path, '\n')
```

- import sys 引入 python 标准库中的 sys.py 模块；这是引入某一模块的方法。
- sys.argv 是一个包含命令行参数的列表。
- sys.path 包含了一个 Python 解释器自动查找所需模块的路径的列表

### import

想使用 Python 源文件，只需在另一个源文件里执行 import 语句

> 语法

```python
import module1[, module2[,... moduleN]
```

> note

整个模块导入

### from … import

Python 的 from 语句让你从模块中导入一个指定的部分到当前命名空间中

> 语法

```python
from modname import name1[, name2[, ... nameN]]
```

> note

这个声明不会把整个模块导入到当前的命名空间中，它只会将模块里的一些内容引入进来

### from … import * 

把一个模块的所有内容全都导入到当前的命名空间也是可行的

> 语法

```python
from modname import *
```

### \_\_name\_\_属性

### dir()

### 标准模块

### 包