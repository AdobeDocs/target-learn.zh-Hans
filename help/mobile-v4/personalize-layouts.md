---
title: 个性化布局
description: '在最后一课中，我们在目标中为受众构建两个个性化活动。 了解如何在应用程序中加载和显示活动，并验证内容在正确时间在正确位置显示。  '
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
thumbnail: null
author: Daniel Wright
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 1%

---


# 个性化布局

现在，是时候将所有内容整合在一起并创建个性化体验了。 _活动_&#x200B;是将位置、受众和优惠链接在一起的[!DNL Target]机制，这样当从应用程序发出请求时，[!DNL Target]会对个性化内容做出响应。 我们将在[!DNL Target]中构建两个个性化活动，并验证在正确的时间和位置向正确的用户显示个性化内容。

## 学习目标

在本课程结束时，您将能够：

* 在Adobe Target中构建活动
* 验证示例应用程序中的活动

## 在Adobe Target中创建活动

了解如何创建吸引用户和上下文优惠活动。

### 第一个活动 — “吸引用户”

以下是我们将构建的活动的摘要：

| 受众 | 位置 | 选件 |
|---|---|---|
| 新移动应用程序用户 | wetravel_engage_home、wetravel_engage_search | 主页：吸引新用户，搜索：吸引新用户 |
| 返回移动App用户 | wetravel_engage_home、wetravel_engage_search | 主页：返回用户，default_content |

在[!DNL Target]接口中，执行以下操作：

1. 选择&#x200B;**[!UICONTROL 活动]** > **[!UICONTROL 创建活动]** > **[!UICONTROL 体验定位]**。

   ![创建活动](assets/activity_create_1.jpg)

1. 单击&#x200B;**[!UICONTROL 移动应用程序]**。
1. 选择&#x200B;**[!UICONTROL 表单书写器]**。
1. 选择您的工作区（与之前的课程中使用的工作区相同）。
1. 选择您的“属性”（您在上一课中使用的相同属性）。
1. 单击&#x200B;**[!UICONTROL 下一步]**。

   ![创建活动](assets/activity_create_2.jpg)

1. 将活动标题更改为&#x200B;**[!UICONTROL Engage Users]**。
1. 选择&#x200B;**[!UICONTROL 省略号]** > **[!UICONTROL 更改受众]**。
   ![新移动应用程序用户更改受众](assets/activity_create_3.jpg)
1. 将受众设置为&#x200B;**[!UICONTROL New Mobile App Users]**。
1. 单击&#x200B;**[!UICONTROL 完成]**。
   ![新移动应用程序用户受众](assets/activity_create_4.jpg)

1. 将位置更改为&#x200B;_wetravel_engage_home_。
1. 选择“默认内容”旁边的下拉箭头，然后选择“**[!UICONTROL 更改HTML优惠]**”。

   ![新移动应用程序用户受众](assets/activity_create_5.jpg)

1. 选择&#x200B;**[!UICONTROL 主页：吸引新用户]**&#x200B;优惠。
1. 选择&#x200B;**[!UICONTROL 完成]**。

   ![新移动应用程序用户受众](assets/activity_create_6.jpg)

1. 选择&#x200B;**[!UICONTROL 添加位置]**。
   ![新移动应用程序用户受众](assets/activity_create_7.jpg)

1. 选择&#x200B;_wetravel_engage_search_&#x200B;位置。
1. 更改HTML优惠。

   ![新移动应用程序用户受众](assets/activity_create_8.jpg)

1. 选择&#x200B;**[!UICONTROL 搜索：吸引新用户]**&#x200B;优惠。
1. 单击&#x200B;**[!UICONTROL 完成]**。

   ![新移动应用程序用户受众](assets/activity_create_9.jpg)

您刚刚将受众连接到位置和优惠，为新移动App用户创造个性化体验！ 现在，体验应该如下：

![体验最终](assets/activity_engage_users_a_final.jpg)

现在，为Returning Mobile App用户创建体验：

1. 在左侧选择&#x200B;**[!UICONTROL 添加体验定位]**。
1. 选择受众&#x200B;**[!UICONTROL 返回移动应用程序用户]**。
1. 选择&#x200B;**[!UICONTROL 完成]**。
   ![返回移动应用用户受众](assets/activity_create_11.jpg)

现在使用之前配置新体验时所用的相同流程。 “返回移动应用程序用户”体验的配置应当如下：

![最终退回移动App用户](assets/activity_engage_users_b_final.jpg)

让我们继续查看设置中的下一个屏幕：

