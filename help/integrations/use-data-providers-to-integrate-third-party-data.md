---
title: 如何使用数据提供商集成第三方数据
description: 本教程将向用户介绍数据提供程序。 了解如何使用数据提供商功能轻松将数据从第三方传递到Adobe Target。
role: User, Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: feature video
kt: null
author: Daniel Wright
exl-id: 1892136e-14e3-4e52-8b1f-aee806d2f83a
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 23%

---

# 使用数据提供商将第三方数据集成到Adobe Target

[!UICONTROL 数据提供程序是一项功能，允许您轻松地将数据从第三方传递到 Target。]第三方可以是气象服务、DMP，甚至是您自己的 Web 服务。然后，您可以使用这些数据来构建受众、定位内容并丰富访客配置文件。

>[!VIDEO](https://video.tv.adobe.com/v/22349/?quality=12)

## 如何使用数据提供程序

1. 实施专家在at.js之前（或在at.js的“库标题”部分中）添加代码，以便对第三方进行API调用，解析响应并使用名称/值对从响应中指定以发送到[!DNL Target]。
1. at.js可管理闪烁，并在全局Target请求中将名称/值对作为自定义参数包含在内。
1. 营销人员基于这些自定义参数在[!DNL Target]界面中构建受众。
1. 营销人员使用这些受众来定位体验、活动和量度，以及报表受众。

>[!NOTE]
>
>[!UICONTROL 数] 据提供程序需要at.js 1.3或更高版本

## 支持材料

* [在at.js和Adobe Target中实施数据提供程序](implement-data-providers-to-integrate-third-party-data.md)
* [数据提供程序文档](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html?lang=en#data-providers)
