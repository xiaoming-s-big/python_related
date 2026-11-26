###### 回顾

//和爬⾍的关联
爬取服务器端的指定数据

【爬虫本质目的: 就是 模拟 客户端请求头 伪装 成为 客户端向 服务器端 爬取数据】



###### 文件操作

//作用:可以将爬取到的数据持久化存储到文件中。

```python
###### 实现流程
打开文件
open(filePath,mode):filePath文件路径，mode表示文件权限(w,r,a...)
读写数据
"read():读取文件中所有的数据
"readlines():按照行对文件数据进行读取
"write():字符串数据写入到文件中

##关闭文件
close()

#### with 关键字
在文件操作中使用with进行文件操作,是可以不需要手动关闭文件
with open() as fp: # fp 自定义变量
    fp.read()


```

###### 序列化

dumps : 将对象转换成字符串

loads：将字符串转换成对象

### 第1章 、Web的基本概念

```python
1.	机制协议的作⽤
2.	http协议⽆状态的特性是什么
3.	cookie是谁创建的，保存在哪⾥，如何实现状态的保持
4.	请求协议：请求头、请求体（请求参数）、请求⽅式（get 和post）

```

#### **软件开发的架构**

```python
#C/S架构    //C/S即：Client与Server ，中⽂意思：客户端与服务器端架构。我们把提供数据的⼀⽅称之为服务器(Server),把访问数据的⼀⽅称为客户端(Client)
#B/S架构   //B/S即：Browser与Server,中⽂意思：浏览器端与服务器端架构。Browser浏览器，其实也是⼀种Client客户端，只是这个客户端不需要⼤家去安装什么应⽤程序，只需在浏览器上通过 HTTP/HTTPS协议请求服务器端相关的资源（⽹⻚资源）即可
```

#### //和爬⾍的关联

爬取服务器端的指定数据  【爬虫本质目的: 就是 模拟 客户端请求头 伪装 成为 客户端向 服务器端 爬取数据】

##### 1.1、HTTP协议

###### 1.1.1 、http协议简介

```python
http协议简介:HTTP协议是Hyper Text Transfer Protocol（超⽂本传输协议）的缩写,是⽤于服务器与本地浏览器之间传输超⽂本的传送协议
#超⽂本：超⽂本就是指“含有指向其他资源链接”内容的⽂本
协议：HTTP协议就是服务器（Server）和客户端（Client）之间进⾏数据交互（相互传输数据）的⼀种形式
```

###### 1.1.2、 http协议特性

###### ##基于请求－响应模式

```python
#HTTP协议规定    请求从客户端发出,后服务器端响应该请求并返回。 //换句话说,肯定是先从客户端开始建⽴通信的,服务器端在没有接收到请求之前不会发送响应
# 基于请求－响应模式 //http协议特性
HTTP 协议自身不具备保存之前发送过的请求或响应的功能 //协议本身并不保留之前⼀切的请求或响应的相关信息
##http协议包含由浏览器发送数据到服务器需要遵循的【请求协议】与服务器发送数据到浏览器需要遵循的【响应协议】。
```

###### ##⽆状态(重要)

```python
# HTTP协议⾃身 背景 协议本身并不保留之前⼀切的请求或响应的相关信息
##状态 
状态可以理解为客户端和服务器在某次会话/通信中产⽣的数据，
##⽆状态
那⽆状态的就以为这些数据不会被保留。如果会话中产⽣的数据是我们需要保存的，也就是说要“保持状态

#cookie 创建的背景  HTTP/1.1虽然是⽆状态协议,但为了实现期望的保持状态功能,于是引⼊了Cookie技术
  可是,随着Web的不断发展,因⽆状态⽽导致业务处理变得棘⼿的情况增多了。⽐如,⽤户登录到⼀家购物⽹站,即使他跳转到该站的其他⻚⾯后,也需要能继续保持登录状态。⽹站为了能够掌握是谁送出的请求,需要保存⽤户的状态,HTTP/1.1虽然是⽆状态协议,但为了实现期望的保持状态功能, 于是引⼊了Cookie技术.
    
#cookie 实现的目的  有了Cookie再⽤HTTP协议通信,就可以管理状态了

```

###### 1.1.3 http请求协议/响应协议

