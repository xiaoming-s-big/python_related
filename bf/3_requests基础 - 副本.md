### 爬虫相关

```python
#什么是爬⾍?
爬⾍程序是需要充当B/S或者C/S架构中的客户端。
爬⾍程序需要模拟客户端进⾏请求发送，然后获取服务器端对应的相关数据。
在B/S架构中爬⾍程序模拟的就是浏览器。

#提问：如果⽇后你的爬⾍程序没有爬取到你想要的数据，
why？  //爬⾍程序模拟浏览器的⼒度不够

#爬⾍在应⽤场景的分类?
通⽤爬⾍：  可以将⼀个⻚⾯中所有的数据都爬取到。
聚焦爬⾍：  建⽴在通⽤爬⾍基础之上。可以将⼀张⻚⾯中局部、指定的数据进⾏抓取
增量式爬⾍: 可以监测⽹站数据更新的情况。目的：以便将最新更新出来的数据进⾏抓取

##///爬⾍的⽭与盾（重点）?   
反爬机制：作⽤在⻔户⽹站中，⽹站会指定出⼀些阻⽌爬⾍程序进⾏数据爬取的机制。
反反爬策略：作⽤在爬⾍程序中，可以指定破解反爬机制的策略，这些策略就是反反爬策略。

```

##### 爬⾍合法性探究【了解即可】

```python
#爬⾍作为⼀种计算机技术就决定了它的中⽴性，因此爬⾍本身在法律上并不被禁⽌，但是利⽤爬⾍技术获取数据这⼀⾏为是具有违法甚⾄是犯罪的⻛险的。所谓具体问题具体分析，正如⽔果⼑本身在法律上并不被禁⽌使⽤，但是⽤来捅⼈，就不被法律所容忍了

#或者我们可以这么理解：爬⾍是⽤来批量获得⽹⻚上的公开信息的，也就是前端显示的数据信息。因此，既然本身就是公开信息，其实就像浏览器⼀样，浏览器解析并显示了⻚⾯内容，爬⾍也是⼀样，只不过爬⾍会批量下载⽽已，所以是合法的。不合法的情况就是配合爬⾍，利⽤⿊客技术攻击⽹站后台，窃取后台数据
（⽐如⽤户数据等）

#爬⾍所带来⻛险主要体现在以下3个⽅⾯：
1、	违反⽹站意愿，例如⽹站采取反爬措施后，强⾏突破其反爬措施；
2、	爬⾍⼲扰了被访问⽹站的正常运营；
3、	爬⾍抓取了受到法律保护的特定类型的数据或信息。

#那么作为爬⾍开发者，如何在使⽤爬⾍时避免进局⼦的厄运呢？
1、	在规避反爬⾍措施的同时，需要优化⾃⼰的代码，避免⼲扰被访问⽹站的正常运⾏；
2、	在使⽤、传播抓取到的信息时，应审查所抓取的内容，如发现属于⽤户的个⼈信息、隐私或者他⼈的商业秘密的，应及时停⽌并删除。

#总结：
  可以说在我们身边的⽹络上已经密密麻麻爬满了各种⽹络爬⾍，它们善恶不同，各怀⼼思。⽽越是每个⼈切身利益所在的地⽅，就越是爬满了爬⾍。//“所以爬⾍是趋利的，它们永远会向有利益的地⽅爬⾏//。技术本身是⽆罪的，问题往往出在⼈⽆限的欲望上。因此爬⾍开发者的道德⾃持和企业经营者的良知才是避免触碰法律底线的根本所在。

```

##### requests基础操作 流程

