---
title: 什么是Adobe Recommendations API？
description: 本教程将指导开发人员完成使用Adobe Target Recommendations API配置和管理“推荐”目录和自定义标准以及使用交付API检索推荐内容的实践操作。
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration, Overview
doc-type: tutorial
kt: 3815
author: Judy Kim
exl-id: 10f80056-fb71-4362-86bc-d161f596cb91
source-git-commit: 542ff406fc24df54a2f1b007422492341ea46507
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 2%

---

# Adobe Recommendations API概述

与[!DNL Recommendations]相关的API包括[管理员API](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=zh-Hans)，它们允许您：

* 管理您的推荐产品或内容目录
* 管理[!DNL Recommendations]算法和活动

通过将[!DNL Target] [投放API](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=zh-Hans)与推荐一起使用，您还可以：

* 检索JSON、HTML或XML对象中的推荐，以便这些推荐可在Web、移动设备、电子邮件、物联网(IOT)和其他渠道中显示。

## 教程说明

本教程将指导开发人员使用[!DNL Recommendations] API配置和管理[!DNL Recommendations]目录和自定义标准以及使用交付API检索推荐内容的实践实践。 在本教程结束时，您将能够：

* 使用推荐API配置和管理实体
* 使用推荐API配置和管理自定义标准
* 了解如何将推荐与投放API结合使用，以在非HTML设备中使用推荐结果

## 受众

本教程面向不熟悉Target API或推荐API的开发人员。

## 先决条件

使用Target管理员API需要[Adobe身份验证设置](https://experienceleague.adobe.com/docs/target-dev/developer/api/configure-authentication.html?lang=zh-Hans){target="_blank"}。 在开始本教程之前，请确保已配置此设置。

## 资源

请注意以下资源，这些资源是理解本教程并成功遵循它所必需的：

| 资源 | 详细信息 |
| --- | --- |
| Postman | 获取适用于您的操作系统的[Postman应用程序](https://www.postman.com/downloads/)。 Postman basic可在创建帐户时免费使用。 虽然总体而言使用Adobe Target API不需要使用，但Postman简化了API工作流程，并且Adobe Target提供了多个Postman收藏集以帮助执行其API并了解其操作方式。 本教程的其余部分假定您了解Postman的工作知识。 如需帮助，请参阅[Postman文档](https://learning.getpostman.com/)。 |
| 引用 | 在本教程的其余部分中，我们假定您已熟悉以下资源：<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Target Adobe I/O文档](https://developers.adobetarget.com/api/#introduction)</li><li>[推荐API文档](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

[下一课程“管理您的推荐目录”>](https://experienceleague.adobe.com/docs/target-dev/developer/api/recommendations-api/manage-catalog.html?lang=zh-Hans){target="_blank"}
