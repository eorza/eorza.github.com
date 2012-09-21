---
layout: post
title: subversion相关
slug: about-subversion
date: 2011-08-09 09:07:55 +0800
excerpt: svn挺好的，当然有人说分布式的git更好。当然那些人不做评价，个人觉得适合自己的是好的，容易使用的是好的，如果你真的高手到了一定程度，我们也不好说什么东西。
categories:
- note
tags:
- svn
- ubuntu
more_categories:
- slug: note
  name: 学习笔记
more_tags:
- slug: svn
  name: svn
- slug: ubuntu
  name: ubuntu
---

svn挺好的，当然有人说分布式的git更好，要让svn去死。当然那些人不做评价，个人觉得适合自己的是好的，容易使用的是好的，如果你真的高手到了一定程度，我们也不好说什么东西。

首先要安装svn服务器，我用的是ubuntu，很简单，apt-get install subversion即可。

装完就好配置一下，下面是要配置的东西。

## 1.创建仓库

	svnadmin create /var/svn

/var/svn 为所创建仓库的路径，理论上可以是任何目录。当然我的目录是/var/svn/


## 2.修改配置文件/var/svn/conf/svnserve.conf

	#去掉#[general]前面的#号
	[general]
	#匿名访问的权限，可以是read,write,none,默认为read
	anon-access = none
	#认证用户的权限，可以是read,write,none,默认为write
	auth-access = write
	#密码数据库的路径，去掉前面的#
	password-db = passwd

注意：所有的行都必须顶格，否则报错。 建议：为了防止不必要的错误，建议你直接用我上面的内容覆盖掉文件原来的内容.

## 3.修改配置文件passwd

	[users]
	svnuser = password
	jesszjessz = jessz

注意：一定要去掉`[users]`前面的#,否则svn只能以匿名用户登录，客户端不会出现登录窗口，除非你的anon不为none,否则将返回一个错误。

这里的密码都是没有加密的，我按照一些教程所说的用htpasswd生成的密码无法使用。

## 4.停止Subversion服务器：

	killall svnserve

## 5.启动Subversion服务器 对于单个代码仓库,启动命令：

	svnserve -d -r /var/svn --listen-host 10.19.3.103

其中-d表示在后台运行，-r指定服务器的根目录，这样访问服务器时就可以直接 用svn://服务器ip来访问了。

------------------------------分割先，你懂的------------------------------

下面是subversion的一些常识，包括基本命令等内容。

先说明一下几个版本概念。

一个是服务器版本，每一次提交svn都会将版本号加1，无论你是修改了文件，还是添加删除了，甚至修改一下文件夹的svn属性，只要你提交都会更新版本；

第二个是本地基础版本，也就是你上次进行update之后的和svn服务器上的版本，比如你update时服务器上是reverion11你的本地基础版本就是reverion11，无论别人改了什么，服务器上更新了多少版，只要你不执行update则你的基础版本永远是reverion11；

第三个是工作版本，就是你当前改着的版本，工作版本是基于基础版本的，如果没改，工作版本就和基础版本一致，如果你改了，你的工作版本就是从基础版本修改过来的。

总是有人问已经在本地删除了某个文件，可是一更新又从svn还原出来了，或者我已经把一个文件移动到另外的地方，可是怎么修改svn让他同步等等。在受svn管理的文件中，所有的文件操作不能想当然的进行，添加删除和移动改名都是有对应的svn操作的，这样才能自动的反映到svn上来，尤其是移动文件这样的操作，如果操作不慎，就会无法将文件的修改历史联系起来。不过，svn的操作有一些是需要连接服务器的“连线操作”有一些是之进行本地操作的“离线操作”。所以下面介绍一些 svn使用的基本操作。

## SVN基本操作之svn checkout

作为svn的用户，拿到一个svn地址，我们首先做的一个事情就是svn checkout，将svn上的关联到本地的一个文件夹中。这个文件夹最好是空的文件夹，或者确保没有和svn上相同名称的路径，当然这也说明这个操作是个连线操作。我们一般在执行checkout的时候只要给出svn的URL和本地的路径两个内容就可以了。这样svn上最新的数据会被传送到这个文件夹，目录结构会自动建好，svn上的文件会自动出现在对应的文件夹中。当然如果你愿意也可以选择一个旧的版本，或者只包含一层目录或者只是这个文件夹中的文件。或许你发现了，每一个文件夹中比服务器上的内容多了个.svn文件夹，这个文件夹中存放着文件夹的属性，这个文件夹中的每个文件的属性、版本还有对应版本的一个副本。

## SVN基本操作之svn update

这个操作就是将本地的的数据更新到svn上的某个版本，默认的操作是更新到最新版本，这个操作也是个连线操作。在这个过程中如果有人删除了文件，它会你机器上的文件删除，如果别人改了某个文件，会将这个文件更新。如果你修改了某个文件，别人删除了它，则这个文件不会被删除，只会和svn没关系了。如果你修改了某个文件，而这个文件别人也修改了，在更新的过程中就会试图自动将你的修改合并，如果成功，他的内容就是你修改的和别人修改的内容的并集，如果失败，svn就会将这个文件标记为冲突。冲突的问题我们放在下个说。