```python
1 安装requests库:
    pip install requests
2 导入requests模块:
在你的Python脚本或交互式环境中，首先需要导入requests模块：
import requests

3 发送GET请求:
使用requests.get()方法发送一个GET请求到指定的URL。例如，获取一个网页的内容：
response = requests.get('https://www.example.com')
print(response.text)  # 打印响应内容

4 处理响应:
response.status_code: 获取响应的状态码（如200表示成功）。
response.headers: 获取响应头。
response.text: 获取响应内容的字符串形式。
response.json(): 如果响应是JSON格式，可以直接解析为字典

5 发送POST请求:
使用requests.post()方法发送一个POST请求。可以传递数据作为参数：
data = {'key': 'value'}
response = requests.post('https://httpbin.org/post', data=data)
print(response.text)

6 设置请求头:
可以在请求中添加自定义的请求头：
headers = {'user-agent': 'my-app/0.0.1'}
response = requests.get('https://www.example.com', headers=headers)

7 处理异常:
使用try-except结构来处理可能发生的异常，如网络连接问题等：
try:
    response = requests.get('https://www.example.com')
    response.raise_for_status()  # 如果响应状态码不是200，将抛出HTTPError异常
except requests.exceptions.HTTPError as errh:
    print("Http Error:", errh)
except requests.exceptions.ConnectionError as errc:
    print("Error Connecting:", errc)
except requests.exceptions.Timeout as errt:
    print("Timeout Error:", errt)
except requests.exceptions.RequestException as err:
    print("OOps: Something Else", err)

8 会话对象:
使用requests.Session()创建一个会话对象，该对象可以跨请求保持某些参数，如cookies等：
with requests.Session() as session:
    session.get('https://www.example.com')
    response = session.get('https://www.example.com/somepage')
    print(response.text)
    
```

###### ##接下来是示例代码：

1  代码说明：
      	导入库：我们首先导入了requests库。

2  定义函数：
		  send_get_request：用于发送GET请求，接受URL和可选的查询参数。如果请求成功，返回JSON格式的响应数据；否则打印错误信息。
          send_post_request：用于发送POST请求，接受URL、表单数据或JSON数据。如果请求成功，返回JSON格式的响应数据；否则打印错误信息。

3   主程序：在主程序中，我们定义了两个示例URL，并分别调用GET和POST请求函数，输出结果。

验证：
你可以运行这段代码来验证其功能。确保你的网络连接正常，并且可以访问示例URL。如果需要测试其他API端点，只需替换相应的URL即可

```python
1 安装requests库:
    pip install requests 
    
import requests

# 发送GET请求
def send_get_request(url, params=None):
    try:
        response = requests.get(url, params=params)
        response.raise_for_status()  # 如果响应状态码不是200，抛出异常
        return response.json()  # 返回JSON格式的数据
    except requests.exceptions.RequestException as e:
        print(f"GET请求失败: {e}")
        return None

# 发送POST请求
def send_post_request(url, data=None, json=None):
    try:
        response = requests.post(url, data=data, json=json)
        response.raise_for_status()  # 如果响应状态码不是200，抛出异常
        return response.json()  # 返回JSON格式的数据
    except requests.exceptions.RequestException as e:
        print(f"POST请求失败: {e}")
        return None

if __name__ == "__main__":
    # 示例URL（请替换为实际的API端点）
    get_url = "https://jsonplaceholder.typicode.com/posts"
    post_url = "https://jsonplaceholder.typicode.com/posts"
    
    # 发送GET请求
    get_response = send_get_request(get_url, params={'userId': 1})
    if get_response:
        print("GET请求成功:")
        print(get_response)
    
    # 发送POST请求
    post_data = {'title': 'foo', 'body': 'bar', 'userId': 1}
    post_response = send_post_request(post_url, json=post_data)
    if post_response:
        print("POST请求成功:")
        print(post_response)

```



###### ##基础 编码流程

