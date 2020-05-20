# three.js

## 基本步骤

### 创建场景

#### 创建场景

- ```var scene = new THREE.Scene()```

#### 创建相机

##### 创建一个透视摄像机

`````javascript
camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 0.1, 1000 );
camera.position.set(x,y,z);//设置相机位置
camera.lookAt(camera.position);//设置相机方向(指向的场景对象)
`````

- 第一个参数是**视野角度（FOV）**,**长宽比（aspect ratio)**,**近截面**（near）和**远截面**（far)

##### 创建一个正投摄像机

```javascript
var camera = new THREE.OrthographicCamera(45,window.innerWidth / window.innerHeight, 0.1, 1000);
```



#### 创建渲染器

```javascript
var renderer = new THREE.WebGLRenderer();
renderer.setSize(window.innerWidth,window.innerHeight);//设置渲染区域尺寸
renderer.setClearColor(0x000000, 1);//设置背景颜色
```

### 整个程序的结构

<img src="C:\Users\asus\Documents\makedown\three.png" alt="iconfinder" style="zoom:100%;" />

### 创建物体

#### 创建一个立方体

```javascript
var geometry = new THREE.BoxGeometry( 1, 1, 1 );
```

+ 这个对象包含了一个立方体中所有的顶点（**vertices**）和面（**faces**）,长宽高都是1

#### 创建一个球体

```javascript
var geometry=new THREE.SphereGenmetry(40,50,60)
```



#### 给物体添加材质

+ ```var material = new THREE.MeshBasicMaterial( { color: 0x00ff00 } );```
+ Three.js自带了几种材质，在这里我们使用的是**MeshBasicMaterial**

#### 放入网格中

+ ```var cube = new THREE.Mesh( geometry, material );```
+ 网格包含一个几何体以及作用在此几何体上的材质，我们可以直接将网格对象放入到我们的场景中，并让它在场景中自由移动。

#### 将网格添加到场景中

+ ```scene.add( cube ); ```
+ ```camera.position.z = 5;```
+ 默认情况下，当我们调用**scene.add()**的时候，物体将会被添加到**(0,0,0)**坐标
+ 为了防止这种情况的发生，我们只需要将摄像机稍微向外移动一些即可。

### 渲染场景

+ ```renderer.render( scene, camera );```

### demo1

```javascript
<html>
	<head>
		<title>My first three.js app</title>
		<style>
			body { margin: 0; }
			canvas { width: 100%; height: 100% }
		</style>
	</head>
	<body>
		<script src="js/three.js"></script>
		<script>
			var scene = new THREE.Scene();
			var camera = new THREE.PerspectiveCamera( 75, window.innerWidth/window.innerHeight, 0.1, 1000 );

			var renderer = new THREE.WebGLRenderer();
			renderer.setSize( window.innerWidth, window.innerHeight );
			document.body.appendChild( renderer.domElement );

			var geometry = new THREE.BoxGeometry( 1, 1, 1 );
			var material = new THREE.MeshBasicMaterial( { color: 0x00ff00 } );
			var cube = new THREE.Mesh( geometry, material );
			scene.add( cube );

			camera.position.z = 5;

			var animate = function () {
				requestAnimationFrame( animate );

				cube.rotation.x += 0.01;
				cube.rotation.y += 0.01;

				renderer.render( scene, camera );
			};

			animate();
		</script>
	</body>
</html>
```

### 光源设置

#### 点光源

```javascript
var point = new THREE.PointLight(0xffffff) 
point.position.set(x,y,z);//点光源位置
scene.add(point)//点光源添加到场景中
```

#### 环境光

```javascript
var ambient=new THREE.ambientLight(0x444444);
scene.add(ambient);
```



## 简单的动画

### 周期性渲染

### 让物体动起来1

```javascript
//setInterval()是一个周期性函数，就像一个定时器，每隔多少毫秒ms执行一次某个函数
function render(){
    renderer.render(scene,camera);
    mesh.rotateY(1);
}
setInterval("renderer",20);
//间隔20ms周期性调用函数fun,20ms也就是刷新频率是50FPS(1s/20ms)，每秒渲染50次
```



### 让物体动起来2

``` javascript
function animate() {
	requestAnimationFrame( animate );
	//效果比setInterval,一般默认保持60FPS的频率
	cube.rotation.x += 0.01; cube.rotation.y += 0.01;
	renderer.render( scene, camera ); 
}
animate();
```

## 鼠标操作

### 准备工作

