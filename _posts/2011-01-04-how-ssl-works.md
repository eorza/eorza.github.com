---
layout: post
title: SSL握手过程
slug: how-ssl-works
date: 2011-01-04 13:55:20 +0800
excerpt: 这两天要准备一下公司邮件服务器的问题，就学习了一下关于ssl的东西，东西很简单，就是脑子得转几个弯，哈哈，一时半会接受不了。发现现在接受一些新东西的时候都要推翻以前的概念或者要重新理解以前的概念，比如这次，我就要重新理解一下这个认证跟加密的区别。真是头疼啊。
categories:
- note
tags:
- apache
- ssl
---

这两天要准备一下公司邮件服务器的问题，就学习了一下关于ssl的东西，东西很简单，就是脑子得转几个弯，哈哈，一时半会接受不了。发现现在接受一些新东西的时候都要推翻以前的概念或者要重新理解以前的概念，比如这次，我就要重新理解一下这个认证跟加密的区别。真是头疼啊。


## SSL协议的工作流程

服务器认证阶段：1）客户端向服务器发送一个开始信息“Hello”以便开始一个新的会话连接；2）服务器根据客户的信息确定是否需要生成新的主密钥，如 需要则服务器在响应客户的“Hello”信息时将包含生成主密钥所需的信息；3）客户根据收到的服务器响应信息，产生一个主密钥，并用服务器的公开密钥加 密后传给服务器；4）服务器恢复该主密钥，并返回给客户一个用主密钥认证的信息，以此让客户认证服务器。

用户认证阶段：在此之前，服务器已经通过了客户认证，这一阶段主要完成对客户的认证。经认证的服务器发送一个提问给客户，客户则返回（数字）签名后的提问和其公开密钥，从而向服务器提供认证。

从SSL 协议所提供的服务及其工作流程可以看出，SSL协议运行的基础是商家对消费者信息保密的承诺，这就有利于商家而不利于消费者。在电子商务初级阶段，由于运 作电子商务的企业大多是信誉较高的大公司，因此这问题还没有充分暴露出来。但随着电子商务的发展，各中小型公司也参与进来，这样在电子支付过程中的单一认 证问题就越来越突出。虽然在SSL3.0中通过数字签名和数字证书可实现浏览器和Web服务器双方的身份验证，但是SSL协议仍存在一些问题，比如，只能 提供交易中客户与服务器间的双方认证，在涉及多方的电子交易中，SSL协议并不能协调各方间的安全传输和信任关系。在这种情况下，Visa和 MasterCard两大信用卡公组织制定了SET协议，为网上信用卡支付提供了全球性的标准。

## SSL协议的握手过程 　　

为了便于更好的认识和理解 SSL 协议，这里着重介绍 SSL 协议的握手协议。SSL 协议既用到了公钥加密技术(非对称加密)又用到了对称加密技术，SSL对传输内容的加密是采用的对称加密，然后对对称加密的密钥使用公钥进行非对称加密。这样做的好处是，对称加密技术比公钥加密技术的速度快，可用来加密较大的传输内容， 公钥加密技术相对较慢，提供了更好的身份认证技术，可用来加密对称加密过程使用的密钥。

SSL 的握手协议非常有效的让客户和服务器之间完成相互之间的身份认证，其主要过程如下：