```python
##http协议包含由浏览器发送数据到服务器需要遵循的【请求协议】与服务器发送数据到浏览器需要遵循的【响应协议】。
⽤于HTTP协议交互的信息被称为HTTP报⽂。
请求端(客户端) HTTP报⽂叫做请求报⽂,响应端(服务器端)的叫做响应报⽂
HTTP报⽂本身是由多⾏数据构成的字⽂本。
```

###### (1) 请求协议（重要）

##请求方式 /请求头/请求参数 

 <a key:'value'> 写文本</a> 

4 报文头/请求头 // 5 报文体/请求体/请求参数【重要】

```xml
1 请求方法  <POST> 
2 请求URL </chapter17/user.html>
3 HTTP协议及版本 <HTTP/1.1>
4 报文头/请求头    < 4 报文头/请求头>
5 报文体  <name=tom&password=1234&realName=tomson>
    <下面格式为请求协议 参考> <>
POST   /chapter17/user.html  HTTP/1.1
< 4 报文头/请求头
Accept:image/jpeg,application/x-ms-application,米/※’”””
Referer: http://localhost:8088/chapter17/user/register.html?
code=100&time=123123
Accept-Language:zh-CN
User-Agent: Mozilla/4.0(compatible, MSIE 8.0; Windows NT 6.1;
Content-Type:application/x-www-form-urlencoded
Host: localhost:8088
Content-Length:112
Connection:Keep-Alive
Cache-Control:no-cache
Cookie:JSESSIONID=24DF2688E37EE4F66D9669D2542AC17B
> </4>
name=tom&password=1234&realName=tomson

----- <a key:'value'> 写文本</a> ------
  4 报文头/请求头  
<请求头中存储的是该请求的⼀些主要说明（⾃我介绍）。
服务器据此获取客户端的信息。                       
accept:  		 	 浏览器通过这个头告诉服务器，它所⽀持的数据类型
Referer：    		浏览器通过这个头告诉服务器，客户机是哪个⻚⾯来的 防盗链
Accept-Language：	浏览器通过这个头告诉服务器，它的语⾔环境
User-Agent：			请求载体的身份标识
Host：				浏览器通过这个头告诉服务器，想访问哪台主机
Connection：			浏览器通过这个头告诉服务器，请求完后是断开链接还是何持链接
Accept-Charset:  	 浏览器通过这个头告诉服务器，它⽀持哪种字符集
Accept-Encoding：	浏览器通过这个头告诉服务器，⽀持的压缩格式
If-Modified-Since:   浏览器通过这个头告诉服务器，缓存数据的时间
X-Requested-With: XMLHttpRequest 代表通过ajax⽅式进⾏访问
>
    </请求头中存储的是该请求的⼀些主要说明（⾃我介绍）。>
 ----- <a key:'value'> 写文本</a> ------
  5 报⽂体/请求体/请求参数：双标签描述
<        
5 报⽂体/请求体/请求参数：
 常被叫做请求体/请求参数，请求体中存储的是将要传输/ 发送给服务器的数据信息。
请求⽅式: get与post请求
   get请求
    get请求:GET提交的数据会放在URL之后，以?分割URL和传输数据，参数之间以&相连，如EditBook?
   name=test1&id=123456
    post请求:POST⽅法是把提交的数据放在HTTP包的请求体中.
	GET提交的数据⼤⼩有限制（因为浏览器对URL的⻓度有限制），⽽POST⽅法提交的数据没有⼤⼩限制，且携带的请求数据不可以 明⽂⽅式 连接在url中
    >
   报⽂体/请求体/请求参数 概述
    <>
    

```

###### ##请求⽅式 get//post请求

##请求方式 /请求头/请求参数  //请求协议 

```xml
<#请求⽅式: get与post请求>
   get请求
    get请求:GET提交的数据会放在URL之后，以? 分割URL和传输数据，参数之间以&相连，如EditBook?
   name=test1&id=123456
    
   post请求:POST⽅法是把提交的数据放在HTTP包的请求体中.
	GET提交的数据⼤⼩有限制（因为浏览器对URL的⻓度有限制），⽽POST⽅法提交的数据没有⼤⼩限制，且携带的请求数据不可以明⽂⽅式 连接在url中
```



