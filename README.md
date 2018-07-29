# webserviceByHTTP
使用HTTP原生方式调用webservice





## webservice是什么
webservice的概念，这是一种技术，是一种跨越编程语言和操作系统平台的远程调用技术.<br>

* 跨越编程语言
> 就是服务器和客户端可以使用不同的语言(貌似现在的都是这样的)，例如：服务器使用Java语言，客户端可以使用其他的语言编写，反之亦然。<br>

* 跨越操作系统平台
> 就是指服务器端和客户端可以在不同的操纵系统上运行。<br>
* 远程调用
> 即一台计算机的应用可以调用其他计算机上的应用。<br>
简单的说，wenservice 可以让我们调用一些接口或者方法(已经有人写好的）例如关于天气，可以在 http://www.webxml.com.cn/WebServices/WeatherWebService.asmx?wsdl 中使用getWeatherbyCityName方法来获得城市的天气，这个方法就是我们在WSDL文件中找到的。

## webservice运行原理
webservice中，有三种技术：XML,SOAP，WSDL。<br>
XML 简单就是我们所想的那个xml(常见于web.xml，spring-config.xml等等)。<br>
SOAP 是一种协议（TCP/IP概念一样，就是协议，一种webservice中认可的规则），是基于XML的简易协议，可以使应用程序在HTTP之上进行信息交换，也就是说SOAP是用于访问网络服务的协议。<br>
WSDL 相当于目录，可以同过这个文件查找到我们所用到的接口方法。<br>

## 简单的示例
所有的关于Java成语的示例一般都是 HelloWorld ， 或者 Hello... 的，我也不例外。<br>
在eclipse中新建Java项目，命名为HelloWeb。<br>
我的是这样的<br>
![HelloWeb项目](https://github.com/Zhangchao999/webserviceByHTTP/raw/master/pictures/1.png)
<br>
通过Endponint.publish(address,implement);发布服务，我发布的是 http://127.0.0.1:8888/HelloWeb/sayHello
可以在 地址后加?wsdl 来查看WSDL文件 例如：http://127.0.0.1:8888/HelloWeb/sayHello?wsdl 
这个服务是我现在发布的，只是用来测试的，如果你要访问肯定是不会访问到的。<br>
让我们来看看这个WSDL文件，顺便分析分析他的结构。
![WSDL文件](https://github.com/Zhangchao999/webserviceByHTTP/raw/master/pictures/2.png)
<br>
先来解释一下标签的意思：<br>
* service 
	> 相关端口的集合，包括其关联的接口、操作、消息等。
* Binding
	> 特定端口类型的具体协议和数据格式规范。
* portType
	> 服务端点，描述webservice可被执行的操作方法，以及相关的消息，通过Binding指向portType。
* message 
	> 定义一个操作方法的数据类型。
* type 
	> 定义webservice使用的全部数据类型。
<br>
如何查看：
WSDL文档应该从下往上看，以我们的为例：<br>
1、先看service标签，这个标签下的binding="tns:HelloServiceImplPortBinding" ,我们看HelloServiceImplPortBinding。<br>
2、往上找，找到binding标签，找到name 为 HelloServiceImplPortBinding 的，这里只有一个，但是第三方提供的或有很多个，
找到type="tns:HelloServiceImpl".<br>
3、继续往上找，找到portType 标签 ，找operation ,这就是我们可以用的方法，详细的数据可以在之上的message标签中找到详细的输入输出参数。<br>
也可以看图片，基本都标了出来。<br>

### 调用
重点来了，以上的部署及解释都是为了现在的调用。<br>
##### 方法一、使用JDK 自带的wsimport 生成webservice客户端。
在eclipse中新建Java项目，项目名为getHelloWeb，使用cmd进入该项目的src文件下<br>
之后输入 wsimport -p com.zc.hello -s . http://127.0.0.1:8888/HelloWeb/sayHello?wsdl 命令。就会在src目录下生成可直接使用的客户端。<br>
cmd界面：<br>
![wsimport命令界面](https://github.com/Zhangchao999/webserviceByHTTP/raw/master/pictures/3.png)
形成的客户端：<br>
![客户端界面](https://github.com/Zhangchao999/webserviceByHTTP/raw/master/pictures/4.png)
使用方式：<br>
新建一个Java文件(HelloClient.java)：<br>

```java 
package com.zc.hello;

public class HelloClient {
	public static void main(String[] args) {
		HelloServiceImpl helloServiceImpl = new HelloServiceImplService().getHelloServiceImplPort();
		String result = helloServiceImpl.sayHello(" ,哈哈哈我是输出");
		System.out.println("Result:"+result);
	}
}
```
```java
// 输出显示

Result:你好  ,哈哈哈我是输出
```
这样，我们就使用了自己发布的service，若是把该WSDL地址，告诉伙伴，他们也是可以访问到的(前提是你的先发布service),是不是很神奇。

#### 第二种、


