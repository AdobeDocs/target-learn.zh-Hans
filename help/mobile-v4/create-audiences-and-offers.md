---
title: 在Adobe Target中创建受众和优惠
seo-title: 在Adobe Target中创建受众和优惠
description: '在本课中，我们将为前几课中我们实施的三个地点建立Adobe Target受众和优惠。 这些内容将用于在下一课中展示个性化体验。   '
seo-description: 在本课中，我们将为前几课中我们实施的三个地点建立Adobe Target受众和优惠。 这些内容将用于在下一课中展示个性化体验。
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 1%

---


# 在Adobe Target中创建受众和优惠

在本课中，我们将进入界面， [!DNL Target] 为前几课中我们实施的三个位置构建受众和优惠。

## 学习目标

在本课程结束时，您将能够：

* 在 Adobe Target 中创建受众
* 以Adobe Target创建优惠

更具体地说，在本课中，我们将创建完成教程开头定义的个性化使用案例所需的受众和优惠。 我们希望使用“主页”和“搜索”屏幕帮助应用程序用户预订其行程，并希望使用“感谢”屏幕根据用户的目标显示一些相关促销。 下面是一个表，表示我们将在每个位置在本课中构建的内容：

| 位置 | 受众 | 优惠 |
| --- | --- | --- |
| wetravel_engage_home | 新移动应用程序用户 | &quot;选择您的来源和目标以搜索可用的巴士路线&quot; |
| wetravel_engage_search | 新移动应用程序用户 | “使用过滤器缩小搜索结果范围” |
| wetravel_engage_home | 返回移动应用程序用户 | “欢迎回来！ 在结帐时使用促销代码BACK30可享受10%折扣。” |
| wetravel_engage_search | 返回移动应用程序用户 | default content（默认内容） |
| wetravel_context_dest | 目标： 圣地亚哥 | “DJ” |
| wetravel_context_dest | 目标： 洛杉矶 | “通用” |

## 选择工作区

如果您的公司使用“属性”和“工作区”来为个性化应用程序和网站建立界限，并且您在上一课中实现了at_property参数，则您应首先确保您位于正确的工作区中，然后继续本课。 如果不使用“属性”(Properties)和“工作区”(Workspaces)，只需忽略此步骤。 选择您在上一课中使用的工作区以复制at_property值：

![工作区示例](assets/workspace.jpg)

## 创建受众

现在，让我们创建将用于个性化应用程序的受众。

### 为新用户创建受众

Adobe Target受众用于标识特定的访客组。 优惠随后可以定位到这些特定组。 对于前两个位置，我们将使用“新用户”受众:

1. 单击 **[!UICONTROL 顶部导]** 航中的受众。
1. Click the **[!UICONTROL Create Audience]** button.
   ![创建新用户受众](assets/audience_new_mobile_app_users_1.jpg)

1. 输入 **[!UICONTROL 新移动应用程序用]** 户作为受众名称。
1. 选择 **[!UICONTROL 添加规则]**。
1. 选择自 **[!UICONTROL 定义]** 规则。
   ![创建新用户受众](assets/audience_new_mobile_app_users_2.jpg)

1. 选 **[!UICONTROL 择启动项]**。
1. Select **[!UICONTROL is less than]**.
1. Enter **5**.
1. 保存新受众。
   ![创建新用户受众](assets/audience_new_mobile_app_users_3.jpg)

### 为返回用户创建受众

按照上面列出的相同步骤为返回用户创建受众。

1. 命名受众 _返回移动应用程序用户_。
1. 使 **[!UICONTROL 用a.Launches大于或等于]** 5作为自定义规则。
1. 保存新受众。

   ![创建返回用户受众](assets/audience_returning_mobile_app_users.jpg)

>[!NOTE] 在移动SDK中收集的所 [!DNL Target] 有生命周期指标和维都以“a”（例如，a.Launches）为前缀，并且在下拉菜单的“自定义”选项中可用，可用于构建受众。

### 为预订圣地亚哥之旅的用户创建受众

接下来，我们将为We.Travel应用程序提供的一些目标创建一些受众。 在上一课中，我们将目标作为位置参数在wetravel_context_dest位置请求中传递。 该参数在下拉菜单的“自定义”选项中可用。

>[!NOTE] 如果界面中未显示您期望在“自定义”下拉框中看到的 [!DNL Target] 参数，请多次检查该参数是否确实在请求中传递。 如果已验证请求中的参数，但未延迟加载到接口中，则只需键入参 [!DNL Target] 数名称并按Enter键，即可继续定义受众

1. 命名受众 _目标： 圣地亚哥_。
1. 对此定义使用自定义规则： _locationDest包含圣地亚哥_。
1. 保存新受众。

   ![创建“圣地亚哥”受众](assets/audience_locationDest_san_diego.jpg)

### 为预订洛杉矶之旅的用户创建受众

1. 命名受众 _目标： 洛杉矶_
1. 对此定义使用自定义规则： _locationDest包含洛杉矶_
1. 保存新受众。

![创建“洛杉矶”受众](assets/audience_locationDest_los_angeles.jpg)

## 创建选件

现在，让我们创建优惠来显示这些消息。 作为提醒，优惠是代码／内容的片段，在响应中提供 [!DNL Target] 它们。 它们通常在用户界面 [!DNL Target] 中创建，但也可以通过API或使用与Adobe Experience Manager的体验片段集成来创建。 在移动应用程序中，JSON优惠很常见。 在本教程中，我们将使用HTML优惠，它可用于将任何纯文本内容（包括JSON）交付到应用程序。

### 为新用户创建优惠

首先，让我们为发送给新用户的消息创建优惠:

1. 单击 **[!UICONTROL 顶部导]** 航中的优惠。
1. 单击&#x200B;**[!UICONTROL 创建]**。
1. 选择 **[!UICONTROL HTML优惠]**。

   ![创建主页优惠](assets/offer_home_1.jpg)

1. 命名优惠 _主页： 吸引新用户_。
1. 输入 _选择源和目标以搜索可用的总线_ （作为代码）。
1. 保存新优惠。

   ![创建主页HTML优惠](assets/offer_home_2.jpg)

### 为返回用户创建优惠

现在，让我们为返回用户创建一个优惠(第二个优惠将是默认内容，它将不显示任何内容):

1. 命名优惠 _主页： 返回用户_。
1. 进入 _欢迎回来！ 在结帐时使用促销代码BACK30可享受10%折扣。_ 作为HTML代码。
1. 保存新优惠。

   ![创建主页HTML优惠](assets/offer_home_returning_users.jpg)

### 创建圣地亚哥优惠

当“DJ”返回到ThankYou活动时，filterRecommendationBasedOnOffer()函数中的逻辑将显示“Rock Night with DJ SAM”的横幅：

1. 为圣迭戈 _命名优惠促销_。
1. 输入 _DJ_ 作为HTML代码。
1. 保存新优惠。

![创建“圣地亚哥”优惠](assets/offer_san_diego.jpg)

### 为前往洛杉矶的用户创建优惠

当“Universal”返回到ThankYou活动时，filterRecommendationBasedOnOffer()函数中的逻辑将显示“Universal Studios”的横幅：

1. 为洛杉矶 _指定优惠促销_。
1. 输 _入_ Universal作为HTML代码。
1. 保存新优惠。

![创建“洛杉矶”优惠](assets/offer_los_angeles.jpg)

## 结论

现在我们有受众和优惠。 在下一课中，我们将构建将位置、受众和优惠绑定在一起的活动，以创建个性化体验！

**[下一个： “个性化布局”>](personalize-layouts.md)**
