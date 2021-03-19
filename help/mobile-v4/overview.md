---
title: Adobe Target，带Adobe Mobile Services SDK v4 for Android
description: Adobe Target with Adobe Mobile Services SDK v4 for Android是Android开发人员的绝佳起点，他们已经在使用Adobe Mobile Services SDK v4，并且希望使用Adobe Target开始个性化应用程序体验。
role: 开发人员
level: 中间
topic: 移动、个性化
feature: 实施移动，概述
doc-type: tutorial
kt: 3040
thumbnail: null
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 2%

---


# Adobe Target with Adobe Mobile Services SDK v4 for Android — 概述

_Adobe Target with Adobe Mobile Services SDK v4 for_ Android是Android开发人员的绝佳起点，他们已经在使用Adobe Mobile Services SDK v4，并希望使用Adobe Target开始个性化应用程序体验。

您可以使用Android演示应用程序完成课程。 完成本教程后，您应准备好在自己的Android应用程序中实现[!DNL Target]的开始!

完成此教程后，您将能够：

* 验证[Adobe Mobile Services SDK](https://docs.adobe.com/content/help/en/mobile-services/android/getting-started-android/requirements.html)设置
* 实现以下类型的[!DNL Target]请求：
   * [!DNL Target]内容的预取
   * 在单个请求中批处理多个[!DNL Target]位置(mbox)
   * 阻止请求（在应用程序显示之前运行）
   * 非阻塞请求（在后台运行）
   * 实时（非缓存）
   * 缓存破坏重取
* 为请求添加参数以增强个性化
* 创建受众和优惠
* 个性化布局
* 利用功能标记推出新功能

## 先决条件

在这些教训中，我们假定您：

* 具有AdobeID和审批者级别的Adobe Target界面访问权限（请参阅下面的验证步骤）
* 了解Adobe Target客户代码，以便向您自己的帐户发出请求。 客户端代码显示在Adobe Target   “设置”>“实施”>“编辑at.js设置”屏幕
* 访问并熟悉[Mobile Services用户界面](https://mobilemarketing.adobe.com)
* 拥有用于Android移动应用程序开发的IDE。 本教程通过各种步骤和屏幕截图提供[ Android Studio](https://developer.android.com/studio/install)功能

如果您没有访问Experience Cloud解决方案所需的权限，请联系您的Experience Cloud管理员。

此外，还假定您熟悉Java中的Android开发。 您不需要成为Java专家来完成课程，但如果您能轻松阅读和理解代码，您将从中获得更多好处。

### 验证对Adobe Target的访问

本课需要访问Adobe Target。 在完成后续步骤之前，请执行以下操作，确保您有权访问Adobe Target:

1. 登录[Adobe Experience Cloud](https://experience.adobe.com/)
1. 在Experience Cloud主屏幕中，单击[!DNL Target]:
   ![Experience Cloud主屏幕](assets/aec_homeScreen_clickTarget.png)
1. 如下图所示，您应进入Adobe Target中的活动列表，并且您的用户应具有审批者级别的访问权限。 如果您无法访问[!DNL Target]或无法验证审批者级别的访问，请联系您的公司的Experience Cloud管理员，请请求此访问权限，并在授予后继续本教程：

   ![AdobeUI](assets/targetUI_approver.png)

## 关于经验教训

在这些课程中，您将使用您自己的Adobe Target帐户将Adobe Target应用程序实施到名为“We.Travel”的演示旅行应用程序中。 在教程结束时，您将根据用户对应用程序的使用情况向用户发送个性化消息！ 最终的个性化体验将如下所示：

![We.Travel应用程序最终版](assets/overview_final_result.jpg)

在We.Travel应用程序中完成实施后，您将能够在自己的移动应用程序中使用[!DNL Target]进行开始。

开始吧！

**[下一个：“下载并更新示例应用程序”>](download-and-update-the-sample-app.md)**
