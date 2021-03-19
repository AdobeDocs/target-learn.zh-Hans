---
title: 什么是Adobe Recommendations API?
description: 本教程指导开发人员通过实践，使用Adobe Target Recommendations API配置和管理Recommendations目录和自定义条件，以及使用投放 API检索推荐内容。
role: 开发人员
level: 中间
topic: 个性化、管理、集成、开发
feature: API/SDK、Recommendations、管理和配置、概述
doc-type: tutorial
kt: 3815
thumbnail: null
author: Judy Kim
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 1%

---


# Adobe Recommendations API概述

与[!DNL Recommendations]相关的API包括[管理API](https://docs.adobe.com/content/help/en/target/using/apis/api-overview.html)，允许您：

* 管理推荐产品或内容目录
* 管理[!DNL Recommendations]算法和活动

将[!DNL Target] [投放API](https://docs.adobe.com/content/help/en/target/using/apis/api-overview.html)与Recommendations一起使用，您还可以：

* 检索JSON、HTML或XML对象中的推荐，以便在Web、移动设备、电子邮件、物联网(IOT)和其他渠道中显示。

## 教程说明

本教程指导开发人员通过实践，使用[!DNL Recommendations] API配置和管理[!DNL Recommendations]目录和自定义条件，并使用投放 API检索推荐内容。 在本教程结束前，您将能够：

* 使用Recommendations API配置和管理实体
* 使用Recommendations API配置和管理自定义条件
* 了解如何将Recommendations与投放 API结合使用，以在非HTML设备中使用推荐

## 受众

本教程面向初次使用目标 API或Recommendations API的开发人员。

## 先决条件

使用目标管理API需要[Adobe身份验证设置](../apis/configure-io-target-integration.md)。 在开始本教程之前，请确保已配置此项。

## 资源

请注意以下资源，这些资源是理解本教程并成功遵循它所必需的：

| 资源 | 详细信息 |
| --- | --- |
| 邮递员 | 获取操作系统的[Postman应用程序](https://www.postman.com/downloads/)。 Postman Basic免费创建帐户。 Postman通常不需要使用Adobe Target API，但它使API工作流更简单，而Adobe Target提供了多个Postman集合来帮助执行其API并了解它们的操作方式。 本教程的其余部分假定是Postman的工作知识。 如需帮助，请参考[邮递员文档](https://learning.getpostman.com/)。 |
| 引用 | 在本教程的其余部分中，假定您熟悉以下资源：<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[目标Adobe I/O文档](https://developers.adobetarget.com/api/#introduction)</li><li>[Recommendations API文档](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

[下一个“管理Recommendations目录”>](manage-catalog.md)
