---
layout: post
title: 第一篇博客
description: "使用jekyll模板生成个人blog,并挂在github"
tags: [jekyll,github,markdown]
modified:   2015-08-12 10:18:38 +0800
share: false
comments: false
mathjax: false
image:
  
---


作为一名IT爱好者，也基本认定以后会投身到IT事业中，确实也应该需要有一个博客，可以记一些技术笔记供自己查阅。web技术我涉猎不够多，基本只是个入门级别，所以选择了jekyll模板+github+markdown来写博客。这第一篇博客就写写这个过程吧。

<!--more-->

## 安装本地Jekyll环境（windows）

windows 上安装还是挺繁琐的，大致分为以下几个步骤：

* 安装Ruby
* 安装Devkit
* 安装Jekyll
* 安装Pygments
* 启动Jekyll

### 安装Ruby

1. 在<http://rubyinstaller.org/downloads/>中的**RubyInstallers**下载相应的安装包，这次下的是`Ruby 2.2.2 (x64)`
2. 安装并配置好环境变量
3. 通过`ruby -v`来检查是否成功安装

### 安装Devkit

DevKit是一个在Windows 帮助简化安装及使用Ruby C/C++扩展如RDiscount和RedCloth的工具箱。

1. 仍然在<http://rubyinstaller.org/downloads/>中的**DEVELOPMENT KIT**中下载与Ruby对应的版本。版本一定要对应，不对应的话在安装jekyll时会出现问题
2. 安装解压到相应文件夹
3. 通过`cd`命令到该文件夹或者直接 在该文件夹打开命令行
4. 输入`ruby dk.rb init`初始化创建`config.yml`，并确保`config.yml`最后一行是Ruby目录
5. 通过`ruby dk.rb review`命令检测配置是否正确，最后通过`ruby dk.rb install`安装Devkit。
6. 通过`gem -v`来检查是否成功安装gem，gem可以用来安装各种包，包括jekyll

### 安装Jekyll

因为伟大的万里长城，Rubygems很难连接上，这也导致直接通过gem安装是件很困难的事，万幸的是国内已经有同步更新的镜像站，由淘宝提供：<http://ruby.taobao.org/>。

1. 把默认的官方源换成镜像源,并确保只有镜像源 

        ~ $ gem sources --remove https://rubygems.org/
        ~ $ gem sources -a https://ruby.taobao.org/
        ~ $ gem sources -l

2. 通过`gem install jekyll`命令安装，会安装许多相关的包，这需要一些时间

### 安装Pygments

