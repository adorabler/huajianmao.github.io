---
title: "Github Pages博客搭建过程记录"
tags:
  - Step by step
---

原来的博客许久没有打理了，想着重新在[Github Pages](https://github.io)上架个博客系统，以便对自己的一些想法、工作等有个记录。

Github Pages已经被用的很多了，它支持[Jekyll](https://jekyllrb.com/)作为后台将用户基于Markdown的博文等转换为静态页面。既然已经被广泛使用了，有许多的大牛已经为Github Pages提供了既美观又功能强大的模板。[Jekyll Themes](http://jekyllthemes.org/)上列出了许多Jekyll主题模板，并且基本上都可以直接下载使用。[Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/)是这些众多主题模板中，我认为比较漂亮并且功能强大的模板之一。因此，便选定它作为本博客的模板了。本文所有的设置及配置等都是基于Minimal Mistakes完成。

除了博客功能以外，我还需要的一个功能是托管我的简历信息的页面。虽然Minimal Mistakes整体已经挺漂亮了，但是，从简历的角度来看，它似乎并不太合适将简历漂亮的显示出来。所以在Jekyll Themes上我又找了另外一个比较漂亮的面向简历的Jekyll模板[Online CV](http://jekyllthemes.org/themes/online-cv/)。这个模板按简历的布局将页面展示出来。还是比较适合做简历页面使用的。

综上，我的博客主要是基于[Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/)以及[Online CV](http://jekyllthemes.org/themes/online-cv/)这两个Jekyll模板进行整合，过程当中略微做了一些小改动。

其实，不管Minimal Mistakes还是Online CV的搭建步骤已经写的非常详细了。本篇记录仅是为自己记录一下整个过程，以免下次如果有需要重新搭的时候还要看完整个文档才能构建。如果本文恰好能帮到您，那最好不过了！ :) 


{% include toc %}

## 搭建基础框架
Minimal Mistakes的主页就是基于Github Pages运行的，因此，想要搭建起一个可用的Blog系统，只要从它的[github repo](https://github.com/mmistakes/minimal-mistakes)拷贝或者[fork](https://github.com/mmistakes/minimal-mistakes#fork-destination-box)一份即可。Minimal Mistakes的[Quick-Start Guide](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/)给了更详细的过程。本博客仅记录我使用到的步骤。

原本我是从Minimal Mistakes上fork的一份代码，但后来发现我自己的commit和原作者的commits是混合在一起的，特别是想要看自己博客的Graphs里的Network的时候，Github会提醒

 > **Couldn't load network graph.**
 Too many forks to display.

所以，为了避免这个问题，我最终是将Minimal Mistakes的代码[下载](https://github.com/mmistakes/minimal-mistakes/archive/master.zip)下来再提交到自己的github中的。另外，这个方法也可以使我们的博客github库变得稍微小一些。

### 创建一个Github Page的Repo
[Github Pages的主页](https://pages.github.com/)给出了详细的创建过程。直接参考它即可。

 1. Create a repository：用我自己的帐号登录进去后，新建**huajianmao.github.io**
 2. Set it public: 将**huajianmao.github.io**库设置为Public
 3. Clone it to local: `git clone git clone https://github.com/huajianmao/huajianmao.github.io`

### Copy files from Minimal Mistakes
 1. [下载](https://github.com/mmistakes/minimal-mistakes/archive/master.zip)Minimal Mistakes代码包
 2. 将包的内容解压到clone的库目录中
 3. 根据Minimal Mistake的[Quick Start](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/)的说明，删除多余的文件：`rm -r .editorconfig .gitattributes .github docs test CHANGELOG.md minimal-mistakes-jekyll.gemspec README.md screenshot-layouts.png screenshot.png`
 4. commit添加的文件，并push到github中：`git commit -a && git push -u origin master`

## 配置Minimal Mistakes
在上面的步骤完成后，如果一切顺利的话，那么在浏览器里打开username.github.io应该就能看到一个什么内容也没有的页面。
![Page after first commit]({{site.url}}{{site.baseurl}}/assets/images/after-first-commit.jpg)

### 博客基础信息配置
Jekyll的配置文件为`_config.yml`，该文件可以对大部分的系统信息进行配置。
这个过程中，我主要对以下参数进行了设置，需要将`profile.png`放到`assets/images`目录中：

``` yaml
locale                   : "zh_CN"
title                    : "HJ's Homepage"
title_separator          : "<"
name                     : "Huajian Mao"
description              : "Log my life."
repository               : huajianmao/huajianmao.github.io

# Site Author
author:
  name             : "Huajian Mao"
  avatar           : /assets/images/profile.png
  bio              : "System Architect"
  location         : "Beijing, China"
  email            : huajianmao@gmail.com
  github           : huajianmao
  linkedin         : huajianmao
  weibo            : huajianmao

timezone: Asia/Shanghai
```

### 配置系统的favicon
默认模板中并没有放置favicon，所以浏览器tab栏里显示的是好丑的一个file图标。
为了能够调整favicon，先在网上找了个可以将图片转换为favicon的[网站](http://www.favicon-generator.org/)，然后将自己的一张图片转换成了一个favicon.ico，并将favicon.ico放置在`assets/images/favicon.ico`，同时在`_include/head/custom.html`文件中添加一行：

``` html
<link rel="shortcut icon" href="{{site.baseurl}}/assets/images/favicon.ico">
```
在完成这一步并commit后，便可以看到浏览器的tab栏中的favicon变成了自己的图片了。


### 配置导航栏
Jekyll的导航栏数据主要在`_data/navigation.yml`中指定。
我主要是希望自己能在本博客中，记录一些平时的想法（Blog），研究的一些内容(Research)，平时的一些项目(Projects)，经常使用的一些工具的配置及使用心得(Tools)，以及我的个人简历(About)。
因此，我将我的`_data/navigation.yml`做了如下修改。

``` yaml
main:
  - title: "Blog"
    url: /
  - title: "Research"
    url: /research/
  - title: "Projects"
    url: /projects/
  - title: "Tools"
    url: /tools/
  - title: "About"
    url: /cv/
```

其中，`title`是在导航栏中显示的条目名称，而`url`则是导航内容对应的地址。
但如果直接使用的话，github会告诉你说：

 > `**404** File not found`

产生这个问题的原因是，github pages不知道`/research/`或者`/projects/`或者`/cv/`等这些地址对应的访问内容放在哪里。
因此，我们需要对这些地址进行相应的配置。

#### 设置配置文件

 - 修改`_config.yml`文件

   ``` yaml
   # Collections
   collections:
     tools:
       output: true
       permalink: /:collection/:path/
   
   # Defaults
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
   
     # _pages
     - scope:
         path: ""
         type: pages
       values:
         layout: single
         author_profile: true
   
     - scope:
         path: ""
         type: tools
       value:
         layout: single
         author_profile: true
         share: true
         comments: false
   ```

#### 添加所需的文件
创建`_pages`目录，并在该目录下创建相应的文件：

 - `_pages/research.md`


   ``` markdown
   ---
   layout: archive
   title: "Research"
   permalink: /research/
   author_profile: true
   ---

   ## Coming soon...
   ```

 - `_pages/projects.md`

   ``` markdown
   ---
   layout: archive
   title: "Projects"
   permalink: /projects/
   author_profile: true
   ---

   ## Coming soon...
   ```

 - `_pages/tool-archive.md`

   ``` markdown
   ---
   layout: archive
   permalink: /tools/
   title: "Tools"
   author_profile: true
   ---

   Coming soon...
   ```

文件内容中的`layout`指这个页面应该用`_layout`目录中的那个页面布局，`permalink`指得是给这个页面赋予一个什么永久的URL地址，该地址和`_data/navigation.yml`中的各`url`字段对应。需要注意的是，这里的permalink是源，也就是说，navigation中的url是有这些文件中的`permalink`字段决定的。


## 添加并配置Online CV
前面提到，Minimal Mistakes的页面布局直接拿来做简历模板的话，感觉不够美观。
在网上查找后，[Online CV](http://jekyllthemes.org/themes/online-cv/)相对来说还是挺不错的，配色、布局等都挺好。
所以考虑着将Online CV整合到Minimal Mistake这个模板中。

### 将Online CV融合进Minimal Mista
本着偷懒的原则，怎么快怎么来，基本上是无脑将Online CV中的文件搬到了Minimal Mistakes中。
**FIXME**

 1. [下载](https://github.com/sharu725/online-cv/archive/master.zip)Online CV的代码库。
 2. 将代码库中的`index.html`放入到github pages代码库（例如，我这里是刚才建立的huajianmao.github.io）的根目录下，但是由于根目录下已经有一个同名的存在，所以，我将Online CV的`index.html`文件搬过来的时候将它重命名为了`cv.html`。 [^cv-navigation]
 3. 将`_layouts/default.html`文件拷贝为github pages代码库的`_layouts/cv.html`。这里相当于在Minimal Mistakes中新建立了一个简历模板布局。同时需要修改`cv.html`文件中对布局的引用，将`layout`字段的`default`改为`cv`。
 4. 将`_includes`目录拷贝为github pages代码库的`_includes/cv`目录。
 5. 由于我们是将Online CV的文件合并到了不同的目录中，我们需要对Online CV代码中的include路径进行相应调整。通过`grep include _config.yml _layouts _includes -r`，便可以直到哪些文件需要进行目录调整。[^include-dir-adjust]
 6. 将Online CV的assets目录中的各个子目录分别移动倒相应的目录中
 7. 修改目录变动引起的所有文件变更。
 8. 整合`_config.yml`内容
 9. 将Online CV中的所有对配置文件的变量引用合并倒Minimal Mistakes中的对相应字段的引用。

[^cv-navigation]: `_data/navigation.yml`中的About项设定的`url`字段就是由这里将`cv.html`放置在根目录下决定的，如果我们将它的名字命名为`resume.html`的话，那么`_data/navigation.yml`中的相应url也需要改为`resume`。
[^include-dir-adjust]: 我们主要调整了[`_layouts/cv.html`](https://github.com/huajianmao/huajianmao.github.io/blob/master/_layouts/cv.html)和[`_includes/cv/sidebar.html`](https://github.com/huajianmao/huajianmao.github.io/blob/master/_includes/cv/sidebar.html)两个文件中的include内容。

### Online CV页面微调整

#### 添加页面导航按钮

#### 添加PDF版本下载按钮

#### 修改footer内容


## 开始写博客

### 调整页面内容


## 配置评论模块

### 评论模块原理

### Staticman配置

Step 1. Add Staticman to your repository
connect your page to staticman.net
Step 2. Create a configuration file

