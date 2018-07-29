# webserviceByHTTP
使用HTTP原生方式调用webservice





## webservice是什么
webservice的概念，这是一种技术，是一种跨越编程语言和操作系统平台的远程调用技术.<br>
所谓的跨越编程语言，就是服务器和客户端可以使用不同的语言(貌似现在的都是这样的)，例如：服务器使用Java语言，客户端可以使用其他的语言编写，反之亦然。<br>
跨越操作系统平台，就是指服务器端和客户端可以在不同的操纵系统上运行。<br>
远程调用，即一台计算机的应用可以调用其他计算机上的应用。<br>
简单的说，wenservice 可以让我们调用一些接口或者方法(已经有人写好的）例如关于天气，可以在 http://www.webxml.com.cn/WebServices/WeatherWebService.asmx?wsdl 中使用getWeatherbyCityName方法来获得城市的天气

## webservice运行原理
webservice中，有三种技术：XML,SOAP，WSDL。<br>
XML 简单就是我们所想的那个xml(常见于web.xml，spring-config.xml等等)。<br>
SOAP 是一种协议（TCP/IP概念一样，就是协议，一种webservice中认可的规则），是基于XML的简易协议，可以使应用程序在HTTP之上进行信息交换，也就是说SOAP是用于访问网络服务的协议。<br>
WSDL 相当于目录，可以同过这个文件查找到我们所用到的接口方法。<br>