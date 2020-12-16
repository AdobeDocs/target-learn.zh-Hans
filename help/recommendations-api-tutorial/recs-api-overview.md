---
title: Adobe RecommendationsAPI概述
keywords: recommendations;adobe recommendations;premium;api;apis
description: Adobe Target·Recommendations包含一组专用的API，允许您管理推荐产品和／或内容目录；管理推荐算法和活动;并在JSON、HTML或XML对象中提供推荐，以便在Web、移动、电子邮件、物联网和其他渠道中显示。
kt: 3815
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: c221f434ce9daec03dbb4d897343775b40b14462
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 1%

---


# Adobe RecommendationsAPI概述

与[!DNL Recommendations]相关的API包括允许您：[](https://docs.adobe.com/content/help/en/target/using/apis/api-overview.html)

* 管理推荐产品或内容目录
* 管理[!DNL Recommendations]算法和活动

将[!DNL Target] [投放API](https://docs.adobe.com/content/help/en/target/using/apis/api-overview.html)与Recommendations结合使用，您还可以：

* 检索JSON、HTML或XML对象中的推荐，以便在Web、移动、电子邮件、物联网(IOT)和其他渠道中显示。

## 教程说明

本教程指导开发人员通过实践，使用[!DNL Recommendations] API配置和管理[!DNL Recommendations]目录和自定义条件，以及使用投放API检索推荐内容。 在本教程结束时，您将能够：

* 使用RecommendationsAPI配置和管理实体
* 使用RecommendationsAPI配置和管理自定义条件
* 了解如何将Recommendations与投放API结合使用以在非HTML设备中使用建议

## 受众

本教程面向不熟悉目标API或RecommendationsAPI的开发人员。

## 先决条件

使用目标管理API需要[Adobe身份验证设置](../apis/configure-io-target-integration.md)。 请确保在开始本教程之前已配置此功能。

## 资源

请注意以下资源，这些资源是理解本教程并成功遵循它所必需的：

| 资源 | 详细信息 |
| --- | --- |
| 邮递员 | 获取操作系统的[邮递员应用程序](https://www.postman.com/downloads/)。 Postman Basic免费创建帐户。 虽然一般来说，使用Adobe TargetAPI并非必需，但邮递员使API工作流更加简单，而Adobe Target公司提供多个邮递员集合来帮助执行其API并了解它们的操作方式。 本教程的其余部分假定是邮递员的工作知识。 要获得帮助，请参考[邮递员文档](https://learning.getpostman.com/)。 |
| 引用 | 在本教程的其余部分中，假定您熟悉以下资源：<UL><li>[Adobe I/O·吉图布](https://github.com/adobeio)</li><li>[目标Adobe I/O文档](https://developers.adobetarget.com/api/#introduction)</li><li>[RecommendationsAPI文档](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

[下一个“管理您的Recommendations目录”>](manage-catalog.md)
