---
title: 下载和更新We.Travel示例应用程序
description: 'We.Travel示例应用程序是通过Mobile Services SDK v4预先实施的Adobe。 您只需更新它，即可将其指向您自己的Experience Cloud组织和解决方案帐户。   '
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
exl-id: 244bcf7a-b59b-4dd1-bd05-0a55ce7a7132
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# 下载和更新We.Travel示例应用程序

We.Travel示例应用程序是通过Mobile Services SDK v4预先实施的Adobe。 您只需更新它，即可将其指向您自己的Experience Cloud组织和解决方案帐户。

## 学习目标

在本课程结束时，您将能够：

* 在Android Studio中下载并打开We.Travel示例应用程序
* 验证并更新[!DNL Target]的Mobile Services SDK设置

## 下载We.Travel应用程序

* 下载[sample-app-android-SDKv4-Base-Version.zip](assets/sample-app-android-SDKv4-Base-Version.zip)
* 解压缩zip文件
* 在Android Studio中作为现有项目打开应用程序（忽略有关“VCS根映射无效”的任何错误）
* 在模拟器中运行应用程序，以确认应用程序已构建，并且您可以看到主屏幕
* 浏览应用程序并验证是否可以完成预订流程（选择任何付款选项，然后单击“继续”以跳过帐单屏幕！）

   ![打开appConfirmation](assets/wetravel_homeScreen.png)![屏幕](assets/wetravel_confirmationScreen.png)

## 验证并更新[!DNL Target]的Mobile Services SDK设置

AdobeMobile Services SDK已根据文档](https://experienceleague.adobe.com/docs/mobile-services/android/getting-started-android/requirements.html?lang=en)在We.Travel应用程序[中预装。 现在，您将更新安装以指向您自己的[!DNL Target]帐户。

首先，在Mobile Services用户界面中创建新应用程序：

1. 登录到[AdobeMobile Services界面](https://mobilemarketing.adobe.com/)。
1. 转到[!UICONTROL 管理应用程序]，然后单击&#x200B;**[!UICONTROL 添加]**&#x200B;以添加要与本教程一起使用的新应用程序（**[!UICONTROL 管理应用程序]** > **[!UICONTROL 添加]**）。
1. 选择一个包含非生产数据的Analytics报表包，为应用程序提供一个名称，选择&#x200B;**[!UICONTROL Standard]**&#x200B;类型，然后单击&#x200B;**[!UICONTROL 保存]**。
1. 添加应用程序后，在[!UICONTROL SDK目标选项]部分的下一个屏幕中添加您的[!DNL Target]客户端代码（您可以在&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL 实施]** > **[!UICONTROL 编辑设置]**&#x200B;下方的[!DNL Target]界面中找到您的客户端代码，位于“下载`at.js`”按钮旁边）。
1. [!UICONTROL 请求超时]设置确定应用程序在执行超时指令之前需要等待来自[!DNL Target]服务器的响应多长时间。 只需保留默认设置。
1. 启用[!UICONTROL 访客ID服务]，并确保在下拉列表中选择了您的[!UICONTROL 组织]。
1. 单击窗口右上方的&#x200B;**[!UICONTROL Save]**（而不是[!UICONTROL 通用链接]、[!UICONTROL 应用程序链接]选项或[!UICONTROL 推送服务]部分中的），可保存更改。
1. 滚动到页面底部的应用程序SDK下载部分，然后下载配置文件：

   ![下载配置文件](assets/config_file.jpg)

1. 替换Android Studio项目资产文件夹中的`ADBMobileConfig.json`文件（应用程序> src >主>资产）。

1. 现在，打开`ADBMobileConfig.json`文件，并确保它包含预期的更改，如[!DNL Target]客户端代码和Analytics详细信息：
   ![下载配置文件](assets/client_code.jpg)

如果看不到设置，请确认您单击了[!UICONTROL Mobile Services]界面中右侧的&#x200B;**[!UICONTROL Save]**&#x200B;按钮，并将文件复制到正确的位置。

恭喜！ 您已使用[!DNL Target]帐户详细信息更新SDK! 在下一课程中添加[!DNL Target]请求后，我们将对配置进行其他验证。

**[下一步：“添加Target请求”>](add-requests.md)**
