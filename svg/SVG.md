# SVG

## demo

```xml
<?xml version="1.0" standalone="no"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN"
"http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">

<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <circle cx="100" cy="50" r="40" stroke="black"
  stroke-width="2" fill="red" />
</svg>
```

> 解析

+ 第一行包含了 XML 声明。请注意 standalone 属性！该属性规定此 SVG 文件是否是"独立的"，或含有对外部文件的引用.standalone="no" 意味着 SVG 文档会引用一个外部文件 - 在这里，是 DTD 文件

+ 第二和第三行引用了这个外部的 SVG DTD。该 DTD 位于 "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd"。该 DTD 位于 W3C，含有所有允许的 SVG 元素

+ SVG 代码以 `<svg>`元素开始，包括开启标签 `<svg>`和关闭标签 `</svg>` 。这是根元素。width 和 height 属性可设置此 SVG 文档的宽度和高度。version 属性可定义所使用的 SVG 版本，xmlns 属性可定义 SVG 命名空间
+ SVG 的 <circle> 用来创建一个圆。cx 和 cy 属性定义圆中心的 x 和 y 坐标。如果忽略这两个属性，那么圆点会被设置为 (0, 0)。r 属性定义圆的半径
+ stroke 和 stroke-width 属性控制如何显示形状的轮廓。我们把圆的轮廓设置为 2px 宽，黑边框

+ fill 属性设置形状内的颜色

## 在HTML

> 使用

SVG 文件可通过以下标签嵌入 HTML 文档：<embed>、<object> 或者 <iframe>。

SVG的代码可以直接嵌入到HTML页面中，或您可以直接链接到SVG文件

> `<embed>`

- 优势：所有主要浏览器都支持，并允许使用脚本
- 缺点：不推荐在HTML4和XHTML中使用（但在HTML5允许）

```html
<embed src="circle1.svg" type="image/svg+xml" />
```

> `<object>`

- 优势：所有主要浏览器都支持，并支持HTML4，XHTML和HTML5标准
- 缺点：不允许使用脚本

```html
<object data="circle1.svg" type="image/svg+xml"></object>
```

> `<iframe>`

- 优势：所有主要浏览器都支持，并允许使用脚本
- 缺点：不推荐在HTML4和XHTML中使用（但在HTML5允许）

```html
<iframe src="circle1.svg"></iframe>
```

> `<svg>`

<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
    <circle cx="100" cy="50" r="40" stroke="black" stroke-width="2" fill="red" />
</svg>

```html
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
    <circle cx="100" cy="50" r="40" stroke="black" stroke-width="2" fill="red" />
</svg>
```



> <a>`

```html
<a href="circle1.svg">View SVG file</a>
```

## 矩形

> 预定义形状

- 矩形 <rect>
- 圆形 <circle>
- 椭圆 <ellipse>
- 线 <line>
- 折线 <polyline>
- 多边形 <polygon>
- 路径 <path>

### <rect>1

<rect> 标签可用来创建矩形，以及矩形的变种

<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <rect width="300" height="100"
  style="fill:rgb(0,0,255);stroke-width:1;stroke:rgb(0,0,0)"/>
</svg>

```html
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <rect width="300" height="100"
  style="fill:rgb(0,0,255);stroke-width:1;stroke:rgb(0,0,0)"/>
</svg>
```

> 解析

- rect 元素的 width 和 height 属性可定义矩形的高度和宽度
- style 属性用来定义 CSS 属性
- CSS 的 fill 属性定义矩形的填充颜色（rgb 值、颜色名或者十六进制值）
- CSS 的 stroke-width 属性定义矩形边框的宽度
- CSS 的 stroke 属性定义矩形边框的颜色

### <rect>2

<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <rect x="50" y="20" width="100" height="100"
  style="fill:blue;stroke:pink;stroke-width:5;fill-opacity:0.1;
  stroke-opacity:0.9"/>
</svg>

```html
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <rect x="50" y="20" width="100" height="100"
  style="fill:blue;stroke:pink;stroke-width:5;fill-opacity:0.1;
  stroke-opacity:0.9"/>
</svg>
```

> 解析

- x 属性定义矩形的左侧位置（例如，x="0" 定义矩形到浏览器窗口左侧的距离是 0px）
- y 属性定义矩形的顶端位置（例如，y="0" 定义矩形到浏览器窗口顶端的距离是 0px）
- CSS 的 fill-opacity 属性定义填充颜色透明度（合法的范围是：0 - 1）
- CSS 的 stroke-opacity 属性定义轮廓颜色的透明度（合法的范围是：0 - 1）

### <rect>3

<svg xmlns="http://www.w3.org/2000/svg" version="1.1">  <rect x="50" y="20" rx="20" ry="20" width="100" height="100"  style="fill:red;stroke:black;stroke-width:5;opacity:0.5"/></svg>

```html
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">  
    <rect x="50" y="20" rx="20" ry="20" width="100" height="100" style="fill:red;stroke:black;stroke-width:5;opacity:0.5"/>
