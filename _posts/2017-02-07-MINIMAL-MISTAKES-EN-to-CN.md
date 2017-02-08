和主题相关的一些文字翻译。一些难理解的表达换成中文的。作为修改时候的参考。陷入的一个误区是，不应该把大量的时间花费在修改模板上，而应该放在文字本身。对于计算机语言理解的不到位，jekyll 模板的微言大义，都是耗费很多无意义时间的原因。

# MINIMAL MISTAKES, A JEKYLL THEME

[**JEKYLL THEMES**](https://mademistakes.com/work/jekyll-themes/)  DESIGN & DEVELOPMENT[ 22 COMMENTS](https://mademistakes.com/work/minimal-mistakes-jekyll-theme/#comments)

![Minimal Mistakes, a Jekyll Theme](https://mademistakes.com/assets/images/minimal-mistakes-3-feature-320.jpg)

[![splash layout example](https://mademistakes.com/assets/images/mm-layout-splash.png)](https://mademistakes.com/assets/images/mm-layout-splash.png)[![single layout with comments and related posts](https://mademistakes.com/assets/images/mm-layout-single-meta.png)](https://mademistakes.com/assets/images/mm-layout-single-meta.png)[![archive layout example](https://mademistakes.com/assets/images/mm-layout-archive.png)](https://mademistakes.com/assets/images/mm-layout-archive.png)

Minimal Mistakes is 一个灵活的两列 Jekyll 主题，非常适合在GitHub或您自己的服务器上托管您的个人网站，博客，或作品集（portfolio）。

包括响应布局（`single`, `archive`, 和 `splash` 页）移动设备和桌面浏览器看起来都很棒。顾名思义——简约的风格可以由你来定制或加强其功能 ![:smile:](https://assets-cdn.github.com/images/icons/emoji/unicode/1f604.png).

[ 实时预览](https://mmistakes.github.io/minimal-mistakes/)

#### Ruby Gem 主题

有意参与 Minimal Mistakes [pre-release “gemified” version](https://github.com/mmistakes/minimal-mistakes/tree/feature/theme-gem) beta 版本测试？阅读这篇博客 [learn how](https://mmistakes.github.io/minimal-mistakes/jekyll/gemified-theme-beta/).

## 主题特点:

- 兼容 GitHub Pages
- 多种布局选择（单页面，归档页面，初始页面） 
- 搜索引擎优化，由 [Twitter Cards](https://dev.twitter.com/cards/overview) 和 [Open Graph](http://ogp.me/) 数据支持
- 可选的 header images, sidebars, TOC, galleries, related posts, breadcrumb links（主內容上方，header下方的那個），以及其他。
- 可选的评论系统（[Disqus](https://disqus.com/), [Facebook](https://developers.facebook.com/docs/plugins/comments), Google+, [Staticman](https://staticman.net/),以及自定义）
- 可选的分析系统（[Google Analytics](https://www.google.com/analytics/) 以及自定义）

## Usage | 用法

要了解更多有关如何自定义这个主题的方法，为 posts 加入特征图片，修改外观和感觉，创建新 posts，an或其他 junk, [read up here](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/).

## Questions? | 问题？

Having a problem getting something to work or want to know why I setup something in a certain way? Ping me on Twitter [@mmistakes](http://twitter.com/mmistakes) or [file a GitHub issue](https://github.com/mmistakes/minimal-mistakes/issues/new). And if you make something cool with this theme feel free to let me know.

## License | 版权

This theme is free and open source software, distributed under the [MIT License](https://github.com/mmistakes/minimal-mistakes/blob/master/LICENSE).

​

[PreviouslySkinny Bones, a Jekyll Starter](https://mademistakes.com/work/skinny-bones-jekyll/)

- [Home](https://mademistakes.com/)
- [About](https://mademistakes.com/about/)
- [FAQs](https://mademistakes.com/faqs/)
- [Contact](https://mademistakes.com/contact/)
- [Support Me](https://mademistakes.com/support/)
- [Terms & Policies](https://mademistakes.com/terms/)
- [Sitemap](https://mademistakes.com/sitemap/)

© 2004–2017 Michael Rose. [ Twitter](https://twitter.com/mmistakes) / [ Instagram](https://www.instagram.com/mmistakes/) / [ GitHub](https://github.com/mmistakes)

# Quick-Start Guide

## Installing the Theme

如果你运行 Jekyll v3.3+ 在自托管服务器，你可以使用 Ruby gem 方法快速安装此主题。如果你托管在 GitHub Pages 你需要使用 “repo fork” 方式或直接拷贝这个主题的所有文件 ，[1](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/#fn:structure) 到你的网站.

**ProTip:** 如果你 forked Minimal Mistakes，确保删除 `/docs` 和 `/test`目录。这些文件夹包含主题的说明文档和测试页面。你可能不会在你的 repo 里面乱扔东西。

### Ruby Gem Method | Ruby Gem 方法

在你的 jekyll 网站的 `Gemfile`里面加入这一行：

```
gem "minimal-mistakes-jekyll"
```

在你的 jekyll 网站的 `_config.yml` 文件里面加入这一行：

```
theme: minimal-mistakes-jekyll
```

然后执行 Bundler 安装主题gem和依赖包：

```
bundle install
```

### GitHub Pages Compatible Method | GitHub Pages 拷贝方式

Fork [Minimal Mistakes theme](https://github.com/mmistakes/minimal-mistakes/fork)，重命名这个 repo ，叫 **USERNAME.github.io** — 用你的用户名替换 **USERNAME**。

![fork Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/assets/images/mm-theme-fork-repo.png)

**Note:** 你的 Jekyll 应该马上能在 [http://USERNAME.github.io 上查看。如果不行，你可以强制重建 **Customizing Your Site** （后文查看更多细节）

如果你在同一个 GitHub 用户名下托管多个基于Jekyll的网站， 你需要使用 Project Pages 替换 User Pages。Essentially 你重命名 repo，不是 **USERNAME.github.io** 的其他名字，从 `master`创建一个 `gh-pages`分支 。查看更多细节： [GitHub’s documentation](https://help.github.com/articles/user-organization-and-project-pages/).

![creating a new branch on GitHub](https://mmistakes.github.io/minimal-mistakes/assets/images/mm-gh-pages.gif)

从你的 Jekyll 网站根目录下，用以下文本替换 `Gemfile` 的内容:

```
source "https://rubygems.org"

gem "github-pages", group: :jekyll_plugins

group :jekyll_plugins do
  gem "jekyll-paginate"
  gem "jekyll-sitemap"
  gem "jekyll-gist"
  gem "jekyll-feed"
  gem "jemoji"
end
```

然后执行 `bundle update` ，验证所有的 gem 都已经安装。

### Remove the Unnecessary | 移除不必要的东西

如果你是 forked 或下载 `minimal-mistakes-jekyll` 库你可以安全移除以下的目录或文件：

- `.editorconfig`
- `.gitattributes`
- `.github`
- `/docs`
- `/test`
- `CHANGELOG.md`
- `minimal-mistakes-jekyll.gemspec`
- `README.md`
- `screenshot-layouts.png`
- `screenshot.png`

## Setup Your Site | 设置网站

根据你安装Minimal Mistakes的路径，设置会不大相同。

### Starting Fresh 

从空白目录和 `Gemfile`开始，你需要拷贝或者重建一个 [default `_config.yml`](https://github.com/mmistakes/minimal-mistakes/blob/master/_config.yml) 文件。对于每一个设置的完整解释请务必阅读的[**配置**](https://mmistakes.github.io/minimal-mistakes/docs/configuration/)部分。

处理Jekyll的配置文件后，您需要创建和编辑以下数据文件：

- [`_data/ui-text.yml`](https://github.com/mmistakes/minimal-mistakes/blob/master/_data/ui-text.yml) - UI text [documentation](https://mmistakes.github.io/minimal-mistakes/docs/ui-text/)
- [`_data/navigation.yml`](https://github.com/mmistakes/minimal-mistakes/blob/master/_data/navigation.yml) - navigation [documentation](https://mmistakes.github.io/minimal-mistakes/docs/navigation/)

### Starting from `jekyll new`

使用 `jekyll new`命令搭建一个网站要求您修改它创建的一些文件。

编辑`_config.yml` 并创建 `_data/ui-text.yml`以及`_data/navigation.yml` ，如同其上步骤说明。接着：

- 用修改过的 [Minimal Mistakes `index.html`](https://github.com/mmistakes/minimal-mistakes/blob/master/index.html)，替换 `<site root>/index.md` 。如果使用 [`home` layout](https://mmistakes.github.io/minimal-mistakes/docs/layouts/#home-page)，通过在  **_config.yml** 文件中添加需要的行打开 pagination。
- 改`_posts/0000-00-00-welcome-to-jekyll.markdown`里面的`layout: post`属性为 `layout: single`。
- 删除 `about.md`或在最后更新的文件里面替换 `layout: page` 为 `layout: single`，删掉 `icon-github.html`的索引 (如果需要的话，或许可以 [拷贝到你的`_includes`](https://github.com/jekyll/minima/tree/master/_includes) ).

------

That’s it! If all goes well running `bundle exec jekyll serve` should spin-up your site.



# Configuration | 配置

影响你的整个网站的设置通过改变 [Jekyll’s 设置文件](https://jekyllrb.com/docs/configuration/)改变整个网站: `_config.yml`, 从网站根目录下找. 如果没有你需要拷贝 [default `_config.yml`](https://github.com/mmistakes/minimal-mistakes/blob/master/_config.yml) .

**Note:** 技术原因，使用`jekyll serve`运行网站的时候，改变 `_config.yml` 不会自动应用变更，如果你修改了这个文件，重新启动 server process 才可以使修改的内容被使用。

花一点时间纵览一遍主题包含的 `_config.yml`文件。大多数设置添加了注释和默认值 ，每个的详细说明可以在下面找到。

## Site Settings |网站设置

### Theme

如果你使用Ruby gem版本的主题，你需要这行来激活它：

```
theme: minimal-mistakes-jekyll
```

### Site Locale

`site.locale` 用于声明网站中每个网页的主要语言。

*Example:* `locale: "en-US"` sets the `lang` attribute for the site to the *United States* flavor of English, while `en-GB` would be for the `United Kingdom` style of English. Country codes are optional and the shorter variation `locale: "en"` is also acceptable. To find your language and country codes check this [reference table](https://msdn.microsoft.com/en-us/library/ee825488(v=cs.20).aspx).

Properly setting the locale is important for associating localized text found in the [**UI Text**](https://mmistakes.github.io/minimal-mistakes/docs/ui-text/) data file. 不正确的匹配将导致UI的一部分消失（例如，按钮标签，节标题等）。

**Note:** The theme comes with localized text in English (`en`, `en-US`, `en-GB`). If you change `locale` in `_config.yml` to something else, most of the UI text will go blank. Be sure to add the corresponding locale key and translated text to `_data/ui-text.yml` to avoid this.

### Site Base URL

这个小选项导致Jekyll社区的各种混乱。如果你不作为一个GitHub的页面项目托管网站或子文件夹（例如：`/blog`），那么不要惹它。

 Minimal Mistakes demo site it’s hosted on GitHub at [https://mmistakes.github.io/minimal-mistakes](https://mmistakes.github.io/minimal-mistakes). 要正确设置我用这个基本路径`url: "https://mmistakes.github.io"`和`baseurl: "/minimal-mistakes"`。

For more information on how to properly use `site.url` and `site.baseurl` as intended by the Jekyll maintainers, check [Parker Moore’s post on the subject](https://byparker.com/blog/2014/clearing-up-confusion-around-baseurl/).

**Note:** When using `baseurl` remember to include it as part of your path when testing your site locally. Values of `url: ` and `baseurl: "/blog"` would make your local site visible at `http://localhost:4000/blog` and not `http://localhost:4000`.

### Site Repository 

在 `_config.yml`加入 your repository name 

```
repository: "username/repo-name"
```

“NWO”代表“与所有者名称。这是 GitHub 上的行话 the username of the owner of the repository plus a forward slash plus the name of the repository。

Your `site.github.*` fields should fill in like normal. 如果你使用-verbose标志运行Jekyll，你应该能够看到所有的API调用。

如果你没有正确设置 `repository` ， to `serve` or `build` your Jekyll site 的时候你估计会看到以下错误：

**Liquid Exceptions:** No repo name found. Specify using `PAGES_REPO_NWO` environment variables, `repository` in your configuration, or set up `origin` git remote pointing to your github.com repository.

For more information on how `site.github` data can be used with Jekyll check out [`github-metadata`’s documentation](https://github.com/jekyll/github-metadata).

### Site Default Teaser Image |网站默认 Teaser 图片

To assign a fallback teaser image used in the “**Related Posts**” module, place a graphic in the `/assets/images/` directory and add the filename to `_config.yml`like so:

```
teaser: /assets/images/500x300.png
```

可以被 YAML Front Matter 覆盖：

```
header:
  teaser: /assets/images/my-awesome-post-teaser.jpg
```

![teaser image example](https://mmistakes.github.io/minimal-mistakes/assets/images/mm-teaser-images-example.jpg)Example of teaser images found in the related posts module.

### Breadcrumb Navigation (Beta)

启用面包屑链接，以帮助访问者更好地浏览深度网站。由于实施它们的脆弱的方法，它们不总是可靠地产生准确的链接。为了获得最佳效果：

1. Use a category based permalink structure e.g. `permalink: /:categories/:title/`
2. 为每个类别页面Manually create pages ，或者使用插件 [jekyll-archives](https://github.com/jekyll/jekyll-archives) 自动生成。如果这些页面不存在，面包屑链接将被破坏。

![breadcrumb navigation example](https://mmistakes.github.io/minimal-mistakes/assets/images/mm-breadcrumbs-example.jpg)

```
breadcrumbs: true  # disabled by default
```

Breadcrumb 开始链接文本和分隔符在 [UI Text data file](https://mmistakes.github.io/minimal-mistakes/docs/ui-text/) 可改。

### Reading Time | 启用与估计阅读时间片段

YAML Front Matter头里面写 `read_time: true` 。

 `200` has been set as 每分钟阅读默认值，在 `words_per_minutes: ` in `_config.yml`里面改动。

![reading time example](https://mmistakes.github.io/minimal-mistakes/assets/images/mm-read-time-example.jpg)

替代方案：apply as a default in `_config.yml` like so:

```
defaults:
  # _posts
  - scope:
      path: ""
      type: posts
    values:
      read_time: true
```

YAML Front Matter 的设置会覆盖 `_config.yml`的设置， `read_time: false` 。

### Comments |评论

[**Disqus**](https://disqus.com/), [**Discourse**](https://www.discourse.org/), [**Facebook**](https://developers.facebook.com/docs/plugins/comments), **Google+**, and static-based commenting via [**Staticman**](https://staticman.net/) are built into the theme. First set the comment provider you’d like to use:

| Name            | Comment Provider  |
| --------------- | ----------------- |
| **disqus**      | Disqus            |
| **discourse**   | Discourse         |
| **facebook**    | Facebook Comments |
| **google-plus** | Google+ Comments  |
| **staticman**   | Staticman         |
| **custom**      | Other             |

方法一：Then add `comments: true` to each document  YAML Front Matter

方法二： to each document, apply as a default in `_config.yml`. Static-Based Comments via Staticman

Transform user comments into `_data` files that live inside of your GitHub repository by enabling Staticman.

###### Add Staticman as a Collaborator

1. Allow Staticman push access to your GitHub repository by clicking on **Settings**, then the **Collaborators** tab and adding `staticmanapp` as a collaborator.
2. To accept the pending invitation visit: `https://api.staticman.net/v1/connect/{your GitHub username}/{your repository name}`. Consult the Staticman “[Get Started](https://staticman.net/get-started)” guide for more info.

###### Configure Staticman

Default settings have been provided in `_config.yml`. The important ones to set are `provider: "staticman"`, `branch`, and `path`. View the [full list of configurations](https://github.com/eduardoboucas/staticman#jekyll-configuration).

**Branch setting:** This is the branch comment files will be sent to via pull requests. If you host your site on GitHub Pages it will likely be `master` unless your repo is setup as a project — use `gh-pages`in that case.

```
comments:
  provider: "staticman"
staticman:
  allowedFields          : ['name', 'email', 'url', 'message']
  branch                 : # "master", "gh-pages"
  commitMessage          : "New comment."
  filename               : comment-{@timestamp}
  format                 : "yml"
  moderation             : true
  path                   : "_data/comments/{options.slug}"
  requiredFields         : ['name', 'email', 'message']
  transforms:
    email                : "md5"
  generatedFields:
    date:
      type               : "date"
      options:
        format           : "iso8601" # "iso8601" (default), "timestamp-seconds", "timestamp-milliseconds"
```

###### Comment Moderation

By default comment moderation is enabled in `_config.yml`. As new comments are submitted Staticman will send a pull request. Merging these in will approve the comment, close the issue, and automatically rebuild your site (if hosted on GitHub Pages).

To skip this moderation step simply set `moderation: false`.

**ProTip:** Create a GitHub webhook that sends a `POST` request to the following payload URL `https://api.staticman.net/v1/webhook` and triggers a “Pull request” event to delete Staticman branches on merge.

![pull-request webhook](https://mmistakes.github.io/minimal-mistakes/assets/images/mm-staticman-pr-webhook.jpg)

##### Other Comment Providers

To use another provider not included with the theme set `provider: "custom"`then add their embed code to `_includes/comments-providers/custom.html`.

### Custom Feed URL 

需要去 feeds.feedburner.com 之类的网站注册。

By default the theme links to `feed.xml` generated in the root of your site by the **jekyll-feed** plugin. To link to an externally hosted feed update `atom_feed`in `_config.yml` like so:

```
atom_feed:
  path: "http://feeds.feedburner.com/youFeedname"
```

**Note:** By default the site feed is linked in 两个地方 : inside the [`` element](https://mmistakes.github.io/master/_includes/head.html) and at the bottom of every page in the [site footer](https://github.com/mmistakes/minimal-mistakes/master/_includes/footer.html).

### SEO, Social Sharing, and Analytics Settings

All optional, but a good idea to take the time setting up to improve SEO and links shared from the site.

#### Google Search Console

Formerly known as [Google Webmaster Tools](https://www.google.com/webmasters/tools/), add your [verification code](https://support.google.com/analytics/answer/1142414?hl=en) like so: `google_site_verification: "yourVerificationCode"`.

**Note:** You likely won’t have to do this if you verify site ownership through **Google Analytics** instead.

#### Bing Webmaster Tools

There are several ways to [verify site ownership](https://www.bing.com/webmaster/help/how-to-verify-ownership-of-your-site-afcfefc6) — the easiest adding an authentication code to your config file.

Copy and paste the string inside of `content`:

```
<meta name="msvalidate.01" content="0FC3FD70512616B052E755A56F8952D" />
```

Into `_config.yml`

```
bing_site_verification: "0FC3FD70512616B052E755A56F8952D"
```

#### Alexa

To [claim your site](http://www.alexa.com/siteowners/claim) with Alexa add the provided verification ID `alexa_site_verification: "yourVerificationID"`.

#### Yandex

To verify site ownership copy and paste the string inside of `name`:

```
<meta name='yandex-verification' content='2132801JL' />
```

Into `_config.yml`

```
yandex_site_verification: "2132801JL"
```

#### Twitter Cards and Facebook Open Graph

To improve the appearance of links shared from your site to social networks like Twitter and Facebook be sure to configure the following.

##### Site Twitter Username

Twitter username for the site. For pages that have custom author Twitter accounts assigned in their YAML Front Matter or data file, they will be attributed as a **creator** in the Twitter Card.

For example if my site’s Twitter account is `@mmistakes-theme` I would add the following to `_config.yml`

```
twitter:
  username: "mmistakes-theme"
```

And if I assign `@mmistakes` as an author account it will appear in the Twitter Card along with `@mmistakes-theme`, attributed as a creator of the page being shared.

**Note**: You need to [apply for Twitter Cards](https://dev.twitter.com/docs/cards) and validate they’re working on your site before they will begin showing up.

##### Facebook Open Graph

If you have a Facebook ID or publisher page add them:

```
facebook:
  app_id:  # A Facebook app ID
  publisher:  # A Facebook page URL or ID of the publishing entity
```

开始前，您需要执行以下操作：

- [创建 Facebook 应用编号](https://developers.facebook.com/docs/opengraph/getting-started#create-app)
- [配置应用，以便配合 Facebook 使用](https://developers.facebook.com/docs/opengraph/getting-started#setup-app)
- 拥有某个公共 Web 服务器的访问权限并且能够在该服务器上创建一个静态网页

While not part a part of Open Graph, you can also add your Facebook username for use in the sidebar and footer.

```
facebook:
  username: "michaelrose"  # https://www.facebook.com/michaelrose
```

**ProTip:** To debug Open Graph data use [this tool](https://developers.facebook.com/tools/debug/og/object?q=https%3A%2F%2Fmademistakes.com) to test your pages. If content changes aren’t reflected you will probably have to hit the **Fetch new scrape information** button to refresh.

##### Open Graph Default Image

For pages that don’t have a `header.image` assigned in their YAML Front Matter, `site.og_image` will be used as a fallback. Use your logo, icon, avatar or something else that is meaningful. Just make sure it is place in the `/assets/images/` folder, a minimum size of 120px by 120px, and less than 1MB in file size.

```
og_image: /assets/images/site-logo.png
```

![Twitter Card summary example](https://mmistakes.github.io/minimal-mistakes/assets/images/mm-twitter-card-summary-image.jpg)Example of a image placed in a Summary Card.

Documents who have a `header.image` assigned in their YAML Front Matter will appear like this when shared on Twitter and Facebook.

![page shared on Twitter](https://mmistakes.github.io/minimal-mistakes/assets/images/mm-twitter-card-summary-large.jpg)Shared page on Twitter with header image assigned.

![page shared on Facebook](https://mmistakes.github.io/minimal-mistakes/assets/images/facebook-share-example.jpg)Shared page on Facebook with header image assigned.

##### Include your social profile in search results

Use markup on your official website to add your [social profile information](https://developers.google.com/structured-data/customize/social-profiles#adding_structured_markup_to_your_site) to the Google Knowledge panel in some searches. Knowledge panels can prominently display your social profile information.

```
social:
  type:  # Person or Organization (defaults to Person)
  name:  # If the user or organization name differs from the site's name
  links:
    - "https://twitter.com/yourTwitter"
    - "https://facebook.com/yourFacebook"
    - "https://instagram.com/yourProfile"
    - "https://www.linkedin.com/in/yourprofile"
    - "https://plus.google.com/your_profile"
```

#### Analytics

Analytics is disabled by default. To enable globally select one of the following:

| Name                 | Analytics Provider                       |
| -------------------- | ---------------------------------------- |
| **google**           | [Google Standard Analytics](https://www.google.com/analytics/) |
| **google-universal** | [Google Universal Analytics](https://www.google.com/analytics/) |
| **custom**           | Other analytics providers                |

For Google Analytics add your Tracking Code:

```
analytics:
  provider: "google-universal"
  google:
    tracking_id: "UA-1234567-8"
```

To use another provider not included with the theme set `provider: "custom"`then add their embed code to `_includes/analytics-providers/custom.html`.

## Site Author

Used as the defaults for defining what appears in the author sidebar.



To add social media links not included with the theme or customize the author sidebar further, read the full [layout documentation](https://mmistakes.github.io/minimal-mistakes/docs/layouts/#author-profile).

## Reading Files 

Nothing out of the ordinary here. `include` and `exclude` may be the only things you need to alter.

## Conversion and Markdown Processing

Again nothing out of the ordinary here as the theme adheres to the defaults used by GitHub Pages. [**Kramdown**](http://kramdown.gettalong.org/) for Markdown conversion, [**Rouge**](http://rouge.jneen.net/) syntax highlighting, and incremental building disabled. Change them if you need to.

## Front Matter Defaults

To save yourself time setting [Front Matter Defaults](https://jekyllrb.com/docs/configuration/#front-matter-defaults) for posts, pages, and collections is the way to go. Sure you can assign layouts and toggle settings like **reading time**, **comments**, and **social sharing** in each file, but that’s not ideal.

Using the `default` key in `_config.yml` you could set the layout and enable author profiles, reading time, comments, social sharing, and related posts for all posts — in one shot.

```
defaults:
  # _posts
  - scope:
      path: ""
      type: posts
    values:
      layout: single
      author_profile: true
      read_time: true
      comments: true
      share: true
      related: true
```

Pages Front Matter defaults can be scoped like this:

```
defaults:
  # _pages
  - scope:
      path: ""
      type: pages
    values:
      layout: single
```

And collections like this:

```
defaults:
  # _foo
  - scope:
      path: ""
      type: foo
    values:
      layout: single
```

And of course any default value can be overridden by settings in a post, page, or collection file. All you need to do is specify the settings in the YAML Front Matter. For more examples be sure to check out the demo site’s [`_config.yml`](https://github.com/mmistakes/minimal-mistakes/gh-pages/_config.yml).

## Outputting

The default permalink style used by the theme is `permalink: /:categories/:title/`. If you have a post named `2016-01-01-my-post.md` with `categories: foo` in the YAML Front Matter, Jekyll will generate `_site/foo/my-post/index.html`.

**Note:** If you plan on enabling breadcrumb links — including category names in permalinks is a big part of how those are created.

### Paginate

If [using pagination](https://github.com/jekyll/jekyll-paginate) on the homepage you can change the amount of posts shown with:

```
paginate: 5
```

You’ll also need to include some Liquid and HTML to properly use the paginator, which you can find in the **Layouts** section under [Home Page](https://mmistakes.github.io/minimal-mistakes/docs/layouts/#home-page).

**Please note:** [Jekyll’s pagination](http://jekyllrb.com/docs/pagination/) may have unexpected results when used on pages other than the home page eg. `/blog/index.html`.

### Timezone

This sets the timezone environment variable, which Ruby uses to handle time and date creation and manipulation. Any entry from the [IANA Time Zone Database](http://en.wikipedia.org/wiki/List_of_tz_database_time_zones) is valid. The default is the local time zone, as set by your operating system.

```
timezone: America/New_York
```

## Plugins

When hosting with GitHub Pages a small [set of gems](https://pages.github.com/versions/) have been whitelisted for use. The theme uses a few of them which can be found under `gems`. Additional settings and configurations are documented in the links below.

| Plugin                                   | Description                              |
| ---------------------------------------- | ---------------------------------------- |
| [jekyll-paginate](https://github.com/jekyll/jekyll-paginate) | Pagination Generator for Jekyll.         |
| [jekyll-sitemap](https://github.com/jekyll/jekyll-sitemap) | Jekyll plugin to silently generate a sitemaps.org compliant sitemap for your Jekyll site. |
| [jekyll-gist](https://github.com/jekyll/jekyll-gist) | Liquid tag for displaying GitHub Gists in Jekyll sites. |
| [jekyll-feed](https://github.com/jekyll/jekyll-feed) | A Jekyll plugin to generate an Atom (RSS-like) feed of your Jekyll posts. |
| [jemoji](https://github.com/jekyll/jemoji) | GitHub-flavored emoji plugin for Jekyll. |

If you’re hosting elsewhere then you don’t really have to worry about what is whitelisted as you are free to include whatever [Jekyll plugins](https://jekyllrb.com/docs/plugins/) you desire.

## Archive Settings |

The theme ships with support for taxonomy (category and tag) pages. GitHub Pages hosted sites need to use a *Liquid only* approach while those hosted elsewhere can use plugins like [**jekyll-archives**](https://github.com/jekyll/jekyll-archives) to generate these pages automatically.

The default `type` is set to use Liquid.

**Note:** `category_archive` and `tag_archive` were previously named `categories` and `tags`. Names were changed to avoid possible conflicts with `site.categories` and `site.tags`.

```
category_archive:
    type: liquid
  path: /categories/
tag_archive:
  type: liquid
  path: /tags/
```

Which would create category and tag links in the breadcrumbs and page meta like: `/categories/#foo` and `/tags/#foo`.

**Note:** for these links to resolve properly, category and tag index pages need to exist at [`/categories/index.html`](https://github.com/mmistakes/minimal-mistakes/blob/master/docs/_pages/category-archive.html) and [`/tags/index.html`](https://github.com/mmistakes/minimal-mistakes/blob/master/docs/_pages/tag-archive.html). The necessary Liquid code to build these pages can be taken from the demo site.

If you have the luxury of using Jekyll Plugins then [**jekyll-archives**](https://github.com/jekyll/jekyll-archives) will make your life much easier as category and tag pages are created for you.

Change `type` to `jekyll-archives` and apply the following [configurations](https://github.com/jekyll/jekyll-archives/blob/master/docs/configuration.md):

```
category_archive:
  type: jekyll-archives
  path: /categories/
tag_archive:
  type: jekyll-archives
  path: /tags/
jekyll-archives:
  enabled:
    - categories
    - tags
  layouts:
    category: archive-taxonomy
    tag: archive-taxonomy
  permalinks:
    category: /categories/:name/
    tag: /tags/:name/
```

**Note:** The `archive-taxonomy` layout used by jekyll-archives is provided with the theme and can be found in the `_layouts` folder.

## HTML Compression

If you care at all about performance (and really who doesn’t) compressing the HTML files generated by Jekyll is a good thing to do.

If you’re hosting with GitHub Pages there aren’t many options afforded to you for optimizing the HTML Jekyll generates. Thankfully there is some Liquid wizardry you can use to strip whitespace and comments to reduce file size.

There’s a variety of configurations and caveats to using the `compress` layout, so be sure to read through the [documentation](http://jch.penibelst.de/) if you decide to make change the defaults set in the theme’s `_config.yml`.

```
compress_html:
  clippings: all
  ignore:
    envs: development  # disable compression in dev environment
```

**Caution:** Inline JavaScript comments can cause problems with `compress.html`, so be sure to `/* comment this way */` and avoid `// these sorts of comments`.



# Structure

Nothing clever here ![:wink:](https://assets-cdn.github.com/images/icons/emoji/unicode/1f609.png). Layouts, data files, and includes are all placed in their default locations. Stylesheets and scripts in `assets`, and a few development related files in the project’s root directory.

**Please note:** If you installed Minimal Mistakes via the Ruby Gem method, theme files like `_layouts`, `_includes`, `_sass`, and `/assets/` will be missing. This is normal as they are bundled with the [`minimal-mistakes-jekyll`](https://rubygems.org/gems/minimal-mistakes-jekyll) Ruby gem.

```
minimal-mistakes
├── _data                      # data files for customizing the theme
|  ├── navigations.yml         # main navigation links
|  └── ui-text.yml             # text used throughout the theme's UI
├── _includes
|  ├── analytics-providers     # snippets for analytics (Google and custom)
|  ├── comments-providers      # snippets for comments (Disqus, Facebook, Google+, and custom)
|  ├── footer                  # custom snippets to add to site footer
|  ├── head                    # custom snippets to add to site head
|  ├── base_path               # site.url + site.baseurl shortcut
|  ├── feature_row             # feature row helper
|  ├── gallery                 # image gallery helper
|  ├── group-by-array          # group by array helper for archives
|  ├── nav_list                # navigation list helper
|  ├── toc                     # table of contents helper
|  └── ...
├── _layouts
|  ├── archive-taxonomy.html   # tag/category archive for Jekyll Archives plugin
|  ├── archive.html            # archive listing documents in an array
|  ├── compress.html           # compresses HTML in pure Liquid
|  ├── default.html            # base for all other layouts
|  ├── home.html               # home page
|  ├── single.html             # single document (post/page/etc)
|  └── splash.html             # splash page
├── _sass                      # SCSS partials
├── assets
|  ├── css
|  |  └── main.scss            # main stylesheet, loads SCSS partials from _sass
|  ├── fonts
|  |  └── fontawesome-webfont  # Font Awesome webfonts
|  ├── images                  # image assets for posts/pages/collections/etc.
|  ├── js
|  |  ├── plugins              # jQuery plugins
|  |  ├── vendor               # vendor scripts
|  |  ├── _main.js             # plugin settings and other scripts to load after jQuery
|  |  └── main.min.js          # optimized and concatenated script file loaded before </body>
├── _config.yml                # site configuration
├── Gemfile                    # gem file dependencies
├── index.html                 # paginated home page showing recent posts
└── package.json               # NPM build scripts
```



# UI Text

大概意思是各种UI元素的文字，可以在[`_data/ui-text.yml`](https://github.com/mmistakes/minimal-mistakes/blob/master/_data/ui-text.yml) 文件中修改为其他的语言。

 `_layouts`和 `_includes` have all been grouped together as a set of translation keys. This is by no means a full-on i18n solution, but it does help make customizing things a bit easier.

Currently the English[1](https://mmistakes.github.io/minimal-mistakes/docs/ui-text/#fn:yaml-anchors) main keys in [`_data/ui-text.yml`](https://github.com/mmistakes/minimal-mistakes/blob/master/_data/ui-text.yml) are translated to the following languages:

- Brazilian Portuguese (Português brasileiro)
- Chinese
- French (Français)
- German (Deutsch)
- Italian (Italiano)
- Nepali (Nepalese)
- Spanish (Español)
- Turkish (Türkçe)

If you’re are interested in localizing them into other languages feel free to submit a pull request and I will be happy to look it over.

Many of the label based keys like `meta_label`, `categories_label`, `tags_label`, `share_on_label`, and `follow_label` can be left blank if you’d like to omit them from view. It really depends on you and if you want an even more minimal look to your site.

![UI text labels](https://mmistakes.github.io/minimal-mistakes/assets/images/mm-ui-text-labels.jpg)

**Note:** The theme comes with localized text in English (`en`, `en-US`, `en-GB`). If you change `locale` in `_config.yml` to something else, most of the UI text will go blank. Be sure to add the corresponding locale key and translated text to `_data/ui-text.yml` to avoid this.



# Navigation

## Masthead

The masthead links use a “priority plus” design pattern. Meaning, 尽可能多的显示导航项目，水平放置一个切换显示其余。

To define these links add titles and URLs under the `main` key in `_data/navigation.yml`:

```
main:
  - title: "Quick-Start Guide"
    url: /docs/quick-start-guide/
  - title: "Posts"
    url: /year-archive/

```

Which will give you a responsive masthead similar to this:

![priority plus masthead animation](https://mmistakes.github.io/minimal-mistakes/assets/images/mm-priority-plus-masthead.gif)

**ProTip:**重要的链接放前面 they’re always visible and 不是隐藏在后的**菜单切换**.

## Breadcrumbs (Beta)

Enable breadcrumb links to help visitors better navigate deep sites. Because of the fragile method of implementing them they don’t always produce accurate links reliably. For best results:

1. Use a category based permalink structure e.g. `permalink: /:categories/:title/`
2. Manually create pages for each category or use a plugin like [jekyll-archives](https://github.com/jekyll/jekyll-archives) to auto-generate them. If these pages don’t exist breadcrumb links to them will be broken.

![breadcrumb navigation example](https://mmistakes.github.io/minimal-mistakes/assets/images/mm-breadcrumbs-example.jpg)

```
breadcrumbs: true  # disabled by default
```

Breadcrumb start link text and separator character can both be changed in `_data/ui-text.yml`.

```
breadcrumb_home_label : "Home"
breadcrumb_separator  : "/"
```

For breadcrumbs that resemble something like `Start > Blog > My Awesome Post`you’d apply these settings:

```
breadcrumb_home_label : "Start"
breadcrumb_separator  : ">"
```

-------------------------------

## Default Layout

其他布局继承于这个就基本布局。这个布局没有太多其他东西 ，除了 `_includes`里面:

- `<head>` elements
- masthead 导航链接·
- `{{ content }}`
- page footer
- scripts

**Note:**  a post or page 不要直接使用这个布局，其他 layouts 会在 YAML Front Matter 设置 `layout: default`。

### Layout Based and User-Defined Classes

Class names corresponding to each layout are automatically added to the `` element eg. ``.

| layout                | class name                  |
| --------------------- | --------------------------- |
| archive               | `.layout--archive`          |
| archive-taxonomy 归档分类 | `.layout--archive-taxonomy` |
| single                | `.layout--single`           |
| splash                | `.layout--splash`           |
| home                  | `.layout--home`             |

使用YAML Front Matter，您还可以使用CSS或JavaScript指定自定义类来定位。Perfect for “art directed” posts or adding custom styles to specific pages.

举例：

```
---
layout: splash
classes:
  - landing
  - dark-theme
---
```

输出：

```
<body class="layout--splash landing dark-theme">
```

## Compress Layout | 压缩布局

A Jekyll layout that compresses HTML in pure Liquid. To enable add `layout: compress` to `_layouts/default.html`.

**Note:** Has been known to mangle markup and break JavaScript… especially if inline `// comments` are present. For this reason it has been disabled by default.

- [Documentation](http://jch.penibelst.de/)

## Single Layout | 单页面

The layout you’ll likely use the most — sidebar and main content combo.

**Includes:**

- Optional header image with caption
- Optional header overlay (solid color/image) + text and optional “call to action” button
- Optional social sharing links module
- Optional comments module
- Optional related posts module

![single layout with header example](https://mmistakes.github.io/minimal-mistakes/assets/images/mm-layout-single-header.png)![single layout with comments and related posts](https://mmistakes.github.io/minimal-mistakes/assets/images/mm-layout-single-meta.png)Image header and meta info examples for `single` layout

Assign with `layout: single`, or better yet apply as a [Front Matter default](https://mmistakes.github.io/minimal-mistakes/docs/configuration/#front-matter-defaults) in `_config.yml`.

## Archive Layout | 归档页

Essentially the same as `single` with markup adjustments and some modules removed.

**Includes:**

- Optional header image with caption
- Optional header overlay (solid color/image) + text and optional “call to action” button
- List and grid views

![archive layout example](https://mmistakes.github.io/minimal-mistakes/assets/images/mm-layout-archive.png)List view example.

Below are sample archive pages you can easily drop into your project, taking care to rename `permalink`, `title`, or the filename  100% 匹配才行.

- [All Posts Grouped by Category – List View](https://github.com/mmistakes/minimal-mistakes/blob/master/docs/_pages/category-archive.html)
- [All Posts Grouped by Tags – List View](https://github.com/mmistakes/minimal-mistakes/blob/master/docs/_pages/tag-archive.html)
- [All Posts Grouped by Year – List View](https://github.com/mmistakes/minimal-mistakes/blob/master/docs/_pages/year-archive.html)
- [All Posts Grouped by Collection – List View](https://github.com/mmistakes/minimal-mistakes/blob/master/docs/_pages/collection-archive.html)
- [Portfolio Collection – Grid View](https://github.com/mmistakes/minimal-mistakes/blob/master/docs/_pages/portfolio-archive.html)

Post and page excerpts are auto-generated by Jekyll which grabs the first paragraph of text. To override this text with something more specific use the following YAML Front Matter:

```
excerpt: "A unique line of text to describe this post that will display in an archive listing and meta description with SEO benefits."
```

### Grid View

Adding `type=grid` to `archive-single` helper will display archive posts in a 4 column grid. For example to create an archive displaying all documents in the portfolio collection:

**Step 1:** Create a portfolio archive page (eg. `_pages/portfolio-archive.html`) with the following YAML Front Matter:

```
---
layout: archive
title: "Portfolio"
permalink: /portfolio/
author_profile: false
---
```

**Step 2:** Loop over all documents in the portfolio collection and output in a grid:

```
<div class="grid__wrapper">
  {% for post in site.portfolio %}
    {% include archive-single.html type="grid" %}
  {% endfor %}
</div>
```

To produce something like this:

![archive grid view example](https://mmistakes.github.io/minimal-mistakes/assets/images/mm-archive-grid-view-example.jpg)Grid view example.

**Note:** More information on using this `_include` can be found under [**Helpers**](https://mmistakes.github.io/minimal-mistakes/docs/helpers/).

### Taxonomy Archive

If you have the luxury of using Jekyll plugins the creation of category and tag archives is greatly simplified. Enable support for the [`jekyll-archives`](https://github.com/jekyll/jekyll-archives) plugin with a few `_config.yml` settings as noted in the [**Configuration**](https://mmistakes.github.io/minimal-mistakes/docs/configuration/#archive-settings) section.

![archive taxonomy layout example](https://mmistakes.github.io/minimal-mistakes/assets/images/mm-layout-archive-taxonomy.png)

### Home Page

A derivative archive page layout to be used as a simple home page. It is built to show a paginated list of recent posts based off of the [pagination settings](https://mmistakes.github.io/minimal-mistakes/docs/configuration/#paginate) in `_config.yml`.

![paginated home page example](https://mmistakes.github.io/minimal-mistakes/assets/images/mm-home-post-pagination-example.jpg)Example of a paginated home page showing 5 recent posts.

To use create `index.html` at the root of your project and add the following YAML Front Matter:

```
---
layout: home
---
```

Then configure pagination in `_config.yml`.

```
paginate: 5 # amount of posts to show
paginate_path: /page:num/
```

If you’d rather have a paginated page of posts reside in a subfolder instead of acting as your homepage make the following adjustments.

Create `index.html` in the location you’d like. For example if I wanted it to live at **/blog** I’d create `/blog/index.html` with `layout: home` in its YAML Front Matter.

Then adjust the `paginate_path` in **_config.yml** to match.

```
paginate_path: /blog/page:num
```

**Note:** Jekyll can only paginate a single `index.html` file. If you’d like to paginate more pages (e.g. category indexes) you’ll need the help of a custom plugin. For more pagination related settings check the [**Configuration**](https://mmistakes.github.io/minimal-mistakes/docs/configuration/#paginate) section.

## Splash Page Layout

For full-width landing pages that need a little something extra add `layout: splash` to the YAML Front Matter.

**Includes:**

- Optional header image with caption
- Optional header overlay (solid color/image) + text and optional “call to action” button
- Feature blocks (`left`, `center`, and `right` alignment options)

![splash page layout example](https://mmistakes.github.io/minimal-mistakes/assets/images/mm-layout-splash.png)

Feature blocks can be assigned and aligned to the `left`, `right`, or `center`with a sprinkling of YAML. For full details on how to use the `feature_row`helper check the [**Content**](https://mmistakes.github.io/minimal-mistakes/docs/helpers/) section or review a [sample splash page](https://github.com/mmistakes/minimal-mistakes/blob/master/docs/_pages/splash-page.md).

------

## Headers

To add some visual punch to a post or page, a large full-width header image can be included.

Be sure to resize your header images. `~1280px` is a good width if you aren’t [responsively serving up images](http://alistapart.com/article/responsive-images-in-practice). Through the magic of CSS they will scale up or down to fill the container. If you go with something too small it will look like garbage when upscaled, and something too large will hurt performance.

**Please Note:** Paths for image headers, overlays, teasers, [galleries](https://mmistakes.github.io/minimal-mistakes/docs/helpers/#gallery), and [feature rows](https://mmistakes.github.io/minimal-mistakes/docs/helpers/#feature-row) have changed and require a full path. Instead of just `image: filename.jpg` you’ll need to use the full path eg: `image: /assets/images/filename.jpg`. The preferred location is now `/assets/images/`, but can be placed elsewhere or external hosted. This all applies for image references in `_config.yml` and `author.yml` as well.

![single layout header image example](https://mmistakes.github.io/minimal-mistakes/assets/images/mm-single-header-example.jpg)

Place your images in the `/assets/images/` folder and add the following YAML Front Matter:

```
header:
  image: /assets/images/image-filename.jpg
```

For externally hosted images include the full image path instead of just the filename:

```
header:
  image: http://some-site.com/assets/images/image.jpg
```

To include a caption or attribution for the image:

```
header:
  image: /assets/images/unsplash-image-1.jpg
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
```

**ProTip:** Captions written in Markdown are supported, so feel free to add links, or style text. Just be sure to wrap it in quotes.

### Header Overlay

To overlay text on top of a header image you have a few more options:

| Name               | Description                              | Default                           |
| ------------------ | ---------------------------------------- | --------------------------------- |
| **overlay_image**  | Header image you’d like to overlay. Same rules as `header.image` from above. |                                   |
| **overlay_filter** | Color/opacity to overlay on top of the header image eg: `0.5` or `rgba(255, 0, 0, 0.5)`. |                                   |
| **excerpt**        | Auto-generated page excerpt is added to the overlay text or can be overridden. |                                   |
| **cta_label**      | Call to action button text label.        | `more_label` in UI Text data file |
| **cta_url**        | Call to action button URL.               |                                   |

With this YAML Front Matter:

```
excerpt: "This post should display a **header with an overlay image**, if the theme supports it."
header:
  overlay_image: /assets/images/unsplash-image-1.jpg
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
  cta_label: "More Info"
  cta_url: "https://unsplash.com"

```

You’d get a header image overlaid with text and a call to action button like this:

![single layout header overlay example](https://mmistakes.github.io/minimal-mistakes/assets/images/mm-single-header-overlay-example.jpg)

You also have the option of specifying a solid background-color to use instead of an image.

![single layout header overlay with background fill](https://mmistakes.github.io/minimal-mistakes/assets/images/mm-single-header-overlay-fill-example.jpg)

```
excerpt: "This post should display a **header with a solid background color**, if the theme supports it."
header:
  overlay_color: "#333"

```

You can also specifying the opacity (between `0` and `1`) of a black overlay like so:

![transparent black overlay](https://mmistakes.github.io/minimal-mistakes/assets/images/mm-header-overlay-black-filter.jpg)

```
excerpt: "This post should [...]"
header:
  overlay_image: /assets/images/unsplash-image-1.jpg
  overlay_filter: 0.5 # same as adding an opacity of 0.5 to a black background
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
  cta_label: "More Info"
  cta_url: "https://unsplash.com"

```

Or if you want to do more fancy things, go full rgba:

![transparent red overlay](https://mmistakes.github.io/minimal-mistakes/assets/images/mm-header-overlay-red-filter.jpg)

```
excerpt: "This post should [...]"
header:
  overlay_image: /assets/images/unsplash-image-1.jpg
  overlay_filter: rgba(255, 0, 0, 0.5)
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
  cta_label: "More Info"
  cta_url: "https://unsplash.com"

```

------

## Sidebars

The space to the left of a page’s main content is blank by default, but has the ability to show an author profile (name, short biography, social media links), custom content, or both.

### Author Profile

Add `author_profile: true` to a post or page’s YAML Front Matter.

![single layout example](https://mmistakes.github.io/minimal-mistakes/assets/images/mm-layout-single.png)

Better yet, enable it with Front Matter Defaults set in `_config.yml`.

```
defaults:
  # _posts
  - scope:
      path: ""
      type: posts
    values:
      author_profile: true

```

**Note:** To disable the author sidebar profile for a specific post or page, add `author_profile: false` to the YAML Front Matter instead.

The theme comes pre-built with a selection of links for the most common social media networks. These are all optional and can be [assigned in `_config.yml`](https://mmistakes.github.io/minimal-mistakes/docs/configuration/).

To add more links you’ll need to crack open [`_includes/author-profile-custom-links.html`](https://github.com/mmistakes/minimal-mistakes/blob/master/_includes/author-profile-custom-links.html) and add the appropriate `` markup shown below.

**Please note:** Links added here will appear after the ones in [`_includes/author-profile.html`](https://github.com/mmistakes/minimal-mistakes/blob/master/_includes/author-profile.html). If you’d like to change the order of appearance you’ll need to edit that file directly.

#### Social network link example

```
<li>
  <a href="https://whatever-social-network.com/username">
    <i class="fa fa-fw" aria-hidden="true"></i> Awesome Social Network
  </a>
</li>

```

To add a new link you’ll need three things:

1. Destination URL
2. [Font Awesome icon](http://fontawesome.io/icons/) (`fa-` class)
3. Label for the link

It’s up to you if you want to wrap it in a `{% if %} ... {% endif %}`conditional and add a variable to `_config.yml`. If you don’t plan to change it then hard-coding the string is perfectly acceptable.

Let’s run through how you’d add a new link that points to a Reddit profile. Starting with the three things from above:

1. `https://www.reddit.com/user/username`
2. [`fa-reddit`](http://fontawesome.io/icon/reddit/)
3. `Reddit`

And plug them into the appropriate locations:

```
<li>
  <a href="[1]">
    <i class="fa fa-fw [2]" aria-hidden="true"></i> [3]
  </a>
</li>

```

To end up with:

```
<li>
  <a href="https://www.reddit.com/user/username">
    <i class="fa fa-fw fa-reddit" aria-hidden="true"></i> Reddit
  </a>
</li>

```

![Reddit link in author profile](https://mmistakes.github.io/minimal-mistakes/assets/images/mm-author-profile-reddit-gs.png)

To add a touch of color to the default black (`#000`) icon a few more steps are necessary.

Start by copying [`_utilities.scss`](https://github.com/mmistakes/minimal-mistakes/blob/master/_sass/_utilities.scss) `/_sass`. Open it up to the icon section (it’s near the bottom) and nest a new class beneath `.social-icons` that matches the one used to declare the Font Awesome icon. In our case `.fa-reddit`.

Simply add a `color` declaration and the corresponding hex code.

```
.social-icons {
  
  .fa-reddit {
    color: #ff4500;
  }
}

```

![Reddit link in author profile with color](https://mmistakes.github.io/minimal-mistakes/assets/images/mm-author-profile-reddit-color.png)

**ProTip:** For bonus points you can add it as a Sass `$variable` that you set in [`_variables.scss`](https://github.com/mmistakes/minimal-mistakes/blob/master/_sass/_variables.scss) like the other [“brand” colors](http://brandcolors.net/). You’ll need to add this file to `/_sass/` as well if you’re using the Ruby Gem version of the theme.

**Please please please** don’t submit [pull requests](https://mmistakes.github.io/minimal-mistakes/docs/contributing/) adding in support for “missing” social media links. I’m trying to keep things down to the minimum (hence the theme’s name) and have no interest in merging such PRs ![:expressionless:](https://assets-cdn.github.com/images/icons/emoji/unicode/1f611.png).

### Custom Sidebar Content

Blocks of content can be added by using the following under `sidebar`:

| Name          | Description                              |
| ------------- | ---------------------------------------- |
| **title**     | Title or heading.                        |
| **image**     | Image path placed in `/images/` folder or an external URL. |
| **image_alt** | Alternate description for image.         |
| **text**      | Text. Markdown is allowed.               |

Multiple blocks can also be added by following the example below:

```
sidebar:
  - title: "Title"
    image: http://placehold.it/350x250
    image_alt: "image"
    text: "Some text here."
  - title: "Another Title"
    text: "More text here."

```

![custom sidebar content example](https://mmistakes.github.io/minimal-mistakes/assets/images/mm-custom-sidebar-example.jpg)Example of custom sidebar content added as YAML Front Matter.

**Note:** Custom sidebar content added to a post or page’s YAML Front Matter will appear below the author profile if enabled with `author_profile: true`.

### Custom Sidebar Navigation Menu

To create a sidebar menu[1](https://mmistakes.github.io/minimal-mistakes/docs/layouts/#fn:sidebar-menu) similar to the one found in the theme’s documentation pages you’ll need to modify a `_data` file and some YAML Front Matter.

![sidebar navigation example](https://mmistakes.github.io/minimal-mistakes/assets/images/mm-custom-sidebar-nav.jpg)Custom sidebar navigation menu example.

To start, add a new key to `_data/navigation.yml`. This will be referenced later in via YAML Front Matter so keep it short and memorable. In the case of the theme’s documentation menu I used `docs`.

**Sample sidebar menu links:**

```
docs:
  - title: Getting Started
    children:
      - title: "Quick-Start Guide"
        url: /docs/quick-start-guide/
      - title: "Structure"
        url: /docs/structure/
      - title: "Installation"
        url: /docs/installation/
      - title: "Upgrading"
        url: /docs/upgrading/

  - title: Customization
    children:
      - title: "Configuration"
        url: /docs/configuration/
      - title: "Navigation"
        url: /docs/navigation/
      - title: "UI Text"
        url: /docs/ui-text/
      - title: "Authors"
        url: /docs/authors/
      - title: "Layouts"
        url: /docs/layouts/

  - title: Content
    children:
      - title: "Working with Posts"
        url: /docs/posts/
      - title: "Working with Pages"
        url: /docs/pages/
      - title: "Working with Collections"
        url: /docs/collections/
      - title: "Helpers"
        url: /docs/helpers/
      - title: "Utility Classes"
        url: /docs/utility-classes/

  - title: Extras
    children:
      - title: "Stylesheets"
        url: /docs/stylesheets/
      - title: "JavaScript"
        url: /docs/javascript/

```

Now you can pull these links into any page by adding the following YAML Front Matter.

```
sidebar:
  nav: "docs"

```

**Note:** `nav: "docs"` references the `docs` key in `_data/navigation.yml` so make sure they match.

If you’re adding a sidebar navigation menu to several pages the use of Front Matter Defaults is a better option. You can define them in `_config.yml` to avoid adding it to every page or post.

**Sample sidebar nav default:**

```
defaults:
  # _docs
  - scope:
      path: ""
      type: docs
    values:
      sidebar:
        nav: "docs"

```

------

## Social Sharing Links

The `single` layout has an option to enable social links at the bottom of posts for sharing on Twitter, Facebook, Google+, and LinkedIn. Similar to the links found in the author sidebar, the theme ships with defaults for the most common social networks.

![default social share link buttons](https://mmistakes.github.io/minimal-mistakes/assets/images/mm-social-share-links-default.png)

To enable these links add `share: true` to a post or page’s YAML Front Matter or use a [default](https://jekyllrb.com/docs/configuration/#front-matter-defaults) in your `_config.yml` to apply more globally.

If you’d like to add, remove, or change the order of these default links you can do so by editing [`_includes/social-share.html`](https://github.com/mmistakes/minimal-mistakes/blob/master/_includes/social-share.html).

Let’s say you wanted to replace the Google+ button with a Reddit one. Simply replace the HTML with the following:

```
<a href="https://www.reddit.com/submit?url={{ page.url | absolute_url }}&title={{ page.title }}" class="btn" title="{{ site.data.ui-text[site.locale].share_on_label }} Reddit"><i class="fa fa-fw fa-reddit" aria-hidden="true"></i><span> Reddit</span></a>

```

The important parts to change are:

1. Share point URL *eg. `https://www.reddit.com/submit?url=`
2. Link `title`
3. [Font Awesome icon](http://fontawesome.io/icons/) (`fa-` class)
4. Link label

![Reddit social share link button](https://mmistakes.github.io/minimal-mistakes/assets/images/mm-social-share-links-reddit-gs.png)

To change the color of the button use one of the built in [utility classes](https://mmistakes.github.io/minimal-mistakes/docs/utility-classes/#buttons). Or you can create a new button class to match whatever color you want.

Under the `$social` color map in `assets/_scss/_buttons.scss` simply add a name (this will be appened to `btn--`) that matches the new button class. In our case `reddit` ~> `.btn--reddit`.

```
$social:
(facebook, $facebook-color),
(twitter, $twitter-color),
(google-plus, $google-plus-color),
(linkedin, $linkedin-color);
(reddit, #ff4500;)
```

**ProTip:** For bonus points you can add it as a Sass `$variable` that you set in `_variables.scss` like the other [“brand” colors](http://brandcolors.net/).

Add the new `.btn--reddit` class to the `[`](undefined) element from earlier, [compile `main.css`](https://mmistakes.github.io/minimal-mistakes/docs/stylesheets/) and away you go.

```
<a href="https://www.reddit.com/submit?url={{ page.url | absolute_url }}&title={{ page.title }}" class="btn btn--reddit" title="{{ site.data.ui-text[site.locale].share_on_label }} Reddit"><i class="fa fa-fw fa-reddit" aria-hidden="true"></i><span> Reddit</span></a>
```

![Reddit social share link button](https://mmistakes.github.io/minimal-mistakes/assets/images/mm-social-share-links-reddit-color.png)

1. Sidebar menu supports 1 level of nested links. [↩](https://mmistakes.github.io/minimal-mistakes/docs/layouts/#fnref:sidebar-menu)