---
title: 如何使用响应令牌和at.js自定义事件
description: 了解如何使用响应令牌和at.js自定义事件将Target中的配置文件信息共享到第三方系统。
role: Developer
level: Experienced
topic: Personalization, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: d6ce5367-a453-4e6c-8545-9fa676977f04
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 3%

---

# 将响应令牌和at.js自定义事件与Adobe Target结合使用

响应令牌和`at.js`自定义事件允许您将配置文件信息从[!DNL Target]共享到第三方系统。 [!DNL Target]访客配置文件中的任何对象（包括自定义配置文件属性、地理信息、活动详细信息和内置配置文件）都可以添加到[!DNL Target]响应中，您可以在此响应中使用自定义JavaScript与第三方集成。

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)

## 如何使用响应令牌和at.js自定义事件

1. 确定[!DNL Target]中需要哪些数据
1. 通过在“设置” — >“响应令牌”屏幕上翻转切换开关，为您需要的数据打开响应令牌
1. 确定您需要使用的事件侦听器
1. 编写侦听Adobe Target事件、读取响应令牌以及执行集成所需操作所需的JavaScript
1. 在“Load Target”操作后，使用Launch中的自定义代码操作部署事件侦听器JavaScript，或将其添加到“设置” — >“实施”屏幕上at.js的库页脚部分，然后保存一个新的at.js文件
1. QA并发布集成

## 其他资源

* [将Experience Cloud Debugger与Adobe Target结合使用](../troubleshooting/troubleshoot-with-the-experience-cloud-debugger.md)
* [响应令牌文档](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=en)
* [at.js自定义事件文档](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/atjs-custom-events.html?lang=en)
* [在 Adobe Target 中使用数据提供程序](use-data-providers-to-integrate-third-party-data.md)
