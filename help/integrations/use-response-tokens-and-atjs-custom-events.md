---
title: 如何使用响应令牌和at.js自定义事件
description: 了解如何使用响应令牌和at.js自定义事件共享从目标到第三方系统的用户档案信息。
role: 开发人员
level: 富有经验
topic: 个性化、架构、开发
feature: 实施
doc-type: technical video
kt: null
thumbnail: null
author: Daniel Wright
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 4%

---


# 将响应令牌和at.js自定义事件与Adobe Target

响应令牌和`at.js`自定义事件允许您将用户档案信息从[!DNL Target]共享到第三方系统。 [!DNL Target]访客用户档案中的任何对象(包括自定义用户档案属性、地理信息、活动详细信息和内置用户档案)都可以添加到[!DNL Target]响应中，在该响应中，您可以使用自定义JavaScript与第三方集成。

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)

## 如何使用响应令牌和at.js自定义事件

1. 确定您需要[!DNL Target]中的哪些数据
1. 通过翻转“设置” — >“响应令牌”屏幕上的切换键，打开所需数据的响应令牌
1. 确定您需要使用哪个事件侦听器
1. 编写侦听Adobe Target事件、读取响应令牌以及执行集成所需操作所需的JavaScript
1. 在“加载目标”操作后，使用Launch中的自定义代码操作部署您的事件侦听器JavaScript，或将其添加到“设置” — >“实施”屏幕上at.js的“库页脚”部分，并保存一个新的at.js文件
1. QA并发布您的集成

## 其他资源

* [将Experience Cloud Debugger与Adobe Target](../troubleshooting/troubleshoot-with-the-experience-cloud-debugger.md)
* [响应令牌文档](https://docs.adobe.com/help/en/target/using/administer/response-tokens.html)
* [At.js自定义事件文档](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/atjs-custom-events.html)
* [在 Adobe Target 中使用数据提供程序](use-data-providers-to-integrate-third-party-data.md)