> 1 客户端的浏览器向服务器传送客户端 SSL 协议的版本号，加密算法的种类，产生的随机数，以及其他服务器和客户端之间通讯所需要的各种信息。
> 2 服务器向客户端传送 SSL 协议的版本号，加密算法的种类，随机数以及其他相关信息，同时服务器还将向客户端传送自己的证书。
> 3 客户利用服务器传过来的信息验证服务器的合法性，服务器的合法性包括：证书是否过期，发行服务器证书的 CA 是否可靠，发行者证书的公钥能否正确解开服务器证书的“发行者的数字签名”，服务器证书上的域名是否和服务器的实际域名相匹配。如果合法性验证没有通过， 通讯将断开；如果合法性验证通过，将继续进行第四步。
> 4 用户端随机产生一个用于后面通讯的“对称密码”，然后用服务器的公钥（服务器的公钥从步骤②中的服务器的证书中获得）对其加密，然后将加密后的“预主密码”传给服务器。
> 5 如果服务器要求客户的身份认证（在握手过程中为可选），用户可以建立一个随机数然后对其进行数据签名，将这个含有签名的随机数和客户自己的证书以及加密过的“预主密码”一起传给服务器。
> 6 如果服务器要求客户的身份认证，服务器必须检验客户证书和签名随机数的合法性，具体的合法性验证过程包括：客户的证书使用日期是否有效，为客户提供 证书的CA 是否可靠，发行CA 的公钥能否正确解开客户证书的发行 CA 的数字签名，检查客户的证书是否在证书废止列表（CRL）中。检验如果没有通过，通讯立刻中断；如果验证通过，服务器将用自己的私钥解开加密的“预主密码 ”，然后执行一系列步骤来产生主通讯密码（客户端也将通过同样的方法产生相同的主通讯密码）。
> 7 服务器和客户端用相同的主密码即“通话密码”，一个对称密钥用于 SSL 协议的安全数据通讯的加解密通讯。同时在 SSL 通讯过程中还要完成数据通讯的完整性，防止数据通讯中的任何变化。
> 8 客户端向服务器端发出信息，指明后面的数据通讯将使用的步骤⑦中的主密码为对称密钥，同时通知服务器客户端的握手过程结束。
> 9 服务器向客户端发出信息，指明后面的数据通讯将使用的步骤⑦中的主密码为对称密钥，同时通知客户端服务器端的握手过程结束。
> 10 SSL 的握手部分结束，SSL 安全通道的数据通讯开始，客户和服务器开始使用相同的对称密钥进行数据通讯，同时进行通讯完整性的检验。


双向认证 SSL 协议的具体过程

> 1 浏览器发送一个连接请求给安全服务器。
> 2 服务器将自己的证书，以及同证书相关的信息发送给客户浏览器。
> 3 客户浏览器检查服务器送过来的证书是否是由自己信赖的 CA 中心所签发的。如果是，就继续执行协议；如果不是，客户浏览器就给客户一个警告消息：警告客户这个证书不是可以信赖的，询问客户是否需要继续。
> 4 接着客户浏览器比较证书里的消息，例如域名和公钥，与服务器刚刚发送的相关消息是否一致，如果是一致的，客户浏览器认可这个服务器的合法身份。
> 5 服务器要求客户发送客户自己的证书。收到后，服务器验证客户的证书，如果没有通过验证，拒绝连接；如果通过验证，服务器获得用户的公钥。
> 6 客户浏览器告诉服务器自己所能够支持的通讯对称密码方案。
> 7 服务器从客户发送过来的密码方案中，选择一种加密程度最高的密码方案，用客户的公钥加过密后通知浏览器。
> 8 浏览器针对这个密码方案，选择一个通话密钥，接着用服务器的公钥加过密后发送给服务器。
> 9 服务器接收到浏览器送过来的消息，用自己的私钥解密，获得通话密钥。
> 10 服务器、浏览器接下来的通讯都是用对称密码方案，对称密钥是加过密的。

上面所述的是双向认证 SSL 协议的具体通讯过程，这种情况要求服务器和用户双方都有证书。单向认证 SSL 协议不需要客户拥有 CA 证书，具体的过程相对于上面的步骤，只需将服务器端验证客户证书的过程去掉，以及在协商对称密码方案，对称通话密钥时，服务器发送给客户的是没有加过密的 （这并不影响 SSL 过程的安全性）密码方案。 这样，双方具体的通讯内容，就是加过密的数据，如果有第三方攻击，获得的只是加密的数据，第三方要获得有用的信息，就需要对加密的数据进行解密，这时候的 安全就依赖于密码方案的安全。而幸运的是，目前所用的密码方案，只要通讯密钥长度足够的长，就足够的安全。这也是我们强调要求使用 128 位加密通讯的原因。