```python
#基本介绍
reqeusts 是⽤来进⾏⽹络请求的⼀个python模块，其作⽤可以使⽤程序模拟浏览器进⾏请求发送。
#对网页的请求并不一定是从网页上的URL 获取  //  需要分析抓包工具【network】分析url

#环境安装
pip install requests  #环境安装

#编码流程 如下
1 指定url
2 发起请求 get()/post()  ###请求方式 /请求头/请求参数  //请求协议 
3 获取响应数据（想爬取的数据）
4 持久化存储

#Response对象的处理
1、发送给客户端:
2、设置响应头:
3、设置状态码:
4、添加Cookie:
5、发送文件:
```

###### ##python中 reqeusts 库下   get()/post() 都可以带什么函数  

在Python中使用`requests`库发送HTTP请求时，`GET`和`POST`方法可以携带不同的参数。以下是它们各自支持的函数及其参数详解：

```python
#GET请求
requests.get()函数
用于发送HTTP GET请求，基本语法如下：
response = requests.get(url, params=None, headers=None, auth=None, timeout=None)

url: 字符串，表示请求的目标URL。
params: 字典或字节 序列，作为URL的查询参数。  #请求参数
headers: 字典，包含请求头的键值对。		    #请求头的键值对
auth: 元组，表示HTTP认证的用户名和密码。
timeout: 超时时间，以秒为单位，表示在请求过程中等待服务器响应的最大时间。

###示例
import requests

url = "https://example.com/api"
params = {"key1": "value1", "key2": "value2"}
headers = {"Authorization": "Bearer <your_access_token>"}

#requests.get 向指定的URL发送了一个带有查询参数和自定义请求头的GET请求
response = requests.get(url, params=params, headers=headers) 
print(response.status_code)
print(response.text)


#POST请求
requests.post()函数
用于发送HTTP POST请求，基本语法如下：
response = requests.post(url, data=None, json=None, headers=None, params=None, auth=None, timeout=None)

url: 字符串，表示请求的目标URL。
data: 字典、字节序列或文件，作为请求的正文发送给服务器。
json: JSON可序列化的对象，作为请求的正文发送给服务器。如果同时传递了data和json，json参数会覆盖data。
headers: 字典，包含请求头的键值对。		  #请求头的键值对
params: 字典或字节序列，作为URL的查询参数。 #请求参数
auth: 元组，表示HTTP认证的用户名和密码。
timeout: 超时时间，以秒为单位，表示在请求过程中等待服务器响应的最大时间

##示例
import requests

url = "https://example.com/api"
data = {"key1": "value1", "key2": "value2"}
headers = {"Content-Type": "application/json"}

#requests.post发送了一个JSON数据到指定的URL，并通过响应对象访问了服务器返回的状态码和响应内容
response = requests.post(url, json=data, headers=headers)
print(response.status_code)
print(response.text)

##总结
GET请求：通过requests.get()发送，主要通过URL的查询字符串传递参数，适用于获取资源或数据。
POST请求：通过requests.post()发送，主要通过请求体传递参数，适用于提交数据进行存储或处理。可以使用表单数据（data参数）或JSON数据（json参数）
```



#### **案例应⽤**

###### 东⽅财富⾸⻚数据爬取

// https://www.eastmoney.com/

```python
import requests
#1.指定url
url = 'https://www.eastmoney.com/'
#2.发起请求:向指定url发起请求

#get()函数会返回⼀个响应对象
response = requests.get(url=url)

#3.获取响应数据
page_text = response.text #text是返回字符串类型的响应数据
#4.持久化存储
with open('dongfang.html','w') as fp:
	fp.write(page_text)
```

发现：爬取的⻚⾯数据出现了中⽂乱码。

###### 中⽂乱码解决

#设置响应对象的编码格式，以此来处理响应数据中中⽂乱码

```python
import requests

#1.指定url
url = 'https://www.eastmoney.com/'

#2.发起请求:向指定url发起请求
#get()函数会返回⼀个响应对象
response = requests.get(url=url)

#设置响应对象的编码格式，以此来处理响应数据中中⽂乱码
response.encoding = 'utf-8'

#3.获取响应数据
page_text = response.text #text是返回字符串类型的响应数据

#4.持久化存储
with open('dongfang.html','w') as fp:
	fp.write(page_text)
```

