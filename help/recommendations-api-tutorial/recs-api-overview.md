---
title: Adobe RecommendationsAPI概述
keywords: recommendations;adobe recommendations;premium;api;apis
description: Adobe Target·Recommendations包含一组专用的API，允许您管理推荐产品和／或内容目录； 管理推荐算法和活动; 并在JSON、HTML或XML对象中提供推荐，以便在Web、移动、电子邮件、物联网和其他渠道中显示。
kt: 3815
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Adobe Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: 78b30bc0018527f9d8b2a5b50edee86e877d14c7
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 1%

---


# Adobe RecommendationsAPI概述

与包含管 [!DNL Recommendations] 理 [API相关](https://docs.adobe.com/content/help/en/target-learn/apis/api-overview.md) 的API，允许您：

* 管理推荐产品或内容目录
* 管理算 [!DNL Recommendations] 法和活动

将投放 [!DNL Target] API [与Recommendations一起](https://docs.adobe.com/content/help/en/target-learn/apis/api-overview.md) ，您还可以：

* 检索JSON、HTML或XML对象中的推荐，以便在Web、移动、电子邮件、物联网(IOT)和其他渠道中显示。

## 教程说明

本教程指导开发人员实践使用API [!DNL Recommendations] 配置和管理目 [!DNL Recommendations] 录和自定义条件，以及使用投放API检索推荐内容。 在本教程结束时，您将能够：

* 使用RecommendationsAPI配置和管理实体
* 使用RecommendationsAPI配置和管理自定义条件
* 了解如何将Recommendations与投放API结合使用以在非HTML设备中使用建议

## 受众

本教程面向不熟悉目标API或RecommendationsAPI的开发人员。

## 先决条件

使用目标管理员API需要 [Adobe身份验证设置](../apis/configure-io-target-integration.md)。 请确保在开始本教程之前已配置此功能。

## 资源

请注意以下资源，这些资源是理解本教程并成功遵循它所必需的：

| 资源 | 详细信息 |
| --- | --- |
| 邮递员 | 获取适 [用于您的操作](https://www.postman.com/downloads/) 系统的Postman应用程序。 Postman Basic免费创建帐户。 虽然一般来说，使用Adobe TargetAPI并非必需，但邮递员使API工作流更加简单，而Adobe Target公司提供多个邮递员集合来帮助执行其API并了解它们的操作方式。 本教程的其余部分假定是邮递员的工作知识。 要获得帮助，请参考邮 [递员文档](https://learning.getpostman.com/)。 |
| 引用 | 在本教程的其余部分中，假定您熟悉以下资源：<UL><li>[AdobeI/O Github](https://github.com/adobeio)</li><li>[目标AdobeI/O文档](https://developers.adobetarget.com/api/#introduction)</li><li>[RecommendationsAPI文档](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

[下一个“管理您的Recommendations目录”>](manage-catalog.md)