###### (2) 响应协议（了解）

```xml
<  ###//// 响应报文的构成
1 协议版本 <HTTP/1.1>
2  < # 关于状态码下文还有例子解释> 状态码 <200>
3       <> 状态码的原因短语 <OK>
             
HTTP/1.1 200  OK

Date:Tue,10 Jul 2012 06:50:15 GMTContent-Length:362Content-Type:text/html
	<html> 
    .......    主体
					主体
  >  

///响应头
<响应头
响应头中存储的是该响应的⼀些主要说明（⾃我介绍）。客户端据此获取服务器的相关信息   
        
Location: 				 服务器通过这个头，来告诉浏览器跳到哪⾥
Server：					服务器通过这个头，告诉浏览器服务器的型号

Content-Encoding：		服务器通过这个头，告诉浏览器，数据的压缩格式
Content-Length: 		 服务器通过这个头，告诉浏览器回送数据的⻓度
Content-Language: 		 服务器通过这个头，告诉浏览器语⾔环境
Content-Type：			服务器通过这个头，告诉浏览器回送数据的类型
Refresh：				服务器通过这个头，告诉浏览器定时刷新
Content-Disposition: 	 服务器通过这个头，告诉浏览器以下载⽅式打数据
Transfer-Encoding：		服务器通过这个头，告诉浏览器数据是以分块⽅式回送的
Expires: -1 			 控制浏览器不要缓存

Cache-Control: no-cache
Pragma: no-cache >
    
///响应体   
    <
        响应体  根据客户端指定的请求信息，发送给客户端的指定数据
         根据客户端指定的请求信息，发送给客户端的指定数据响应状态码：
         状态码指的是是当客户端向服务器端发送请求时, 返回的请求结果。借助状态码,⽤户可以知道服务器端是正常受理了请求,还是出现了什么问题错误
code        	类别				  	  原因短语
1xX		Informational(信息性状态码)	 接收的请求正在处理
2XX		Success(成功状态码)			  请求正常处理完毕
3XX		Redirection(重定向状态码)		 需要进行附加操作以完成请求
4XX		Client Error(客户端错误状态码)	服务器无法处理请求
5XX		Server Error(服务器错误状态码)	服务器处理请求出错

>
```

##### 1.2 Cookie 概述

###### ## COOKIE的由来

```python
⼤家都知道HTTP协议是⽆状态的。
状态可以理解为客户端和服务器在某次会话中产⽣的数据，那⽆状态的就以为这些数据不会被保留。每当有新的请求发送时,就会有对应的新响应产⽣。协议本身并不保留之前⼀切的请求或响应的相关信息

对服务器来说，每次的请求都是全新的，及时同⼀个客户端发起的多个请求间。随着Web的不断发展,因⽆状态⽽导致业务处理变得棘⼿的情况增多，因此我们需要解决这个问题，也就是说要让http可以“保持状态”，那么Cookie就是在这样
⼀个场景下诞⽣

#cookie 创建的背景  HTTP/1.1虽然是⽆状态协议,但为了实现期望的保持状态功能,于是引⼊了Cookie技术

可是,随着Web的不断发展,因⽆状态⽽导致业务处理变得棘⼿的情况增多了。⽐如,⽤户登录到⼀家购物⽹站,即使他跳转到该站的其他⻚⾯后,也需要能继续保持登录状态。⽹站为了能够掌握是谁送出的请求,需要保存⽤户的状态,HTTP/1.1虽然是⽆状态协议,但为了实现期望的保持状态功能, 于是引⼊了Cookie技术.
#cookie 实现的目的  有了Cookie再⽤HTTP协议通信,就可以管理状态了

```

###### ##什么是cookie

cookie表示的键值对数据是由服务器创建，且存储在客户端浏览器中

```python
#什么是cookie?
cookie是浏览器的技术，Cookie具体指的是⼀段⼩信息，它是服务器发送出来存储在浏览器上的⼀组组键值对,
创建后  下次访问服务器时浏览器会⾃动携带这些键值对，以便服务器提取有⽤信息.
#注意记住：cookie表示的键值对数据是由服务器创建，且存储在客户端浏览器中

```

###### ##cookie的原理（重点）

