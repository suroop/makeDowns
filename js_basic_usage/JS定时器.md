# JS定时器

## 启动定时器

### setTimeout(code,millisec)

可以使一段代码在指定时间后运行

``` javascript
setTimeout(test,1000)	//函数名 一秒后执行
setTimeout('test()',1000)	//字符串 一秒后执行
setTimeout(function(){},1000)//匿名函数 一秒后执行
note:
setTimeout(test(),1000)	//test方法将会立即执行
```





### setInterval(code,millisec)

可以使一段代码每过一段时间就运行一次

直到clearInterval()被调用或窗口关闭

用法同setTimeout()

定时器在调用的时候回返回一个整型数字

## 清除定时器

### clearTimeout(obj)

要清除定时器,必须先定义一个变量来记录定时器的返回值

### clearInterval(obj)

``` javascript
var test=setInterval(function(){},1000);
clearInterval(test);
```



## demo1

``` javascript
<style>
    #div1{
	width:200px;
    height:200px;
	background:red;
}
</style>
<script>
    var oBtn=doucument.getElementbyId("btn");
    var oDiv=document.getElementbyId("div1");
	function move(){
        timer=setInterval(function(){
        var speed=1;
        if(oDiv.offsetLeft>=300){
            clearInterval(timer);
        }
        else{
            oDiv.style.Left=oDiv.offsetLeft+speed+'px';
        }
        },30);
    }
</script>
<body>
    <button id="btn">move</button>
    <div id="div1" onclick=(move)></div>
</body>
```





