---
title: Adobe TargetAndroidAdobeMobile Services SDK v4
description: Adobe TargetAndroid的AdobeMobile Services SDK v4对于已经使用AdobeMobile Services SDK v4并希望开始具有Adobe Target的个性化应用程序体验的Android开发人员来说是一个完美的起点。
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 2%

---


# 概述

_Adobe TargetAndroid版Mobile Services SDK v4_ ，对于已经使用AdobeMobile Services SDK v4并希望开始具有Adobe Target的个性化应用程序体验的Android开发人员来说，这是一个完美的起点。

您可以使用演示版Android应用程序完成课程。 完成本教程后，您应准备好在自己的Android应 [!DNL Target] 用程序中开始实施！

完成此教程后，您将能够：

* 验证 [AdobeMobile Services SDK设置](https://docs.adobe.com/content/help/en/mobile-services/android/getting-started-android/requirements.html)
* 实施以下类型的 [!DNL Target] 请求：
   * 内容预取 [!DNL Target]
   * 在单个 [!DNL Target] 请求中批处理多个位置(mbox)
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

* 具有AdobeID和审批者级别的Adobe Target界面访问权限（请参阅下面的验证步骤）
* 了解Adobe Target客户代码，以便向您自己的帐户发出请求。 “设置”>“实施”>“编辑at.js”设置屏幕的Adobe Target界面中显示客户代码
* 有权访问并熟悉Mobile [Services用户界面](https://mobilemarketing.adobe.com)
* 拥有用于Android移动应用程序开发的IDE。 本教程通过 [各种步骤](https://developer.android.com/studio/install) 、以及截屏方式提供Android Studio

如果您没有访问Experience Cloud解决方案所需的权限，请联系您的Experience Cloud管理员。

此外，还假定您熟悉Java中的Android开发。 您不需要成为Java专家来完成课程，但如果您能轻松阅读和理解代码，您会从中获得更多的帮助。

### 验证对Adobe Target的访问

本课需要访问Adobe Target。 在完成后续步骤之前，请执行以下操作，确保您有权访问Adobe Target:

1. 登录 [Adobe Experience Cloud](https://experience.adobe.com/)
1. From the Experience Cloud home screen, click [!DNL Target]:
   ![Experience Cloud主屏幕](assets/aec_homeScreen_clickTarget.png)
1. 您应当按Adobe Target进入活动列表，如下图所示，并且您应当看到您的用户具有审批者级别的访问权限。 如果您无法访问或 [!DNL Target] 无法验证审批者级别的访问权限，请与公司的Experience Cloud管理员之一联系，请求此访问权限，并在授予后继续本教程：

   ![AdobeUI](assets/targetUI_approver.png)

## 关于课程

在这些课程中，您将使用您自己的Adobe Target帐户将Adobe Target应用程序实现到名为“We.Travel”的演示旅行应用中。 在教程结束时，您将根据用户对应用程序的使用情况向用户发送个性化消息！ 最终的个性化体验将如下所示：

![We.Travel应用程序最终版](assets/overview_final_result.jpg)

在We.Travel应用程序中完成实施后，您将能够在自己的移动应用 [!DNL Target] 程序中开始使用。

开始吧！

**[下一个： “下载并更新示例应用程序”>](download-and-update-the-sample-app.md)**
