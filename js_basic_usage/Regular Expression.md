#  Regular Expression

## 格式

### 直接量语法

- /正则表达式主体/修饰符(可选)

```javascript
var name = /surp/i;
```



### 创建RegExp对象语法

- new RegExp(正则表达式主体,修饰符)

```javascript
var name=RegExp(surp,i)
```



## 修饰符

+ | 修饰符 | 描述                                                     |
  | ------ | -------------------------------------------------------- |
  | i      | 执行对大小写不敏感的匹配。                               |
  | g      | 执行全局匹配（查找所有匹配而非在找到第一个匹配后停止）。 |
  | m      | 执行多行匹配。                                           |

## 方法

### search()

+ 使用表达式来搜索匹配，然后返回匹配的位置。

#### 字符串方法

```javascript
var name='surp';
return name.search("s");
//return 0;
```



#### 正则表达式方法

```javascript
var name="I am a surp";
return name.search(/S/i);
//return 0;
```



### replace()

+ 返回模式被替换处修改后的字符串。

#### 字符串方法

```javascript
var website="hello yahoo";
return website.replace("yahoo","google");
//return "hello google"; 
```



#### 正则表达式方法

```javascript
var website="hello yahoo hello baudu ";
return website.replace(/HeLlO/i,"fuck");
//return fuck yahoo fuck baudu 
```



### test()

+ 如果字符串中含有匹配的文本，则返回 true，否则返回 false

```javascript
var Test=/e/;
Test.test("the best thing in life is free");
//return true
```



### exec()

+ 该函数返回一个数组，其中存放匹配的结果。如果未找到匹配，则返回值为 null

  ```javascript
  var test=/e/;
  test.exec("today is a perfect day,oh shit");
  //return e;
  ```

  

## 模式

### 表达式

- | 表达式 | 描述                       |
  | ------ | -------------------------- |
  | [abc]  | 查找方括号之间的任何字符。 |
  | [0-9]  | 查找任何从 0 至 9 的数字。 |
  | (x\|y) | 查找任何以 \| 分隔的选项。 |

### 元字符

+ | 元字符 | 描述           |
  | ------ | -------------- |
  | \d     | 查找数字       |
  | \s     | 查找空白字符   |
  | \b     | 匹配单词边界   |
  | \w     | 查找非字母     |
  | \D     | 查找非数字     |
  | \S     | 查找非空白字符 |
  | \W     | 查找非字母     |
  |        |                |

### 量词

+ | 量词 | 描述                                  |
  | ---- | ------------------------------------- |
  | n+   | 匹配任何包含至少一个 *n* 的字符串。   |
  | n*   | 匹配任何包含零个或多个 *n* 的字符串。 |
  | n?   | 匹配任何包含零个或一个 *n* 的字符串。 |