```python
cookie的⼯作原理是:
    step 1:浏览器访问服务端，带着⼀个空的cookie，然后由服务器产⽣内容，浏览器收到相应后保存在本地；
    step 2:当浏览器再次访问时，浏览器会⾃动带上Cookie，这样服务器就能通过Cookie的内容来判断这个是“谁”了.
    cookie的内容是有服务器⾃主设计的，客户端⽆法⼲涉！
#注意，不同浏览器之间是不共享Cookie的。也就是说在你使⽤IE访问服务器时，服务器会把Cookie发给IE，然后由IE保存起来，当你在使⽤FireFox/guge访问服务器时，不可能把IE保存的Cookie发送给服务器。

```

### 第2章 、HTML 相关

```python
#前言
了解了web相关基本概念以后，我们开始正式接触⽹⻚开发，⽹⻚开发的基础是HTML，所以，本章内容主要是学会如何新建⼀个 HTML ⻚⾯和熟记HTML⽂档的基本结构和主要标签

```

##### 2.1、 HTML概述  {了解}

```xml
HTML，即超⽂本标记语⾔（HyperText Markup Language ]），也可叫做web⻚⾯。扩展名是 .html 或是 .htm
HTML，是⼀种⽤来制作⽹⻚的标准标记语⾔。超⽂本，指的就是超出普通⽂本范畴的⽂档，可以包含⽂本、图⽚、视频、⾳频、链接等元素。
HTML 不是⼀种编程语⾔，⽽是⼀种写给⽹⻚浏览器、具有描述性的标记语⾔。
<总结>
    使⽤HTML语⾔描述的⽂件，需要通过⽹⻚浏览器显示出效果。⽤户在访问⽹⻚时，是把服务器的HTML⽂档下载 到本地客户设备中，然后通过本地客户设备的浏览器将⽂档按顺序解释渲染成对应的⽹⻚效果<>
  < fp 
    ⽹⻚本身是⼀种⽂本⽂件，通过在⽂本⽂件中添加各种各样的标记标签，可以告诉浏览器如何显示标记中的代表的内容，如：HTML中有的标签可以告诉浏览器要把字体放⼤，就像 word⼀样，也有的标签可以告诉浏览器显示指定的图⽚，还有的标签可以告诉浏览器把内容居中或者倾斜等等。
每⼀个HTML标签代表的意义都不⼀样。同样，他们在浏览器中表现出来的外观也是不⼀样的。> 

```

##### 2.2、 HTML结构和标签格式

```xml
<!DOCTYPE html>

<html lang="en">
    
    <head>
<metacharset="UTF-8">
<title>123</title)
    </head>

        <body>
        </body>
</html>
    
1 <!DOCTYPE html> 告诉浏览器使⽤什么样的解析器来 解析html文档
2 <html></html>是文档的开始标记和结束标记。此元素告诉浏览器其自身是一个HTML文档，在它们之间是文档的
    头部<heady>和主体<body>.
3 元素出现在文档的开头部分.与间的内容不会在览器的文档窗口显示，但是其间的元素有特殊要的意义.
4 <title> </title> 定义网页标题，在浏览器标题栏显示
5 <body> </body>  之间的文本是可见的网页主体内容
6 <meta charset="UTF-8">  声明编码方式用tf8
    
```

##### 2.3、标签的语法

```xml
#双标签
<标签名 属性1=“属性值1” 属性2=“属性值2”……>内容部分</标签名>  
#单标签
<标签名 属性1=“属性值1” 属性2=“属性值2”…… />

1、	HTML标签是由尖括号包围的特定关键词
2、	标签分为闭合和⾃闭合两种标签
3、	HTML不区分⼤⼩写
4、	标签可以有若⼲个属性,也可以不带属性,⽐如就不带任何属性

##注意：⽹⻚中显示的我们可以看到的数据/内容都只可以存储或者写在标签之间或者属性中！
```

##### 2.4、基本标签  

