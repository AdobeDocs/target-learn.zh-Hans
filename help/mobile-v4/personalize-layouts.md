---
title: 个性化布局
description: '在最后一课中，我们在Target中为我们的受众构建了两个个性化活动。 了解如何在应用程序中加载和显示活动，并验证内容是否在正确的时间在正确的位置显示。  '
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
author: Daniel Wright
exl-id: a9f033d9-9f72-4154-88f5-d36423a404d0
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 1%

---

# 个性化布局

现在，该将所有内容整合在一起并创建个性化体验了。 _Activity_&#x200B;是[!DNL Target]机制，用于将位置、受众和选件链接在一起，这样当从应用程序发出请求时，[!DNL Target]就会回复个性化内容。 我们将在[!DNL Target]中构建两个个性化活动，并验证在正确的时间和位置向正确的用户显示个性化内容。

## 学习目标

在本课程结束时，您将能够：

* 在Adobe Target中构建活动
* 验证示例应用程序中的活动

## 在Adobe Target中创建活动

了解如何创建参与用户和上下文选件活动。

### 首个活动 — “吸引用户”

以下是我们将构建的活动的摘要：

| 受众 | 位置 | 选件 |
|---|---|---|
| 新移动设备应用程序用户 | wetravel_engage_home、wetravel_engage_search | 主页：吸引新用户，搜索：吸引新用户 |
| 返回移动设备应用程序用户 | wetravel_engage_home、wetravel_engage_search | 主页：返回用户， default_content |

在[!DNL Target]接口中，执行以下操作：

1. 选择&#x200B;**[!UICONTROL 活动]** > **[!UICONTROL 创建活动]** > **[!UICONTROL 体验定位]**。

   ![创建活动](assets/activity_create_1.jpg)

1. 单击&#x200B;**[!UICONTROL 移动设备应用程序]**。
1. 选择&#x200B;**[!UICONTROL 表单编辑器]**。
1. 选择您的工作区（与您在以前的课程中使用的工作区相同）。
1. 选择您的资产（您在上一课程中使用的相同资产）。
1. 单击&#x200B;**[!UICONTROL 下一步]**。

   ![创建活动](assets/activity_create_2.jpg)

1. 将活动标题更改为&#x200B;**[!UICONTROL Engage Users]**。
1. 选择&#x200B;**[!UICONTROL 省略号]** > **[!UICONTROL 更改受众]**。
   ![新移动设备应用程序用户更改受众](assets/activity_create_3.jpg)
1. 将受众设置为&#x200B;**[!UICONTROL 新移动设备应用程序用户]**。
1. 单击&#x200B;**[!UICONTROL 完成]**。
   ![新的移动设备应用程序用户受众](assets/activity_create_4.jpg)

1. 将位置更改为&#x200B;_wetravel_engage_home_。
1. 选择默认内容旁边的下拉箭头，然后选择&#x200B;**[!UICONTROL 更改HTML选件]**。

   ![新的移动设备应用程序用户受众](assets/activity_create_5.jpg)

1. 选择&#x200B;**[!UICONTROL 主页：吸引新用户]**&#x200B;选件。
1. 选择&#x200B;**[!UICONTROL 完成]**。

   ![新的移动设备应用程序用户受众](assets/activity_create_6.jpg)

1. 选择&#x200B;**[!UICONTROL 添加位置]**。
   ![新的移动设备应用程序用户受众](assets/activity_create_7.jpg)

1. 选择&#x200B;_wetravel_engage_search_&#x200B;位置。
1. 更改HTML选件。

   ![新的移动设备应用程序用户受众](assets/activity_create_8.jpg)

1. 选择&#x200B;**[!UICONTROL 搜索：吸引新用户]**&#x200B;选件。
1. 单击&#x200B;**[!UICONTROL 完成]**。

   ![新的移动设备应用程序用户受众](assets/activity_create_9.jpg)

您刚刚将受众关联到位置和选件，为新的移动设备应用程序用户创建个性化体验！ 现在，体验应当如下所示：

![体验A最终版](assets/activity_engage_users_a_final.jpg)

现在，为旧移动设备应用程序用户创建体验：

1. 选择左侧的&#x200B;**[!UICONTROL 添加体验定位]** 。
1. 选择受众&#x200B;**[!UICONTROL 返回移动设备应用程序用户]**。
1. 选择&#x200B;**[!UICONTROL 完成]**。
   ![返回移动设备应用程序用户受众](assets/activity_create_11.jpg)

现在，使用我们之前用于配置新体验的相同流程。 返回移动设备应用程序用户体验的配置应当如下所示：

![返回移动设备应用程序最终用户](assets/activity_engage_users_b_final.jpg)

让我们继续查看设置中的下一个屏幕：

1. 单击&#x200B;**[!UICONTROL Next]**&#x200B;以前进到&#x200B;**[!UICONTROL Targeting]**&#x200B;屏幕。
1. 使用“定位”的默认设置。 如果您的受众体验与&#x200B;_纽约用户_&#x200B;和&#x200B;_首次用户_)可以在此屏幕上排列优先级顺序。
1. 单击&#x200B;**[!UICONTROL Next]**&#x200B;前进到&#x200B;**[!UICONTROL 目标和设置]**。

   ![参与用户活动 — 默认定位](assets/activity_engage_users_targeting.jpg)

