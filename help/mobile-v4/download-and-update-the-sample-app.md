---
title: 下载和更新We.Travel示例应用程序
description: 'We.Travel范例应用程序是通过Adobe Mobile Services SDK v4预实施的。 您只需更新它，它就指向您自己的Experience Cloud组织和解决方案帐户。   '
role: 开发人员
level: 中间
topic: 移动、个性化
feature: 实施移动
doc-type: tutorial
kt: 3040
thumbnail: null
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---


# 下载和更新We.Travel示例应用程序

We.Travel范例应用程序是通过Adobe Mobile Services SDK v4预实施的。 您只需更新它，它就指向您自己的Experience Cloud组织和解决方案帐户。

## 学习目标

在本课程结束时，您将能够：

* 下载并打开Android Studio中的We.Travel范例应用程序
* 验证并更新[!DNL Target]的Mobile Services SDK设置

## 下载We.Travel应用程序

* 下载[sample-app-android-SDKv4-Base-Version.zip](assets/sample-app-android-SDKv4-Base-Version.zip)
* 解压缩zip文件
* 在Android Studio中将应用程序作为现有项目打开（忽略有关“VCS根映射无效”的任何错误）
* 在模拟器中运行应用程序以确认应用程序是构建的并且您可以看到主屏幕
* 浏览应用程序并验证您是否可以完成预订流程（选择任何付款选项，然后点击“继续”跳过账单屏幕！）

   ![打开appConfirmation](assets/wetravel_homeScreen.png)![屏幕](assets/wetravel_confirmationScreen.png)

## 验证并更新[!DNL Target]的Mobile Services SDK设置

Adobe Mobile Services SDK已根据文档](https://docs.adobe.com/content/help/en/mobile-services/android/getting-started-android/requirements.html)预装在We.Travel应用程序[中。 现在，您将更新安装以指向您自己的[!DNL Target]帐户。

首先，在Mobile Services用户界面中创建新的应用程序：

1. 登录到[Adobe Mobile Services接口](https://mobilemarketing.adobe.com)。
1. 转至[!UICONTROL 管理应用程序]，然后单击&#x200B;**[!UICONTROL 添加]**&#x200B;以添加要与本教程一起使用的新应用程序（**[!UICONTROL 管理应用程序]** > **[!UICONTROL 添加]**）。
1. 选择包含非生产数据的Analytics报表包，为应用程序指定名称，选择&#x200B;**[!UICONTROL Standard]**&#x200B;类型，然后单击&#x200B;**[!UICONTROL 保存]**。
1. 添加应用程序后，在[!UICONTROL SDK目标选项]部分的下一个屏幕上添加您的[!DNL Target]客户端代码（可以在&#x200B;**[!UICONTROL 安装]** > **[!UICONTROL 实施]** > **[!UICONTROL 编辑设置]**&#x200B;下的[!DNL Target]接口中找到您的客户端代码，）。`at.js`
1. [!UICONTROL 请求超时]设置确定应用程序在执行超时指令之前等待来自[!DNL Target]服务器的响应的时间。 只需保留默认设置。
1. 启用[!UICONTROL 访客ID服务]并确保在下拉列表中选择了[!UICONTROL 组织]。
1. 单击窗口右上方的&#x200B;**[!UICONTROL 保存]**（而不是[!UICONTROL 通用链接]、[!UICONTROL 应用程序链接]选项或[!UICONTROL 推送服务]部分中的更改），保存您的更改。
1. 滚动到页面底部的“App SDK下载”部分并下载配置文件：

   ![下载配置文件](assets/config_file.jpg)

1. 替换Android Studio项目资源文件夹(app > src > main > assets)中的`ADBMobileConfig.json`文件。

1. 现在打开`ADBMobileConfig.json`文件，确保它包含预期更改，如[!DNL Target]客户端代码和Analytics详细信息：
   ![下载配置文件](assets/client_code.jpg)

如果看不到设置，请确认您单击了[!UICONTROL Mobile Services]界面中的右&#x200B;**[!UICONTROL Save]**&#x200B;按钮，并将文件复制到正确位置。

恭喜！ 您已使用[!DNL Target]帐户详细信息更新了SDK! 在下一课中添加[!DNL Target]请求后，我们将对配置进行其他验证。

**[下一个：&quot;添加目标请求&quot; >](add-requests.md)**
