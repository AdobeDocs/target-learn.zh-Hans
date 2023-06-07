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
source-git-commit: 80208b3ecbc0d627d2afe72f882e91c9800d2726
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 3%

---

# 将响应令牌和at.js自定义事件与Adobe Target结合使用

响应令牌和 `at.js` 自定义事件允许您共享来自的配置文件信息 [!DNL Target] 到第三方系统。 中的任何对象 [!DNL Target] 访客资料，包括自定义资料属性、地理信息、活动详细信息和内置资料，可添加到 [!DNL Target] 响应，您可以在其中使用自定义JavaScript与第三方集成。

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)

## 如何使用响应令牌和at.js自定义事件

1. 确定您需要从哪些数据中获取数据 [!DNL Target]
1. 在设置 — >响应令牌屏幕上翻转开关，打开所需数据的响应令牌
1. 确定需要使用的事件侦听器
1. 编写监听Adobe Target事件所需的JavaScript、读取响应令牌并执行集成所需的操作
1. 在“加载Target”操作之后，使用Launch中的自定义代码操作部署事件侦听器JavaScript，或将其添加到at.js的“设置” — >“实施”屏幕上的“库页脚”部分，并保存新的at.js文件
1. QA和发布集成

## 其他资源

* [将Experience Cloud Debugger与Adobe Target结合使用](../troubleshooting/troubleshoot-with-the-experience-cloud-debugger.md)
* [响应令牌文档](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=en)
* [在 Adobe Target 中使用数据提供程序](use-data-providers-to-integrate-third-party-data.md)
