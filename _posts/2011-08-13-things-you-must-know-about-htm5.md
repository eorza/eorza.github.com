---
layout: post
title: HTML5须知
slug: things-you-must-know-about-htm5
date: 2011-08-13 08:04:44 +0800
excerpt: html5是个好东西，主要原因是因为个人痛恨flash，因为我不会flash。flash是我第一个学的有关计算机的只是，也是我最不了解的flash知识，所以我痛恨。
categories:
- note
tags:
- html
---

一两年前，HTML5似乎还是一个模糊的概念，只有少数几个互联网的书呆子才会关心。而现在，却感觉仿佛HTML5无所不在了。感谢Mozilla和 Chrome的快速发布，以及微软IE9的部署（IE 10现在也处于“技术预览”状态了），数量有限（或者说比有限要更好些）的支持HTML 5的浏览器已将近人人皆可享受。

开发人员开始利用那些得到广泛实现的功能特性。不出1年HTML 5就将得到完全支持，而规范也正在迅速到达稳定状态，现在正是了解一些HTML 5须知的好时机。

## 1: XHTML不再，（支持XML 语法的）HTML 5永存

XHTML是喜欢精确，尤其是在解析方面精确的人的选择。HTML外观一直都有很多与XML相似的地方，但却永远都无法跟XML一模一样，因此，试图把它当做XML来解析必将失败。因此不久前，XHTML被制定出来替代HTML语言，并把它归到XML的术语里面。当HTML 5的 工作首次启动的时候，同时也在进行着XHTML 2的工作，但它最终还是被封存了。相反地，HTML 5规范制定出来的目的在于，让你能够编写遵循严格的XML语法的，并能工作的HTML 5文件。 如果你把它跟XML MIME类型一并发送出去的话，用户代也会把它作为XML文档来进行解析。这把两个世界最好的东西都给了开发人员。


## 2: 2022之神话，2011之现实

对于HTML 5，流传很广的误解之一是“到2022年之前都不会完成”。其典型的支持证据是若干年前我对HTML 5规范的编辑兰·希克森（Ian Hickson）的一次采访。具有讽刺意味的是，即便是在那次采访中，他对2022年这个日期也很明确。但是有些人对此很激动，其愤怒的文章引起的注意要比实际的事实引发的关注多得多。

事实是2022年是希克森预期HTML5规范成为完全W3C推荐的日子，到那个时候将会有两个100%完成的、可验证的实现。这既相当的没有意义的同时又称得上是一次巨大的飞跃，为了让大家了解为什么说，可以想想，没有其他版本的HTML规范曾经达到过那样的地位，这主要是因为对于任何实现来说要做到可验证的正确都太含糊了。而HTML 5规范正接近于固化不变，就是现在，2011年。

## 3: 对大多开发人员而言，这是Flash和Silverlight杀手

在如何用于对文档进行标记方面，尽管HTML 5的确做了若干的改进，大的关注点仍是应用。HTML 5所引入的用于支持应用开发的特性的数量是令人惊愕的。这并不是说Flash和Sliverlight很快就会消失。但是微软已经宣布其对Sliverlight重新定位关注点为浏览器以外的体验。Flash和Silverlight仍拥有一些HTML 5不具备的能力，但是对于许多共同目标来说，现在鸿沟不再了，这要归功于HTML 5的新能力。可能重写已有应用并不值得，但是你应该看看HTML 5对于新应用来说是否有意义。

## 4: 它是许多新工具的基石

随着HTML 5成为一个完全成熟的应用框架，工具制造商，尤其是那些设计用于克服跨平台开发问题的，现在正把他用作其产品的基础技术。如果你正在寻求编写跨平台运行的应用，并且其也在HTML 5的能力范围之内，那么你应当考虑一下这些工具。这对于移动领域尤其重要，否则的话，对于每一个你打算作为目标的手机平台来说，都需要去学习全新的语言、API以及框架。