Jekyll里默认的语法高亮插件是[Pygments](http://pygments.org)。它需要安装Python并在配置文件`_config.yml`里加入`highlighter: pygments`。

1. 在<http://www.python.org/download/>中下载适合的安装包并安装，尽量选择Python 2版本，我使用Python 3时不能正常使用高亮插件，不知道哪里出了问题
2. 配置环境变量，通过`python -v`检测是否成功安装   
3. 安装"Easy Install"，跟gem作用类似，<https://pypi.python.org/pypi/setuptools#installation-instructions>是详细的安装指南。
4. win7环境下载[ez_setup.py](http://pan.baidu.com/s/1AuYey)，并通过命令`python ez_setup.py`运行次文件。
5. 把python根目录中的Scripts目录加入环境变量，依然通过`easy_install --version`检查是否成功。
6. 通过`easy_install Pygments`命令安装
7. jekyll中也要安装，通过`gem install pygments.rb`命令安装

### 启动Jekyll

1. 通过`jekyll new blog`命令创建新的模板或者直接找别人已经做好的模板，我是在<http://jekyllthemes.org/>中找的一个模板，改了一些css。以后熟悉了可以定制更个性化的东西，可以在<http://jekyll.bootcss.com/>查看相关的中文文档。
2. 在blog根目录运行`jekyll serve`启动jekyll serve，这样就可以通过<http://localhost:4000/>本地看效果了，并且是可以实时监测变化的。

## 建立Github博客

使用Github不用负担域名和空间的费用，很适合用来写个人博客。

1. 新建名为`yourusername.github.io`的Repository，其中的`yourusername`是你的Github用户名。这样就可以直接通过`http://yourusername.github.io/`访问博客了
2. Github是使用Jekyll解析该Repository，所以我们可以直接把刚才在本地的Jekyll博客push到master分支，不出意外这时候我们的博客就建立成功了

## 使用markdown写博客

在Jekyll中，每篇博客都是一个独立的在`_post`中以`.md`或者`.markdown`为后缀的文件，可以通过Ruby脚本快速生成md文件。使用[markdown](http://wowubuntu.com/markdown/)书写。这里记录一些常用基本语法以便可以随时查看。

1. 两种标题语法
    类Setext形式，利用`=`（最高阶标题）和`-`（第二阶标题）：
    
        第一级标题
        ================
        
        第二级标题
        ----------------
    
    类Atx形式，利用行首插入1到6个`#`，对应相应级别的标题：
            
        # 第一级标题
        
        ### 第三级标题

2. 列表
    无序列表使用`*`、`-`和`+`后紧跟一个空格做标记，这三个符号作用是相同的。有序列表使用数字紧接英文句点作为标记，序号不是根据所写的数字而是自动排序：

        * A
        * B
        * C
    
    和

        1. A
        2. B
        3. C
    
    列表项可以有多个段落或者其他区块，但需要靠缩进来表示是在当前列表项中，这样就可以做到列表的嵌套：

    靠四个空格或一个制表符来缩进

        1.  第一段
        
            第二段

        2.  另一个列表项

    嵌套列表或者其他区块（引用、代码块等）

        1. ol level
            1. li level
            2. li level
        2. ol level

3. 区块引用
    区块引用的标记为`>`，在每行前加上`>`代表区块引用，也允许在整个段落首行前加上`>`：

        > blockquote 区块引用
        > blockquote 区块引用
    
    区块引用也可以嵌套使用，包括嵌套其他语法：

        > blockquote 区块引用
        > 
        >> 嵌套blockquote 区块引用
        > 
        > ## 标题
        > 
        > 1. 列表项
        > 2. 列表项
    
4. 代码区块
    代码区块简单的通过四个空格或者一个制表符缩进来表示，代码块会被`pre`和`code`标签包裹：

        普通段落

            代码块

    GFM语法还允许包裹型的代码块：

        ~~~ language
        代码块
        ~~~

    小段的行内代码可以通过反引号`` ` ``包裹:

        `代码`

5. 强调
    Markdown使用`*`和`_`来标记强调，被一个`*`或`_`包裹的会被转换为`<em>`标签包裹，两个则会被转换为`<strong>`标签包裹。

6. 链接
    Markdown支持两种形式，*行内式*和*参考式*。 

    *行内式*[方括号]标记链接文字，后面紧跟圆括号并插入链接，链接后还可以用双引号加上title文字，如果链接即为链接文字，也可简单在尖括号中插入链接：

        [text](http://example.com/ "title")

        <http://example.com/>

    *参考式*在链接文字方括号后再加一个方括号，并在第二个方括号中填入辨识标记，并在文章任意处把标记的联机内容定义出来：

        [text][id]

        [id]: http://example.com/ "title"



7. 图片
    Markdown标记图片语法与链接类似，也分为*行内式*和*参考式*。基本就是在链接的语法前面加一个`!`，链接改为图片的链接或者本地相对路径：

        ![img](images/img.jpg "title")

        ![img][id]

        [id]：images/img.jpg "title"

    基本的语法没有办法定义大小，有需要的话可以使用标签定义。

8. 分割线
    可以在一行中用三个`*`或者`-`表示分割线:

        ---
        ----------
        * * * 
        ******
         
9. 表格
    Markdown基本语法中没有表格，扩展语法可以这样表示表格：

        |   默认   |   中间对齐   |   右对齐  |
        |----------|:------------:|----------:|
        |   1  1   |   2  1       |   3  1    |
        |   2  1   |   2  2       |   3  2    |
        |   3  1   |   3  2       |   3  3    |


8. 转义
    Markdown转义字符为反斜杠`\`，可以再前面加上`\`来输入一些有特殊意义的符号：

        \   反斜线
        `   反引号
        *   星号
        _   底线
        {}  花括号
        []  方括号
        ()  括弧
        #   井字号
        -   加号
        *   减号
        .   英文句点
        !   惊叹号

## 遇到的问题

*   使用`gem isntall`安装时不能正常安装，出现time out。

    官方源被墙，换成淘宝的镜像源即可。
*   安装Jekyll时，某些包安装不正常，报错
   
        ERROR: Failed to build gem native extension

    导致不能成功安装Jeklly。

    Ruby版本安的是32位，而DevKit却是64位，版本的不匹配导致某些包不能安装DevKit中的本地扩展，统一为64位即可。
*   启动jekyll serve的时候，不能导入`.sass`文件，报错

        Syntax error: File to import not found or unreadable

    目录包含中文，可能ruby不能正常识别，改为全英文即可。
*   启动jekyll serve的时候，博客中使用高亮语句会报错
    
        undefined method `[]` for nil:NilClass
    
    高亮插件Pygments是Python语言写的，怀疑是Ptyhon的问题，最终发现把Python版本由3改为2就可以正常使用高亮语句了，原因不明。
*   代码块不能正常显示。

    MarkDown解析器kramdown默认使用代码高亮coderay，可是Github却不支持很多插件。只好把解析器换成redcarpet，并修改相应css。
*   模板中的估计阅读时间不正确。

    liquid中的number_of_words变量只记录英文单词，造成估计阅读时间不正确。因为不清楚怎么通过liquid统计汉字，直接去掉了。

*   脚本`rake post`生成新文章失败。

    查看`Rakefile`脚本文件发现，task命令为`new_post`，并且需要在`Gemfile`文件中导入脚本文件中用到的包。

*   图片Markdown语法失效。

    不要用汉字标点，用英文标点`!`。



    








    
