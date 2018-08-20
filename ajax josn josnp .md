

## 局部刷新如何实现？

​	AJAX技术可以实现局部刷新；

# AJAX简介

- AJAX是一种在无需重新加载整个网页的情况下，能够更新部分网页的技术。

- AJAX是一种用于创建快速动态网页的技术。通过在后台与服务器进行少量数据交换。

- AJAX可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。

- AJAX应用可以仅向服务器发送并取回必需的数据，并在客户端采用JavaScript处理来自服务器的响应。因此在服务器和浏览器之间交换的数据大量减少，同时很多的处理工作可以在发出请求的客户端机器上完成，所以Web服务器的处理时间也减少了。

  ​

  ​

### AJAX：是一个技术的组合；

A：Async：异步；             J： Javascript；

A：AND；                            X： XML：可扩展的  标签语言 ，也是一种数据格式；

##### XML：可以自定义标签 如下：

```html
<?xml version="1.0" encoding="UTF-8"?>
<studentlist>
    <student>
        <name>高文静</name>
        <age>18</age>
        <height>172</height>
        <sex>2</sex>
        <address>
            <province>四川</province>
            <city>成都</city>
            <area>武侯区</area>
        </address>
    </student>
    <student>
        <name>屈向</name>
    </student>
    <student>
        <name>康若曼</name>
    </student>

```

### JSON:一种对象类型的数据格式

JSON数据集使用数组来表示；

```json
[{
		Name:’李老板’,
		Age:20,
		Height:180
},
{
		Name:’雷超’,
		Age:20,
		Height:180
}]

```



## XMLHttpRequest：

实现AJAX的核心对象

XMLHttpRequest 对象用于在后台与服务器交换数据。

XMLHttpRequest 对象是*开发者的梦想*，因为您能够：

- 在不重新加载页面的情况下更新网页
- 在页面已加载后从服务器请求数据
- 在页面已加载后从服务器接收数据
- 在后台向服务器发送数据



```js
//创建一个xhr对象
        var xhr = new XMLHttpRequest();

```

请求的服务器地址是html、jsp、aspx等等都是可以的，也就是说AJAX和后台服务器语言没有关系，只需要返回对应的数据即可；

### XMlHTTPrequest的属性

| 属性                 | 说明                                       |
| ------------------ | ---------------------------------------- |
| readyState         | 表示XMLHttpRequest对象的状态：0：未初始化。对象已创建，未调用open；1：open方法成功调用，但Sendf方法未调用；2：send方法已经调用，尚未开始接受数据；3：正在接受数据。Http响应头信息已经接受，但尚未接收完成；4：完成，即响应数据接受完成。 |
| Onreadystatechange | 请求状态改变的事件触发器（readyState变化时会调用这个属性上注册的javascript函数）。 |
| responseText       | 服务器响应的文本内容                               |
| responseXML        | 服务器响应的XML内容对应的DOM对象                      |
| Status             | 服务器返回的http状态码。200表示“成功”，404表示“未找到”，500表示“服务器内部错误”等。 |
| statusText         | 服务器返回状态的文本信息。                            |

### XMlHTTPrequest的属性

| 方法                                       | 说明                                       |
| ---------------------------------------- | ---------------------------------------- |
| Open(string method,string url,boolean asynch,String username,string password) | 指定和服务器端交互的HTTP方法，URL地址，即其他请求信息；Method:表示http请求方法，一般使用"GET","POST".url：表示请求的服务器的地址；asynch：表示是否采用异步方法，true为异步，false为同步；后边两个可以不指定，username和password分别表示用户名和密码，提供http认证机制需要的用户名和密码。 |
| Send(content)                            | 向服务器发出请求，如果采用异步方式，该方法会立即返回。content可以指定为null表示不发送数据，其内容可以是DOM对象，输入流或字符串。 |
| SetRequestHeader(String header,String Value) | 设置HTTP请求中的指定头部header的值为value.此方法需在open方法以后调用，一般在post方式中使用。 |
| getAllResponseHeaders()                  | 返回包含Http的所有响应头信息，其中相应头包括Content-length,date,uri等内容。返回值是一个字符串，包含所有头信息，其中每个键名和键值用冒号分开，每一组键之间用CR和LF（回车加换行符）来分隔！ |
| getResponseHeader(String header)         | 返回HTTP响应头中指定的键名header对应的值                |
| Abort()                                  | 停止当前http请求。对应的XMLHttpRequest对象会复位到未初始化的状态。 |

xhr.responseText接收的数据是string类型，需要转换成JSON

```json
JSON.parse();//是把JSON格式的字符串转成对象；
JOSN.stringify;//把JSON格式的数据转成字符串；
```



## 事件处理过程

​	*事件源**.**事件** = function(){*

​		事件处理过程;*

*}*



## 安全的同源策略

​	出于安全及数据保护考虑，浏览器中有“同源策略”这么个概念。同源策略不允许用一个域上的脚本代码去获取或操作另一个域上的数据，比如AJAX你在请求数据时，如果数据处理域和当前访问域不同，是无法正常执行的。比如www.my.com下的一个页面使用AJAX的方式访问www.your.com.cn/c.php页面，是行不通的，浏览器不允许这种操作套路存在。

我们的AJAX请求只能请求自己的域下的地址；

#### 同源：

- 域名要相同；
- 端口要相同；
- 协议要相同；http   https



## JSONP的基本原理

AJAX请求受同源策略影响，不允许跨域

然而script标签src属性中的引用地址却可以访问其它域下的JS文件，

比如我们在使用jQuery时，就可以使用如下文件地址：https://cdn.bootcss.com/jquery/3.2.1/jquery.js。

这么一来，Server上的数据处理程序可以不返回JSON格式的数据，而是返回调用一个函数的js代码，这样就可以实现跨域。





​       

​       