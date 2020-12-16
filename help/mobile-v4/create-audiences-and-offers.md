---
title: 在Adobe Target创建受众和优惠
seo-title: 在Adobe Target创建受众和优惠
description: '在本课中，我们将在Adobe Target建立受众和优惠，用于我们在前几课中所实施的三个地点。 这些内容将用于在下一课中展示个性化体验。   '
seo-description: 在本课中，我们将在Adobe Target建立受众和优惠，用于我们在前几课中所实施的三个地点。 这些内容将用于在下一课中展示个性化体验。
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: 199fbde58696a0511623c5500cc6afbbcfdd67a3
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 1%

---


# 在Adobe Target创建受众和优惠

在本课中，我们将进入[!DNL Target]界面，为前几节课中所实施的三个位置构建受众和优惠。

## 学习目标

在本课程结束时，您将能够：

* 在 Adobe Target 中创建受众
* 在Adobe Target创建优惠

更具体地说，在本课中，我们将创建完成教程开头定义的个性化使用案例所需的受众和优惠。 我们希望使用“主页”和“搜索”屏幕帮助应用程序用户预订其行程，并希望使用“感谢”屏幕根据用户的目标显示一些相关促销。 下面是一个表，表示我们将在每个位置在本课中构建的内容：

| 位置 | 受众 | 优惠 |
| --- | --- | --- |
| wetravel_engage_home | 新移动应用程序用户 | &quot;选择您的来源和目标以搜索可用的巴士路线&quot; |
| wetravel_engage_search | 新移动应用程序用户 | “使用过滤器缩小搜索结果范围” |
| wetravel_engage_home | 返回移动应用程序用户 | “欢迎回来！ 在结帐时使用促销代码BACK30可享受10%折扣。” |
| wetravel_engage_search | 返回移动应用程序用户 | default content（默认内容） |
| wetravel_context_dest | 目标：圣地亚哥 | “DJ” |
| wetravel_context_dest | 目标：洛杉矶 | “通用” |

## 选择工作区

如果您的公司使用“属性”和“工作区”来为个性化应用程序和网站建立界限，并且您在上一课中实现了at_property参数，则应首先确保您位于正确的工作区中，然后继续本课。 如果不使用“属性”(Properties)和“工作区”(Workspaces)，只需忽略此步骤。 选择您在上一课中使用的工作区以复制at_property值：

![工作区示例](assets/workspace.jpg)

## 创建受众

现在，让我们创建将用于个性化应用程序的受众。

### 为新用户创建受众

Adobe Target受众用于识别特定访客群。 优惠随后可以定位到这些特定组。 对于前两个位置，我们将使用“新用户”受众:

1. 单击顶部导航中的&#x200B;**[!UICONTROL 受众]**。
1. 单击&#x200B;**[!UICONTROL 创建受众]**按钮。
   ![创建新用户受众](assets/audience_new_mobile_app_users_1.jpg)

1. 输入&#x200B;**[!UICONTROL 新移动应用程序用户]**&#x200B;作为受众名。
1. 选择&#x200B;**[!UICONTROL 添加规则]**。
1. 选择&#x200B;**[!UICONTROL Custom]**规则。
   ![创建新用户受众](assets/audience_new_mobile_app_users_2.jpg)

1. 选择&#x200B;**[!UICONTROL a.Launches]**。
1. 选择&#x200B;**[!UICONTROL 小于]**。
1. 输入&#x200B;**5**。
1. 保存新受众。
   ![创建新用户受众](assets/audience_new_mobile_app_users_3.jpg)

### 为返回用户创建受众

按照上面列出的相同步骤为返回用户创建受众。

1. 将受众命名为&#x200B;_Returning Mobile App Users_。
1. 使用&#x200B;**[!UICONTROL a。启动项大于或等于5]**&#x200B;作为自定义规则。
1. 保存新受众。

   ![创建返回用户受众](assets/audience_returning_mobile_app_users.jpg)

