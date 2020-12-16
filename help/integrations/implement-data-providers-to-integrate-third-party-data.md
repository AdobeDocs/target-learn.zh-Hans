---
title: 实施数据提供商以将第三方数据集成到Adobe Target
seo-title: 实施数据提供商以将第三方数据集成到Adobe Target
description: 实施细节和如何使用Adobe Target数据提供者功能从第三方数据提供者检索数据并在目标请求中传递数据的示例。
audience: developer
difficulty: 5
author: Daniel Wright
doc-type: implement
activity-type: technical-video
translation-type: tm+mt
source-git-commit: 37443ae4c1cdda387c8db0053201d520fa1ec224
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# 实施[!UICONTROL 数据提供者]以将第三方数据集成到Adobe Target

实施细节和如何使用Adobe Target[!UICONTROL 数据提供者]功能从第三方数据提供者检索数据并在目标请求中传递数据的示例。

>[!NOTE]
>
>[!UICONTROL 数据] 提供 `at.js` 程序需要1.3或更高版本

## 实施数据提供者的基本组件

>[!VIDEO](https://video.tv.adobe.com/v/22348/?quality=12)

快速概述`dataProvider`的基本组件以及如何按正确的顺序获取代码。\
有关视频中使用的代码的有效示例，请参阅：
[https://target.enablementadobe.com/data-providers/simple.html](https://target.enablementadobe.com/data-providers/simple.html)

## 与第三方API集成

>[!VIDEO](https://video.tv.adobe.com/v/22345/)

一个更真实的示例，集成天气API。\
有关视频中使用的代码的有效示例，请参阅：
[https://target.enablementadobe.com/data-providers/3rdparty.html](https://target.enablementadobe.com/data-providers/3rdparty.html)

## 与多个提供商集成

>[!VIDEO](https://video.tv.adobe.com/v/22346/)

如何将来自多个提供程序的数据并入全局[!DNL Target]请求中。\
有关视频中使用的代码的有效示例，请参阅：
[https://target.enablementadobe.com/data-providers/combined.html](https://target.enablementadobe.com/data-providers/combined.html)

## 最小化页面加载影响

>[!VIDEO](https://video.tv.adobe.com/v/22347/)

通过将数据存储在会话存储对象中，将对页面加载时间的影响降至最低。 或者，您也可以使用`profile.`前缀将这些值作为用户档案参数进行传递，并在会话的第一个[!DNL Target]请求中传递它们。 但是，每个请求只能传递50个用户档案参数。

有关视频中使用的代码的有效示例，请参阅：[https://target.enablementadobe.com/data-providers/reducedCalls.html](https://target.enablementadobe.com/data-providers/reducedCalls.html)

## 支持材料

* [将数据提供商与Adobe Target](use-data-providers-to-integrate-third-party-data.md)

* [数据提供者文档](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/targetgobalsettings.html#data-providers)