---
title: 下载并更新We.Travel示例应用程序
description: We.Travel示例应用程序是使用AdobeMobile Services SDK v4预先实现的。 您只需要更新它，让它指向您自己的Experience Cloud组织和解决方案客户。
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
exl-id: 244bcf7a-b59b-4dd1-bd05-0a55ce7a7132
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---

# 下载并更新We.Travel示例应用程序

We.Travel示例应用程序是使用AdobeMobile Services SDK v4预先实现的。 您只需要更新它，让它指向您自己的Experience Cloud组织和解决方案客户。

## 学习目标

在本课程结束时，您将能够：

* 在Android Studio中下载并打开We.Travel示例应用程序
* 验证并更新[!DNL Target]的Mobile Services SDK设置

## 下载We.Travel应用程序

* 下载[sample-app-android-SDKv4-Base-Version.zip](assets/sample-app-android-SDKv4-Base-Version.zip)
* 解压缩zip文件
* 在Android Studio中将应用程序作为现有项目打开（忽略任何有关“无效VCS根映射”的错误）
* 在模拟器中运行应用程序，以确认应用程序已生成，并且您可以看到主屏幕
* 浏览应用程序并确认您可以完成预订流程（选择任何付款选项，然后单击“继续”以跳过计费屏幕！）

  ![打开应用程序](assets/wetravel_homeScreen.png)![确认屏幕](assets/wetravel_confirmationScreen.png)

## 验证并更新[!DNL Target]的Mobile Services SDK设置

根据文档[&#128279;](https://experienceleague.adobe.com/docs/mobile-services/android/getting-started-android/requirements.html?lang=zh-Hans)，已在We.Travel应用程序中预安装了AdobeMobile Services SDK。 现在将更新安装以指向您自己的[!DNL Target]帐户。

首先，在Mobile Services用户界面中创建一个新应用程序：

1. 登录到[AdobeMobile Services接口](https://mobilemarketing.adobe.com/)。
1. 转到[!UICONTROL Manage Apps]，然后单击&#x200B;**[!UICONTROL Add]**&#x200B;以添加要与此教程(**[!UICONTROL Manage Apps]** > **[!UICONTROL Add]**)一起使用的新应用。
1. 选择包含非生产数据的Analytics报表包，为应用程序命名，选择&#x200B;**[!UICONTROL Standard]**&#x200B;类型并单击&#x200B;**[!UICONTROL Save]**。
1. 添加应用后，在下一个屏幕的[!UICONTROL SDK Target Options]部分添加您的[!DNL Target]客户端代码（您可以在[!DNL Target]界面的&#x200B;**[!UICONTROL Setup]** > **[!UICONTROL Implementation]** > **[!UICONTROL Edit Settings]**&#x200B;下“下载`at.js`”按钮旁的找到您的客户端代码）。
1. [!UICONTROL Request Timeout]设置确定在执行超时指令之前，应用程序等待来自[!DNL Target]服务器的响应的时间。 只需保留默认设置。
1. 启用[!UICONTROL Visitor ID Service]并确保在下拉菜单中选择您的[!UICONTROL Organization]。
1. 单击窗口右上角的&#x200B;**[!UICONTROL Save]**（而不是[!UICONTROL Universal Links]、[!UICONTROL App Links]选项或[!UICONTROL Push Services]部分中的选项）以保存更改。
1. 滚动到页面底部的应用程序SDK下载部分，并下载配置文件：

   ![下载配置文件](assets/config_file.jpg)

1. 替换Android Studio项目资产文件夹中的`ADBMobileConfig.json`文件（应用程序> src >主页>资产）。

1. 现在打开`ADBMobileConfig.json`文件并确保它包含预期的更改，如您的[!DNL Target]客户端代码和Analytics详细信息：
   ![下载配置文件](assets/client_code.jpg)

如果未看到您的设置，请确认您在[!UICONTROL Mobile Services]界面中单击了正确的&#x200B;**[!UICONTROL Save]**&#x200B;按钮，并将文件复制到正确的位置。

恭喜！您已使用您的[!DNL Target]帐户详细信息更新SDK！ 在下一课程中添加[!DNL Target]请求后，我们将对配置进行其他验证。

**[下一步：“添加Target请求”>](add-requests.md)**
