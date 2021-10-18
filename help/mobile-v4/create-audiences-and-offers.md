---
title: 在Adobe Target中创建受众和选件
description: '在本课程中，我们将在Adobe Target中为之前课程中实施的三个位置构建受众和选件。 这些体验将用于在下一课程中显示个性化体验。   '
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
exl-id: 4b153e4f-a979-49a8-8c26-f7ac95162a2f
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 1%

---

# 在Adobe Target中创建受众和选件

在本课程中，我们将转到[!DNL Target]界面，为我们在前面的课程中实施的三个位置构建受众和选件。

## 学习目标

在本课程结束时，您将能够：

* 在 Adobe Target 中创建受众
* 在Adobe Target中创建选件

更具体地说，在本课程中，我们将创建受众和选件，以完成在教程开始时定义的个性化用例。 我们希望使用“主页”和“搜索”屏幕来帮助应用程序用户预订其行程，并且我们希望使用“感谢”屏幕来根据用户的目标显示一些相关的促销活动。 下面是一个表，它表示我们将在本课程中为每个位置构建的内容：

| 位置 | 受众 | 选件 |
| --- | --- | --- |
| wetravel_engage_home | 新移动设备应用程序用户 | &quot;选择您的原点和目的地以搜索可用的巴士路线&quot; |
| wetravel_engage_search | 新移动设备应用程序用户 | “使用过滤器缩小搜索结果” |
| wetravel_engage_home | 返回移动设备应用程序用户 | “欢迎回来！ 在结帐期间使用促销代码BACK30可享受10%的折扣。” |
| wetravel_engage_search | 返回移动设备应用程序用户 | default content（默认内容） |
| wetravel_context_dest | 目标：圣地亚哥 | &quot;DJ&quot; |
| wetravel_context_dest | 目标：洛杉矶 | &quot;通用&quot; |

## 选择工作区

如果您的公司使用“属性”和“工作区”来为个性化应用程序和网站建立边界（您在上一课程中实施了at_property参数），则在继续学习本课程之前，应首先确保您位于正确的工作区中。 如果不使用“属性”和“工作区”，只需忽略此步骤。 选择您在上一课程中使用的工作区以复制at_property值：

![工作区示例](assets/workspace.jpg)

## 创建受众

现在，让我们创建将用于个性化应用程序的受众。

### 为新用户创建受众

Adobe Target受众用于识别特定的访客组。 然后，可以将选件定位到这些特定群组。 对于前两个位置，我们将使用“新用户”受众：

1. 单击顶部导航中的&#x200B;**[!UICONTROL Audiences]**。
1. 单击&#x200B;**[!UICONTROL 创建受众]**按钮。
   ![创建新用户受众](assets/audience_new_mobile_app_users_1.jpg)

1. 输入&#x200B;**[!UICONTROL 新移动设备应用程序用户]**&#x200B;作为受众名称。
1. 选择&#x200B;**[!UICONTROL Add Rule]**。
1. 选择&#x200B;**[!UICONTROL Custom]**规则。
   ![创建新用户受众](assets/audience_new_mobile_app_users_2.jpg)

1. 选择&#x200B;**[!UICONTROL a.Launches]**。
1. 选择&#x200B;**[!UICONTROL 小于]**。
1. 输入&#x200B;**5**。
1. 保存新受众。
   ![创建新用户受众](assets/audience_new_mobile_app_users_3.jpg)

### 为回访用户创建受众

按照上面所列的相同步骤为旧用户创建受众。

1. 将受众命名为&#x200B;_Returning Mobile App用户_。
1. 使用&#x200B;**[!UICONTROL a.Launches大于或等于5]**&#x200B;作为自定义规则。
1. 保存新受众。

   ![创建回访用户受众](assets/audience_returning_mobile_app_users.jpg)

>[!NOTE]
>
>在[!DNL Target] Mobile SDK中收集的所有生命周期量度和维度都带有“a”前缀（例如a.Launchs），并且可在下拉菜单的“自定义”选项中使用，并可用于构建受众。

