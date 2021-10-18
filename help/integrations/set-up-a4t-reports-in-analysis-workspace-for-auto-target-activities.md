---
title: 如何在Analysis Workspace中为自动定位活动设置A4T报表
description: 在您部署了Analytics for Target(A4T)集成并运行自动定位活动后，如何确保正确解释结果？ 请按照以下步骤在Analysis Workspace中配置A4T报表，以在运行自动定位活动时获得预期结果。
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 58006a25-851e-43c8-b103-f143f72ee58d
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '2252'
ht-degree: 1%

---

# 在Analysis Workspace中为[!DNL Auto-Target]活动设置A4T报表

用于[!DNL Auto-Target]活动的Analytics for Target(A4T)集成使用Adobe Target的组合机器学习(ML)算法，在使用Adobe Analytics目标量度的同时，根据每位访客的配置文件、行为和上下文为其选择最佳体验。

虽然Adobe Analytics Analysis Workspace中提供了丰富的分析功能，但由于实验活动（手动A/B和自动分配）与个性化活动([!DNL Auto-Target])之间存在差异，因此需要对默认的&#x200B;**[!UICONTROL Analytics for Target]**&#x200B;面板进行一些修改，才能正确解释[!DNL Auto-Target]活动。

本教程将介绍为分析工作区中的[!DNL Auto-Target]活动而推荐进行的修改，这些修改基于以下关键概念：

* **[!UICONTROL 控制与目标]**&#x200B;维度可用于区分控制体验与[!DNL Auto-Target]集成ML算法提供的控制体验。
* 在查看体验级别的性能划分时，应将访问次数用作标准化量度。 此外， [Adobe Analytics的默认计数方法可能包括用户实际上没有看到活动内容的访问](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-viewing-reports.html?lang=en#metrics)，但可以使用适当范围的区段修改此默认行为（详情如下）。
* 访问回顾范围的归因（在指定的归因模型上也称为“访问回顾窗口”）在Adobe Target的ML模型的培训阶段中使用，在划分目标量度时应使用相同的（非默认）归因模型。

## 在工作区中为[!DNL Auto-Target]面板创建A4T

要为[!DNL Auto-Target]报表创建A4T，请从工作区中的&#x200B;**[!UICONTROL Analytics for Target]**&#x200B;面板开始（如下所示），或从自由格式表开始。 然后，进行以下选择：

1. **[!UICONTROL 控制体验]**:您可以选择任何体验；但是，您以后将覆盖此选项。请注意，对于[!DNL Auto-Target]活动，控制体验实际上是一种控制策略，它可以是a)在所有体验中随机提供，或者b)提供单个体验(在Adobe Target中创建活动时做出此选择)。 即使您选择了选择(b)（即您的[!DNL Auto-Target]活动将特定体验指定为控制体验），您仍应遵循本教程中概述的用于分析[!DNL Auto-Target]活动的A4T的方法。
2. **[!UICONTROL 标准化量度]**:选择访问。
3. **[!UICONTROL 成功量度]**:尽管您可以选择要报告的任何量度，但通常应查看与在Adobe Target中创建活动期间为优化而选择的相同量度的报表。

![图1.](assets/Figure1.png)
*png图1:为活动设置Analytics for Target面 [!DNL Auto-Target] 板。*

>[!NOTE]
>
>要为自动定位活动设置Analytics for Target面板，请选择任意控制体验，选择访问量作为标准化量度，然后选择在Target活动创建过程中为优化而选择的相同目标量度。

## 使用控件与目标维度将Adobe Target的集成ML模型与您的控件进行比较

默认的A4T面板专为经典（手动）A/B测试或自动分配活动而设计，其目标是将各个体验的性能与控制体验进行比较。 但是，在[!DNL Auto-Target]活动中，第一阶比较应在控制&#x200B;*策略*&#x200B;和目标&#x200B;*策略*&#x200B;之间（即，确定[!DNL Auto-Target]集成ML模型在控制策略上的整体性能提升度）。

要执行此比较，请使用&#x200B;**[!UICONTROL 控制与目标(Analytics for Target)]**&#x200B;维度。 拖放以替换默认A4T报表中的&#x200B;**[!UICONTROL Target体验]**&#x200B;维度。

请注意，此替换操作将使A4T面板上的默认提升度和置信度计算失效。 为避免混淆，您可以从默认面板中删除这些量度，并保留以下报表：

![图2.](assets/Figure2.png)
*png图2:建议的活动基准 [!DNL Auto-Target] 报告。此报表已配置为将目标流量（由组合ML模型提供）与您的控制流量进行比较。*