>[!NOTE]
>
>在[!DNL Target]移动SDK中收集的所有生命周期指标和维都以“a”（例如，a.Launches）为前缀，并且在下拉菜单的“Custom”选项中可用，可用于构建受众。

### 为预订圣地亚哥之旅的用户创建受众

接下来，我们将为We.Travel应用程序提供的一些目标创建一些受众。 在上一课中，我们将目标作为位置参数在wetravel_context_dest位置请求中传递。 该参数在下拉菜单的“自定义”选项中可用。

>[!NOTE]
>
>如果您希望在“自定义”下拉菜单中看到的参数未出现在[!DNL Target]接口中，请多次检查请求中是否确实正在传递该参数。 如果已验证请求中的参数，但未延迟加载到[!DNL Target]接口，您只需键入参数名称并按Enter即可继续定义受众

1. 将受众命名为&#x200B;_目标：圣地亚哥_。
1. 对此定义使用自定义规则：_locationDest包含San Diego_。
1. 保存新受众。

   ![创建“圣地亚哥”受众](assets/audience_locationDest_san_diego.jpg)

### 为预订洛杉矶之旅的用户创建受众

1. 将受众命名为&#x200B;_目标：洛杉矶_
1. 对此定义使用自定义规则：_locationDest包含洛杉矶_
1. 保存新受众。

![创建“洛杉矶”受众](assets/audience_locationDest_los_angeles.jpg)

## 创建选件

现在，让我们创建优惠来显示这些消息。 作为提醒，优惠是代码／内容的片段，它们在[!DNL Target]响应中提供。 它们通常在[!DNL Target]用户界面中创建，但也可以通过API或使用与Adobe Experience Manager的集成的Experience Fragments创建。 在移动应用程序中，JSON优惠很常见。 在本教程中，我们将使用HTML优惠，它可用于将任何纯文本内容（包括JSON）交付到应用程序。

### 为新用户创建优惠

首先，让我们为发送给新用户的消息创建优惠:

1. 单击顶部导航中的&#x200B;**[!UICONTROL 优惠]**。
1. 单击&#x200B;**[!UICONTROL 创建]**。
1. 选择&#x200B;**[!UICONTROL HTML优惠]**。

   ![创建主页优惠](assets/offer_home_1.jpg)

1. 命名优惠&#x200B;_主页：吸引新用户_。
1. 输入&#x200B;_选择源和目标以搜索可用总线_&#x200B;作为代码。
1. 保存新优惠。

   ![创建主页HTML优惠](assets/offer_home_2.jpg)

### 为返回用户创建优惠

现在，让我们为返回用户创建一个优惠(第二个优惠将是默认内容，它将不显示任何内容):

1. 命名优惠&#x200B;_主页：返回用户_。
1. 输入&#x200B;_欢迎返回！ 在结帐时使用促销代码BACK30可享受10%折扣。_ 作为HTML代码。
1. 保存新优惠。

   ![创建主页HTML优惠](assets/offer_home_returning_users.jpg)

### 创建圣地亚哥优惠

当“DJ”返回到ThankYou活动时，filterRecommendationBasedOnOffer()函数中的逻辑将显示“Rock Night with DJ SAM”的横幅：

1. 将优惠命名为&#x200B;_Promotion for San Diego_。
1. 输入&#x200B;_DJ_&#x200B;作为HTML代码。
1. 保存新优惠。

![创建“圣地亚哥”优惠](assets/offer_san_diego.jpg)

### 为前往洛杉矶的用户创建优惠

当“Universal”返回到ThankYou活动时，filterRecommendationBasedOnOffer()函数中的逻辑将显示“Universal Studios”的横幅：

1. 将优惠命名为&#x200B;_洛杉矶促销_。
1. 输入&#x200B;_Universal_&#x200B;作为HTML代码。
1. 保存新优惠。

![创建“洛杉矶”优惠](assets/offer_los_angeles.jpg)

## 结论

现在我们有受众和优惠。 在下一课中，我们将构建将位置、受众和优惠绑定在一起的活动，以创建个性化体验！

**[下一个：“个性化布局”>](personalize-layouts.md)**