</svg>
```

> 解析

+ rx 和 ry 属性可使矩形产生圆角
+ CSS opacity 属性用于定义了元素的透明值 (范围: 0 到 1)

## 圆形

### <circle>

<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <circle cx="100" cy="50" r="40" stroke="black"
  stroke-width="2" fill="red"/>
</svg>

```html
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <circle cx="100" cy="50" r="40" stroke="black"
  stroke-width="2" fill="red"/>
</svg>
```

## 椭圆

### <ellipse>

<svg xmlns="http://www.w3.org/2000/svg" version="1.1">   <ellipse cx="150" cy="70" rx="100" ry="50"   style="fill:yellow;stroke:purple;stroke-width:2"/> </svg>



```html
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <ellipse cx="300" cy="80" rx="100" ry="50"
  style="fill:yellow;stroke:purple;stroke-width:2"/>
</svg>
```

> 解析

- CX属性定义的椭圆中心的x坐标
- CY属性定义的椭圆中心的y坐标
- RX属性定义的水平半径
- RY属性定义的垂直半径

## 直线

### <line>

<svg xmlns="http://www.w3.org/2000/svg" version="1.1">  <line x1="0" y1="0" x2="200" y2="200"  style="stroke:rgb(255,0,0);stroke-width:2"/></svg>

```html
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <line x1="0" y1="0" x2="200" y2="200"
  style="stroke:rgb(255,0,0);stroke-width:2"/>
</svg>
```

> 解析

- x1 属性在 x 轴定义线条的开始
- y1 属性在 y 轴定义线条的开始
- x2 属性在 x 轴定义线条的结束
- y2 属性在 y 轴定义线条的结束

## 多边形

### <polygon>1

<svg  height="210" width="500">   <polygon points="200,10 250,190 160,210"   style="fill:lime;stroke:purple;stroke-width:1"/> </svg>

```html
<svg  height="210" width="500">
  <polygon points="200,10 250,190 160,210"
  style="fill:lime;stroke:purple;stroke-width:1"/>
</svg>
```

> 解析

+ points 属性定义多边形每个角的 x 和 y 坐标

### <polygon>2

<svg height="210" width="500">   <polygon points="100,10 40,198 190,78 10,78 160,198"   style="fill:lime;stroke:purple;stroke-width:5;fill-rule:evenodd;" /> </svg>

```html
<svg height="210" width="500">
  <polygon points="100,10 40,198 190,78 10,78 160,198"
  style="fill:lime;stroke:purple;stroke-width:5;fill-rule:evenodd;" />
</svg>
```

> 解析

+ fill-rule:用于指定如何判断图形的“内部”
  + **nonzero**:字面意思是非零。按照规则，要判断一个点是否在图形内，从该点作任意方向的一条射线，然后检测射线与图形路径的交点情况。从0开始计数，路径从左向右穿过射线则计数加1，从右向左穿过射线则计数减1。得出计数结果后，如果结果是0，则认为点在图形外部，否则认为在内部
  + **evenodd**:字面意思是“奇偶”。按照规则，要判断一个点是否在图形内，该点作任意方向的一条射线，然后检测射线与图形路径的交点的数量。如果结果是奇数则认为点在内部，是偶数则认为点在外部

## 曲线

### <polyline>

<svg xmlns="http://www.w3.org/2000/svg" version="1.1">   <polyline points="20,20 40,25 60,40 80,120 120,140 200,180"   style="fill:none;stroke:black;stroke-width:3" /> </svg>

```html
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <polyline points="20,20 40,25 60,40 80,120 120,140 200,180"
  style="fill:none;stroke:black;stroke-width:3" />
</svg>
```

## 路径

### <path>

下面的命令可用于路径数据

- M = moveto
- L = lineto
- H = horizontal lineto
- V = vertical lineto
- C = curveto
- S = smooth curveto
- Q = quadratic Bézier curve
- T = smooth quadratic Bézier curveto
- A = elliptical Arc
- Z = closepath

NOTE:以上所有命令均允许小写字母。大写表示绝对定位，小写表示相对定位

### <path>1

<svg xmlns="http://www.w3.org/2000/svg" version="1.1">     <path d="M150 0 L75 200 L225 200 Z" /> </svg>

```html
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
    <path d="M150 0 L75 200 L225 200 Z" />