## 5: 重要而有争议的tag

“HTML 5最佳新特性”我的个人之选是tag（标签）。之前（也有tag），你自己得求助于Flash 或Silverlight来为你的网站提供一个媒体播放器。而有了这些新的标签之后，从理论上来说，那些日子一去不复返了。为什么只是“理论上”呢？令人悲哀的的是，由于专利的缘故，对于应该支持哪种格式，不同的浏览器制造商尚不太能确定。而一旦尘埃落定，Flash和Silverlight都会失去其#1用户案例。

## 6: 谷歌谷歌，带头大哥

如果说似乎Chrome浏览器在HTML 5上有了一个极好的开端的话，那么这里也有一个好的理由。HTML 5规范的制定进程中给编写和部署代码赋以浓彩重墨。我这么说并不是指他们不管任何浏览器供应商做了什么都会盖上“橡皮图章”了事。但你是很难说服那些参与编写规范的人接受尚未实现的特性，已实现的特性更有可能被列入为规范新项目的基础。由于Chrome似乎每几周就会有一个新版本出来，因此谷歌加进去的新特性也被纳入到HTML5规范里面的机会就会很大。

## 7: “标准兼容”终获证明

每当有人宣称某个浏览器是或不是“标准兼容”的时候，我都不得不笑起来。在HTML 5之前，标准兼容简直就不可能被加以证明。许多情况下，当前的规范都太过含糊或干脆对重要问题默不作声（像处理解析错误），结果就是不同的浏览器都可以做范围很广的不同事情，并依然要么是标准兼容的，要么是被归类为“不兼容性无法证实”。即便是最著名的ACID测试也证实不了太多东西，由于它只测试了HTML的子集。而HTML 5的门槛则提高了不少，证明一个用户代理是标准兼容的终于有可能了。的确，2022这个到达“建议”状态的日期背后的其中一个原因就是需要编写完全测试包。

## 8: “标准兼容”仍无法保证外观

Web浏览器里面的标准兼容并没有像人们通常所认为那样的行为，HTML 5也没有改变这一事实。HTML的一个大的困惑是许多的Web设计者和开发人员认为HTML规范控制着屏幕项目的外观；其实不然。举个例子，如果它喜欢的话，Web浏览器可令tag使用更大或不同颜色的字体而非加粗字体，也还能保持兼容性。许多时候，当设计者说浏览器与标准不兼容的时候，其所遭遇到的实际上是赋予用户代理的在如何显示标签方面的灵活性。HTML5并没有改变这一事实。如果你一定要让标签按照精确地方式显示，别指望浏览器的缺省行为；把你的需求在CSS中指定。

## 9: 解析更为精确

HTML5规范终于引入了精确解析规则，并定义了像用户代理遭遇解析错误时应该做的事情。因此，你可以预期，过去一些习惯于被当做可接受乃至“合法”HTML而通过的东西不再符合要求。你将会想要去熟悉HTML5的解析规则并确保你的代码符合其要求。

## 10: HTML5远非浏览器

在HTML之前的版本中，存在着一种与生俱来的假设，那就是传统的Web浏览器是用户代理的选择。尽管其他的用户代理和内容类型也得到了支持，隐含的想法是它们并非同等的重要。但是，针对于非浏览器、非桌面大小的用户代理，HTML5在与浏览器更为平等地相待方面做出了很多的改变。像在屏幕阅读器和手机上工作得有多好之类的东西取得了许多进展。因此，对于需要它的开发人员来说，写得好的HTML5是能够“一次编写，随处查看”的框架，它也能够对那些否则就要与Web做斗争的用户（尤其是那些存在各种障碍的人士）起作用。

个人读后感：html5是个好东西，主要原因是因为个人痛恨flash，因为我不会flash。flash是我第一个学的有关计算机的只是，也是我最不了解的flash知识，所以我痛恨。
