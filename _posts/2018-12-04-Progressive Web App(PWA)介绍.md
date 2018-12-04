---
layout: post

title: Progressive Web App(PWA)介绍

cover: /img/cover/chrome-extensions.jpg

tags: ['PWA', 'Progressive Web App']
---

## Progressive Web App(PWA)背景介绍

很多人似乎都认为Web，应用永远不会与本机竞争，移动应用程序的可靠性速度和用户参与，很难建立一个他们的商业案例。



你知道吗？你知道他们曾经是对的，但有两件事情发生了变化。



首先，事实证明，大多数人在购买手机时购买了大部分应用程序，或者不久之后大多数人安装了一些常见应用程序并只用了一天，这使得开发人员难以参与竞争，但人们仍然继续使用网络和 一些新技术，让你可以从中提供客户所需的关键功能。我们称它为**渐进式网络应用程序(Progressive Web Apps).**



**渐进式网络应用程序**是采用所有正确组成要素的网络应用程序，这些体验结合了最好的网络和最好的应用程序，它们为用户提供了他们期望从本机应用程序获得的可靠快速和引人入胜的体验，但通过网络传递。



## 什么是Progressive？

**PWA不是API或技术，但它是一种Web开发方法**，它使用已有的工具和技术组合来创建有针对性的理想用户体验。

它展示了如何使用服务工作者(service workers,)，API和应用程序shell体系结构来实现有意义的离线体验，快速首次加载以及重复访问时轻松重新访问用户。



**Progressive Web App一词由[Alex Russell](https://medium.com/@slightlylate)和Frances Berriman创造。用Alex的话说：**

> Progressive Web Apps are just websites that took all the right vitamins.
> 
>     [——_Alex Russell](https://medium.com/@slightlylate)



**渐进式网络应用程序是采用所有正确组成要素的网络应用程序。**



[渐进式Web应用程序](https://developers.google.com/web/progressive-web-apps)是将最佳网络和最佳应用程序相结合的体验。从浏览器选项卡中的第一次访问开始，它们对用户非常有用，无需安装。随着用户逐渐与应用程序建立关系，它变得越来越强大。即使在片状网络上，它也能快速加载，发送相关的推送通知，主屏幕上有一个图标，并作为顶级全屏体验加载。



渐进式Web应用程序是：

- **渐进式**- 适用于每个用户，无论浏览器选择如何，因为它是以渐进增强为核心原则构建的。
- **自适应**- 适合任何形式：桌面设备，移动设备，平板电脑或其他任何设备。
- **独立连接**- 增强服务人员脱机工作或低质量网络。
- **APP样**-感觉就像是一个应用程序，因为应用程序壳模型分离的应用程序*的功能*从应用*内容*。
- **新鲜**- 由于[服务工作者](https://developers.google.com/web/fundamentals/getting-started/primers/service-workers)更新过程，始终保持最新状态。
- **安全**- 通过HTTPS提供服务以防止窥探并确保内容未被篡改。
- **可发现**- 由于[W3C清单](https://developers.google.com/web/updates/2014/11/Support-for-installable-web-apps-with-webapp-manifest-in-chrome-38-for-Android)和[服务工作者注册](https://developers.google.com/web/fundamentals/instant-and-offline/service-worker/registration)范围，可以识别为“应用程序”，允许搜索引擎找到它。
- **可**重新参与 - 通过推送通知等功能轻松实现重新参与。
- **可安装**- 允许用户将他们认为最有用的应用添加到其主屏幕，而无需使用应用商店的麻烦。
- **可链接**- 通过URL轻松共享应用程序，不需要复杂的安装。



## 为什么我们需要Progressive Web App？

网络应用程序是结合了最好的网络和最好的应用程序的体验。

它们为用户提供了一种可靠的快速和引人入胜的体验，这些体验是他们从原生应用程序中获得的，但是通过网络传递它们是可靠的，

并且它们给予我们更棒的用户体验：

1. **F**ast：PWA提供始终如一的快速体验。从用户下载应用程序到他们开始与之交互的那一刻起，一切都发生得非常快。因为您可以缓存数据，即使没有访问网络，也可以非常快速地再次启动应用程序。

   
2. **I**ntegrated user experience：PWA的感觉和行为就像本机应用程序一样。它们位于用户的主屏幕中，发送推送通知，如本机应用程序，并可访问设备的功能，如本机应用程序。体验感觉无缝集成。

   
3. **R**eliable experience：随着服务人员的帮助下，我们能够可靠地描绘出用户的屏幕上的图片，即使网络出现故障。

   
4. **Ë**ngaging：因为我们可以发送通知给用户，才能真正推动参与了由保持用户通知，并与应用程式互动。



这就是**FIRE**.






