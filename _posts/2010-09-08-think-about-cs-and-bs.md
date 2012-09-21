---
layout: post
title: 关于C/S和B/S的思考
slug: think-about-cs-and-bs
date: 2010-09-08 17:14:06 +0800
excerpt: 终于下定决心写点自己对计算机科学的认识了，或许（是有很大的可能），你看到这里，笑了，觉得很幼稚，那请你指出不足之处，我也不会觉得丢脸，因为是自己思考的结果，错了可以改。
categories:
- note
tags:
- software
more_categories:
- slug: note
  name: 学习笔记
more_tags:
- slug: software
  name: 计算机软件
---

<span style="color: #3366ff;">终于下定决心写点自己对计算机科学的认识了，或许（是有很大的可能），你看到这里，笑了，觉得很幼稚，那请你指出不足之处，我也不会觉得丢脸，因为是自己思考的结果，错了可以改。</span>

今天看了一下PHP的东西，然后研究了一下MVC的东西，然后又发展到设计模式的问题，然后不知怎么的又转到了两种软件架构模式，就自己考虑了一下，这两者之间的本质区别。

最早软件出现的时候，好像都是单机的，因为那个时候网络还没有出现。


等到网络出现了，计算机之间需要连网传送数据，这时，C/S出现了，人们编写客户端（client）的程序，人们再写服务端（server）的程序，人们再约定客户端和服务器端传输数据的格式，然后C端发送请求到S端，S端返回数据到C端。

再后来，网络普及了，上网的人多了，需要的应用程序也多起来，于是我们的软件工程师们就很努力的写程序，写完服务器再写客户端。这个时候有些人在想，是不是可以简化一下呢，可不可以编写一个万能的客户端呢？当他这样想的时候，WWW出现了，浏览器（browser）出现了，由于浏览器的种种特性，它成功的成为了一个万能的C/S客户端。而数据返回的格式就是HTML了，哈哈（也有XML，等数据格式）。

再再后来，XML啊、AJAX啊等东东的出现是的浏览器更牛逼起来了，所以这里总结了一下，应该是B/S是C/S的一种特殊形式罢了，就是不知道有没有其他的形式，这我就不知道了。如果你看到了这里，请留言告诉我。

如果，你觉得这篇文章很好笑，你可以留言骂我，但要指出我哪里理解错了，谢谢。