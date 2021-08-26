---
title: at.js 2.0的工作原理是什么？
description: at.js 2.0增强了Adobe Target对单页应用程序(SPA)的支持，并与其他Experience Cloud解决方案集成。 此视频和随附的图表说明了如何将所有内容整合在一起。
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
thumbnail: null
author: Daniel Wright
exl-id: 7f037665-88a7-469c-8df5-c82cb0f65382
source-git-commit: a6b645b6d9693a4c8882fd47ee0d61698c0b834d
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 11%

---

# 了解Adobe Target at.js 2.0的工作原理

`at.js` 2.0增强了Adobe Target对单页应用程序(SPA)的支持，并与其他Experience Cloud解决方案集成。此视频和随附的图表说明了如何将所有内容整合在一起。

>[!VIDEO](https://video.tv.adobe.com/v/26250?quality=12)

## 架构图

![at.js 2.0页面加载时的行为](assets/pageload.png)

1. 调用会返回Experience CloudID(ECID)。 如果用户通过了身份验证，则另一个调用会同步客户ID。

1. `at.js` 库同步加载并隐藏文档正文(`at.js` 也可以通过页面上实施的可选预隐藏代码片段异步加载)。

1. 将发出页面加载请求，其中包括已配置的所有参数、ECID、SDID和客户ID。

1. 配置文件脚本执行并馈送到[!UICONTROL 配置文件存储区]中。 存储区向[!UICONTROL 受众库]请求符合条件的受众(例如从[!DNL Analytics]、Audience Manager等共享的受众)。 [!UICONTROL 客户] 属性会以批量过程 [!UICONTROL 发] 送到配置文件存储区。
1. [!DNL Target]根据URL、请求参数和配置文件数据确定要返回给访客的当前页面和未来视图的活动和体验

1. 目标内容会发送回页面，其中可能包含其他个性化的配置文件值。

   当前页面上的目标内容会在默认内容不发生闪烁的情况下尽快显示。

   单页应用程序的未来视图的目标内容会缓存在浏览器中，因此在触发视图时，无需额外的服务器调用即可立即应用该内容。 （请参阅下一个图表，了解`triggerView()`行为）。

1. [!DNL Analytics] 从页面向数据收集服务器发送 [!UICONTROL 的数] 据
1. [!DNL Target] 数据会通过 SDID 匹配到 数据，并且会进行相应处理以保存到 Analytics 报表存储中。[!DNL Analytics][!DNL Analytics] 然后，便可以在和中通过 [!DNL Analytics] A4T [!DNL Target] 报表查看数据。

![使用triggerView()函数时的at.js 2.0行为](assets/triggerview.png)

1. `adobe.target.triggerView()` 在单页应用程序中调用
1. 从缓存中读取视图的目标内容

1. 目标内容会在默认内容不发生闪烁的情况下尽快显示

1. 通知请求将发送到[!DNL Target] [!UICONTROL 配置文件存储区]，以计算活动中的访客和递增量度
1. [!DNL Analytics] 数据从SPA发送到数据收 [!UICONTROL 集服] 务器

1. [!DNL Target] 数据会从后端发 [!DNL Target] 送到数据收集 [!UICONTROL 服] 务器。[!DNL Target] 数据会通过 SDID 匹配到 [!DNL Analytics] 数据，并且会进行相应处理以保存到 [!DNL Analytics] 报表存储中。[!DNL Analytics] 然后，便可以在和中通过 [!DNL Analytics] A4T [!DNL Target] 报表查看数据。

## 其他资源

* [在单页应用程序中实施at.js 2.0](implement-atjs-20-in-a-single-page-application.md)
* [使用Adobe Target的单页应用程序可视化体验编辑器(SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
* [at.js的工作原理文档](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html?lang=en)
