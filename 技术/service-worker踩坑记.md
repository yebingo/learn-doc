# service worker踩坑记

## 引言
> Service worker是一个在浏览器后台运行的脚本，与网页不相干，专注于那些不需要网页或用户互动就能完成的功能。它目前主要用于操作离线缓存。最近在使用它的过程碰到一个巨坑，遂分享出来，防止有同学再次掉入😉

## 关于service worker
未听过service worker可以先看下以下几篇文章了解下：

[谷歌开发者文档](https://developers.google.com/web/fundamentals/primers/service-workers/?hl=zh-cn)

[阮一峰博客](http://javascript.ruanyifeng.com/htmlapi/webworker.html#toc14)

## 踩坑起因
项目需要改一处文案，但发现无论如何修改上线都无法生效(`连续上线四次均未生效!!`)，遂开始排查

## 排查过程
1、先看项目引用的资源缓存，发现使用了`service-worker`来管理项目，便想找项目中的`service-worker`代码看是否出现异常

2、经过一番寻找，发现项目中使用的是一个`webpack`插件，名称为：`sw-precache-webpack-plugin`，如下图：

<img src="https://www.superbed.cn/pic/5bee94969dc6d61ad66ee762" width="800px">

便想到github上找到此项目，看插件的配置文档，另再看下issue中有没有同学碰到类似的缓存不更新的问题

3、然而，github上的介绍非常的简单，并且api也并没有列全。再看下issue，和自己的问题边都粘不上。无奈，看来只能靠自己了

4、首先蹦出的想法是看下webpack插件打包出的`service-worker.js`文件，看下能不能从源码找突破口

5、然后看到的打包出的文件那一刹那我是绝望，代码不仅仅经过压缩，而且逻辑相当复杂，即便格式化要理解其中的逻辑也有一定的成本，各位看官可以看下图自行体会下：

<img src="https://www.superbed.cn/pic/5bee95a79dc6d61ad66ee764" width="800px">

6、万念俱灰之下，只好将该项目下的`service-worker.js`和另一个也使用`service-worker`但能正常更新的项目下`service-worker.js`进行对比，这不对比不要紧，一对比确实发现了区别：

能正常更新service-worker.js文件是这样的：

<img src="https://www.superbed.cn/pic/5bee98b69dc6d61ad66ee76e" width="800px">

而无法更新缓存的service-worker.js文件是这样的：

<img src="https://www.superbed.cn/pic/5bee98979dc6d61ad66ee76d" width="800px">

相信眼睛锐利的小伙伴的已经看出二者的区别了，就是无法更新缓存的`service-worker.js文件配置里没有hash！`

遂看打包出的dist文件夹下的文件：

<img src="https://www.superbed.cn/pic/5bee998c9dc6d61ad66ee773" width="400px">

果然都是没有`hash`，难道是这个问题是因为它引起的？

于是自我推论开始：

以往我们的http请求缓存步骤：

<img src="https://www.superbed.cn/pic/5bf13cc5c4ff9e24bf0ee0f7" width="800px">

让我们来看看原先service worker缓存更新的步骤：

<img src="https://www.superbed.cn/pic/5bf219c4c4ff9e24a0d68757" width="1000px">

原本我看到这张图，会以为service worker会全权接管页面资源的缓存，而完全忽视http协议中的强缓存和协商缓存，然而我注意到了这个步骤：

<img src="https://www.superbed.cn/pic/5bf21a3dc4ff9e24bf0ee189" width="1000px">

service worker自身去fetch资源时，会不会也受到http协议缓存的影响，从而实际的步骤是这样的：

<img src="https://www.superbed.cn/pic/5bf21c1ec4ff9e24bf0ee1a3" width="1000px">

是不是想到了`双重缓存？`

上网一搜，果然证实了我的想法：

<img src="https://www.superbed.cn/pic/5bf17115c4ff9e24bf0ee11c" width="800px">

也就是说如果你要使用service worker，有两个选择：

1、去除所有请求资源的http缓存头（包括强缓存和协商缓存），如此一来，service worker在fetch资源时便不会受到http缓存的影响，可以及时更新资源；

2、保留原有http缓存头，修改一个文件后更改更改文件名（如前文提到的更改文件名中的hash），如此http也会去请求新的资源，service worker也可以fetch到新的资源。

## 总结
本次所踩的坑是由于随意更改webpack配置引起，所以以后若是从网上下的项目模板，不要随意更改它webpack配置。如若非要更改，需在配置中或git commit上写好备注，这样若出问题，对排查问题会很有帮助。



