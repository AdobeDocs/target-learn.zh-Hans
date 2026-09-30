---
title: 如何使用数据提供程序集成第三方数据
description: 本教程向用户介绍数据提供程序。 了解如何使用数据提供商功能轻松地将数据从第三方传递到Adobe Target。
role: User, Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: feature video
kt:
author: Daniel Wright
exl-id: 1892136e-14e3-4e52-8b1f-aee806d2f83a
TQID: 'https://experienceleague.adobe.com/XiUlJGHSFVxAMqdl6Y7hK9PoXOgiiUI43vrFeAj2Rpo'
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
    internal-label: Audiences
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
    internal-label: Implementation
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
    internal-label: Integrations
  - id: a19e8738-9679-599a-b83b-5f2f15f8e4d6
    internal-label: APIs/SDKs
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
    internal-label: at.js
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
    internal-label: Experienced
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
source-git-commit: d11449f8685d14c2bbd1e70f80711d4edab9d3a1
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 16%
---
# 使用数据提供程序将第三方数据集成到Adobe Target

[!UICONTROL 数据提供程序]是一种功能，可让您轻松地将数据从第三方传递到Target。  第三方可以是气象服务、DMP，甚至是您自己的 Web 服务。 然后，您可以使用这些数据来构建受众、定位内容并丰富访客配置文件。

>[!VIDEO](https://video.tv.adobe.com/v/22349/?quality=12)

## 如何使用数据提供程序

1. 实施专家在at.js之前添加代码（或在at.js的Library Header部分中添加代码），以便向第三方发起API调用、解析响应并从响应中指定名称/值对以发送到[!DNL Target]。
1. at.js可管理闪烁，并在全局Target请求中包含名称/值对作为自定义参数。
1. 营销人员根据这些自定义参数在[!DNL Target]界面中构建受众。
1. 营销人员使用这些受众来定位体验、活动和量度以及报表受众。

>[!NOTE]
>
>[!UICONTROL 数据提供程序]需要at.js 1.3或更高版本

## 支持材料

* [在at.js和Adobe Target中实施数据提供程序](implement-data-providers-to-integrate-third-party-data.md)
