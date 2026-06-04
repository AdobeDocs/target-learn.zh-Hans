---
title: at.js 2.0如何工作？
description: 了解at.js 2.0如何增强Adobe Target对单页应用程序(SPA)的支持并与其他Experience Cloud解决方案集成。
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: 7f037665-88a7-469c-8df5-c82cb0f65382
TQID: https://experienceleague.adobe.com/yi78hasak-rtlhpCG4-UnewWXAwMfPZJSpw9sFzRenU
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: adee20bd-51f4-461d-b9db-d215f8756eebid: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: d3cdead0-685a-4489-9250-4bb709942f66id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: c0b4abf2d4ead4d58a8db6e8970857b7b50dbe5c
workflow-type: tm+mt
source-wordcount: 412
ht-degree: 0%

---

# 了解Adobe Target的at.js 2.0的工作原理

`at.js` 2.0增强了Adobe Target对单页应用程序(SPA)的支持并与其他Experience Cloud解决方案集成。 此视频和随附的图表说明了如何将所有内容组合在一起。

>[!VIDEO](https://video.tv.adobe.com/v/26250?quality=12)

## 架构图

![at.js 2.0在页面加载时的行为](assets/pageload.png)

1. 调用返回Experience Cloud ID (ECID)。 如果用户通过了身份验证，则另一调用会同步客户ID。

1. `at.js`库同步加载并隐藏文档正文（`at.js`也可以使用页面上实施的可选预隐藏代码片段异步加载）。

1. 将会发出页面加载请求，其中包括已配置的所有参数，如ECID、SDID和客户ID。

1. 配置文件脚本执行并进入[!UICONTROL 配置文件存储区]。 存储区向[!UICONTROL 受众库]请求符合条件的受众（例如从[!DNL Analytics]、Audience Manager等共享的受众）。 [!UICONTROL 客户属性]在批处理过程中发送到[!UICONTROL 配置文件存储区]。
1. 根据URL、请求参数和配置文件数据，[!DNL Target]可决定哪些活动和体验可返回给当前页面和未来视图的访客

1. 目标内容会发送回页面，其中可能包含其他个性化的配置文件值。

   当前页面上的目标内容会在默认内容不发生闪烁的情况下尽快显示。

   单页应用程序的未来视图的目标内容将缓存在浏览器中，因此当视图触发时，可以立即应用它而无需额外的服务器调用。 （有关`triggerView()`行为，请参阅下图）。

1. 从页面向[!UICONTROL 数据收集]服务器发送的[!DNL Analytics]数据
1. [!DNL Target]数据通过SDID匹配到Analytics数据，并且已处理到[!DNL Analytics]报表存储中。 然后，便可以在[!DNL Analytics]和[!DNL Target]中通过A4T报表查看[!DNL Analytics]数据。

使用triggerView()函数时的![at.js 2.0行为](assets/triggerview.png)

1. 在单页应用程序中调用`adobe.target.triggerView()`
1. 从缓存中读取视图的目标内容

1. 目标内容会在默认内容不发生闪烁的情况下尽快显示

1. 通知请求将发送到[!DNL Target] [!UICONTROL 配置文件存储区]以计算活动中的访客和递增量度
1. [!DNL Analytics]数据从SPA发送到[!UICONTROL 数据收集]服务器

1. [!DNL Target]数据从[!DNL Target]后端发送到[!UICONTROL 数据收集]服务器。 [!DNL Target]数据通过SDID与[!DNL Analytics]数据匹配，并且已处理到[!DNL Analytics]报表存储中。 然后，便可以在[!DNL Analytics]和[!DNL Target]中通过A4T报表查看[!DNL Analytics]数据。

## 其他资源

* [在单页应用程序中实施at.js 2.0](implement-atjs-20-in-a-single-page-application.md)
* [使用Adobe Target的可视化体验编辑器处理单页应用程序(SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
