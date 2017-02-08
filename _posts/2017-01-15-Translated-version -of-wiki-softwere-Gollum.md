----------------

Title:Gollum翻译

Author:E.A.

Date:2017-01-15

------

# 前言

Gollum是一个很好用的开源维基软件，但是中文资料很少。因此将官方github上的内容翻译了一下，以供学习。

原文地址：[https://github.com/gollum/gollum](https://github.com/gollum/gollum)

# 译文

Gollum 是一个简单的wiki system，建立在git的基础上. 一个 Gollum Wiki是一个简单的 git 库 (无论是空的还是常见的) ，拥有以下特性:

- 一个 Gollum 库的内容是可编辑的, 除非这个库是空的. 
- Pages 是独立的文本文件， 可以用任何你喜欢的方式添加。
- gollum的目录. 其他类型也文件也可被包含在内，比如图片, PDF 以及Pages的页头、页脚.

Gollum pages:

- 可以用不同的方式（[markups](https://github.com/gollum/gollum#markups)）组织文本.
- 可以被你喜欢的编辑器、IDE(变化将在记录（committing）后被显示出来)或者开发的 web 界面编辑.
- 可以显示所有的版本(每一次的记录commits).


Gollum 可以加载为"有界面的webserver" 或者是 "console 模式", 你可以在这里使用 一个预定义 API 去查询（query）或者操作（manipulate） 库. 更多信息可以看 [Running](https://github.com/gollum/gollum#running) 和 [Configuration](https://github.com/gollum/gollum#configuration) 的章节.

Gollum的能力（capabilities）与陷阱（pitfalls）的更多信息:

- [Syntax/capability  overview for pages](https://github.com/gollum/gollum/wiki).句法规则/能力导航页面

- [Known limitations](https://github.com/gollum/gollum/wiki/Known-limitations).已知的限制

- [Troubleshoot guide](https://github.com/gollum/gollum/wiki/Troubleshoot-guide).问题列表指南

- [Security overview](https://github.com/gollum/gollum/wiki/Security).安全概述


gollum快速入门, 见 [this video](https://www.youtube.com/watch?v=gj1qqK3Oku8). 更多高级功能特性,见这个 [this video](https://www.youtube.com/watch?v=EauxgxsLDC4) (docker的配置).

##系统要求

| 操作系统OS          | Ruby                                     | 適配器   Adapters                           | 支持   Supported |
| --------------- | ---------------------------------------- | ---------------------------------------- | -------------- |
| Unix/Linux-like | Ruby 1.9.3+                              | 除了 [RJGit](https://github.com/repotag/rjgit) | yes            |
| Unix/Linux-like | [JRuby](https://github.com/jruby/jruby) (1.9.3+   兼容) | [RJGit](https://github.com/repotag/rjgit) | yes            |
| Windows         | Ruby 1.9.3+                              | 除了 [RJGit](https://github.com/repotag/rjgit) | no             |
| Windows         | [JRuby](https://github.com/jruby/jruby) (1.9.3+   兼容) | [RJGit](https://github.com/repotag/rjgit) | 大多数支持          |

>   注记:
>
>   这里仍然存在很多已知BUG，这个设置仍然不具备成为产品的特性. 你可以在 [Support Windows via JRuby - Meta Issue](https://github.com/gollum/gollum/issues/1044)追踪后续内容.

##   安装

依赖于操作系统（operating system）、包管理工具（package manage）以及Ruby 的安装. 一般来说,你应该先进行 Ruby 的安装，然后安装 Gollum.

1. Ruby 最方便的是选择通过 [RVM](https://rvm.io/) 或者包管理工具进行安装.
2. Gollum
   最好使用 RubyGems 安装:
```
[sudo] gem install gollum 
```
每种系统不同的安装例程可以看这里 [here](https://github.com/gollum/gollum/wiki/Installation).

> 注记:无论你正在使用的是哪一个版本的 Ruby,  Gollum 恰如其分的使用默认的 git 适配器（adapter）.因此，如上安装过程对 MRI 和 JRuby来说是相同的.

如果你从源码（source）安装:

1. （可选）卸载任何Gollum 前面的版本:```[sudo] gem uninstall -aIx gollum ```

2. 安装 [Bundler](http://bundler.io/).

3. 进入克隆   Gollum 源码的位置.

4. 安装独立文件:```[sudo] bundle install``` 

5. 编译:``` rake build x```

6. 并且安装:

   ```[sudo] gem install --no-ri --no-rdoc pkg/gollum*.gem``` 

##Markups：文本组织方式

Gollum 目前支持以下文本编辑方式:

- [Markdown](http://daringfireball.net/projects/markdown/syntax)

- [RDoc](http://rdoc.sourceforge.net/)


由于所有 markups are rendered by the [github-markup](https://github.com/github/markup) gem, 你可以通过 增量安装（additional installation）方便的添加其他被支持的 markups:

- 
  [AsciiDoc](http://asciidoctor.org/docs/asciidoc-syntax-quick-reference/) -- [sudo]  gem install asciidoctor

- [Creole](http://www.wikicreole.org/wiki/CheatSheet) -- [sudo]  gem install creole

- [MediaWiki](http://www.mediawiki.org/wiki/Help:Formatting) -- [sudo]  gem install wikicloth

- [Org](http://orgmode.org/worg/dev/org-syntax.html) -- [sudo]  gem install org-ruby

- [Pod](http://perldoc.perl.org/perlpod.html) -- 需要环境 Perl  >= 5.10 (你的 Command Line 必须支持 perl  命令)低版本需要从CPAN安装 Pod::Simple.

- [ReStructuredText](http://docutils.sourceforge.net/docs/ref/rst/restructuredtext.html) -   需要环境 python >= 2 ((你的 Command  Line 必须支持  python2 命令)

- > 注： Gollum   同样需要你为 Python 2 安装 docutils .   安装方式同样依赖于操作系统与包管理工具（package manager）.

- 
  [Textile](http://redcloth.org/hobix.com/textile/quick.html) -- [sudo]  gem install RedCloth


默认的, Gollum 使用 kramdown gem to render Markdown. 因此, 你可以使用任何 [Markdown renderer supported by github-markup](https://github.com/github/markup/blob/master/lib/github/markup/markdown.rb). 需要记住的是，列表自上而下被使用. 因此, 比方说,如果你安装了 github/markdown 的话，那么 redcarpet 就不会被你使用.

##RUNNING：运行

### 简单入门

1. 在 command   line 中导航到你的 git 库 (wiki) .
2. 运行: gollum.
3. 在浏览器中打开 [http://localhost:4567](http://localhost:4567) .

这会打开名叫 WEBrick 的 web 服务（server）以一个网页界面运行 Gollum , 你可以在网页上编辑你的 wiki.

### 从源代码运行

1. git clone [https://github.com/gollum/gollum](https://github.com/gollum/gollum)

2. cd gollum

3. [sudo] bundle  install (may not always be necessary).

4. bundle exec  bin/gollum

   > 像这个,   gollum 假设目标 wiki （git 库）项目库本身.如果不是的话, 执行```bundle exec bin/gollum <path-to-wiki> ```安装.

5. 在浏览器中打开 [http://localhost:4567](http://localhost:4567) .

###Rack：机架式

 Gollum 可以使用 [rack-compatible web server ](https://github.com/rack/rack#supported-web-servers)运行. 去 [over here](https://github.com/gollum/gollum/wiki/Gollum-via-Rack)这里查看.

###Rack, with an authentication server：机架与认证服务器

 Gollum 可以使用集中身份认证（CAS，Central Authentication Service）、单点登录（SSO,single sign-on）服务器运行. 需要一点小小的调整，使 Gollum 成为支持用户登录的系统.例子与说明，请点击 [over here](https://github.com/gollum/gollum/wiki/Gollum-via-Rack-and-CAS-SSO). 

###Docker

Gollum 可以通过 [Docker ](https://www.docker.com/)运行. More on that [over here](https://github.com/gollum/gollum/wiki/Gollum-via-Docker).

### Service

Gollum 可以作为服务运行. More on that [over here](https://github.com/gollum/gollum/wiki/Gollum-as-a-service).

## CONFIGURATION配置

Gollum 支持如下命令选项:

| 选项Option          | 参数Arguments | 描述                                       |
| ----------------- | ----------- | ---------------------------------------- |
| --host            | [HOST]      | 指定 hostname 或者 IP 地址用以监听. 默认: 0.0.0.0.1  |
| --port            | [PORT]      | 指定 Gollum 使用的端口. 默认: 4567.               |
| --config          | [FILE]      | 指定    Gollum配置文件路径.                      |
| --ref             | [REF]       | 指定 serve 的 git 分支. 默认: master.           |
| --adapter         | [ADAPTER]   | 使用特殊 git 适配器运行 Gollum . 默认: grit.2       |
| --bare            | none        | 告诉 Gollum git 库应当当作空的. 只有在使用默认 grit 适配器的时候才需要. |
| --base-path       | [PATH]      | 指定 the leading portion of all Gollum URLs   (path info). 设置成 /wiki 将会方面的在 [http://localhost:4567/wiki/ ](http://localhost:4567/wiki/)中加入 wiki   . 默认: /. |
| --page-file-dir   | [PATH]      | 指定所有 Pages 的亚路径. 如果设置, Gollum 只会在此路径以及其下亚路径中被使用. 默认: 库的根目录. |
| --css             | none        | 告诉 Gollum 为每一个页面加入自定义 CSS. 从库的根目录开始使用 custom.css .3,5 |
| --js              | none        | 告诉 Gollum 为每一个页面加入自定义 JS. 从库的根目录开始使用 custom.js .3,5 |
| --emoji           | none        | 分析和解释表情标签   (比如 ❤️).                     |
| --no-edit         | none        | 放弃 编辑文档的功能   Disable the feature of editing pages. |
| --live-preview    | none        | 支持 页编辑的实时预览功能                            |
| --no-live-preview | none        | 放弃 页编辑的实时预览功能                            |
| --allow-uploads   | [MODE]      | 支持文件上传. 如果设置为 dir, Gollum 将会在库的根目录中存储所有上传文档至 /uploads/ 目录. 如果设置为 page, Gollum 会存储所有上传在当前编辑文档中.4 |
| --mathjax         | none        | 支持 MathJax (显示数学公式). 默认地, 使用 TeX-AMS-MML_HTMLorMML 配置和 autoload-all 插件.5 |
| --irb             | none        | 使用 [predefined API ](https://github.com/gollum/gollum-lib/)运行 Gollum 的 "控制台模式". |
| --h1-title        | none        | 告诉 Gollum 使用·第一个 <h1> 标签作为 page 标题.      |
| --show-all        | none        | 告诉 Gollum 展示所有页面. 默认地, 仅显示有效页面.          |
| --collapse-tree   | none        | 告诉 Gollum 折叠文件树, 当文件视图打开时。默认, 文件树是展开的.   |
| --user-icons      | [MODE]      | 告诉 Gollum 历史视图中使用不同的用户标签 。可以设置为 gravatar, identicon 或 none. 默认: none. |
| --mathjax-config  | [FILE]      | 指定自定义 MathJax 设置路径.如果不指定， 使用库文件根目录的 mathjax.config.js 文件. |
| --template-dir    | [PATH]      | 指定自定义 mustache 临时目录.                     |
| --help            | none        | 展示选项列表.                                  |
| --version         | none        | 展示 Gollum 当前版本.                          |

> 注记:
>
> 1. IP地址 0.0.0.0  支持远程登陆. 如果你想要个人 Wiki 使用IP地址 127.0.0.1.
> 2. 使用 --adapter  之前, 你应该阅读 [this](https://github.com/gollum/gollum/wiki/Git-adapters) .
> 3. 当使用 --css 或者 --js 之前, 各自的文件必须提交到你的  git 库，否则你会收到一个 302 重定向到重建的这一Page.
> 4. 文件可以通过拖拽到编辑器文本区域简单上传 (但是，这是默认编辑器独有的, 实时显示编辑器没有).
> 5. 阅读相关 [Security note](https://github.com/gollum/gollum/wiki/Security#custom-cssjs--mathjax-config) 使用之前.
>

## Config file配置文件

当 --config 使用时, Gollum 内部结构可以使用自定义方案. 这个设定贯穿 wiki 在一定程度上 用户级别的改变, 伴随 [customizing supported markups](https://github.com/gollum/gollum/wiki/Formats-and-extensions) 有很大可能失效.

所有提到的改变工作包含 Gollum 的配置文件(config.rb) 和架构的配置文件 (config.ru).

