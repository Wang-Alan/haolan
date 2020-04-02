---
title: 为什么要把 R 代码写在 R markdown 上
author: whl
date: '2020-03-16'
slug: 为什么要把-r-代码写在-r-markdown-上
categories:
  - 个人
tags:
  - 总结
  - R语言
comments: no
images: ~
---

1. R 代码原来写在哪里？

R 代码最常见的是写在脚本（.r）里，文字可以通过注释加在脚本的字里行间。但是存在一些问题：

- 在数据分析中，注释通常会涉及公式，在脚本中无法呈现

- 如果与他人交流数据分析过程，将代码与输出结果对应，沟通交流会很高效

- 数据分析过程中对代码参数修改过多，如果不做好记录，很容易忘记一些重要的细节

- 数据分析通常需要保存中间步骤的输出结果

于是 jupyter notebook 被开发出来了。最开始的 jupyter notebook 是给 python 语言开发的，现在也广泛的被数据分析师应用。但是最开始的 jupyter notebook 是在浏览器中运行的，浏览器中的 jupyter notebook 使用中有一些弊端，比如代码开发、调试等开发过程对 IDE 的使用频率非常高，将  jupyter notebook 放在浏览器运行会导致很多额外的步骤。

2. 为什么使用 R markdown

目前，它被整合进了 VS code - 非常有些的IDE -弊端也逐渐消失。而 VS code 下的 jupyter notebook 并不支持 R 语言，而 R 语言原生的与 jupyter notebook 对应的，便是 R markdown。

此外，R markdown 相比于 jupyter notebook 还有额外的优势，包括：

- 自定义是否输出代码或结果

- 与最好用的 R 语言开发软件 R Studio 深度集成

- 不必安装其他软件就可以查看，因为 R markdown 文件的实质是文本文件

- 可借助 R 包导出成 pdf、html、word

- 语法与 markdown 高度相似，几乎无学习成本，jupyter notebook也有这个优点

3. R markdown 有什么局限

对我而言，R markdown 唯一的缺点在于不能实时查看 markdown 效果。详见 [是莽撞人就来单挑：一个所见即所得的（R）Markdown 编辑器？](https://yihui.org/cn/2018/06/wysiwyg-r-markdown/)
 