```xml
##标题标签
<h1>标题1</h1>
<h2>标题2</h2>
<h3>标题3</h3>
<h4>标题4</h4>
<h5>标题5</h5>
<h6>标题6</h6>

##段落标签
<p>大家好，我是段落1。<p>
<p>大家好，我是段落2。<p>
<p>大家好，我是段落3。<p>

##换⾏标签  <br/>
    <p>大家好，我是段落标签p我按了enter-下
        换行了</p>
    
<p>大家好，我是段落标签p我按了enter-下<br/>换行了
    <//p>
    
##⽂本格式化标签
    HTML提供了⼀系列的⽤于格式化⽂本的标签，可以让我们输出不同外观的元素，⽐如粗体和斜体字。如果需要在⽹⻚中，需要让某些⽂本内容展示的效果丰富点，可以使⽤以下的标签来进⾏格式化
<b>定义粗体文本</b> <br />
    <strong>定义粗体文本方式2</strong><br />
    <em>定义斜体字</em><br />
    <i>定义斜体字方式2</i><br />
    <del>定义删除文本</del><br />
    
##特殊符号
    &nbsp;
    
##<标签⼤致可分为两类
    在XML中，标签主要分为块标签和行标签两大类。以下是对这两种标签的详细介绍：
##块标签 div 盒子
独占一行：块标签总是在新行上开始，并且默认占据整行。
高度宽度可设置：可以设置高度（height）、宽度（width）以及内外边距（margin、padding）。
容纳其他元素：可以包含内联元素和其他块级元素。
##行标签  span 盒子
同行显示：行标签不会自动换行，多个行标签可以在一行内显示。
宽高不可设置：不能直接设置宽度和高度，其尺寸由内容决定。
嵌套限制：只能包含文本或其他内联元素，不能包含块级元素。
总而言之，理解这些标签的特性对于网页布局和样式设计至关重要。通过合理使用块标签和行标签，开发者可以创建出结构清晰、样式美观的网页>
    </标签⼤致可分为两类>
    
##<div和span标签>
     <div> 只是一个块级元素，并无实际的意义。主要通过 css样式为其赋予不同的表现
     <span> 表示了内联行(行内元素),并无实际的意义，主要通过csS样式为其赋予不同的表现
    </div和span标签>
         
块级元素与⾏内元素的区别：所谓块元素，是以另起⼀⾏开始渲染的元素，⾏内元素则不需另起⼀⾏。如果单独在⽹⻚中插⼊这两个元素，不会对⻚⾯产⽣任何的影响。这两个元素是专⻔为定义CSS样式⽽⽣的

```

##### 2.5、超链接标签

###### **2.5.1、超链接基本使用**

```sql
/*超链接是浏览者和服务器的交互的主要⼿段，也叫超级链接或 a链接，是⽹⻚中指向⼀个⽬标的连接关系，这个⽬标可以是⽹⻚、⽹⻚中的具体位置、图⽚、邮件地址、⽂件、应⽤程序等

超链接是⽹⻚中 要的元素之⼀。⼀个⽹站的各个⽹⻚就是通过超链接关联起来的，⽤户通过点击超链接可以从⼀个⽹⻚ 跳转到另⼀个⽹⻚。*/

超链接的属性：
属性		值		描述
href	"网络链接[例如: http://www.baidu.com]本地链接[例如:  F:\htmlindex.html"	 规定链接的跳转目标
title   "百度 "	链接的提示信息
target	"blank[在新建窗口中打开网页]self【默认值，覆盖自身窗口打开网页]"	       与前面四项固定值不同framename是泛指，并不是这个值，这点将在后面框架部分内容中详细介绍，这里可以暂时先略过

```

##### 2.6、img标签

```xml
<在HTML中，图像由标签定义的，它可以⽤来加载图⽚到html ⽹⻚中显示。⽹⻚开发过程中，有三种图⽚格式被⼴泛应⽤到 web⾥，分别是 jpg、png、gif
img标签的属性：
     src属性：指定图像的URL地址，是英⽂source的简写，表示引⼊资源。
    src的值可以是本地计算机存储的图⽚的地址，也可以是⽹络上外部⽹站的图⽚的地址。
    如果src的值不正确，那么浏览器就⽆法正确的图⽚，⽽是显示⼀张裂图。
                                
     alt属性：指定图像⽆法显示时的替换⽂本。当图像显示错误时，在图像位置上显示alt的值。如上所示，就是⾕歌浏览器中，引⼊图像失败后，显示了替换⽂本。
		width属性： 指定引⼊图⽚的显示宽度。 height属性：指定引⼊图⽚的显示⾼度。
		border属性：指定引⼊图⽚的边框宽度，默认为0。
		title属性：悬浮图⽚上的提示⽂字></在HTML中，图像由标签定义的，它可以⽤来加载图⽚到html>
点击图⽚跳转可以配合a标签使⽤
<a><img src="" alt=""></a>
```