>[!NOTE]
>
>目前，对于自动定位的A4T报表，无法使用控制维度和目标维度的提升度和置信度数值。 在添加支持之前，可以通过下载[置信度计算器](https://experienceleague.adobe.com/docs/target/assets/complete_confidence_calculator.xlsx?lang=en)来手动计算提升度和置信度。

## 添加量度的体验级别划分

要进一步了解组合ML模型的执行方式，您可以检查&#x200B;**[!UICONTROL 控制与目标]**&#x200B;维度的体验级别划分。 在工作区中，将&#x200B;**[!UICONTROL 定位体验]**&#x200B;维度拖动到您的报表上，然后分别划分控制维度和目标维度。

![图3.](assets/Figure3.png)
*png图3:按Target体验划分目标维度*

此处显示了结果报表的示例。

![图4.](assets/Figure4.png)
*png图4:具有体 [!DNL Auto-Target] 验级别划分的标准报表。请注意，您的目标量度可能不同，并且您的控制策略可能具有单个体验。*

>[!TIP]
>
>在工作区中，单击齿轮图标以隐藏转化率列中的百分比，以帮助保持对体验转化率的关注。 请注意，转换率随后将格式化为小数，但会相应地将其解释为百分比。

## 为什么“访问次数”是[!DNL Auto-Target]活动的正确标准化量度

分析[!DNL Auto-Target]活动时，请始终选择“访问次数”作为默认的标准化量度。 [!DNL Auto-Target] 个性化会为访客在每次访问时选择一次体验(正式为每个Adobe Target会话选择一次)，这意味着向用户显示的体验可以在每次访问时发生更改。因此，如果您使用独特访客作为标准化量度，那么单个用户最终可能会看到多个体验（跨不同访问）的事实会导致转化率混乱。

一个简单的示例说明了这一点：假设有两位访客进入一个只有两个体验的营销活动。 第一个访客两次访问。 在首次访问时，会为体验A分配配置文件，而在第二次访问时，则会为体验B分配配置文件状态（由于第二次访问时，其配置文件状态发生了更改）。 第二次访问后，访客通过下订单进行转化。 转化归因于最近显示的体验（体验B）。 第二位访客也访问了两次，并且两次都显示了体验B，但从不进行转化。

让我们比较访客级别和访问级别的报表：

| 体验 | 独特访客 | 访问次数 | 转化 | 访客标准。 康夫。 比率 | 访问标准。 康夫。 比率 |
| --- | --- | --- | --- | --- | --- |
| 同类群组 | 1 | 1 | - | 0% | 0% |
| B | 2 | 3 | 1 | 50% | 33.3% |
| 总计 | 2 | 4 | 1 | 50% | 25% |
*表1:对于决策对访问具有粘滞性（与常规A/B测试一样，对于不是访客）的情况，比较访客标准化报表和访问标准化报表的示例。在此方案中，访客标准化量度会令人困惑。*

如表中所示，访客级别的数字存在明显的不协调性。 尽管存在两个独特访客总数，但这并不是每个体验的各个独特访客总数。 虽然访客级别的转化率不一定是错误的，但在比较各个体验时，访问级别的转化率可以说更有意义。 从形式上讲，分析单位（“访问次数”）与决策吸引力单位相同，这意味着可以添加和比较量度的体验级别划分。

## 过滤活动的实际访问量

Adobe Analytics的Target活动访问次数默认计数方法可能包括用户未与Target活动进行交互的访问次数。 这是由于Target活动分配在Analytics访客上下文中持久保留的方式所致。 因此，Target活动的访问次数有时可能会被夸大，从而导致转化率下降。

如果您希望报告用户实际与自动定位活动进行交互的访问（通过进入活动、显示/访问事件或转化），则可以：

1. 创建一个特定区段，该区段包含来自相关Target活动的点击，然后
1. 使用此区段过滤访问量度。

**要创建区段，请执行以下操作：**

1. 选择工作区工具栏中的&#x200B;**[!UICONTROL 组件>创建区段]**&#x200B;选项。
2. 为区段输入&#x200B;**[!UICONTROL 标题]**。 在以下示例中，该区段名为[!DNL "Hit with specific Auto-Target activity"]。
3. 将&#x200B;**[!UICONTROL 目标活动]**&#x200B;维度拖动到区段&#x200B;**[!UICONTROL 定义]**&#x200B;部分。
4. 使用&#x200B;**[!UICONTROL equals]**&#x200B;运算符。
5. 搜索您的特定Target活动。
6. 选择齿轮图标，然后选择&#x200B;**[!UICONTROL 归因模型>实例]**，如下图所示。
7. 单击&#x200B;**[!UICONTROL 保存]**。

![图5.](assets/Figure5.png)
*png图5:使用如此处显示的区段，在A4T报表中过滤访问量 [!DNL Auto-Target] 度*

创建区段后，使用该区段过滤访问量度，因此访问量度仅包括用户与Target活动进行交互的访问。

**要使用此区段过滤访问，请执行以下操作：**

1. 将新创建的区段从组件工具栏中拖动，并将鼠标悬停在&#x200B;**[!UICONTROL 访问]**&#x200B;量度标签的基上，直到出现蓝色的&#x200B;**[!UICONTROL 按]**&#x200B;过滤提示。
2. 释放区段。 过滤器将应用于该量度。

最终面板将如下所示。

![图6.](assets/Figure6.png)
*png图6:“具有特定自动定位活动的点击”区段的报表面板应用于“访客”  量度。这可确保仅当用户实际与相关Target活动进行交互时，访问才会包含在报表中。*

## 在ML模型培训和目标量度生成之间调整归因

A4T集成允许[!DNL Auto-Target]的ML模型使用Adobe Analytics用于&#x200B;*生成性能报表*&#x200B;的相同转化事件数据进行&#x200B;*培训*。 然而，于培训ML模型时，在解释此数据时必须采用若干假设，该等假设与Adobe Analytics报告阶段所作之默认假设不同。

具体而言，Adobe Target的ML模型使用访问范围的归因模型。 也就是说，他们假定必须在同一访问中发生转化，以显示活动的内容，以便将转化“归因”到ML模型做出的决策。 这是Target保证及时培训其模型所必需的；在将转化(Adobe Analytics中报表的默认归因窗口)包含到其模型的培训数据中之前，Target无法等待长达30天的转化。

因此，Target模型（在培训期间）使用的归因与在查询数据（在报表生成期间）中使用的默认归因之间的差异可能会导致差异。 实际上，ML模型的问题与归因有关，这甚至可能表现不佳。

>[!TIP]
>
>如果ML模型针对与您在报表中查看的量度不同的量度进行了优化，则这些模型可能无法按预期执行！ 要避免这种情况，请确保报表中的目标量度使用Target ML模型所使用的相同归因。

要查看与Adobe Target ML模型所用归因方法相同的目标量度，请执行以下步骤：

1. 将鼠标悬停在目标量度的齿轮图标上：
   ![gearicon.png](assets/gearicon.png)
1. 在生成的菜单中，滚动到&#x200B;**[!UICONTROL 数据设置]**。
1. 选择&#x200B;**[!UICONTROL 使用非默认归因模型]**（如果尚未选择）：
   ![nondefaultattributionmodel.png](assets/non-defaultattributionmodel.png)
1.  点击&#x200B;**[!UICONTROL 编辑]**。
1. 选择&#x200B;**[!UICONTROL Model]**:**[!UICONTROL 参与率]**&#x200B;和&#x200B;**[!UICONTROL 回顾窗口]**:**[!UICONTROL 访问]**。
   ![ParticitionbyVisit.png](assets/ParticipationbyVisit.png)
1. 单击&#x200B;**[!UICONTROL 应用]**。

这些步骤可确保您的报表将目标量度归因于体验的显示，前提是目标量度事件在显示体验的同一访问中随时发生&#x200B;**（“参与”）。

## 最后一步：创建可捕获上述神奇功能的转化率

通过修改前面各节中的访问和目标量度，您对[!DNL Auto-Target]报表面板的默认A4T所做的最终修改是创建与适当过滤的“访问次数”量度的转化率（具有正确归因的目标量度的转化率）相比的正确比率。

通过使用以下步骤创建计算量度来执行此操作：

1. 选择工作区工具栏中的&#x200B;**[!UICONTROL 组件>创建量度]**&#x200B;选项。
1. 为量度输入&#x200B;**[!UICONTROL 标题]**。 例如，“活动XXX的访问更正转化率”。
1. 选择&#x200B;**[!UICONTROL 格式]** =百分比，**[!UICONTROL 小数位]** = 2。
1. 将您活动的相关目标量度（例如，活动转化）拖到定义中，然后使用此目标量度上的齿轮图标将归因模型调整为（参与率|访问），如前面所述。
1. 从&#x200B;**[!UICONTROL Definition]**&#x200B;部分的右上角选择&#x200B;**[!UICONTROL Add > Container]**。
1. 选择两个容器之间的除法(÷)运算符。
1. 拖动您之前创建的区段（在本教程中名为“通过特定[!DNL Auto-Target]活动点击”），以用于此特定[!DNL Auto-Target]活动。
1. 将&#x200B;**[!UICONTROL 访问次数]**&#x200B;量度拖到区段容器中。
1. 单击&#x200B;**[!UICONTROL 保存]**。

此处显示了完整的计算量度定义。

![图7.](assets/Figure7.png)
*png图7:访问和归因更正的模型转化率量度定义。(请注意，此量度取决于您的目标量度和活动。 换言之，此量度定义在活动中不可重复使用。)*

>[!IMPORTANT]
>
>A4T面板中的转化率量度未链接到表格中的转化事件或标准化量度。 当您进行本教程中建议的修改时，转化率不会自动适应更改。 因此，如果您对转化事件归因和标准化量度之一（或两者兼有）进行了修改，则必须记住最后一步来修改转化率，如上所示。

## 摘要：[!DNL Auto-Target]报表的最终工作区面板示例

将上述所有步骤组合到一个面板中，下图显示了[!DNL Auto-Target] A4T活动推荐报表的完整视图。 此报表与Target机器学习模型用于优化目标量度的报表相同，它包含了本教程中讨论的所有细微差别和建议。 此报表还最接近传统Target报表驱动的[!DNL Auto-Target]活动中使用的计数方法。

![图8.](assets/Figure8.png)
*png图8:Adobe Analytics Workspace中的最终 [!DNL Auto-Target] A4T报表，该报表整合了对本文档前几节所述量度定义所做的所有调整。*
