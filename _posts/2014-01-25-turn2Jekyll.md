---
layout: post
title:  "从wp搬家到Jekyll，认识markdown和pandoc"
date:   2014-01-25 10:15:26
categories: IT
tags: Jekyll markdown pandoc LaTeX
---

# 比较Jekyll和WordPress

自从用上Mac后，对Unix纯文本概念越来越喜欢，纯文本简洁，小巧，安全，只需要设定字符编码就可以，而现在通用UTF-8可以兼容几乎任何文字符号，十分方便。

而从某种意义上讲，任何我们所用到的计算机二进制文件和程序，包括我们看到的富文本，都是从纯文本编译而成，而所见即所得的软件如*wordpress*，*word*是软件帮我们做这样的事，故我们看不到源代码，当然也不需要编译过程，也就缺少了灵活小巧安全。

使用WordPress感觉不太好的有

- 写文章管理站点需要登录站点，即使用发布程序，也不能方便在本地保存修改已经发布的文章
- 程序臃肿，备份需要插件，服务器跑起来，打开网页较慢，这也是动态页面的弱势

总的来说，就是不够轻量，不够灵活，离线能力不强，不能分秒转移站点。只是比较傻瓜化，所见即所得，与Jekyll相比就如同word之于$\LaTeX$(其实$\LaTeX$也不够轻量，后面有讨论)。

# 认识Jekyll

我在看技术牛人binix的博客时看了一下博客引擎，看到powered by Jekyll。便搜寻了Jekyll的信息，认识了markdown这个语言，发现Jekyll是一个静态站点生成脚本，将以markdown语言写的文章用一定的解释器编译成HTML文件生成站点，这个过程可以在github上驱动，也可以自己编译后用rsync等方式上传站点到自己的vps，相当于服务器的站点只是我离线源代码的一个镜像，实在太灵活了。

$$markdown code \rightarrow markdown parser \rightarrow HTML site$$

对于markdown的解释器，由于我希望能够显示$\LaTeX$数学公式，所以不能不用原版的markdown，而要用markdown扩展语言，扩展语言主要有multimarkdown与pandoc markdown，pandoc这个软件异常强大，不止能把markdown转换为HTML，还能在HTML，markdown，$\LaTeX$等代码之间互转，还能将代码转为docx等等，是转换的瑞士军刀。pandoc就不止用于Jekyll，以后写文章都可以从直观的markdown出发，转换为$\LaTeX$，进行排版微调，再输出PDF，pandoc还有个功能是自定义$\LaTeX$的模板，可以加入论文模板，中文环境等。

$$markdown \rightarrow pandoc \rightarrow \LaTeX \rightarrow docx/PDF$$

# Jekyll配置

Jekyll使用pandoc需要一点hack，具体可以看[这里][1]

在_config里解释器改为pandoc，下面加入

```yaml
markdown: pandoc
pandoc:
	extension: [mathjax, standalone, smart]
```

里面可以加入pandoc的任何命令选项

# text editor

Mac下一直用textwrangler，但它的中文换行一直有问题，写代码还好，写文章就不太舒服，了解了下sublime text，换行正常，左边有文件夹导航功能，跨三大平台，推荐使用，另外需要加入一个代码高亮[插件][2]，不然markdown代码高亮不太明显。不过textwrangler可以用applescript，可以一键转换markdown到PDF，最好两者一起使用

Windows下就用sublime text和notepad++，iOS下textastic非常不错，运行速度快，可以与sftp同步，这篇文章就用textastic在iPhone4下完成

[1]: http://dannpu.com/blog/2013/08/02/new-post/
[2]: /assets/Made-of-Code.tmTheme