为了使用鼠标操作三维场景，可以借助three.js众多控件之一`OrbitControls.js`，可以在下载的`three.js-master`文件中找到(`three.js-master\examples\js\controls)`。 然后和引入`three.js`文件一样在html文件中引入控件`OrbitControls.js `

 ```javascript
var controls=new THREE.OrbitControls(camera,renderer,domElement);
//创建控件对象
controls.addEventListener('change',render);
//监听鼠标、键盘事件
 ```

### 场景操作

+ 缩放：滚动—鼠标中键

+ 旋转:拖动—鼠标左键
+ 平移:拖动—鼠标右键

### 注意

```javascript
function render() {
  renderer.render(scene,camera);//执行渲染操作
  // mesh.rotateY(0.01);//每次绕y轴旋转0.01弧度
  requestAnimationFrame(render);//请求再次执行渲染函数render
}
render();
var controls = new THREE.OrbitControls(camera);
//创建控件对象
// 已经通过requestAnimationFrame(render);周期性执行render函数，没必要再通过监听鼠标事件执行render函数
// controls.addEventListener('change', render)
```

## 插入图形

### SphereGeometry构造函数

```javascript
var box=new THREE.SphereGeometry(60,40,40);
//radius, widthSegments, heightSegments
//widthSegments, heightSegments表示细分曲线,越多越接近圆
//创建一个球体几何对象
```

### BoxGeometry构造函数

```javascript
var geometry = new THREE.BoxGeometry(100, 100, 100);
//长方体 参数：长，宽，高
```

### CylinderGeometry构造函数

```javascript
var geometry = new THREE.CylinderGeometry( 50, 50, 100, 25 );
//圆柱  参数：圆柱面顶部、底部直径50,50   高度100  圆周分段数
```

### OctahedronGeometry构造函数

```javascript
var geometry = new THREE.OctahedronGeometry(50);
// 正八面体
```

### DodecahedronGeometry构造函数

```javascript
var geometry = new THREE.DodecahedronGeometry(50);
// 正十二面体
```

### IcosahedronGeometry构造函数

```javascript
var geometry = new THREE.IcosahedronGeometry(50);
// 正二十面体
```

### 辅助三维坐标系AxisHelper

```javascript
var axisHelper = new THREE.AxisHelper(250);
scene.add(axisHelper);
```

threejs三维坐标系老版本名称是`AxisHelper`,新版本名称[AxesHelper](http://www.yanhuangxueyuan.com/threejs/docs/index.html#api/zh/helpers/AxesHelper)。

### demo3

```javascript
// 立方体网格模型
var geometry1 = new THREE.BoxGeometry(100, 100, 100);
var material1 = new THREE.MeshLambertMaterial({
  color: 0x0000ff
}); //材质对象Material
var mesh1 = new THREE.Mesh(geometry1, material1); //网格模型对象Mesh
scene.add(mesh1); //网格模型添加到场景中

// 球体网格模型
var geometry2 = new THREE.SphereGeometry(60, 40, 40);
var material2 = new THREE.MeshLambertMaterial({
  color: 0xff00ff
});
var mesh2 = new THREE.Mesh(geometry2, material2); //网格模型对象Mesh
mesh2.translateY(120); //球体网格模型沿Y轴正方向平移120
scene.add(mesh2);

// 圆柱网格模型
var geometry3 = new THREE.CylinderGeometry(50, 50, 100, 25);
var material3 = new THREE.MeshLambertMaterial({
  color: 0xffff00
});
var mesh3 = new THREE.Mesh(geometry3, material3); //网格模型对象Mesh
// mesh3.translateX(120); //球体网格模型沿Y轴正方向平移120
mesh3.position.set(120,0,0);//设置mesh3模型对象的xyz坐标为120,0,0
scene.add(mesh3); //
```

## 材质效果

### 半透明效果

#### 在构造函数中设置

```javascript
var sphereMaterial=new THREE.MeshLamberMaterial({
    color:0xff0000,
    opacity:0.7,
    transparent:true,
    wireframe:false	
})
```

opacity`的值是`0~1`之间，`transparent`表示是否开启透明度效果， 默认是`false`表示透明度设置不起作用，值设置为`true,呈现透明的效果.`wireframe`:将几何图形渲染为线框。 默认值为false

#### 访问材质对象属性

```javascript
material.opacity = 0.5 ;
material.transparent = true ;
```

### 添加高光效果

```javascript
var sphereMaterial=new THREE.MeshPhongMaterial({
    color:0x0000ff,
    specular:0x4488ee,
    shininess:12
})
```

属性`specular`表示球体网格模型的高光颜色

`shininess`属性可以理解为光照强度的系数

### 材质类型

| 材质类型                                                     | 功能                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [MeshBasicMaterial](http://www.yanhuangxueyuan.com/threejs/docs/index.html#api/zh/materials/MeshBasicMaterial) | 基础网格材质，不受光照影响的材质                             |
| [MeshLambertMaterial](http://www.yanhuangxueyuan.com/threejs/docs/index.html#api/zh/materials/MeshLambertMaterial) | Lambert网格材质，与光照有反应，漫反射                        |
| [MeshPhongMaterial](http://www.yanhuangxueyuan.com/threejs/docs/index.html#api/zh/materials/MeshPhongMaterial) | 高光Phong材质,与光照有反应                                   |
| [MeshStandardMaterial](http://www.yanhuangxueyuan.com/threejs/docs/index.html#api/zh/materials/MeshStandardMaterial) | PBR物理材质，相比较高光Phong材质可以更好的模拟金属、玻璃等效果 |

## 光源

### 光源类型

| 光源                                                         | 简介               |
| :----------------------------------------------------------- | :----------------- |
| [AmbientLight](http://www.yanhuangxueyuan.com/threejs/docs/index.html#api/zh/lights/AmbientLight) | 环境光             |
| [PointLight](http://www.yanhuangxueyuan.com/threejs/docs/index.html#api/zh/lights/PointLight) | 点光源             |
| [DirectionalLight](http://www.yanhuangxueyuan.com/threejs/docs/index.html#api/zh/lights/DirectionalLight) | 平行光，比如太阳光 |
| [SpotLight](http://www.yanhuangxueyuan.com/threejs/docs/index.html#api/zh/lights/SpotLight) | 聚光源             |

光源通过`add`方法插入场景中，不插入的话，渲染的时候不会获取光源的信息进行光照计算

### 光源光照强度

通过光源构造函数的参数可以设置光源的颜色,`THREE.AmbientLight(0x444444);`的光照参数`0x444444`改为`0xffffff`,你会发现场景中的立方体渲染效果更明亮

### 光源位置

```javascript
var point = new THREE.PointLight(0xffffff);
point.position.set(400, 200, 300); //点光源位置
scene.add(point); //点光源添加到场景中
```

