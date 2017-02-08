# 2017-02-03-python爬虫：使用Requests+Beautifulsoup爬取Tripadvisor

第一步，服务器与本地交换机制

第二步，解析真实网页的方法

## 第一步，服务器与本地交换机制

HTTP协议：request  response

request  方法：

| get   | post    | head    |
| ----- | ------- | ------- |
|       |         |         |
| put   | options | connect |
| trace | delete  |         |

爬虫主要使用get

```
GET /page_one.html HTTP/1.1
Host: www.sample.com
```

Response  方法

status_code:200

在chrome浏览器中，点击Network，监视网络行为：request 和 response 信息都记录在这里;

## 第二步，爬取信息

```python
#导入库
from bs4 import BeautifulSoup
import requests

url='http://localhost:4000/%E4%B8%BB%E9%A2%98/2013/08/11/kunka-back.html'
wb_data = requests.get(url) #请求网页会返回一个response，存储，并为其命名
Soup = BeautifulSoup(wb_data.text,'lxml')
#使用text方法，使网页可读
#然后使用 BeautifulSoup 方法
print(Soup) #打印测试一下，正确的话，会返回网页
```

描述要爬取元素位置：

找到元素，使用CSS secletor，复制。常规方法无法选择“：

```python
title =soup.seclect('div.property_title' > a)
img = soup.seclect('img[width="60"]')
```

### 登录		

使用 request header 中 cookie 表示自己已经登陆：

```python
#导入库
from bs4 import BeautifulSoup
import requests
#构造request信息
header={
	'user-Agent' = '',
	'cookie' = ''
	#从网页中复制这些信息即可
}
url_saves =''
wb_data = request.get(url,header = header)
soup = 
titles =
for title,xx,xxx, in zip(titles,xxs,xxxs):
	data = {
	}
	print(data)
```

### 设置函数

```python
def function_name(url , data = None):
```

### 爬取连续多个页面

```python
urls = ['xxxxxxxx{}xxx',format(str(i)) for i in range(30,930,30)]

for single_url in urls:
    get_attractions(single_url,data = None)
```

防止反爬取的一个手段：

```python
#每次请求之间的延时：
time.sleep(2)#停滞 2s
```

### 图片怎么处理？

因为图片采取了一定的反爬取手段，图片放在了JS里面。因为不是所有的手机都会加载所有的 js ，所以优先采用手机端进行分析。

更改 User-Agent 即可。

## 小结和完整代码

理解Request 和 Response 的原理。

Request 库的 get 方法怎么使用。

真实网页中定位元素的方法：唯一特征。

使用headers，假装人类访问。

爬取连续页面找连续页面的关系。 

反爬取，使用手机页面分析。

```python
from bs4 import BeautifulSoup
import requests
import time

url_saves = 'http://www.tripadvisor.com/Saves#37685322'
url = 'https://cn.tripadvisor.com/Attractions-g60763-Activities-New_York_City_New_York.html'
urls = ['https://cn.tripadvisor.com/Attractions-g60763-Activities-oa{}-New_York_City_New_York.html#ATTRACTION_LIST'.format(str(i)) for i in range(30,930,30)]

headers = {
    'User-Agent':'',
    'Cookie':''
}


def get_attractions(url,data=None):
    wb_data = requests.get(url)
    time.sleep(4)
    soup = BeautifulSoup(wb_data.text,'lxml')
    titles    = soup.select('div.property_title > a[target="_blank"]')
    imgs      = soup.select('img[width="160"]')
    cates     = soup.select('div.p13n_reasoning_v2')

    if data == None:
        for title,img,cate in zip(titles,imgs,cates):
            data = {
                'title'  :title.get_text(),
                'img'    :img.get('src'),
                'cate'   :list(cate.stripped_strings),
                }
        print(data)


def get_favs(url,data=None):
    wb_data = requests.get(url,headers=headers)
    soup      = BeautifulSoup(wb_data.text,'lxml')
    titles    = soup.select('a.location-name')
    imgs      = soup.select('div.photo > div.sizedThumb > img.photo_image')
    metas = soup.select('span.format_address')

    if data == None:
        for title,img,meta in zip(titles,imgs,metas):
            data = {
                'title'  :title.get_text(),
                'img'    :img.get('src'),
                'meta'   :list(meta.stripped_strings)
            }
            print(data)

for single_url in urls:
    get_attractions(single_url)


# from mobile web site
'''
headers = {
    'User-Agent':'', #mobile device user agent from chrome
}


mb_data = requests.get(url,headers=headers)
soup = BeautifulSoup(mb_data.text,'lxml')
imgs = soup.select('div.thumb.thumbLLR.soThumb > img')
for i in imgs:
    print(i.get('src'))
'''

```

## 作业中的难点：房东性别

