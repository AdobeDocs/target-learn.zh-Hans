---
title: at.js 2.0如何工作？
description: at.js 2.0增强了Adobe Target对单页应用程序(SPA)的支持，并与其他Experience Cloud解决方案集成。 此视频和随附的图解说明了一切如何结合在一起。
role: 开发人员
level: 中间
topic: SPA，架构，开发
feature: 实施
doc-type: technical video
kt: null
thumbnail: null
author: Daniel Wright
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 12%

---


# 了解Adobe Target的at.js 2.0的工作原理

`at.js` 2.0增强了Adobe Target对单页应用程序(SPA)的支持，并与其他Experience Cloud解决方案集成。此视频和随附的图解说明了一切如何结合在一起。

>[!VIDEO](https://video.tv.adobe.com/v/26250?quality=12)

## 架构图

![at.js 2.0页面加载行为](assets/pageload.png)

1. 调用返回Experience CloudID(ECID)。 如果用户已通过身份验证，则另一个调用将同步客户ID。

1. `at.js` 库同步加载并隐藏文档正文(`at.js` 也可以使用页面上实现的可选预隐藏片段异步加载)。

1. 会发出页面加载请求，包括所有已配置的参数、ECID、SDID和客户ID。

1. 用户档案脚本执行并馈送到[!UICONTROL 用户档案存储]中。 商店从[!UICONTROL 受众库]请求限定受众(例如，从[!DNL Analytics]、Audience Manager等共享的受众)。 [!UICONTROL 客户] 属性在批处理 [!UICONTROL 中发] 送到用户档案存储。
1. [!DNL Target]根据URL、请求参数和用户档案数据，决定哪些活动和体验要返回到当前页面和将来视图的访客

1. 目标内容发送回页面，（可选）包括用户档案值，以实现其他个性化。

   当前页面上的目标内容会在默认内容不发生闪烁的情况下尽快显示。

   在浏览器中缓存针对将来视图的单页应用程序的目标内容，因此在触发视图时，无需额外的服务器调用即可立即应用该内容。 （请参见下一个图表了解`triggerView()`行为）。

1. [!DNL Analytics] 从页面发送到Data CollectionServer [!UICONTROL 的数] 据
1. [!DNL Target] 数据会通过 SDID 匹配到 数据，并且会进行相应处理以保存到 Analytics 报表存储中。[!DNL Analytics][!DNL Analytics] 然后，可以在A4T报 [!DNL Analytics] 表中 [!DNL Target] 和通过A4T报表查看数据。

![at.js 2.0行为](assets/triggerview.png)

1. `adobe.target.triggerView()` 在单页应用程序中调用
1. 从缓存中读取视图的目标内容

1. 目标内容尽可能快地显示，而不会闪烁默认内容

1. 通知请求发送到[!DNL Target] [!UICONTROL 用户档案存储]以计算活动中的访客和增量量度
1. [!DNL Analytics] 数据从SPA发送到数 [!UICONTROL 据收] 集

1. [!DNL Target] 数据从后端发 [!DNL Target] 送到数 [!UICONTROL 据收] 集服务器[!DNL Target] 数据会通过 SDID 匹配到 [!DNL Analytics] 数据，并且会进行相应处理以保存到 [!DNL Analytics] 报表存储中。[!DNL Analytics] 然后，可以在A4T报 [!DNL Analytics] 表中 [!DNL Target] 和通过A4T报表查看数据。

## 其他资源

* [在单页应用程序中实施at.js 2.0](implement-atjs-20-in-a-single-page-application.md)
* [将Adobe Target的Visual Experience Composer用于单页应用程序(SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
* [at.js工作方式文档](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/at-js/how-atjs-works.html)