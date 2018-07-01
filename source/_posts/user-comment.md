---
title: gitment使用
date: 2018-07-02 23:50:22
tags:
---
## 简短介绍
gitment是[imsun](https://github.com/imsun/gitment)开源的一款基于github issues的评论系统，因为不需要任何后端，所以尤为适合那些使用hexo搭建在github pages上的静态博客或项目。
虽然只能使用github账号，但是可以进行评论、点赞操作，而且支持markdown格式，功能比较丰富。demo例子在[Gitment](https://imsun.github.io/gitment/)。
## 基本使用
看到官网的文档，使用起来还算比较方便的，先去注册一个github的OAuth Apps，把生成的clientId和clientSecret放到gitment生成的对象里，然后再填写githubId和储存评论的repo。最后初始化生成评论的dom元素就ok了。
## 小问题
目前每个页面都要进行gitment的初始化和渲染dom元素，后续作者可能会推出全局初始化。
我在开发的时候页面访问的是localhost:4000，但是部署后访问的是https://leepcell.xyz ，而我OAuth Apps中Authorization callback URL填写的是部署后的url，所以我在本地点击评论的login按钮时返回的是[这一大长串的东东](https://leepcell.xyz/?error=redirect_uri_mismatch&error_description=The+redirect_uri+MUST+match+the+registered+callback+URL+for+this+application.&error_uri=https%3A%2F%2Fdeveloper.github.com%2Fapps%2Fmanaging-oauth-apps%2Ftroubleshooting-authorization-request-errors%2F%23redirect-uri-mismatch) ，看了一下大致是验证错误。
我明确自己配置没有问题，认为估计是当前url和验证返回url不一样导致的，于是就直接部署了。发现果然没有问题了，在此mark一下  ┐(・o・)┌ 