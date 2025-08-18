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
source-git-commit: 80208b3ecbc0d627d2afe72f882e91c9800d2726
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# 实施[!UICONTROL Data Providers]以将第三方数据集成到Adobe Target中

有关如何使用Adobe Target的[!UICONTROL Data Providers]功能从第三方数据提供程序中检索数据并将其传递到Target请求的实施详细信息和示例。

>[!NOTE]
>
>[!UICONTROL Data Providers]需要`at.js` 1.3或更高版本

## 实施数据提供程序的基本组件

>[!VIDEO](https://video.tv.adobe.com/v/33359/?quality=12&captions=chi_hans)

简要概述`dataProvider`的基本组件以及如何按正确顺序获取代码。\
您可以在此处找到视频中使用的代码的工作示例：
[https://target.enablementadobe.com/data-providers/simple.html](https://target.enablementadobe.com/data-providers/simple.html)

## 与第三方API集成

>[!VIDEO](https://video.tv.adobe.com/v/33360?captions=chi_hans)

更实际的示例，即集成天气API。\
您可以在此处找到视频中使用的代码的工作示例：
[https://target.enablementadobe.com/data-providers/3rdparty.html](https://target.enablementadobe.com/data-providers/3rdparty.html)

## 与多个提供商集成

>[!VIDEO](https://video.tv.adobe.com/v/36824?captions=chi_hans)

如何将来自多个提供商的数据合并到您的全局[!DNL Target]请求中。\
您可以在此处找到视频中使用的代码的工作示例：
[https://target.enablementadobe.com/data-providers/combined.html](https://target.enablementadobe.com/data-providers/combined.html)

## 最大程度降低页面加载影响

>[!VIDEO](https://video.tv.adobe.com/v/36825?captions=chi_hans)

通过将数据存储到会话存储对象中，最大程度地减小对页面加载时间的影响。 或者，您可以使用前缀`profile.`将这些值作为配置文件参数进行传递，并且只需在会话的第一个[!DNL Target]请求中传递它们。 但是，每个请求只能传递50个配置文件参数。

可以在此处找到视频中使用的代码的工作示例：[https://target.enablementadobe.com/data-providers/reducedCalls.html](https://target.enablementadobe.com/data-providers/reducedCalls.html)

## 支持材料

* [将数据提供程序用于Adobe Target](use-data-providers-to-integrate-third-party-data.md)