##### 2.7、列表标签

```xml
<ul type="square">
<li>item1</li>
<li>item2</li>
<li>item3</li>
</ul>
<ol start="100">
<li>item1</li>
<li>item2</li>
<li>item3</li>
</ol>
```

##### 2.8、表格标签

```xml
在HTML中使⽤table来定义表格。⽹⻚的表格和办公软件⾥⾯的xls⼀样，都是有⾏有列的。HTML使⽤tr标签定义⾏，使⽤ td标签定义列。
语法：
<table border="1">
<tr>
<td>单元格的内容</td>
……
</tr>
……
</table>

1、<table>和</table>表示一个表格的开始和结束。一组<table>...</table>表示一个表格。
2、border用于设置整个表格的边框宽度，默认为0，表示不显示边框。
3、<tr>和</tr>表示表格中的一行的开始和结束。一组<tr>...</tr>，一个表格可以有多行。通过计算table标签中包含多少对tr子标签即可知道一个表格有多少行。
4、<td>和</td>表示表格中的一个单元格的开始和结束。通过计算一个tr里面包含了多少对td自标签即可知道一个表格有多少列，多少的单元格了。

table属性：
属性		值	 描述
<width px、%	  规定表格的宽度。> </width>
<height	px、%	规定表格的⾼度。></height>
<align
left、center、right	规定表格相对周围元素的对⻬⽅式。></align>
<bgcolor rgb(x,x,x)、#xxxxxx、 colorname	规定表格的背景颜⾊。></bgcolor>
<background	url	规定表格的背景图⽚。></background>
<border px	规定表格边框的宽度。></border>
<cellpadding px、%	规定单元格边框与其内容之间的空⽩。></cellpadding>
<cellspacing  px、%	规定单元格之间的空隙。></cellspacing>


td属性:
表格中除了⾏元素以外，还有单元格，单元格的属性和⾏的属性类似。td和th都是单元格

属性		    值								 描述
height		 px、%							 规定单元格的⾼度。
width		 px、%							 规定单元格的宽度。
align 		 left、center、right				规定单元格内容的对⻬⽅式。
valign		 top、middle、 bottom				规定单元格内容的垂直对⻬⽅式。
bgcolor 	 rgb(x,x,x)、#xxxxxx、 colorname	规定单元格的背景颜⾊。
background	 url							 规定单元格的背景图⽚。
rowspan	 	 number							 规定单元格合并的⾏数
colspan		 number							 规定单元格合并的列数


<html>
<head>
	<title>i am title</title>
	<meta charset="utf-8">
</head>
    <body>
		<table border=1px width="700" height="500">
	<tr>
		<td colspan="2">1</td>
		<td rowspan="2">3</td>
	</tr>
	<tr>
		<td>5</td>
		<td>6</td>
	</tr>
    </table>
</body>
</html>

```

##### 2.9、表单标签  <form

```sql
'表单主要是⽤来收集客户端提供的相关信息，提供了⽤户数据录⼊的⽅式，有多选、单选、单⾏⽂本、下拉列表等输⼊框，便于⽹站管理员收集⽤户的数据，是Web浏览器和Web服务器之间实现信息交流和数据传递的桥梁'.

'表单被 form 标签包含，内部使⽤不同的表单元素来呈现不同的⽅式来供⽤户输⼊或选择。当⽤户输⼊好数据后，就可以把表单数据提交到服务器端'。
"⼀个表单元素有三个基本组成部分"：
 /*表单标签，包含了表单处理程序所在的URL以及数据提交到服务器的⽅法等表单信息。 
 表单域，包含了⽂本框、密码框、隐藏域、多⾏⽂本框、复选框、单选框、下拉选择框和⽂件上传框等表单控件。
 表单按钮，包括提交按钮、复位按钮和⼀般按钮，⽤于将数据传送到服务器上。*/
 
在HTML中创建表单⽤ form 标签。每个表单都可以包含⼀到多个表单域或按钮。form标签属性：
属性			值							描述
action		访问服务器地址服务器端         表单处理程序的URL地址
method		post、get[默认值]	         表单数据的提交⽅法
target	   参考超链接的target属性		  表单数据提交时URL的打开⽅式
enctype	 'application/x-www-formurlencoded[默认值] multipart/form-data [⽤于⽂件上传] text/plain [⽤于纯⽂本数据发送]' 	       表单提交数据时的编码⽅式

```

