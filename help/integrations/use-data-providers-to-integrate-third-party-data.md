---
title: 使用数据提供者将第三方数据集成到Adobe Target
seo-title: 使用数据提供者将第三方数据集成到Adobe Target
description: 数据提供程序是一项功能，允许您轻松地将数据从第三方传递到 Target。第三方可以是气象服务、DMP，甚至是您自己的 Web 服务。然后，您可以使用这些数据来构建受众、定位内容并丰富访客配置文件。
audience: marketer
difficulty: 5
author: Daniel Wright
doc-type: use
activity-type: feature-video
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 40%

---


# 使用数据提供者将第三方数据集成到Adobe Target

[!UICONTROL 数据提供程序是一项功能，允许您轻松地将数据从第三方传递到 Target。]第三方可以是气象服务、DMP，甚至是您自己的 Web 服务。然后，您可以使用这些数据来构建受众、定位内容并丰富访客配置文件。

>[!VIDEO](https://video.tv.adobe.com/v/22349/?quality=12)

## 如何使用数据提供者

1. 实施专家在at.js之前（或在at.js的“库头”部分）添加代码，该代码对第三方进行API调用，分析响应，并从要发送的响应中指定名称／值对 [!DNL Target]。
1. at.js管理闪烁，并在全局目标请求中将名称／值对作为自定义参数。
1. 营销人员根据这些自 [!DNL Target] 定义参数在界面中构建受众。
1. 营销人员使用这些受众来目标体验、活动和指标，以及报告受众。

>[!NOTE]
>
>[!UICONTROL 数据提供者] 需要at.js 1.3或更高版本

## 支持材料

* [在at.js和Adobe Target中实施数据提供者](implement-data-providers-to-integrate-third-party-data.md)
* [数据提供者文档](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/targetgobalsettings.html#data-providers)