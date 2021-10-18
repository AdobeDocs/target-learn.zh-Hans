---
title: 什么是Adobe Recommendations API?
description: 本教程将指导开发人员通过实践，使用Adobe Target Recommendations API配置和管理Recommendations目录和自定义标准，以及使用交付API检索推荐内容。
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration, Overview
doc-type: tutorial
kt: 3815
author: Judy Kim
exl-id: 10f80056-fb71-4362-86bc-d161f596cb91
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 3%

---

# Adobe Recommendations API概述

与[!DNL Recommendations]相关的API包括[管理员API](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=en)，允许您：

* 管理可推荐产品或内容的目录
* 管理[!DNL Recommendations]算法和活动

将[!DNL Target] [交付API](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=en)与Recommendations结合使用，您还可以：

* 在JSON、HTML或XML对象中检索推荐，以便它们可以在Web、移动设备、电子邮件、物联网(IOT)和其他渠道中显示。

## 教程说明

本教程将指导开发人员实践使用[!DNL Recommendations] API配置和管理[!DNL Recommendations]目录和自定义标准，以及使用交付API检索推荐内容。 在本教程结束时，您将能够：

* 使用Recommendations API配置和管理实体
* 使用Recommendations API配置和管理自定义标准
* 了解如何将Recommendations与交付API结合使用以在非HTML设备中使用推荐

## 受众

本教程面向不熟悉Target API或Recommendations API的开发人员。

## 先决条件

使用Target管理员API需要[Adobe身份验证设置](../apis/configure-io-target-integration.md)。 请确保在开始本教程之前已配置此功能。

## 资源

请注意以下资源，这些资源是了解本教程并成功遵循该教程所必需的：

| 资源 | 详细信息 |
| --- | --- |
| 邮递员 | 获取操作系统的[Postman应用程序](https://www.postman.com/downloads/)。 Postman Basic免费创建帐户。 虽然通常使用Adobe Target API并非必需，但Postman可简化API工作流程，Adobe Target提供了多个Postman集合来帮助执行其API并了解它们的操作方式。 本教程的其余部分假定您具有Postman的工作知识。 如需帮助，请参阅[Postman文档](https://learning.getpostman.com/)。 |
| 引用 | 在本教程的其余部分中，我们假定您熟悉以下资源：<UL><li>[Adobe I/OGithub](https://github.com/adobeio)</li><li>[TargetAdobe I/O文档](https://developers.adobetarget.com/api/#introduction)</li><li>[Recommendations API文档](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

[下一课程“管理Recommendations目录”>](manage-catalog.md)
