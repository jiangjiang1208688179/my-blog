---
title: 浏览器的工作原理之html页面渲染
date: 2019-3-3 18:21:03
tags:
cover: https://github.com/jiangjiang1208688179/my-blog/tree/master/themes/hexo-theme-diaspora/source/img/awesome.jpg
---

 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;浏览器对于我们而言是再熟悉不过的了，但是你知道，当你在浏览器中输入一个URL，按回车键，到你看到展示出来的信息，这个过程中，浏览器到底做了什么呢?想要理解透彻这整个过程是比较复杂的，需要积累很多东西，那么我这里主要简单说一下，当浏览器拿到了html文件是怎样解析然后呈现给我们的，废话不多说，直接看下边。

 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在讲之前需要补充一点，就是html文件中一般都会有html标签、css、js脚本对吧，那么浏览器是按照什么方式来加载的呢？从上到下一一解析，遇到script标签会暂停页面代码解析（此处有一个暂停，如果不想因为加载js而影响页面加载速度呢，可以采用异步加载js的方式），先下载js代码然后解析执行，然后再往下加载解析HTML、css，所以为了不影响网页速度，js代码尽可能的放在代码的下边。

 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;好，言归正传，从访问URL，拿到HTML文件到看到网页呈现其实是比较简单的，主要有步骤：下载资源-->解析资源-->渲染-->计算-->显示

### 一、下载相应资源

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;当用户输入URL后，浏览器回向服务器发送请求，请求成功后，服务器会响应相应的html页面（html在解析的过程中会导入css、js、image等资源文件）

### 二、解析资源、渲染、计算、显示

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;HTML/svg会解析成dom tree,css会解析成css rule tree，这两种结合会生成render tree。当然，在解析HTML的时候除了会遇到css外，还会遇到js，遇到js就会下载解析执行，执行过程中会调用DOM API 和 CSSOM API，来改动dom tree 和 css rule tree。当渲染树（render tree）完成之后,就会进入layout，layout阶段是计算每个DOM元素最终在屏幕上显示的大小和位置（遍历顺序为从左至右，从上到下），这个阶段也会出现reflow(它主要是用来确定每个元素在屏幕上的几何属，性，需要大量计算每个元素的位置。在代码里每改变一个元素的几何属性，均会发生一次回流过程，比如说，改变元素 font-size，盒模型margin、border、padding、width等)。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;渲染引擎会遍历渲染树，由用户界面后端层将每个节点绘制出来，最后display出来，这个也是我们在网页上眼睛见到的最终效果

### 三、整个过程图解
https://github.com/jiangjiang1208688179/my-blog/tree/master/themes/hexo-theme-diaspora/source/img/browser-1.jpg
html页面渲染原理
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;这样看来是不是也是非常简单呢，这里讲的比较浅，但是希望能够对前端开发的朋友们一点点帮助。

