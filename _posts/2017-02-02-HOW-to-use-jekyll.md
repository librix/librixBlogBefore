在使用 Jekyll 构建博客的过程中，我记录下了这些常见的函数，例如循环输出文章，输出分页等。

在使用 Jekyll 构建博客的过程中，我记录下了这些常见的函数，例如循环输出文章，输出分页等

#### 一些函数

循环输出 3 篇文章

```
{% for post in site.posts limit:3 %}
{% endfor %}
```

循环输出最近 3 篇

```
{% for post in site.posts offset:3 limit:3 %}
{% endfor %}
```

日期

```
{{ page.date | date:"%B %b, %Y" }}

```

分页输出

```
{% for post in paginator.posts %}
  {{ content }}
{% endfor %}

```

分页

```
{% if paginator.previous_page %}
  //判断输出前一个分页
  //"page" + paginator.previous_page
{% endif %}
{% if paginator.next_page %}
  //判断输出后一个分页
  //"page" + paginator.next_page
{% endif %}
{% for page in (1..paginator.total_pages) %}
  {% if page == paginator.page %}
     //如果是当前分页
     //page
  {% else %}
     //不是的话输出其他分页链接号码
     //"page" + page
  {% endif %}
{% endfor %}

```

文章页面显示前一篇文章和后一篇文章

```
{% if page.previous %}
  //url:    page.previous.url
  //title:  page.previous.title | truncatewords:5
{% endif %}
{% if page.next %}
  //url:    page.next.url
  //title:  page.next.url | truncatewords:5
{% endif %}

```

