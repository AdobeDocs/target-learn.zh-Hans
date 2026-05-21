---
title: 如何实施数据提供程序以集成第三方数据
description: 本教程提供了实施详细信息和示例，说明如何使用Adobe Target的数据提供程序功能从第三方数据提供程序中检索数据，并将其传递到Target请求。
role: Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: fcf6d1a8-e2a7-41ce-9c1c-02985b7afb5a
TQID: https://experienceleague.adobe.com/Oh0ngUGA-ZfpPHnQnN0VRgUG1ta4yqg8Pfm8mhCZTN0
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ceid: f7c7de77-382f-4f48-8b36-61a170f06d3d
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: c0b4abf2d4ead4d58a8db6e8970857b7b50dbe5c
workflow-type: tm+mt
source-wordcount: 293
ht-degree: 0%

---

# 实施[!UICONTROL Data Providers]以将第三方数据集成到Adobe Target中

有关如何使用Adobe Target的[!UICONTROL Data Providers]功能从第三方数据提供程序中检索数据并将其传递到Target请求的实施详细信息和示例。

>[!NOTE]
>
>[!UICONTROL Data Providers]需要`at.js` 1.3或更高版本

## 实施数据提供程序的基本组件

>[!VIDEO](https://video.tv.adobe.com/v/22348/?quality=12)

简要概述`dataProvider`的基本组件以及如何按正确顺序获取代码。\
您可以在此处找到视频中使用的代码的工作示例：
[https://target.enablementadobe.com/data-providers/simple.html](https://target.enablementadobe.com/data-providers/simple.html)

## 与第三方API集成

>[!VIDEO](https://video.tv.adobe.com/v/22345/)

更实际的示例，即集成天气API。\
您可以在此处找到视频中使用的代码的工作示例：
[https://target.enablementadobe.com/data-providers/3rdparty.html](https://target.enablementadobe.com/data-providers/3rdparty.html)

## 与多个提供商集成

>[!VIDEO](https://video.tv.adobe.com/v/22346/)

如何将来自多个提供商的数据合并到您的全局[!DNL Target]请求中。\
您可以在此处找到视频中使用的代码的工作示例：
[https://target.enablementadobe.com/data-providers/combined.html](https://target.enablementadobe.com/data-providers/combined.html)

## 最大程度降低页面加载影响

>[!VIDEO](https://video.tv.adobe.com/v/22347/)

通过将数据存储到会话存储对象中，最大程度地减小对页面加载时间的影响。 或者，您可以使用前缀`profile.`将这些值作为配置文件参数进行传递，并且只需在会话的第一个[!DNL Target]请求中传递它们。 但是，每个请求只能传递50个配置文件参数。

可以在此处找到视频中使用的代码的工作示例：[https://target.enablementadobe.com/data-providers/reducedCalls.html](https://target.enablementadobe.com/data-providers/reducedCalls.html)

## 支持材料

* [将数据提供程序用于Adobe Target](use-data-providers-to-integrate-third-party-data.md)