### 为预订圣地亚哥之旅的用户创建受众

接下来，我们将为We.Travel应用程序提供的一些目标创建一些受众。 在上一课中，我们将目标作为位置参数传递到wetravel_context_dest位置请求中。 该参数位于下拉菜单的“自定义”选项中。

>[!NOTE]
>
>如果您希望在“自定义”下拉列表中看到的参数未显示在[!DNL Target]界面中，请仔细检查请求中是否确实传递了该参数。 如果您已验证请求中存在，但未延迟加载到[!DNL Target]界面中，则只需键入参数名称并按Enter键即可继续定义受众

1. 将受众命名为&#x200B;_目标：圣地亚哥_。
1. 使用以下定义的自定义规则：_locationDest包含San Diego_。
1. 保存新受众。

   ![创建“圣地亚哥”受众](assets/audience_locationDest_san_diego.jpg)

### 为预订洛杉矶之行的用户创建受众

1. 将受众命名为&#x200B;_目标：洛杉矶_
1. 使用以下定义的自定义规则：_locationDest包含Los Angeles_
1. 保存新受众。

![创建“洛杉矶”受众](assets/audience_locationDest_los_angeles.jpg)

## 创建选件

现在，让我们创建选件以显示这些消息。 请注意，选件是代码/内容的片段，在[!DNL Target]响应中提供。 这些片段通常在[!DNL Target]用户界面中创建，但也可以通过API或使用体验片段与Adobe Experience Manager的集成来创建。 在移动设备应用程序中，JSON选件很常见。 在本教程中，我们将使用HTML选件，该选件可用于将任何纯文本内容（包括JSON）交付到应用程序中。

### 为新用户创建选件

首先，让我们为发送给新用户的消息创建选件：

1. 单击顶部导航中的&#x200B;**[!UICONTROL 选件]**。
1. 单击&#x200B;**[!UICONTROL 创建]**。
1. 选择&#x200B;**[!UICONTROL HTML选件]**。

   ![创建主页选件](assets/offer_home_1.jpg)

1. 将选件命名为&#x200B;_Home:吸引新用户_。
1. 输入&#x200B;_选择源和目标以搜索可用总线_&#x200B;作为代码。
1. 保存新选件。

   ![创建主页HTML选件](assets/offer_home_2.jpg)

### 为回访用户创建选件

现在，让我们为旧用户创建一个选件（第二个选件将是默认内容，该内容将不显示任何内容）：

1. 将选件命名为&#x200B;_Home:返回用户_。
1. 输入&#x200B;_欢迎返回！ 在结帐期间使用促销代码BACK30可享受10%的折扣。_ 作为HTML代码。
1. 保存新选件。

   ![创建主页HTML选件](assets/offer_home_returning_users.jpg)

### 创建圣地亚哥优惠

当“DJ”返回到ThankYou活动时，filterRecommendationsBasedOnOffer()函数中的逻辑将显示“Rock Night with DJ SAM”的横幅：

1. 将选件命名为&#x200B;_Promotion for San Diego_。
1. 输入&#x200B;_DJ_&#x200B;作为HTML代码。
1. 保存新选件。

![创建“圣地亚哥”优惠](assets/offer_san_diego.jpg)

### 为前往洛杉矶的用户创建选件

当“感谢”活动返回“通用”时，filterRecommendationsBasedOnOffer()函数中的逻辑将显示“通用工作室”的横幅：

1. 将选件命名为&#x200B;_Promotion for Los Angeles_。
1. 输入&#x200B;_Universal_&#x200B;作为HTML代码。
1. 保存新选件。

![创建“洛杉矶”选件](assets/offer_los_angeles.jpg)

## 结论

现在，我们提供了受众和选件。 在下一课程中，我们将构建将位置、受众和选件绑定在一起的活动，以创建个性化体验！

**[下一步：“个性化布局”>](personalize-layouts.md)**
