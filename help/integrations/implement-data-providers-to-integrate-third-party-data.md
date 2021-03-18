---
title: 如何实施数据提供商集成第三方数据
description: 本教程提供了实施详细信息和示例，说明如何使用Adobe Target的数据提供程序功能从第三方数据提供程序检索数据并在目标请求中传递数据。
role: 开发人员
level: 富有经验
topic: 个性化、集成
feature: 实施、集成、API/SDK
doc-type: technical video
kt: null
thumbnail: null
author: Daniel Wright
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# 实施[!UICONTROL 数据提供者]以将第三方数据集成到Adobe Target

实施详细信息和示例，说明如何使用Adobe Target的[!UICONTROL 数据提供者]功能从第三方数据提供者检索数据并在目标请求中传递数据。

>[!NOTE]
>
>[!UICONTROL 数据] 提供 `at.js` 程序要求1.3或更高版本

## 实施数据提供者的基本组件

>[!VIDEO](https://video.tv.adobe.com/v/22348/?quality=12)

`dataProvider`的基本组件以及如何按正确顺序获取代码的快速概述。\
有关视频中使用的代码的有效示例，请参阅：
[https://target.enablementadobe.com/data-providers/simple.html](https://target.enablementadobe.com/data-providers/simple.html)

## 与第三方API集成

>[!VIDEO](https://video.tv.adobe.com/v/22345/)

一个更真实的示例，集成天气API。\
有关视频中使用的代码的有效示例，请参阅：
[https://target.enablementadobe.com/data-providers/3rdparty.html](https://target.enablementadobe.com/data-providers/3rdparty.html)

## 与多个提供商集成

>[!VIDEO](https://video.tv.adobe.com/v/22346/)

如何将来自多个提供程序的数据合并到全局[!DNL Target]请求中。\
有关视频中使用的代码的有效示例，请参阅：
[https://target.enablementadobe.com/data-providers/combined.html](https://target.enablementadobe.com/data-providers/combined.html)

## 最小化页面加载影响

>[!VIDEO](https://video.tv.adobe.com/v/22347/)

通过将数据存储在会话存储对象中，最大限度地减少对页面加载时间的影响。 或者，您也可以使用`profile.`前缀将这些值作为用户档案参数传递，并在会话的第一个[!DNL Target]请求中传递它们。 但是，每个请求只能传递50个用户档案参数。

有关视频中使用的代码的有效示例，请参阅：[https://target.enablementadobe.com/data-providers/reducedCalls.html](https://target.enablementadobe.com/data-providers/reducedCalls.html)

## 支持材料

* [将数据提供者与Adobe Target](use-data-providers-to-integrate-third-party-data.md)

* [数据提供商文档](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/targetgobalsettings.html#data-providers)