现在，让我们完成活动设置：

1. 将&#x200B;**[!UICONTROL 主要目标]**&#x200B;设置为&#x200B;**[!UICONTROL 转化]**。
1. 将操作设置为&#x200B;**[!UICONTROL 已查看mbox]** > _wetravel_context_dest_（由于此位置位于确认屏幕上，因此我们可以使用它来测量转化）。

   ![参与用户活动 — 目标](assets/activity_create_12.jpg)

1. 将屏幕上的所有其他设置保留为默认值。
1. 单击&#x200B;**[!UICONTROL 保存并关闭]**&#x200B;以保存活动。
1. 在下一个屏幕上激活&#x200B;**[!UICONTROL Activity]**。

![体验B受众](assets/activity_create_13.jpg)

我们的第一个活动现已上线，可供测试！

### 第二个活动 — “上下文选件”

以下是我们将构建的第二个活动的摘要：

| 受众 | 位置 | 选件 |
| --- | --- | --- |
| 目标：圣地亚哥 | wetravel_context_dest | 圣地亚哥促销活动 |
| 目标：洛杉矶 | wetravel_context_dest | 洛杉矶升职 |

对下一个活动（“上下文选件”）重复与上述相同的过程。 两个体验的最终配置如下所示：

#### 圣地亚哥

![上下文选件 — 体验A](assets/activity_contextual_a_final.jpg)

#### 洛杉矶

![上下文选件 — 体验B](assets/activity_contextual_b_final.jpg)

在目标和设置步骤中，我们会将主要目标更改为预订确认屏幕上的位置：

1. 在&#x200B;**[!UICONTROL 报表设置]**&#x200B;下，将&#x200B;**[!UICONTROL 主要目标]**&#x200B;设置为&#x200B;**[!UICONTROL 转化]**。
1. 将操作设置为&#x200B;**[!UICONTROL 已查看mbox]** > _wetravel_context_dest_（在本活动中，此量度基本上没有意义，因为这也是提供体验的同一位置）。
1. 单击&#x200B;**[!UICONTROL 保存并关闭]**。

![上下文选件 — 体验](assets/activity_create_14.jpg)

在下一个屏幕上激活活动。

现在，我们的第二个活动已上线，可供测试！

## 验证主页选件

运行模拟器并观看第一个选件在主屏幕底部显示。 如果您是启动了5次或更多应用程序的回访用户，则会看到显示&#x200B;_欢迎返回_&#x200B;选件。 如果您是新用户（应用程序启动次数少于5次），则应会看到&#x200B;_新用户_&#x200B;消息：

![验证主页选件](assets/layout_home_validate.jpg)

如果新用户选件未显示，请尝试为模拟器擦除数据。 这会在您下次启动时将应用程序启动次数重置为1。 此操作在&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL AVD管理器]**&#x200B;下完成。 如果Logcat无法正常工作，您可能还需要重新启动Android Studio:

![擦除模拟器](assets/layout_home_validate_avd_wipe.jpg)

您还可以通过筛选&#x200B;_wetravel_engage_home_&#x200B;来验证Logcat中的响应：

![验证主页选件 — Logcat](assets/layout_home_validate_logcat.jpg)

## 验证搜索选件

选择&#x200B;**[!UICONTROL San Jose]**&#x200B;作为&#x200B;**[!UICONTROL Deparum]**&#x200B;和&#x200B;**[!UICONTROL San Diego]**&#x200B;作为&#x200B;**[!UICONTROL Destination]**，然后单击&#x200B;**[!UICONTROL Find Bus]**&#x200B;以搜索可用的总线。

在结果屏幕上，您应会看到&#x200B;_use filters_&#x200B;消息。 如果您是具有5次或更多次应用程序启动的回访用户，则此处不会显示任何消息，因为此位置设置了默认内容（为空）：

![验证搜索选件](assets/layout_search_validate.jpg)

## 在“谢谢您”屏幕上验证上下文选件

现在继续完成预订流程：

* 在结果屏幕上选择总线。
* 在结账屏幕上选择一个席位。
* 在付款屏幕上选择&#x200B;**[!UICONTROL 信用卡]**（将付款信息留空 — 不会进行实际预订）。

由于选择圣地亚哥作为目标，因此您应会在确认屏幕上看到&#x200B;_DJ SAM_&#x200B;选件横幅：

![验证上下文选件 — 圣地亚哥](assets/layout_context_san_diego.jpg)

现在，选择&#x200B;**[!UICONTROL 完成]**，然后尝试使用洛杉矶作为目的地的其他预订。 确认屏幕应显示&#x200B;_Universal Studios_&#x200B;横幅：

![验证上下文选件 — 洛杉矶](assets/layout_context_los_angeles.jpg)

## 结论

恭喜！ 以下是适用于Android的Adobe Target SDK 4.x教程的主要部分。 现在，您已具备在Android应用程序中实施个性化的技能！ 您可以将本文档和演示应用程序作为未来项目的参考。

下一个：功能标记是Android中可通过Adobe Target实施的另一项功能。 要了解功能标记，请参阅下一课程。

**[下一步：功能标记>](feature-flagging.md)**
