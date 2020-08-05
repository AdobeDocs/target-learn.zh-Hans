---
title: Adobe TargetAPI概述
keywords: recommendations;adobe recommendations;premium;api;apis
description: Adobe Target·Recommendations包含一组专用的API，允许您管理推荐产品和／或内容目录； 管理推荐算法和活动; 并在JSON、HTML或XML对象中提供推荐，以便在Web、移动、电子邮件、物联网和其他渠道中显示。
kt: null
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Adobe Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: b66dbae616c9559f5d1b7bbedf2d9b383840973b
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 2%

---


# Adobe TargetAPI概述

Adobe TargetAPI可以按类型进行分组。

| API 类型 | 它使您能够 | 下载链接 |
| --- | --- | --- |
| 管理员 | 创建、修改和删除活动、受众、优惠和其他对象( [!DNL Recommendations] 包括实体、标准、设计等)。 API [!DNL Recommendations] 是一种管理API类型。) | <UL><li>[目标管理员API邮递员集合](https://developers.adobetarget.com/api/#admin-postman-collection)</li><li>[RecommendationsAPI邮递员集](https://developers.adobetarget.com/api/recommendations/#section/Postman)</li></ul> |
| 交付 | 从中检索优化和个性化的 [!DNL Target] 内容，以便投放给最终用户。 | [目标投放API邮递员集合](https://developers.adobetarget.com/api/delivery-api/#section/Getting-Started/Postman-Collection) |
| 报表 | 导出活动结果和其他报告结果。 | 报告API包含在 [目标管理API邮递员集合中](https://developers.adobetarget.com/api/#admin-postman-collection)。 |
| Profile | 检索和修改存储在Adobe Target的用户用户档案。 | [目标用户档案API邮递员集合](https://developers.adobetarget.com/api/#profiles) |

请注意管理 **API** （包括API）与 [!DNL Recommendations] 投放API的区别 **，前者允许您配置Adobe Target的各个方面，后者则允许您检**&#x200B;索内容。 管理员API需要身份验证，而投放API则不需要。

要使用Adobe Target管理API，您首先需要使用AdobeI/O配置身份验证。

[下一个“配置身份验证”>](configure-io-target-integration.md)
