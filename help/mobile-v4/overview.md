---
title: 带有适用于Android的AdobeMobile Services SDK v4的Adobe Target
description: 对于已经在使用AdobeMobile Services SDK v4，并且希望开始使用Android提供个性化应用程序体验的Android开发人员而言，具有适用于Adobe的Adobe Target Mobile Services SDK v4的Adobe Target是一个完美起点。
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile, Overview
doc-type: tutorial
kt: 3040
exl-id: 20f8ed4f-a86d-4c5e-9296-71a93724caa3
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 2%

---

# 带有适用于Android的AdobeMobile Services SDK v4的Adobe Target — 概述

对于已经在使用AdobeMobile Services SDK v4且希望开始使用Adobe Target进行个性化的Android应用程序体验的Android开发人员而言，_具有适用于Adobe Target的AdobeMobile Services SDK v4的是最佳起点。_

我们为您提供了Android演示应用程序来完成课程。 完成本教程后，您应该可以在自己的Android应用程序中开始实施[!DNL Target]！

完成此教程后，您将能够：

* 验证[AdobeMobile Services SDK](https://experienceleague.adobe.com/docs/mobile-services/android/getting-started-android/requirements.html?lang=en)安装程序
* 实施以下类型的[!DNL Target]请求：
   * 预取[!DNL Target]内容
   * 在单个请求中批处理多个[!DNL Target]位置(mbox)
   * 阻止请求（在应用程序显示之前运行）
   * 非阻塞请求（在后台运行）
   * 实时（非缓存）
   * Cache-busting重新获取
* 向增强个性化请求添加参数
* 创建受众和选件
* 个性化布局
* 推出具有功能标记的新功能

## 先决条件

在这些课程中，假定您：

* 拥有Adobe Target界面的AdobeID和审批者级别访问权限（请参阅下面的验证步骤）
* 了解您的Adobe Target客户端代码，以便能够向自己的帐户发出请求。 客户端代码显示在上的Adobe Target界面中。   “设置”>“实施”>“编辑at.js设置”屏幕
* 有权访问并熟悉[Mobile Services用户界面](https://mobilemarketing.adobe.com/)
* 拥有用于Android移动应用程序开发的IDE。 本教程在各个步骤和屏幕截图中都介绍了[Android Studio](https://developer.android.com/studio/install)

如果您没有访问Experience Cloud解决方案所需的权限，请联系您的Experience Cloud管理员。

此外，我们还假定您熟悉Java中的Android开发。 您无需成为Java专家即可完成课程，但如果您能够轻松阅读和理解代码，将可从这些课程中学到更多知识。

### 验证对Adobe Target的访问权限

本课程需要访问Adobe Target。 在继续后续步骤之前，请执行以下操作以确保您有权访问Adobe Target：

1. 登录[Adobe Experience Cloud](https://experience.adobe.com/)
1. 在Experience Cloud主屏幕中，单击[!DNL Target]：
   ![Experience Cloud主屏幕](assets/aec_homeScreen_clickTarget.png)
1. 您应该转到Adobe Target中的“活动”列表，如下图所示，并且您应该看到用户具有审批者级别的访问权限。 如果您无法访问[!DNL Target]或无法验证审批者级别的访问权限，请联系您公司的某个Experience Cloud管理员，请求此访问权限，并在获得授权后继续学习本教程：

   ![Adobe的UI](assets/targetUI_approver.png)

## 关于课程

在这些课程中，您将使用自己的Adobe Target帐户将Adobe Target实施到名为“We.Travel”的演示旅游应用程序中。 在本教程结束时，您将根据用户对该应用程序的使用情况，向用户发送个性化的消息！ 最终的个性化体验将如下所示：

![We.Travel应用最终](assets/overview_final_result.jpg)

浏览We.Travel应用程序中的实施后，您将能够在自己的移动应用程序中使用[!DNL Target]。

让我们开始吧！

**[下一步：“下载并更新示例应用程序”>](download-and-update-the-sample-app.md)**
