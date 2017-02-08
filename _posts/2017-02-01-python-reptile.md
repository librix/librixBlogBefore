# python 爬虫入门

这是一个入门的路径。

## 准备

测试google chrome，F12打开开发者模式，在“元素”上右击检查（ctrl+shift+I）

安装python库文件

``` cmd
>pip3 install lxml
>pip3 install beautifulsoup4
>pip3 install requests
```

## 开始

 打开sublime，准备好一个页面，置于$.py$文件同层目录下$web$下，输入：

```python
#导入BeautifulSoup库
from bs4 import BeautifulSoup
with open('web/new_index.html','r') as wb_data:
#由于文件在本地，所以使用 open 函数打开，'r'表示模式
	#接下来，构造一个解析文件：
	Soup =BeautifulSoup(wb_data,'lxml')
	#打印看一下解析结果：
	print(Soup)
```

ctrl + B ，build，查看输出：

![2017-02-01-002](E:\2017\picturecut\2017-02-01-002.png)

使用copy-sector复制可能需要找到的几个元素，复制辅助工具可以使用**Ditto**

```python
# copy -->sector
# body > div.main-content > ul > li:nth-child(1) > img
# body > div.main-content > ul > li:nth-child(1) > div.article-info > h3 > a
# body > div.main-content > ul > li:nth-child(1) > div.article-info > p.meta-info > span:nth-child(2)
# body > div.main-content > ul > li:nth-child(1) > div.rate > span
```

查找图片，查看一下结果：

```python
from bs4 import BeautifulSoup
with open('web/new_index.html','r') as wb_data:
	Soup =BeautifulSoup(wb_data,'lxml')
	#选择图片
	images=Soup.select('body > div.main-content > ul > li:nth-child(1) > img')	
	print(images)
```

```
Traceback (most recent call last):
  File "D:\Codework\Plan-for-combating-master\week1\1_2\1_2code_of_video\codebyL.py", line 9, in <module>
    images=Soup.select('body > div.main-content > ul > li:nth-child(1) > img')	
  File "D:\Python\Python36-32\lib\site-packages\bs4\element.py", line 1518, in select
    for candidate in _use_candidate_generator(tag):
  File "D:\Python\Python36-32\lib\site-packages\bs4\element.py", line 1479, in recursive_select
    for i in tag.select(next_token, recursive_candidate_generator):
  File "D:\Python\Python36-32\lib\site-packages\bs4\element.py", line 1437, in select
    'Only the following pseudo-classes are implemented: nth-of-type.')
NotImplementedError: Only the following pseudo-classes are implemented: nth-of-type.
```



因为没有按照规定的方式进行填写，按提示修改一行：

```python
images=Soup.select('body > div.main-content > ul > li:nth-of-type(1) > img')

#[<img height="91" src="images/0001.jpg" width="100"/>]
#[Finished in 0.3s]
```

去掉描述具体位置的信息：

```python
images=Soup.select('body > div.main-content > ul > li > img')	

#[<img height="91" src="images/0001.jpg" width="100"/>, <img height="91" src="images/0002.jpg" width="100"/>, <img height="91" src="images/0003.jpg" width="100"/>, <img height="91" src="images/0004.jpg" width="100"/>]
```

接下来，把其他的信息筛选出来：

```python
titles=Soup.select('body > div.main-content > ul > li > div.article-info > h3 > a')
	descs = Soup.select('body > div.main-content > ul > li:nth-of-type(1) > div.article-info > p.meta-info > span:nth-of-type(2)')
	rates=Soup.select('body > div.main-content > ul > li:nth-of-type(1) > div.rate > span')
	print(titles,descs,rates,sep='\n-------------------------\n')
```

结果，注意sep（分割）的使用：

```
[<a href="www.sample.com">Sardinia's top 10 beaches</a>, <a href="www.sample.com">How to get tanned</a>, <a href="www.sample.com">How to be an Aussie beach bum</a>, <a href="www.sample.com">Summer's cheat sheet</a>]
-------------------------
[<span class="meta-cate">Wow</span>]
-------------------------
[<span class="rate-score">4.5</span>]
[Finished in 0.3s]
```

去掉伪类选择器：

