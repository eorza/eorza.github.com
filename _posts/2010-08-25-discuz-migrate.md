---
layout: post
title: discuz迁移相关
slug: discuz-migrate
date: 2010-08-25 17:23:17 +0800
excerpt: 公司网站马上要迁空间了，老板问我discuz数据能迁移不，当时想都没想就说可以，虽然没有接触过discuz论坛，但是我想应该很简单吧，今天马上就自己做了一下实验，结果觉得没想象的那么简单，成功了，就在这记录一下。
categories:
- note
tags:
- discuz
more_categories:
- slug: note
  name: 学习笔记
more_tags:
- slug: discuz
  name: discuz
---

公司网站马上要迁空间了，老板问我discuz数据能迁移不，当时想都没想就说可以，虽然没有接触过discuz论坛，但是我想应该很简单吧，今天马上就自己做了一下实验，结果觉得没想象的那么简单，成功了，就在这记录一下。

在这里是我自己迁移的步骤，出了好多问题，但是我觉得这些问题反而挺好的，就没改，估计还有好多好多不好的问题，我也没测试，就讲究着用吧，反正公司论坛大家也不怎么看重，等以后再改吧。

一、先安装好新的ucenter，全新哦。

二、将原ucenter数据库中的@_members表替换新的ucenter中的相应表，ucenter数据库中好像还有几个内容需要迁移，如包含留言、短消息内容的表等，我觉得没必要了，就没弄。（补充：将admin账号删除，因为后来安装的discuz论坛会创建一个admin账户，所以会冲突）


三、ucenter头像文件。讲ucenter文件夹中原有的data/avatar/覆盖到新的ucenter目录中，这里主要是解决了头像的问题，如果不覆盖的话，你的用户头像将全部是默认的。

四、安装全新的discuz论坛。然后将源论坛的所有数据替换新的数据库。

五、修改discuz和ucenter的配置文件。discuz在根目录下，config.inc.php。ucenter在data目录下，同样为config.inc.php。

大概就这些了，因为是写个自己备忘的，所以很不详细，见谅。