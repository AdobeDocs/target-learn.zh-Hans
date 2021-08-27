---
title: 如何实施数据提供商以集成第三方数据
description: 本教程提供了实施详细信息和示例，说明如何使用Adobe Target的数据提供程序功能从第三方数据提供程序中检索数据，并在Target请求中传递该数据。
role: Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: technical video
kt: null
thumbnail: null
author: Daniel Wright
exl-id: fcf6d1a8-e2a7-41ce-9c1c-02985b7afb5a
source-git-commit: d1517f0763290eb61a9e4eef4f2eb215a9cdd667
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# 实施[!UICONTROL 数据提供程序]以将第三方数据集成到Adobe Target

有关如何使用Adobe Target的[!UICONTROL 数据提供程序]功能从第三方数据提供程序中检索数据并在Target请求中传递数据的实施详细信息和示例。

>[!NOTE]
>
>[!UICONTROL 数] 据提供 `at.js` 程序要求1.3或更高版本

## 实施数据提供程序的基本组件

>[!VIDEO](https://video.tv.adobe.com/v/22348/?quality=12)

`dataProvider`的基本组件以及如何按正确顺序获取代码的快速概述。\
有关视频中使用的代码的有效示例，请参阅此处：
[https://target.enablementadobe.com/data-providers/simple.html](https://target.enablementadobe.com/data-providers/simple.html)

## 与第三方API集成

>[!VIDEO](https://video.tv.adobe.com/v/22345/)

一个更现实的示例，集成天气API。\
有关视频中使用的代码的有效示例，请参阅此处：
[https://target.enablementadobe.com/data-providers/3rdparty.html](https://target.enablementadobe.com/data-providers/3rdparty.html)

## 与多个提供程序集成

>[!VIDEO](https://video.tv.adobe.com/v/22346/)

如何将来自多个提供程序的数据合并到全局[!DNL Target]请求中。\
有关视频中使用的代码的有效示例，请参阅此处：
[https://target.enablementadobe.com/data-providers/combined.html](https://target.enablementadobe.com/data-providers/combined.html)

## 最大限度地降低页面加载影响

>[!VIDEO](https://video.tv.adobe.com/v/22347/)

通过在会话存储对象中存储数据，最大限度地减少对页面加载时间的影响。 或者，您也可以使用`profile.`前缀将值作为配置文件参数进行传递，并在会话的第一个[!DNL Target]请求中进行传递。 但是，每个请求只能传递50个配置文件参数。

有关视频中使用的代码的有效示例，请参阅此处：[https://target.enablementadobe.com/data-providers/reducedCalls.html](https://target.enablementadobe.com/data-providers/reducedCalls.html)

## 支持材料

* [将数据提供程序与Adobe Target结合使用](use-data-providers-to-integrate-third-party-data.md)

* [数据提供程序文档](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html?lang=en#data-providers)