- 作者「[掌心](http://www.zhanxin.info/contact.html)」于 2012-04-26 14:04 更新本文



今晚吃完饭后，为博客做了简单的搜索功能，因为做的大多是前台方面的工作，所以我个人将其称之为静态搜索。简单介绍下。

今晚吃完饭后，为博客做了简单的搜索功能，因为做的大多是前台方面的工作，所以我个人 将其称之为静态搜索。简单介绍下。

### 一、生成 search.xml

遍历 **Jekyll** 博客中的所有文章，获取其标题、日期和文章链接，整合 到一个 **xml** 文件中。这个 **xml** 文件我们可将其命名为`search.xml`，以便我们后续的工作。

具体的写法如下：

```
<?xml version="1.0" encoding="UTF-8" ?>
<articles>
{% for post in site.posts %}
<article>
    <title>{{ post.title }}</title>
    <url>{{ site.url }}{{ post.url }}</url>
    <date>{{ post.date | date_to_utc | date: '%Y-%m-%d'}}</date>
</article>
{% endfor %}
</articles>
```

### 二、添加 DOM 结构

DOM 结构就是 HTML 代码啦。你可以添加到你希望的地方，但要注意一点，就是你添加 DOM结构的地方要有相应的 CSS 链接和 JS 链接。我把这个简单的搜索功能放在 Archive.html里面，不清楚的同学可以去看源代码哈。

添加 **Jquery UI** 样式和 **JS** 链接。我在这里采用的是 jquery-ui-1.8.18.custom 版本。DOM 结构保存在同一个页面。

```
//样式表
<link rel="stylesheet" href="/css/jquery-ui-1.8.18.custom.css" type="text/css"
/>

//js
<script src="/js/jquery-ui-1.8.18.custom.js"></script>

//添加 DOM
<input id="J_search" placeholder="Simple Search"/>
```

### 三、设置全局地址

在 **Jekyll** 博客的根目录下的 `config.yml` 添加你的博客的全局基本地址。就一句话就 Ok 哈！

```
url: http://www.pizn.me
```

### 四、通过 Javascript 实现搜索功能

简单说明下原理：通过在输入框输入关键词，**Ajax** 匹配 search.xml 中的文章标题里面的词语， 若是，在输入框下方显示出标题。通过选择标题，跳转到搜索到的文章页面。

我的实现方式是这样的，你也可以通过修改 `autocomplete` 的实例来实现不同的展现效果。

```
$(function() {
        $.ajax({
            url: "search.xml",
            dataType: "xml",
            success: function( xmlResponse ) {
                var data = $( "article", xmlResponse ).map(function() {
                    return {
                        value: $( "title", this ).text() + ", " +
                            ( $.trim( $( "date", this ).text() ) ),
                        desc: $("description", this).text(),
                        url: $("url", this).text()
                    };
                }).get();

                $( "#J_search" ).autocomplete({
                    source: data,
                    minLength: 0,
                    select: function( event, ui ) {
                        window.location.href = ui.item.url;
                    }
                });
            }
        });
    });
```

### 五、测试

在输入框中输入你所知道的一些关键词，如果输入框下拉菜单有内容，选中它，成功跳转到对应的文章页面。那么，你成功了。

### 六、总结

这是一个很简单的实现方法，因为就今晚几个小时做出来的，所以可能还有很多不适用性。兼容性方面还没做好测试，只兼容 Firefox 和 Chrome ，还没完善的一个方面是出错处理，有空再补上。

遗憾的是暂时只支持英文关键词搜索，后续，恩，中英文。



GitHub Pages 如今提供快速编辑的功能，方便项目创建一个在线的页面。今天小看了下，很赞，在此推荐给大家。其实现在创建一个页面，只需要 3 个步骤，也不用担心页面长得不好看了。

GitHub Pages 如今提供快速编辑的功能，方便项目创建一个在线的页面。今天小看了下，很赞，在此推荐给大家。其实现在创建一个页面，只需要 3 个步骤，也不用担心页面长得不好看了。

The easiest way to quickly publish beautiful pages for you and your projects.

一，选择自动生成页面
进入项目管理页面，选择自动生成页面： create-github-page2

二，填写项目对应的信息
创建一个页面现在已经提供在线编辑的功能了，非常不错。同时支持 markdown 语法。当你填写完你的项目信息之后，点击 Continue to Layouts 进入下一步。 create-github-page3

三，选择你喜欢的模板
接下来你将进入一个模板页面，这里已经帮你生成了预览。你可以选择 8 套来自 github的开发人员和设计师设计出来的漂亮的模板。选择好之后，点击右上角的确定的勾就 ok 了。 create-github-page4

恩，如此简单！

四，八套美丽的模板



之前在写 Jekyll 主题的时候，使用 Javascript 来高亮菜单，但有一个缺点是需要等到页面加载之后才动态切换。这里介绍下使用 Jekyll 语法的写法。

在主题文件中的`_config.yml`中定义好菜单内容，大致如下：

```
// _config.yml

...

nav:
  - text: about
    url: /about/index.html
  - text: resume
    url: /resume/index.html
  - text: contact
    url: /contact/index.html
  - text: blog
    url: /blog/index.html

```

其次，在使用到 nav 的地方，例如 layout 里面，这样写：

```
<nav>
  {% for link in site.nav %}
    {% assign active = nil %}
    {% if page.url == link.url or page.layout == link.layout %}
      {% assign active = 'class="active"' %}
    {% endif %}
    <li>
        <a {{ active }} href="/{{ link.text }}/">
            {{ link.text }}
        </a>
        {{ indicator }}
    </li>
  {% endfor %}
</nav>
```

这样写大致的意思是：

- 把配置中定义好的 nav 通过循环取出来。
- 判断当前页面的 url，如果是和 nav 中一致的，就赋予一个样式类「active」。
- 随后在模板中把定义好的参数`{{ active }}`写上去。

通过这样写的好处是可以在页面生成的时候就有这个样式，而不需要通过 Javascript 去动态添加。原理是差不多的，但这样写更加合理。

- 作者「[掌心](http://www.zhanxin.info/contact.html)」于 2013-07-16 13:07 更新本文

Jekyll 是一个静态网页生成器，那我们想定义一些内容，例如人物信息数据，菜单数据等，应该放哪里呢？今天介绍下 Jekyll 的数据文件。

Jekyll 如今已经支持加载和读取来自`_data`目录下的[YAML](http://yaml.org/)自定义数据文件。

新增的这个`_data`目录，可以帮我们解决定义在`_config.yml`中的数据。也就是说我们不需要去更改「配置文件」，而是去修改「数据文件」。我觉得这样其实是更加简洁的做法。

### 单做一个示例

- 新建一个`_data`目录
- 新建「YMAL」文件，一般是以`.yml`或`.ymal`结尾
- 假设我们定义了一个 members.yml 文件，数据大概这样写：

```
- name: Tom Preston-Werner
  github: mojombo
- name: Parker Moore
  github: parkr
- name: Liu Fengyun
  github: liufengyun
```

Ok, 我们的数据文件已经定义好了，接下来如何使用？

在我们的「主题」文件中，我们可以使用`site.data.members`来获取。例如：

```
<ul>
{% for member in site.data.members %}
  <li>
    <a href="https://github.com/{{ member.github }}">
      {{ member.name }}
    </a>
  </li>
{% end %}
</ul>
```

### 结语

之前一直在`_config.yml`文件中写数据，现在可以使用数据文件了。

- 作者「[掌心](http://www.zhanxin.info/contact.html)」于 2013-10-30 09:10 更新本文