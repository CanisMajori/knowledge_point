# JS复习笔记（数据类型，变量，对象）

### 	1.弹出选择框：confirm('你确定执行该操作？'); 返回TRUE(确定)或FALSE（取消0）

```js
window.onload=function () {
        document.getElementsByClassName('app')[0].onclick=function () {
            console.log(2);
            confirm('quedign');
        }
    };
```

### 	2.打印信息

```js
	console.log(2);
    console.error(2);//输出2错误
    console.warn(2);//输出2警告
    console.info(2);//同log
```

### 	3.获取元素

```js
	document.querySelector('li');
    document.querySelectorAll('d');
```

### 	4.数据类型分类

```js
原始类型：数字、字符串、布尔值、null(空)、undefined(未定义)；
<!--nusbool--> number null undefind string bool
```

```js
对象类型：原始类型之外的类型，如数组、对象、函数等；
 <!--[] {} ()=>{} -->
```

### 	5.数字类型

```html
<li>正无穷大：Infinity，负无穷大：-Infinity；</li>
<li>  isNaN()：isNaN=isNot(不是)a(一个)Number(数字),检查一个值是不是数字，
    如：isNaN(5)，返回false；
  isNaN('hello')，返回true；</li>
```

​	js实数型有精度误差，js是用二进制来表示的

```js
var a = 0.3 - 0.2;
var b = 0.2 - 0.1;
console.log(a);//0.9999~
console.log(b);//0.1
console.log(a==b);//false

//转成整数后再运算
var a = 0.3*10 - 0.2*10;
var b = 0.2*10 - 0.1*10;
console.log(a/10);//0.1
console.log(b/10);//0.1
console.log(a==b);//true


console.log(12 + NaN);//NaN
console.log(203 + undefined);//NaN
console.log(3 + 5 + '猜猜看');//8cck
```

### 	6.字符串转义

```js
\t：水平制表符；
\n：换行符；
\r：回车符；
\"：双引号，而不是字符串分界符；
\'：单引号，而不是字符串分界符；
\\：反斜杠；
```

### 	7.布尔值转换

js的所有数据都可以转为bool值

以下为false，其余为true

```js
<!--un0''  undefined null NaN 0 -0  '' -->
undefined
null
0
-0
NaN
'' 
```

### 	8.null和 undefined

```js
typeof null：返回的是字符串object
typeof undefined：返回的是字符串undefined
null==undefined   //true
null===undefined  //false
```

### 	9.全局对象

```html
常见全局对象：
<pre>
全局属性：如undefined、Infinity、NaN等；
全局函数：如parseInt()、eval()、isNaN()、toFixed()等；
  parserInt():强转数字类型  
  eval(string):计算js代码字符串结果（如果不是js代码会报错）
  toFixed(number): Number 四舍五入为指定小数位数的数字。

构造函数：如Array()、String()、Date()等；
全局对象：如Math；
</pre>
<h1>匿名函数具有全局性，因此this对象同常指向window</h1>
```

```js
var str = 'hqyj h5';
str.len = 6;
var l   = str.len;
console.log(l);//undefind
```

```js
//创建一个原始类型：字符串
var str = 'hqyj h5';
//只要引用字符串的属性，JavaScript就会调用new String(str)把str转换为对象
str.len = 6;
//一旦属性引用结束，新创建的对象就会销毁，当然该对象的属性也就不存在了
//所以这里再引用时就是一个不存在的属性  
var l   = str.len;
//打印：undefined
console.log(l);
```

###  9.变量提升 

```html
<li>变量的提升是指会提升变量的声明，但是不提升变量的赋值；</li>
<li>解释器在执行js代码的时候，会把所有的声明，包括变量和函数的声明，都会提到最前面<li>
```

### 10.运算符

in运算符：检查右侧对象里面是否拥有左侧属性名，如果有返回true

```js
 var a = {x:1, y:2, z:''};
 console.log(a);
 console.log('x' in a);//true
 console.log('z1' in a);//false
 console.log('toString' in a);//true
 console.log('isPrototypeOf' in a);//true
```

instanceof:检查左侧的对象是否是右侧类的实例，如果是返回true；
如果一个对象是一个“父类”的子类的实例，则一样返回true
还有记住一点所有的对象都是Object的子类

```js
var d = new Date();
        console.log(d instanceof Date);//true
        console.log(d instanceof Array);//false
        console.log(d instanceof String);//false
        console.log(d instanceof Object);//true
```

typeof

```js
X               typeof X
---------------------------
undefined       "undefined"
null            "object"
true||false     "boolean"
数字||NaN       "number"
字符串          "string"
函数            "function"
内置对象        "object"
```

### 11.检测属性

in：检查一个属性是否属于某个对象，包括继承来的属性；

```js
var person = {name:'yourname', age:10};
console.log('name' in person); //true
console.log('sex' in person);  //false
console.log('toString' in person); //true
```

hasOwnProperty() 方法可以接收一个字符参数，用来判断对象中是否存在以字符参数命名的属性。它只会查找自身属性，不会根据原型链进行查找。

```js
var obj = {x:"1"};
obj.y = function(){};
console.log(obj.hasOwnProperty("x")); //true
console.log(obj.hasOwnProperty("y")); //true 方法也是属性
console.log(obj.hasOwnProperty("z")); //false 属性不存在
console.log(obj.hasOwnProperty("toString")); //false hasOwnProperty是继承Object的属性，自身属性中不存在
```

propertyIsEnumerable()方法在 hasOwnProperty() 的基础上，校验属性是否为枚举属性。也就是说属性必须满足为自身属性且为枚举属性时，才会返回 true。

```js
var obj = {x:"1"};
obj.y = function(){};
Object.defineProperty(obj, 'z', {value : '2', enumerable : true });
Object.defineProperty(obj, 'w', {value : '3', enumerable : false });
console.log(obj.propertyIsEnumerable("x")); //true 属性默认为枚举属性
console.log(obj.propertyIsEnumerable("y")); //true 方法也是属性
console.log(obj.propertyIsEnumerable("z")); //true
console.log(obj.propertyIsEnumerable("w")); //false 属性不是枚举属性
console.log(obj.propertyIsEnumerable("v")); //false 属性不存在
console.log(obj.propertyIsEnumerable("toString")); //false propertyIsEnumerable是继承Object的属性，自身属性中不存在
```

检测属性总结：

- hasOwnProperty 自身存在的属性
- propertyIsEnumerable 自身存在的属性，且为枚举属性
- !== undefined 自身存在的属性，继承的属性，不能识别值为 undefined 的属性
- in 自身存在的属性，继承的属性

### 12.对象字符串互转

转成字符串：JSON.stringify()；
还原为对象：JSON.parse()；

```js
var hqyj = {name:'华清远见',add:'科华北路99',tel:['0900', 8304, '0910']};
var str = JSON.stringify(hqyj);
console.log(str);
console.log(typeof str);
var obj1 = JSON.parse(str);
console.log(obj1);
```