## SVN 基本操作之svn resolve

使用svn意味着你已经走在了工作在编辑和合并的道路上，那么冲突的时候svn做了什么，出现了冲突怎么解决？

在标记为冲突的过程中，如果是文本文件，如cpp和h文件，svn会修改它让他不能进行编译，并产生一个theirs和mime，分别包含 svn服务器上的和我自己原来的版本。

如果是二进制文件，svn不会修改它，而会在目录中产生一个r??和r??这两个r??一个是你 update之前的svn基础版本，就是你上次执行update的版本，一个是svn上的当前update下来的版本。

你可以选择直接使用 theirs或者使用mime或者退回到上一个update版本，或者将两个文件放在一起手工合并作为解决的方法。

这个操作是离线操作。

## SVN 基本操作之svn commit

svn的commit操作就是将修改从工作拷贝发送到版本库并将版本标记为新的版本，这个过程中如果有人已经对这个版本进行了操作，也就是你的本地基础版本和服务器不同，将会强制你执行一个update操作，这个操作是个连线操作。commit的过程仅仅是将你本地的一些修改提交到svn中让svn上的和你的一致，在提交之前必须已经解决了需要提交文件已有的冲突才行。

## SVN基本操作之svn add

如果一个文件不受svn管理，你需要把它添加到svn中，这个操作是个离线操作，仅仅是把这个文件标记为需要添加，真正的添加到svn存储的操作将在下一次commit时执行。这个过程中需要注意不要把一些不必要的文件比如编译的临时文件添加到svn。

## SVN基本操作之 svn import

当然你可以将一些文件直接添加到svn而不想修改这些文件的svn管理状态，可以选择将它们导入到svn。注意如果将一个文件导入，则给出的url就是它添加到svn的最终文件名，如果将一个文件夹导入，则会将根据目录树所有的子文件和文件夹放到对应的url的对应目录树中，根文件夹不会被添加。

这个操作是连线操作。

## SVN基本操作之svn cleanup

这个操作清理整个所选择的文件夹及其子文件夹，但是它不是清理垃圾文件什么的，这肯定不是svn的工作。它也不会把冲突自动解决，如果能自动解决，在更新的时候为什么不做。如果你在某个svn操作时强制中断了，比如svn的操作程序停止相应或者以外终止，就有可能导致文件夹处于锁定状态，这时需要清理。如果你的文件夹中的很多文件时间戳发生了变化，也最好执行以下cleanup这样可以加速svn操作的执行。

这个操作是离线操作。

## SVN基本操作之 svn delete

既然有方法添加文件，就一定有方法删除，虽然你看到的效果是文件直接被删除了，但是实际上和添加一样，这个操作是个离线操作，操作的结果将被标记，下次commit时服务器上的文件才会被删除。

## SVN基本操作之svn revert

如果你的修改出现了问题，或者添加或者删除了错误的文件，等等想还原操作，在commit之前可以执行revert操作，退回某步操作，这样这些修改都会被还原到基础版本状态。这个操作不会和svn服务器有关系，不会连接服务器也不会更新文件，只是简简单单的回复到基础版本。

这个操作是个离线操作。

## SVN 基本操作之svn diff

这个操作就是比较你的工作版本和某个svn版本的区别，当然默认是你的基础版本，因为你的工作版本就是从基础版本修改过来的么。

在和基础版本比较时是个离线操作，和历史版本比较时是连线操作。

## SVN基本操作之svn export

这个操作可以将一个已经在svn管理下的文件夹中的所有工作版本导出到一个文件夹中，或者直接从svn服务器上将一个版本导出到一个文件夹中。导出的文件夹不再在svn的管理控制下，也不会有.svn目录，当然也不会包含不在svn管理下的文件。

在导出工作版本时是个离线操作，从svn直接导出时是连线操作。

## SVN基本操作之svn copy

操作的名字显而易见，就是复制操作，在svn上复制文件有什么好处呢，为什么不直接复制文件再添加到svn呢。这个问题我也考虑过，svn copy可以将文件在复制之前的历史保留下来，这应该是最大的好处了。

这个操作是离线操作，需要提交才起效。

## SVN基本操作之svn move

和copy一样，历史的留存也是和复制后删除源文件这个方式最大的区别，并且它也是离线操作，需要提交才起效。

## SVN基本操作之svn lock

如果你想独占修改这个文件，可以把文件锁定，这样就可以锁定这个文件，这样别人必须等待你提交了修改或者释放了锁才能提交他们的修改。这个操作不会对别人的svn本地存储有什么影响，而只是无法进行数据提交。如果某个文件有svn:needs-lock这样的标志时，文件会被设置为只读，提示你需要获得锁来修改。当然你也可以把文件的属性修改直接修改，这个只是防君子不防小人的。

这个操作时连线操作。

## SVN基本操作之svn unlock

虽然是 unlock但是实际上这个我们平常不会将他用来和lock配对，因为commit操作时，svn默认自动将锁释放了。这个操作的用处是在你得到锁了之后，又不想锁定这个文件时执行的。还有就是如果别人锁定了这个文件，想强制把这个文件解锁，就可以强制将这个文件解锁。

这个操作时连线操作。

