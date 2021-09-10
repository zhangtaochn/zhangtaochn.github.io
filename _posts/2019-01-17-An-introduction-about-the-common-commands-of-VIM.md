---
layout:     post
title:      "一些VIM常用命令介绍"
subtitle:   "Make programming more efficient."
date:       2019-01-17 00:19:46 +0800
author:     "ZHANG Tao"
header-img: "img/post-2019-01-17-vim-header.jpeg"
tags:
- vim
---

<script type="text/javascript" async src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.2/MathJax.js?config=TeX-AMS-MML_HTMLorMML"> </script>

*不少人在讲VIM堪称神器，所以那怎么能不去尝试一番呢。据说是需要背很多的命令，但挑战一下也是一件有趣的事嘛，就像曾经刚接触Markdown也觉得好奇怪，如今用起来也很是顺手。那就正好在这里做一个汇总，把常用的命令列出来，也可以当做是一个学习笔记。*

*第一步：**Esc**进入NORMAL模式。*

### 基本命令：

​	**:w**		保存

​	**:q**		退出

​	**:q!**		退出不保存

​	**:qa!**		强行关闭当前所有文档不保存

​	**:wq**		保存并退出

​	**x**		删除光标所在字符

​	**dd**		删除所在行

​	**p**		粘贴

​	**yy**		复制当前行

​	**i**		在当前光标前插入并进入**INSERT**模式

​	**a**		在当前光标后插入并进入**INSERT**模式

​	**o**		在当前行后插入新的一行

​	**O**		在当前行前插入新的一行

​	**hjkl**		光标控制：左 下 上 右

​	**0**		光标跳到当前行头

​	**$**		光标跳到当前行头

​	**NG**		跳转到第N行

​	**:N**		跳转到第N行

​	**gg**		跳转到第一行

​	**G**		跳转到最后一行

​	**^**		到本行第一个不是空格的光标位置

​	**g_**		到本行最后一个不是空格的光标位置

​	**u**		取消上一步操作

​	**Ctrl+r**	重复上一步操作

### 进阶命令：

​	****

​	**.** 		重复上一次的命令

​	**N+command**		 重复命令N次

​	**%** 		匹配括号移动

​	\*** #** 	匹配当前所在单次，*移动到上一个，#移动到下一个

​	**<start position><command><end position>**  从起始位置执行该命令到结束位置

​	**<command><end position>**  从当前位置执行到结束位置

​	**v**		可视化选择

### Reference：

[1] [陈浩：简明VIM练级教程](https://coolshell.cn/articles/5426.html)

[2] [vim常用命令总结 （转)](https://www.cnblogs.com/yangjig/p/6014198.html)