##在HTML中创建表单⽤form标签。每个表单都可以包含⼀到多个表单域或按钮。form标签属性：

```xml
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Title</title>
</head>
    <body>
    <form action="#" method="post">
        <label>⽤户名：</label>
        <input type="text" name="username"/>
<br/>
        <label>密码：</label>
        <input type="password" name="password"/>
<br/>
        <label>爱好：</label>
<!--        value属性就是提交给服务器的内容，服务器根据该内容就是到⽤户选择的是哪⼀项-->
        <input type="checkbox" name="hobby" value="lanqiu">篮球
        <input type="checkbox" name="hobby" value="zuqiu">⾜球
        <input type="checkbox" name="hobby" value="qumao">⽻⽑球
        <input type="checkbox" name="hobby" value="gaoer">⾼尔夫
        <br/>
        <label>性别：</label>
<!--        单选框的name属性值必须⼀样，否则⽆法实现单选-->
        <input type="radio" name="sex" value="male">男
        <input type="radio" name="sex" value="female">⼥
 <br/>
        <label>⽣⽇：</label>
        <input type="date" name="birthday"><br>
        <label>籍贯：</label>
        <select name="jiguan">
            <option>请选择籍贯</option>
            <option value="hebei">河北</option>
            <option value="anhui">安徽</option>
            <option value="liaoning">辽宁
</option>
        </select>
        <br>
        <label>⾃我介绍：</label>
        <textarea cols="30" rows="10" placeholder="请描述" name="self"></textarea>
        <br>
        <input type="submit" value="提交">
        <input type="reset" value="置">
    </form>
</body>
</html>

```

######  ##⽂件上传:必须将⽂件的⼆进制形式的数据提交给服务器

```xml
<form action="#" method="post"
enctype="multipart/form-data">
<input type="file">
<input type="submit" value="􀓤􀖃􀷈􀕯">
</form>
```

##### 2.10、多媒体标签

###### ##视频标签：

```xml
<video src="路径" controls autoplay
width="300px"></video>

标签属性:
autoplay  属性控制是否网页加载自动播放
controls  是否显示播放控件， 默认不显示属性用于控制循环次数，如果值为正整数，则播放指定loop的次数，如果是 1oop 或者是 loop = -1，则无线循环播放。
width  属性设置播放窗口宽度
height 属性设置播放窗口高度

由于版权等原因，不同的浏览器可⽀持播放的格式是不⼀样的
<!DOCTYPE html>
<html lang="en">
<head>
		<meta charset="UTF-8">
		<title>Title</title>
</head>
<body>
	<video
src="https://video.pearvideo.com/mp4/adshort/202
11029/cont-1744852-15789500_adpkg-ad_hd.mp4"
controls autoplay width="600px"></video>
</body>
</html>
```

###### ##⾳频标签：

```xml
<audio src="路径" autoplay="autoplay" controls="true=" loop=2> </audio>                                             
标签属性:
autoplay	属性控制是否网页加载自动播放  
controls 	是否显示播放控件，默认不显示属性用于控制循环次数，如果值为正整数，则播放指定loop的次数，如果是 loop 或者是 loop = -1，则无线循环播放。

由于版权等原因，不同的浏览器可支持播放的格式是不一样的
 
<!DOCTYPE html>
<html lang="en">
<head>
		<meta charset="UTF-8">
		<title>Title</title>
</head>
<body>
		<audio
src="https://video.pearvideo.com/mp4/adshort/202
11029/cont-1744852-15789500_adpkg-ad_hd.mp4"
controls autoplay width="600px"></audio>
    
</body>
</html>                             
```

