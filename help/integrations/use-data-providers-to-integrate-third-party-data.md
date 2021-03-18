---
title: 如何使用数据提供商集成第三方数据
description: 本教程向数据提供者介绍用户。 了解如何使用数据提供商功能轻松将数据从第三方传递到Adobe Target。
role: 商业从业者，开发人员
level: 富有经验
topic: 个性化、集成
feature: 实施、集成、API/SDK
doc-type: feature video
kt: null
thumbnail: null
author: Daniel Wright
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 22%

---


# 使用数据提供商将第三方数据集成到Adobe Target

[!UICONTROL 数据提供程序是一项功能，允许您轻松地将数据从第三方传递到 Target。]第三方可以是气象服务、DMP，甚至是您自己的 Web 服务。然后，您可以使用这些数据来构建受众、定位内容并丰富访客配置文件。

>[!VIDEO](https://video.tv.adobe.com/v/22349/?quality=12)

## 如何使用数据提供者

1. 实施专家在at.js（或在at.js的“库头”部分）之前添加代码，该代码对第三方进行API调用，解析响应，并指定从响应发送到[!DNL Target]的名称/值对。
1. at.js管理闪烁，并在全局目标请求中将名称/值对作为自定义参数。
1. Marketer根据这些自定义参数在[!DNL Target]界面中构建受众。
1. 营销人员使用这些受众来目标体验、活动和指标以及报告受众。

>[!NOTE]
>
>[!UICONTROL 数] 据提供程序要求at.js 1.3或更高版本

## 支持材料

* [在at.js和Adobe Target中实施数据提供程序](implement-data-providers-to-integrate-third-party-data.md)
* [数据提供商文档](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/targetgobalsettings.html#data-providers)