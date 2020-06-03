---
layout:     post
title:      "一个曲折的过程为了给首页新增一个文字显示特效"
subtitle:   "Nothing is easy."
date:       2019-05-05 10:24:43 +0800
author:     "ZHANG Tao"
header-img: "img/post-2019-05-05-ityped-header.jpg"
tags:
- web
- github-pages
- js
- ityped
---

偶然在一个[博客](<https://athityakumar.github.io/>)上看到了一个特别的文字显示特效，文字就如同是键盘敲出来一样逐个显示出来，一时激起了我的兴趣。想知道是怎么实现的，看能不能弄到我的博客上，下图，就是我最后弄出来的效果。

![首页文字效果](/img/post-2019-05-05-ityped-homepage.gif)

搜索 ***web页面上文字像是键盘敲出来的一样逐个显示出来？***Google & 百度都还是不错的，总能给人一些想要的答案。只是坑都还在后面。

最先尝试过，[typetype](<http://www.jq22.com/jquery-info504>)，让人不满意的是生成的框允许用户也敲入文字（[演示](<http://www.jq22.com/yanshi504>)），不知道有没有相关参数能够控制这个设为FALSE之类，但也没见到官方文档。

后来尝试的很多的是[typed.js](<https://mattboldt.com/demos/typed-js/>)，这个给的说明文档，演示Demo，而且能够实现比较复杂的显示效果，甚至实例网站都有，看起来简直完美到极致。结果后来才觉得是好大的一个坑啊。归结原因还是在于自己菜。

我要将这个放在首页，我猜应该是jekyll的`includes/head.html'` 里面，为了确定位置，在`_includes/head.html`里面添加文字，然后通过博客首页来看添加的文字显示在了哪儿，结果并不是，于是最终定位到了，原来是在 `_includes/intro-header.html`当中。

在这个过程当中，终于用上了jekyll的本地预览调试，这个黄轩博主在[博客模板文档](https://github.com/Huxpro/huxpro.github.io/blob/master/README.zh.md#%E5%85%B3%E4%BA%8E%E6%94%B6%E5%88%B0page-build-warning%E7%9A%84email)当中提到过，之前一直觉得安装了也不大能用上，而如今就很需要这个了，否则每次修改了之后都`git push`一次，那也太繁琐了。另外jekyll安装使用会存在bug，附上参考教程【[安装教程](<https://blog.csdn.net/mouday/article/details/79300135>)，[Dependency Error解决教程](<https://blog.csdn.net/mouday/article/details/79300135>)，[permission denied解决教程](<https://blog.csdn.net/mouday/article/details/79300135>)】。

而之后就是利用[typed.js](<https://mattboldt.com/demos/typed-js/>) 提供的[实例](<https://github.com/jessejohnson/jessejohnson.github.io>)进行改造了，去掉没有用处的内容，以最精简版往我的博客`_includes/intro-header.html`上进行合并，然后bug就出现了（*当时有bug忘了截图，只能复现了一遍*），如图。

![bug-1](/img/post-2019-05-05-ityped-error-1.png)



解决这个bug可是累死人，查看了Google & 百度所有检索结果，按照说的方法尝试了都不行，有人说是jquery.js库重复了，于是讲对应替换为jekyll原本的jquery.js库，于是新的问题就出现了。

![bug-2](/img/post-2019-05-05-ityped-error-2.png)

好吧，解决不了，留下了不学无术的泪。

而再然后，很巧合竟然找到了解决方案，在github搜typed相关的项目的时候，看到了[ityped](<https://github.com/luisvinicius167/ityped>)，描述上说的是最大的优点在于无依赖，一个最简单的实例：

```html
  <div id="app">
    <span id="ityped"></span>
  </div>
  <script src="https://unpkg.com/ityped@1.0.2"></script>
  <script>
    ityped.init(document.querySelector("#ityped"), {
      showCursor: false,
      strings: ['Very nice project!', 'Yeah!', 'Shure, awesome!']
    })
    ityped.init("#placeholder", {
      placeholder: true,
      showCursor: false
    })
  </script>
```

当然也存在缺点，显示效果就是对于数组当中的元素以键盘输入效果显示，至于一些回退之类的效果就没有的，以及显示在一行上，数组当中会将换行符</br>之类的变为普通字符。在[issues #21](<https://github.com/luisvinicius167/ityped/issues/21>) 有人提出来了这个问题，但尚且还未能实现该类功能。

![issues](/img/post-2019-05-05-ityped-issues.png)

但是，还要什么自行车啊。

而后又出现了新的问题，在添加之后，原本仅仅想让显示在首页的那段文字却在About、Archive页面以同样的内容同样的效果显示出来了，这不得不让我来现学现用一下看代码里面到底是怎么写的，参数怎么用的，最后通过给index.html页面新增了一个flag参数，通过判断flag为预设值时，就确定当前页面为首页，于是文字显示效果就出来了。

至于后面为了装B弄得[js混淆加密再混淆](<https://www.sojson.com/jscodeconfusion.html>)，只是为了玩一下开心。也发现这样处理之后，解密不回去原本的代码，当然这改变的只是变量名，代码的逻辑还是无密可言。

这基本就完工了，绕了一大圈，遇到了好几个坑，最后看来，原来解决方案是这么简单，当然如果吃七个包子就饱了但却是不能直接吃第七个而忽视了前六个的作用。

最后，感谢这些为开源贡献力量的人。