1. 单击&#x200B;**[!UICONTROL 下一步]**&#x200B;进入&#x200B;**[!UICONTROL 定位]**&#x200B;屏幕。
1. 使用定位的默认设置。 如果您对重叠的受众有经验(例如&#x200B;_New York Users_&#x200B;和&#x200B;_First Time Users_)，您可以在此屏幕上安排优先级顺序。
1. 单击&#x200B;**[!UICONTROL 下一步]**&#x200B;前进到&#x200B;**[!UICONTROL 目标和设置]**。

   ![“吸引用户”活动 — 默认定位](assets/activity_engage_users_targeting.jpg)

现在，让我们完成活动设置：

1. 将&#x200B;**[!UICONTROL 主要目标]**&#x200B;设置为&#x200B;**[!UICONTROL 转换]**。
1. 将操作设置为&#x200B;**[!UICONTROL 已查看mbox]** > _wetravel_context_dest_（由于此位置位于确认屏幕上，因此我们可以使用它来测量转换）。

   ![吸引用户活动 — 目标](assets/activity_create_12.jpg)

1. 将屏幕上的所有其他设置保留为默认值。
1. 单击&#x200B;**[!UICONTROL 保存并关闭]**&#x200B;以保存活动。
1. 在下一个屏幕上激活&#x200B;**[!UICONTROL 活动]**。

![体验B受众](assets/activity_create_13.jpg)

我们的第一个活动现已上线，可供测试！

### 第二个活动 — “情境优惠”

以下是我们将构建的第二个活动的摘要：

| 受众 | 位置 | 选件 |
| --- | --- | --- |
| 目标：圣地亚哥 | wetravel_context_dest | 圣地亚哥 |
| 目标：洛杉矶 | wetravel_context_dest | 洛杉矶促销 |

对下一个活动重复上述步骤 — “上下文优惠”。 两种体验的最终配置如下所示：

#### 圣地亚哥

![情境优惠 — 体验A](assets/activity_contextual_a_final.jpg)

#### 洛杉矶

![情境优惠 — 体验B](assets/activity_contextual_b_final.jpg)

在“目标和设置”(Goals &amp; Settings)步骤中，我们将“主要目标”(Primary Gaol)更改为预订确认屏幕上的位置：

1. 在&#x200B;**[!UICONTROL 报告设置]**&#x200B;下，将&#x200B;**[!UICONTROL 主要目标]**&#x200B;设置为&#x200B;**[!UICONTROL 转换]**。
1. 将操作设置为&#x200B;**[!UICONTROL 已查看mbox]** > _wetravel_context_dest_(在此活动中，此量度基本上没有意义，因为这也是提供体验的同一位置)。
1. 单击&#x200B;**[!UICONTROL 保存并关闭]**。

![情境优惠 — 体验](assets/activity_create_14.jpg)

在下一个屏幕上激活活动。

现在，我们的第二个活动已实时并准备测试！

## 验证主页优惠

运行模拟器并观察在主屏幕底部显示的第一个优惠。 如果您是具有5个或多个应用程序启动的返回用户，您会看到&#x200B;_欢迎返回_&#x200B;优惠。 如果您是新用户（少于5个应用程序启动），则应看到&#x200B;_new user_&#x200B;消息：

![验证主页优惠](assets/layout_home_validate.jpg)

如果未显示新用户优惠，请尝试为您的模拟器擦除数据。 这将在您下次启动时将应用程序启动项重置为1。 此操作在&#x200B;**[!UICONTROL Tools]** > **[!UICONTROL AVD Manager]**&#x200B;下完成。 如果Logcat无法正常工作，您也可能需要重新启动Android Studio:

![擦除模拟器](assets/layout_home_validate_avd_wipe.jpg)

您还可以通过筛选&#x200B;_wetravel_engage_home_&#x200B;验证Logcat中的响应：

![验证主页优惠 — 日志](assets/layout_home_validate_logcat.jpg)

## 验证搜索优惠

选择&#x200B;**[!UICONTROL San Jose]**&#x200B;作为&#x200B;**[!UICONTROL Departo]**&#x200B;和&#x200B;**[!UICONTROL San Diego]**&#x200B;作为&#x200B;**[!UICONTROL Destination]**，然后单击&#x200B;**[!UICONTROL 查找总线]**&#x200B;以搜索可用总线。

在结果屏幕上，您应当看到&#x200B;_使用过滤器_&#x200B;消息。 如果您是具有5个或更多应用程序启动的返回用户，此处不会显示任何消息，因为此位置已设置默认内容（此位置为空）：

![验证搜索优惠](assets/layout_search_validate.jpg)

## 验证感谢屏幕上的上下文优惠

现在继续进行预订过程：

* 在结果屏幕上选择一个总线。
* 在结帐屏幕上选择一个席位。
* 在付款屏幕上选择&#x200B;**[!UICONTROL 信用卡]**（将付款信息留空 — 不进行实际预订）。

由于圣地亚哥被选为目标，您应在确认屏幕上看到&#x200B;_DJ SAM_&#x200B;优惠横幅：

![验证上下文优惠 — 圣地亚哥](assets/layout_context_san_diego.jpg)

现在，选择&#x200B;**[!UICONTROL 完成]**&#x200B;并尝试将洛杉矶作为目的地进行其他预订。 确认屏幕应显示&#x200B;_Universal Studios_&#x200B;横幅：

![验证上下文优惠 — 洛杉矶](assets/layout_context_los_angeles.jpg)

## 结论

恭喜！ 这就是Adobe Target SDK 4.x for Android教程的主要部分。 您现在具备在Android应用程序中实施个性化的技能！ 您可以引用本文档和演示应用程序作为将来项目的参考。

下一步：功能标记是可在Android中使用Adobe Target实现的另一项功能。 要了解功能标记，请查看下一课。

**[下一个：功能标记>](feature-flagging.md)**
