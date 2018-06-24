---
title: prism和animation舔砖加瓦
date: 2018-6-24 23:00:01
tags:
---
# 发现新大陆
今天打算看看主题里面的代码，在查看其引用的文件中，发现了他引用了prism.min.js和animate.min.css这个两个文件。于是我去查了下这两个东东的用途（⊙.⊙），发现是一个用来高亮代码的（感觉不错，以后可以贴代码了，新技能get），一个是常用css动画效果（魅力值+10的好东西），就立马开始用起来的 (..•˘_˘•..) 。
# Prism.js高亮插件
网页代码高亮的插件网上好像很多的，例如：SyntaxHighlighter ，Google Code Prettify和Highlight.js等等。公司项目里用的就是Highlight.js，不过好像用起来有点麻烦。
## 使用
Prism.js有着简单、小巧好用的优点。你需要先去[官网](https://prismjs.com/index.html)下载js和css文件，下载的时候支持自定义，勾选要支持的语言和主题可以减小文件的大小，然后在html中导入js和css文件。
```
<!DOCTYPE html>
<html>
<head>
    <link href="themes/prism.css" rel="stylesheet" />
</head>
<body>
    <script src="prism.js"></script>
</body>
</html>
```
如果要在html中高亮代码：
```
<pre class="lang-js"><code>p { color: red }</code></pre>
```
如果要在js中高亮代码：
```
Prism.highlightElement(element, async, callback)
```
element为有language-xxx的class。
# animotion css动画插件
Animate.css是一个有趣的，跨浏览器的css3动画库，[github地址](https://github.com/daneden/animate.css)。以及有一个[效果展示地址](https://daneden.github.io/animate.css/)，可以查看对比动画效果,对于我这种小白使用起来很方便。
## 使用
引入css文件
```
<head>
  <link rel="stylesheet" href="animate.min.css">
</head>
```
给div加上class
```
    <div class="animated bounceOutLeft"></div>
```
也可以等动画执行完毕后添加回调事件
```
    $('#yourElement').one('webkitAnimationEnd mozAnimationEnd MSAnimationEnd oanimationend animationend', doSomething);
```
# 小结
目前暂时就头像用了动画，后续还要加样式、改自定义样式；以及这个代码高亮也有点问题，我在markdown里面嵌入code标签后预览是好的，但是渲染出来不会换行，只能多个code标签才行，有点吐血。
只能等我有空再慢慢改咯  ╮(๑•́ ₃•̀๑)╭ 。