---
title: 尝尝自动部署的甜头
date: 2018-06-28 22:44:18
tags:
---
# 肥宅都懒？
之前我的博客都是源代码和静态文件共存的，即每次改完代码和写完markdown后，都要hexo clean和hexo g生成更新public目录下的静态文件，然后将静态文件拷贝到最外层目录下，然后github pages就读到了我的index页面。<br>
当我改了几次代码后，发现每次都要重复的操作真的有点小烦(我是在vscode里面写代码，特别是每次要提交还要打开资源管理器  ( (￣^￣) )，然后就考虑自动部署这个好东西了。
# 偷懒不好偷啊
我发现源代码和静态文件放在一起真的不好管理，于是分开建了两个分支master存放生成的静态文件，另外一个hexo分支用来存放开发的源代码。无奈的是平时git真的用的不多，连怎么建分支都不会 o(︶︿︶)o，又花了一个小晚上学习了下。[与水友共勉](https://git-scm.com/book/zh/v2)<br>
搞完了目录结构了后想了下我的需求就是本地hexo分支push的时候，同时执行hexo clean和hexo g，然后将public目录下文件拷贝到master分支下覆盖，然后再执行push到master分支。
其实是比较简单的，一开始打算去找个自动化构建的工具，我想github上应该也支持这些工具插件的。但是后面想到之前学习的时候看到了git hooks刚好能实现我的需求，所以说
<a href="/deps/partial/imgs/article_link/blog-devops/study_happy.png" data-fancybox="images">
![找不到图片了^~~](/deps/partial/imgs/article_link/blog-devops/study_happy.png "学习使我快乐")
</a>
首先我们进入本地clone的repository下，windows设置下查看隐藏文件目录，其中有个.git目录，进入.git/hooks/，里面有一些githooks的样例
<a href="/deps/partial/imgs/article_link/blog-devops/githooks.png" data-fancybox="images">
![找不到图片了^~~](/deps/partial/imgs/article_link/blog-devops/githooks.png "githooks")
</a>
<a href="/deps/partial/imgs/article_link/blog-devops/githook_sample.png" data-fancybox="images">
![找不到图片了^~~](/deps/partial/imgs/article_link/blog-devops/githook_sample.png "githook_sample")
</a>
其中.sample结尾的不会在git命令执行中触发，你可以修改其中的逻辑并删除.sample后缀，然后就可以在git命令时触发这些脚本。具体可以参考[git钩子](https://git-scm.com/book/zh/v2/%E8%87%AA%E5%AE%9A%E4%B9%89-Git-Git-%E9%92%A9%E5%AD%90)<br>
# 又中招了
我一开始在本地用cmd命令写了类似的脚本，然后执行后没有问题，然后把命令拷贝到了pre-push中，然后在hexo分支下执行了git push操作，然而一直报一个无效的参数数量的错误。<br>
经我跟踪是我执行的xcopy命令即将生成的静态文件拷贝到master分支下报错了，但是我在cmd命令下没有问题，而且我直接执行xcopy也不会提示command not found，证明是有这个命令的。然后我就想不通了 (⊙_⊙)?<br>
摇头晃脑的时候发现文件首行写的是#!/bin/bash，我一想这不是shell脚本吗，不应该用的是cp命令吗？于是我把xcopy改成了cp，再push，果然就可以了。但是linux下不是应该没有这个命令的吗？我想到了这个命令的运行的环境是gitbash，我安装的是gitbash for windows，它是兼容了shell和windows命令的一个仿真环境，肯定是有一些特殊之处的 (｡￫‿￩｡)<br>
# 杂谈
最近网易有个游戏逆水寒要内测开服了，29号才开服今天去体验了下捏脸，感觉还不错，最近也get图片了
<a href="/deps/partial/imgs/article_link/blog-devops/nishuihan_nielian.png" data-fancybox="images">
![找不到图片了^~~](/deps/partial/imgs/article_link/blog-devops/nishuihan_nielian.png "这是我捏的哦")
</a>