</svg>
```

## 文本

### <text>1

<svg xmlns="http://www.w3.org/2000/svg" version="1.1">  <text x="0" y="15" fill="black">I love SVG</text></svg>

```html
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <text x="0" y="15" fill="black">I love SVG</text>
</svg>
```

### <text>2

<svg xmlns="http://www.w3.org/2000/svg" version="1.1">  <text x="0" y="15" fill="red" transform="rotate(30 20,40)">I love SVG</text></svg>

```
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <text x="0" y="15" fill="red" transform="rotate(30 20,40)">I love SVG</text>
</svg>
```

## stroke

- stroke
- stroke-width
- stroke-linecap
- stroke-dasharray

### stroke属性

<svg xmlns="http://www.w3.org/2000/svg" version="1.1">  <g fill="none">    <path stroke="red" d="M5 20 l215 0" />    <path stroke="blue" d="M5 40 l215 0" />    <path stroke="black" d="M5 60 l215 0" />  </g></svg>

```html
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <g fill="none">
    <path stroke="red" d="M5 20 l215 0" />
    <path stroke="blue" d="M5 40 l215 0" />
    <path stroke="black" d="M5 60 l215 0" />
  </g>
</svg>
```

### stroke-width

<svg xmlns="http://www.w3.org/2000/svg" version="1.1">  <g fill="none" stroke="black">    <path stroke-width="2" d="M5 20 l215 0" />    <path stroke-width="4" d="M5 40 l215 0" />    <path stroke-width="6" d="M5 60 l215 0" />  </g></svg>

```html
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <g fill="none" stroke="black">
    <path stroke-width="2" d="M5 20 l215 0" />
    <path stroke-width="4" d="M5 40 l215 0" />
    <path stroke-width="6" d="M5 60 l215 0" />
  </g>
</svg>
```

### stroke-linecap

<svg xmlns="http://www.w3.org/2000/svg" version="1.1">  <g fill="none" stroke="black" stroke-width="6">    <path stroke-linecap="butt" d="M5 20 l215 0" />    <path stroke-linecap="round" d="M5 40 l215 0" />    <path stroke-linecap="square" d="M5 60 l215 0" />  </g></svg>

```html
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <g fill="none" stroke="black" stroke-width="6">
    <path stroke-linecap="butt" d="M5 20 l215 0" />
    <path stroke-linecap="round" d="M5 40 l215 0" />
    <path stroke-linecap="square" d="M5 60 l215 0" />
  </g>
</svg>
```

### stroke-dasharray

<svg xmlns="http://www.w3.org/2000/svg" version="1.1">  <g fill="none" stroke="black" stroke-width="4">    <path stroke-dasharray="5,5" d="M5 20 l215 0" />    <path stroke-dasharray="10,10" d="M5 40 l215 0" />    <path stroke-dasharray="20,10,5,5,5,10" d="M5 60 l215 0" />  </g></svg>

```html
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <g fill="none" stroke="black" stroke-width="4">
    <path stroke-dasharray="5,5" d="M5 20 l215 0" />
    <path stroke-dasharray="10,10" d="M5 40 l215 0" />
    <path stroke-dasharray="20,10,5,5,5,10" d="M5 60 l215 0" />
  </g>
</svg>
```



## G

### <g>

SVG中的<g></g>标签用来组织其他SVG元素

G标签不支持X/Y属性来进行定位，需要修改位置时，可以使用transform="translate(x,y)"属性或者CSS来修改。注意：作为属性时，X,Y值不支持单位

## 滤镜

SVG可用的滤镜是：

- feBlend - 与图像相结合的滤镜
- feColorMatrix - 用于彩色滤光片转换
- feComponentTransfer
- feComposite
- feConvolveMatrix
- feDiffuseLighting
- feDisplacementMap
- feFlood
- feGaussianBlur
- feImage
- feMerge
- feMorphology
- feOffset - 过滤阴影
- feSpecularLighting
- feTile
- feTurbulence
- feDistantLight - 用于照明过滤
- fePointLight - 用于照明过滤
- feSpotLight - 用于照明过滤

### <defs>

所有互联网的SVG滤镜定义在<defs>元素中。<defs>元素定义短并含有特殊元素（如滤镜）定义

### <filter>

<filter>标签用来定义SVG滤镜。<filter>标签使用必需的id属性来定义向图形应用哪个滤镜

### 高斯模糊

<svg xmlns="http://www.w3.org/2000/svg" version="1.1">  
    <defs>    
        <filter id="f1" x="0" y="0">      
        	<feGaussianBlur in="SourceGraphic" stdDeviation="10" />    
        </filter>  
    </defs>  
    <rect width="90" height="90" stroke="green" stroke-width="3"  fill="yellow"  filter="url(#f1)" />
</svg>

```html
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <defs>
    <filter id="f1" x="0" y="0">
      <feGaussianBlur in="SourceGraphic" stdDeviation="15" />
    </filter>
  </defs>
  <rect width="90" height="90" stroke="green" stroke-width="3"
  fill="yellow" filter="url(#f1)" />