```python
titles=Soup.select('body > div.main-content > ul > li > div.article-info > h3 > a')
	cates = Soup.select('body > div.main-content > ul > li > div.article-info > p.meta-info > span')
	rates=Soup.select('body > div.main-content > ul > li > div.rate > span')
	print(titles,cates,rates,sep='\n-------------------------\n')
```

使用 get.text() 的方法释放每个标签中的信息：

```python
for title in titles:
	print(title.get_text())	
```

放入同一个字典中，方便查询：

```python
for title,image,cate,rate in zip(titles,images,cates,rates):
	#然后，对所有元素进行字典构造：
	data ={
		'title':title.get_text(),
		'cate':cate.get_text(),
		'rate':rate.get_text(),
		#图片和其他的不同：
		#图片链接不同于 加载标签中的文本，他是一个属性，获取一个属性使用get方法：
		'image':image.get('src')
	}
	print(data)	
```

中间遇到一个问题：

> You are running the `get_text()` function on `selects`, which is a list. Lists don't have that function.
>  Should you not be running it on `select` itself? Or what about each element in selects:
> ```python
> for item in selects:
>    print item.get_text()
> ```
> @Gareth Webber url: http://stackoverflow.com/questions/16167348/python-get-text-not-working

结果是：

```json
{'title': "Sardinia's top 10 beaches", 'cate': 'fun', 'rate': '4.5', 'image': 'images/0001.jpg'}
{'title': 'How to get tanned', 'cate': 'Wow', 'rate': '5.0', 'image': 'images/0002.jpg'}
{'title': 'How to be an Aussie beach bum', 'cate': 'butt', 'rate': '3.5', 'image': 'images/0003.jpg'}
{'title': "Summer's cheat sheet", 'cate': 'NSFW', 'rate': '3.0', 'image': 'images/0004.jpg'}
```

但是，我们忽略了标签——标签是多对一的各系，所以，在获取的时候应当在父级就停下，然后获取父级标签下所有子标签的值：

```python
#cates = Soup.select('body > div.main-content > ul > li > div.article-info > p.meta-info > span') ==>改为：
cates = Soup.select('body > div.main-content > ul > li > div.article-info > p.meta-info')
#data里面，
'cate':list(cate.stripped_strings),
    #stripped_strings:获取父级标签下所有子标签的值
    #list:他们是一个数组
```

然后，可以做一个筛选：

```python
from bs4 import BeautifulSoup
with open('web/new_index.html','r') as wb_data:
	Soup =BeautifulSoup(wb_data,'lxml')
	info =[]   #info是数组
	images=Soup.select('body > div.main-content > ul > li > img')	
	titles=Soup.select('body > div.main-content > ul > li > div.article-info > h3 > a')
	cates = Soup.select('body > div.main-content > ul > li > div.article-info > p.meta-info')
	rates=Soup.select('body > div.main-content > ul > li > div.rate > span')
for title,image,cate,rate in zip(titles,images,cates,rates):
	data ={
		'title':title.get_text(),
		'cate':list(cate.stripped_strings),
		'rate':rate.get_text(),
		'image':image.get('src')
	}
	info.append(data)	#使用append方法在数组尾部加入data元素
	
for i in  info:
	if float(i['rate'])>3:
		print(i['title'],i['cate'],i['image'])
```

小结：

```python
Soup =BeautifulSoup(wb_data,'lxml')
xxx = Soup.select('???')
for title,image,cate,rate in zip(titles,images,cates,rates):
	data ={}
```

作业题中start的处理：

```python
#https://www.crummy.com/software/BeautifulSoup/bs4/doc.zh/#find-all

stars = Soup.select('body > div > div > div.col-md-9 > div > div > div > div.ratings > p:nth-of-type(2)')
# 为了从父节点开始取,此处保留:nth-of-type(2),观察网页,多取几个星星的selector,就发现规律了

#data中：
 'star': len(star.find_all("span", class_='glyphicon glyphicon-star'))
        # 观察发现,每一个星星会有一次<span class="glyphicon glyphicon-star"></span>,所以我们统计有多少次,就知道有多少个星星了;
        # 使用find_all 统计有几处是★的样式,第一个参数定位标签名,第二个参数定位css 样式,具体可以参考BeautifulSoup 文档示例http://www.crummy.com/software/BeautifulSoup/bs4/doc.zh/#find-all;
        # 由于find_all()返回的结果是列表,我们再使用len()方法去计算列表中的元素个数,也就是星星的数量
```