###### 爬取51游戏中任何游戏对应的搜索结果⻚⾯数据

url：https://www.51.com/

```python
import requests

#字典需要存放请求携带的所有的请求参数  目的爬取不同关键字对应的数据//动态爬取
game_title = input('enter a game key:')  #字典需要存放请求携带的所有的请求参数 
#请求参数的数量和字典的键值对的数量保持⼀致
params = {
	'q':game_title
} #请求参数的数量和字典的键值对的数量保持⼀致

#指定url
url = 'https://game.51.com/search/action/game/'
#发起请求:向指定的url携带了指定的请求参数进⾏的请求发送  请求参数//get与post请求//报文体/请求体
response = requests.get(url=url,params=params)

#获取响应数据
page_text = response.text

#持久化存储
with open('games.html','w') as fp:
	fp.write(page_text)
```

###### 中国⼈事考试⽹（UA检测）

##反爬机制：UA检测

###### ##反反爬机制：UA伪装【介绍】

url：http://www.cpta.com.cn/

```python
##爬⾍模拟浏览器主要是模拟请求参数和主要的请求头。
 //User-Agent:请求载体的身份标识。
	使⽤浏览器发请求，则请求载体就是浏览器
	使⽤爬⾍程序发请求，则请求载体就是爬⾍程序

##反爬机制：UA检测
	⽹站后台会检测请求的载体是不是浏览器，如果是则返回正常数据，不是则返回错误数据
##反反爬机制：UA伪装
将爬⾍发起请求的User-Agent伪装成浏览器的身份。

##//Code 例子如下  中国⼈事考试⽹（UA检测）

import requests
url = 'http://www.cpta.com.cn/'

#User-Agent:请求载体（浏览器，爬⾍程序）的身份表示
header = {
'User-Agent':'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36
(KHTML, like Gecko) Chrome/115.0.0.0 Safari/537.36'
}
#伪装了浏览器的请求头
response = requests.get(url=url,headers=header)
page_text = response.text

with open('kaoshi.html','w') as fp:
	fp.write(page_text)
#程序模拟浏览器的⼒度不够
```

###### 中国⼈事考试⽹---站内搜索  【post请求+请求参数】

```python
#通过抓包⼯具定位了指定的数据包：
   #提取：url，请求⽅式，请求参数，请求头信息
import requests
url = 'http://www.cpta.com.cn/category/search'
param = {
   "keywords": "⼈⼒资源",
   "搜 索": "搜 索"
}
header = {
   'User-Agent':'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.0.0 Safari/537.36'   
}
#发起了post请求：通过data参数携带了请求参数
response = requests.post(url=url,data=param,headers=header)

page_text = response.text

 with open('renshi.html','w') as fp:
	fp.write(page_text)
#通过抓包⼯具定位了指定的数据包：
   #提取：url，请求⽅式，请求参数，请求头信息
```

###### 智慧职教（动态加载数据爬取）(重点)

###### ##动态加载数据值的就是：

​	不是直接通过浏览器地址栏的url请求到的数据，这些数据叫做动态加载数据。

url : https://www.icve.com.cn/portal_new/course/course.html