</svg>
```

> 解析

- <filter>元素id属性定义一个滤镜的唯一名称
- <feGaussianBlur>元素定义模糊效果
- in="SourceGraphic"这个部分定义了由整个图像创建效果
- stdDeviation属性定义模糊量
- <rect>元素的滤镜属性用来把元素链接到"f1"滤镜

### 阴影

<feOffset>元素是用于创建阴影效果。我们的想法是采取一个SVG图形（图像或元素）并移动它在xy平面上一点儿。

第一个例子偏移一个矩形（带<feOffset>），然后混合偏移图像顶部（含<feBlend>）

<svg xmlns="http://www.w3.org/2000/svg" version="1.1">  <defs>    <filter id="f1" x="0" y="0" width="200%" height="200%">      <feOffset result="offOut" in="SourceGraphic" dx="20" dy="20" />      <feBlend in="SourceGraphic" in2="offOut" mode="normal" />    </filter>  </defs>  <rect width="90" height="90" stroke="green" stroke-width="3"  fill="yellow" filter="url(#f1)" /></svg>

```html
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <defs>
    <filter id="f1" x="0" y="0" width="200%" height="200%">
      <feOffset result="offOut" in="SourceGraphic" dx="20" dy="20" />
      <feBlend in="SourceGraphic" in2="offOut" mode="normal" />
    </filter>
  </defs>
  <rect width="90" height="90" stroke="green" stroke-width="3"
  fill="yellow" filter="url(#f1)" />
</svg>
```

> 解析

- <filter>元素id属性定义一个滤镜的唯一名称
- <rect>元素的滤镜属性用来把元素链接到"f1"滤镜

## 渐变

### 类型

- Linear
- Radial

### <linearGradient

<linearGradient>元素用于定义线性渐变。

<linearGradient>标签必须嵌套在<defs>的内部。<defs>标签是definitions的缩写，它可对诸如渐变之类的特殊元素进行定义。

线性渐变可以定义为水平，垂直或角渐变

<svg xmlns="http://www.w3.org/2000/svg" version="1.1">   <defs>     <linearGradient id="grad1" x1="0%" y1="0%" x2="100%" y2="0%">       <stop offset="0%" style="stop-color:rgb(255,255,0);stop-opacity:1" />       <stop offset="100%" style="stop-color:rgb(255,0,0);stop-opacity:1" />     </linearGradient>   </defs>   <ellipse cx="200" cy="70" rx="85" ry="55" fill="url(#grad1)" /> </svg>

```html
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <defs>
    <linearGradient id="grad1" x1="0%" y1="0%" x2="100%" y2="0%">
      <stop offset="0%" style="stop-color:rgb(255,255,0);stop-opacity:1" />
      <stop offset="100%" style="stop-color:rgb(255,0,0);stop-opacity:1" />
    </linearGradient>
  </defs>
  <ellipse cx="200" cy="70" rx="85" ry="55" fill="url(#grad1)" />
</svg>
```

> 解析

- <linearGradient>标签的id属性可为渐变定义一个唯一的名称
- <linearGradient>标签的X1，X2，Y1，Y2属性定义渐变开始和结束位置
- 渐变的颜色范围可由两种或多种颜色组成。每种颜色通过一个<stop>标签来规定。offset属性用来定义渐变的开始和结束位置。
- 填充属性把 ellipse 元素链接到此渐变
- 一个渐变上的颜色坡度，是用`stop`元素定义的。`stop`元素可以是[``](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Element/linearGradient)元素或者[``](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Element/radialGradient)元素的子元素

### <radialGradient

<svg xmlns="http://www.w3.org/2000/svg" version="1.1">  <defs>    <radialGradient id="grad1" cx="50%" cy="50%" r="50%" fx="50%" fy="50%">      <stop offset="0%" style="stop-color:rgb(255,255,255);      stop-opacity:0" />      <stop offset="100%" style="stop-color:rgb(0,0,255);stop-opacity:1" />    </radialGradient>  </defs>  <ellipse cx="200" cy="70" rx="85" ry="55" fill="url(#grad1)" /></svg>

```html
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <defs>
    <radialGradient id="grad1" cx="50%" cy="50%" r="50%" fx="50%" fy="50%">
      <stop offset="0%" style="stop-color:rgb(255,255,255);
      stop-opacity:0" />
      <stop offset="100%" style="stop-color:rgb(0,0,255);stop-opacity:1" />
    </radialGradient>
  </defs>
  <ellipse cx="200" cy="70" rx="85" ry="55" fill="url(#grad1)" />
</svg>
```

