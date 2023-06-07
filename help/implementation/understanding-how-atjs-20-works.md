---
title: at.js 2.0如何工作？
description: at.js 2.0增强了Adobe Target对单页应用程序(SPA)的支持，并与其他Experience Cloud解决方案集成。 此视频和随附的图表说明了所有内容是如何组合在一起的。
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: 7f037665-88a7-469c-8df5-c82cb0f65382
source-git-commit: 80208b3ecbc0d627d2afe72f882e91c9800d2726
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 12%

---

# 了解Adobe Target at.js 2.0的工作原理

`at.js` 2.0增强了Adobe Target对单页应用程序(SPA)的支持，并与其他Experience Cloud解决方案集成。 此视频和随附的图表说明了所有内容是如何组合在一起的。

>[!VIDEO](https://video.tv.adobe.com/v/26250?quality=12)

## 架构图

![at.js 2.0页面加载行为](assets/pageload.png)

1. 调用返回Experience CloudID (ECID)。 如果用户通过了身份验证，则另一调用会同步客户ID。

1. `at.js` 库同步加载并隐藏文档正文(`at.js` 也可以使用页面上实施的可选预隐藏代码片段来异步加载)。

1. 发出页面加载请求，其中包括已配置的所有参数、ECID、SDID和客户ID。

1. 配置文件脚本执行并注入到 [!UICONTROL 配置文件存储]. 存储区会从 [!UICONTROL 受众库] (例如，从共享的受众 [!DNL Analytics]、Audience Manager等)。 [!UICONTROL 客户属性] 发送至 [!UICONTROL 配置文件存储] 批处理。
1. 根据URL、请求参数和配置文件数据， [!DNL Target] 决定可为访客返回哪些当前页面和未来视图的活动和体验

1. 目标内容发送回页面，其中可能包括其他个性化的配置文件值。

   当前页面上的目标内容会在默认内容不发生闪烁的情况下尽快显示。

   单页应用程序的未来视图的目标内容会缓存在浏览器中，因此可以在触发视图时即时应用，而无需额外的服务器调用。 (参见下图，了解 `triggerView()` 行为)。

1. [!DNL Analytics] 从页面发送至 [!UICONTROL 数据收集] 服务器
1. [!DNL Target] 数据会通过 SDID 匹配到 数据，并且会进行相应处理以保存到 Analytics 报表存储中。[!DNL Analytics][!DNL Analytics] 然后，便可以在以下两个位置查看数据 [!DNL Analytics] 和 [!DNL Target] 通过A4T报表。

![使用triggerView()函数时的at.js 2.0行为](assets/triggerview.png)

1. `adobe.target.triggerView()` 在单页应用程序中调用
1. 从缓存中读取视图的目标内容

1. 目标内容会在默认内容不发生闪烁的情况下尽快显示

1. 通知请求发送至 [!DNL Target] [!UICONTROL 配置文件存储] 以计算活动中的访客数并递增量度
1. [!DNL Analytics] 数据从SPA发送到 [!UICONTROL 数据收集] 服务器

1. [!DNL Target] 数据发送自 [!DNL Target] 后端到 [!UICONTROL 数据收集] 服务器。 [!DNL Target] 数据会通过 SDID 匹配到 [!DNL Analytics] 数据，并且会进行相应处理以保存到 [!DNL Analytics] 报表存储中。[!DNL Analytics] 然后，便可以在以下两个位置查看数据 [!DNL Analytics] 和 [!DNL Target] 通过A4T报表。

## 其他资源

* [在单页应用程序中实施at.js 2.0](implement-atjs-20-in-a-single-page-application.md)
* [使用Adobe Target的可视化单页应用程序体验编辑器(SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
