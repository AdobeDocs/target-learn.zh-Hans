---
title: 将响应令牌和at.js自定义事件与Adobe Target一起使用
seo-title: 将响应令牌和at.js自定义事件与Adobe Target一起使用
description: 响应令牌和at.js自定义事件允许您将用户档案信息从目标共享到第三方系统。 目标访客用户档案中的任何对象(包括自定义用户档案属性、地理信息、活动详细信息和内置用户档案)都可以添加到目标响应中，在该响应中，您可以使用自定义JavaScript与第三方集成。
audience: developer
difficulty: 5
author: Daniel Wright
doc-type: implement
activity-type: technical-video
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 2%

---


# 将响应令牌和at.js自定义事件与Adobe Target一起使用

响应令牌 `at.js` 和自定义事件允许您从第三方 [!DNL Target] 系统共享用户档案信息。 访客用户档案中 [!DNL Target][!DNL Target] 的任何对象(包括自定义用户档案属性、地理信息、活动详细信息和内置用户档案)都可以添加到响应中，在响应中可以使用自定义JavaScript与第三方集成。

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)

## 如何使用响应令牌和at.js自定义事件

1. 确定您需要的数据 [!DNL Target]
1. 通过翻转“设置”->“响应令牌”屏幕，为所需数据打开响应令牌
1. 确定需要使用哪个事件监听器
1. 编写监听Adobe Target事件、读取响应令牌以及执行集成所需操作所需的JavaScript
1. 在“加载事件”操作后，使用Launch中的自定义代码操作部署目标监听器JavaScript，或将其添加到“设置”->“实施”屏幕上at.js的“库页脚”部分，并保存一个新的at.js文件
1. QA并发布您的集成

## 其他资源

* [将Experience Cloud Debugger与Adobe Target结合使用](../troubleshooting/troubleshoot-with-the-experience-cloud-debugger.md)
* [响应令牌文档](https://docs.adobe.com/help/en/target/using/administer/response-tokens.html)
* [At.js自定义事件文档](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/atjs-custom-events.html)
* [在 Adobe Target 中使用数据提供程序](use-data-providers-to-integrate-third-party-data.md)