```python
##测试：直接使⽤浏览器地址栏中的url，进⾏请求发送查看是否可以爬取到数据？
	不⽤写程序，基于抓包⼯具测试观察即可。
##经过测试发现，我们爬取到的数据并没有包含想要的数据，why？

#动态加载数据：
     在⼀个⽹⻚中看到的数据，并不⼀定是通过浏览器地址栏中的url发起请求请求到的。如果请求不到，⼀定是基于其 他的请求请求到的数据。
#动态加载数据值的就是：
  不是直接通过浏览器地址栏的url请求到的数据，这些数据叫做动态加载数据。
    
#如何获取动态加载数据？
1 确定动态加载的数据是基于哪⼀个数据包请求到的？
2 数据包数据的全局搜索：
#1//点击抓包⼯具中任何⼀个数据包
#2//control+f进⾏全局搜索（弹出全局搜索框）
⽬的：定位动态加载数据是在哪⼀个数据包中

#定位到动态加载数据对应的数据包，模拟该数据包进⾏请求发送即可：
从数据包中提取出：
url
请求参数
获取响应数据（想爬取的数据）持久化存储
【
1 指定url
2 发起请求 get()/post()
3 获取响应数据（想爬取的数据）持久化存储
】

##注意：请求头中需要携带Referer。（体现模拟浏览器的⼒度）
```

注意：请求头中需要携带Referer。（体现模拟浏览器的⼒度）

###### ##代码如下

```python
#爬取第⼀⻚的数据
import requests
headers = {
	'User-Agent':'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36',
	#Referer啥意思？不讲，后⾯单独讲
'Referer':'https://www.icve.com.cn/portal_new/course/course.html?keyvalue=%E6%97%85%E6%B8%B8'
}

url = 'https://www.icve.com.cn/portal/course/getNewCourseInfo'
data = {
	"kczy":"",
	"order":"",
	"printstate":"",
	"keyvalue": "旅游"
}
response = requests.post(url=url,headers=headers,data=data)
#获取响应数据
#json()可以将响应数据进⾏反序列化
page_text = response.json()

for dic in page_text['list']:
	title = dic['Title']
	name = dic['TeacherDisplayname']
	print(title,name)
    
#多⻚数据的爬取
import requests
headers = {
	'User-Agent':'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36',

       #Referer啥意思？不讲，后⾯单独讲
	'Referer':'https://www.icve.com.cn/portal_new/course/course.html?keyvalue=%E6%97%85%E6%B8%B8'
}
for page in range(1,5):
	url = 'https://www.icve.com.cn/portal/course/getNewCourseInfo?page=%d'%page
	data = {
			"kczy":"",
			"order":"",
			"printstate":"",
			"keyvalue": "旅游"
}
response = requests.post(url=url,headers=headers,data=data)

#获取响应数据
#json()可以将响应数据进⾏反序列化
page_text = response.json()  #response 中文意思是响应  自定义变量

for dic in page_text['list']:
	 title = dic['Title']
	 name = dic['TeacherDisplayname']
	 print(title,name)

```

###### ##图⽚数据爬取

爬取图⽚的时候需要做UA伪装使⽤⽅式1，否则使⽤⽅式2

```python
#⽅式1：
import requests
url =
 'https://img0.baidu.com/it/u=540025525,3089532369&fm=253&fmt=auto&app=138&f=JPEG?w=889&h=500'
    
response = requests.get(url=url)
#content获取⼆进制形式的响应数据
img_data = response.content

with open('1.jpg','wb') as fp:
	fp.write(img_data)
    
#⽅式2
from urllib.request import urlretrieve
#图⽚地址
img_url =
'https://img0.baidu.com/it/u=4271728134,3217174685&fm=253&fmt=auto&app=138&f=JPEG?w=400&h=500'

#参数1：图⽚地址
#参数2：图⽚存储路径
#urlretrieve可以根据图⽚地址将图⽚数据请求到直接存储到参数2表示的图⽚存储路径中
urlretrieve(img_url,'1.jpg')
```

#### 作业

##//⼩试⽜⼑：
	url：https://www.xiachufang.com/
	实现爬取下厨房⽹站中任意菜谱搜索结果数据爬取
##//⼩试⽜⼑：
	url ：https://sogou.com/
	爬取任意关键字对应的搜索⻚⾯

##//肯德基（POST请求、动态加载数据、UA检测）
	url ：http://www.kfc.com.cn/kfccda/storelist/index.aspx
     将餐厅的位置信息进⾏数据爬取

```python
--爬取多页数据
```

