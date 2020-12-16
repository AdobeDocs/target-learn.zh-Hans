---
title: Adobe Target，带AdobeMobile Services SDK v4 for Android
description: Adobe TargetAdobeMobile Services SDK v4 for Android是Android开发人员的理想起点，他们已经在使用AdobeMobile Services SDK v4并希望开始与Adobe Target的个性化应用程序体验。
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: d6cedd55dcc9c08d2d2ca5709e15fe5ea9fab8b8
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 2%

---


# Adobe Target,AdobeMobile Services SDK v4 for Android —— 概述

_Adobe Target公司为Android提供AdobeMobile Services SDK v4,_ 对于已经使用AdobeMobile Services SDK v4并希望与Adobe Target开始个性化应用程序体验的Android开发人员来说，这是一个完美的起点。

您可以使用演示版Android应用程序完成课程。 完成本教程后，您应准备好开始在您自己的Android应用程序中实施[!DNL Target]!

完成此教程后，您将能够：

* 验证[AdobeMobile Services SDK](https://docs.adobe.com/content/help/en/mobile-services/android/getting-started-android/requirements.html)设置
* 实现以下类型的[!DNL Target]请求：
   * [!DNL Target]内容的预取
   * 在单个请求中批处理多个[!DNL Target]位置(mbox)
   * 阻止请求（在应用程序显示前运行）
   * 非阻止请求（在后台运行）
   * 实时（非缓存）
   * 缓存破坏重取
* 为请求添加参数以增强个性化
* 创建受众和优惠
* 个性化布局
* 推出功能标记的新功能

## 先决条件

在这些教训中，我们假定您：

* 拥有AdobeID和审批者级别的Adobe Target界面访问权限（请参阅下面的验证步骤）
* 了解您的Adobe Target客户代码，以便向您自己的帐户提出请求。 客户端代码显示在Adobe的Adobe Target   “设置”>“实施”>“编辑at.js设置”屏幕
* 访问并熟悉[Mobile Services用户界面](https://mobilemarketing.adobe.com)
* 拥有用于Android移动应用程序开发的IDE。 本教程以各种步骤和截屏功能提供[Android Studio](https://developer.android.com/studio/install)

如果您没有访问Experience Cloud解决方案所需的权限，请联系您的Experience Cloud管理员。

此外，还假定您熟悉Java中的Android开发。 您不需要成为Java专家来完成课程，但如果您能轻松阅读和理解代码，您会从中获得更多的帮助。

### 验证访问Adobe Target

这一教训需要我们去Adobe Target。 在完成后续步骤之前，请执行以下操作，确保您有权访问Adobe Target:

1. 登录[Adobe Experience Cloud](https://experience.adobe.com/)
1. 在Experience Cloud主屏幕中，单击[!DNL Target]:
   ![Experience Cloud主屏幕](assets/aec_homeScreen_clickTarget.png)
1. 如下图所示，您应该访问Adobe Target的活动列表，并且您应该看到您的用户具有审批者级别的访问权限。 如果您无法访问[!DNL Target]或无法验证审批者级别的访问权限，请联系您的公司的Experience Cloud管理员，请请求此访问权限，并在授予此权限后继续本教程：

   ![AdobeUI](assets/targetUI_approver.png)

## 关于课程

在这些课程中，您将使用您自己的Adobe Target帐户将Adobe Target应用程序实施到名为“We.Travel”的演示旅行应用中。 在教程结束时，您将根据用户对应用程序的使用情况向用户发送个性化消息！ 最终的个性化体验将如下所示：

![We.Travel应用程序最终版](assets/overview_final_result.jpg)

在We.Travel应用程序中完成实施后，您将能够在自己的移动应用程序中使用[!DNL Target]进行开始。

开始吧！

**[下一个：“下载并更新示例应用程序”>](download-and-update-the-sample-app.md)**
