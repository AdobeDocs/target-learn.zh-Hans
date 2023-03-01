---
title: 如何在中设置A4T报表 [!DNL Analysis Workspace] 对象 [!DNL Auto-Target] 活动
description: 如何在中配置A4T报表 [!DNL Analysis Workspace] 以获取运行时的预期结果 [!UICONTROL 自动定位] 活动？
badgePremium: label="Premium" type="Positive" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=en#premium" tooltip="See what's included in Target Premium."
badgeBeta: label="Beta" type="Informative"
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 58006a25-851e-43c8-b103-f143f72ee58d
source-git-commit: 12dc82a96a8df234d02dc56e9e5904571f2152ba
workflow-type: tm+mt
source-wordcount: '2636'
ht-degree: 1%

---

# 在中设置A4T报表 [!DNL Analysis Workspace] 对象 [!DNL Auto-Target] 活动

>[!NOTE]
>
>此功能目前为测试版，可供所有人使用 [Target Premium](https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=en#premium){target=_blank} 即将发布的版本中的客户。

>[!IMPORTANT]
>
>对象 [!UICONTROL 自动定位] 活动，则必须签入报表 [!DNL Analytics Workspace] 和手动创建A4T面板。

此 [!UICONTROL 目标分析] (A4T)集成 [!DNL Auto-Target] 活动使用 [!DNL Adobe Target]的集成机器学习(ML)算法，可在使用 [!DNL Adobe Analytics] 目标量度。

尽管中提供了丰富的分析功能， [!DNL Adobe Analytics] [!DNL Analysis Workspace]，对默认进行了一些修改 **[!UICONTROL 目标分析]** 需要面板才能正确解释 [!DNL Auto-Target] 活动，因为试验活动（手动A/B和自动分配）和个性化活动([!UICONTROL 自动定位])。

本教程介绍了用于分析的建议修改 [!UICONTROL 自动定位] 中的活动 [!DNL Workspace]，它们基于以下关键概念：

* 此 **[!UICONTROL 控制与目标]** 维度可用于区分控制体验与由提供的体验 [!UICONTROL 自动定位] 组合ML算法。
* 在查看体验级别的性能划分时，应将访问用作标准化量度。 此外， [Adobe Analytics的默认计数方法可能包括用户实际上看不到活动内容的访问](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-viewing-reports.html?lang=en#metrics)，但可以使用适当限定范围的区段修改此默认行为（详细信息见下文）。
* 访问回顾范围归因（在规定的归因模型上也称为“访问回顾窗口”）由使用 [!DNL Adobe Target]的ML模型在其培训阶段，在划分目标量度时应使用相同的（非默认）归因模型。

## 为以下对象创建A4T [!UICONTROL 自动定位] 面板位于 [!DNL Workspace]

为创建A4T [!UICONTROL 自动定位] 报告，或者以 **[!UICONTROL 目标分析]** 面板位于 [!DNL Workspace]，如下所示，或以自由格式表开头。 然后，进行以下选择：

1. **[!UICONTROL 控制体验]**：您可以选择任何体验；但是，您稍后将覆盖此选择。 请注意，对于 [!UICONTROL 自动定位] 活动时，控制体验实际上是一种控制策略，即a)在所有体验中随机提供，或b)提供单个体验(此选择在活动创建时于 [!DNL Adobe Target])。 即使您选择了(b)，您的 [!UICONTROL 自动定位] 活动指定特定体验作为控制 — 您仍然应该遵循本教程中概述的方法来分析A4T [!UICONTROL 自动定位] 活动。
2. **[!UICONTROL 标准化量度]**：选择访问次数。
3. **[!UICONTROL 成功量度]**：虽然您可以选择要报告的任何指标，但通常应查看有关在活动创建期间为优化而选择的相同指标的报告 [!DNL Target].

![图1.png](assets/Figure1.png)
*图1： [!UICONTROL 目标分析] 面板设置 [!UICONTROL 自动定位] 活动。*

>[!NOTE]
>
>要设置您的 [!UICONTROL 目标分析] 面板 [!UICONTROL 自动定位] 活动，选择任意控制体验，选择 [!UICONTROL 访问次数] 作为标准化量度，并选择与为优化期间相同的目标量度 [!DNL Target] 活动创建。

## 使用 [!UICONTROL 控制与目标] 用于比较 [!DNL Target] 将ML模型集成到控件

默认A4T面板专为经典（手动）A/B测试或 [!UICONTROL 自动分配] 目标是将各个体验的表现与控制体验进行比较的活动。 In [!UICONTROL 自动定位] 但是，第一级比较应该是在控制项之间 *策略* 和目标 *策略* (换言之，决定整体业绩提升之 [!UICONTROL 自动定位] Ensemble ML model over the Control strategy)。

要执行此比较，请使用 **[!UICONTROL 控制与目标(Analytics for Target)]** 维度。 拖放以替换 **[!UICONTROL Target体验]** 维度。

请注意，此替换会使A4T面板上的默认提升度和置信度计算失效。 为避免混淆，您可以从默认面板中删除这些指标，并留下以下报表：

![图2.png](assets/Figure2.png)

*图2：建议的基线报告 [!DNL Auto-Target] 活动。 此报表已配置为将目标流量（由集成ML模型提供）与控制流量进行比较。*

>[!NOTE]
>
>目前，提升度和置信度数字不适用于 [!UICONTROL 控制与目标] A4T报表的维度 [!UICONTROL 自动定位]. 在添加支持之前，可以通过下载手动计算提升度和置信度 [置信度计算器](https://experienceleague.adobe.com/docs/target/assets/complete_confidence_calculator.xlsx?lang=en).

## 添加体验级别的量度划分

要进一步了解集成ML模型的执行情况，可以检查的体验级别细分 **[!UICONTROL 控制与目标]** 维度。 In [!DNL Workspace]，拖动 **[!UICONTROL Target体验]** 将维度添加到报表中，然后分别划分每个控件维度和目标维度。

![图3.png](assets/Figure3.png)
*图3：按Target体验划分目标维度*

此处显示了生成报告的示例。

![图4.png](assets/Figure4.png)
*图4： A标准 [!UICONTROL 自动定位] 包含体验级别划分的报表。 请注意，您的目标量度可能不同，并且您的控制策略可能只有一个体验。*

>[!TIP]
>
>In [!DNL Workspace]，单击齿轮图标以隐藏 [!UICONTROL 转化率] 列，以帮助保持对体验转化率的关注。 请注意，转换率随后将设置为小数的格式，但会相应地将其解释为百分比。

## 为什么“访问次数”是正确的标准化量度 [!UICONTROL 自动定位] 活动

分析 [!UICONTROL 自动定位] 活动，始终选择 [!UICONTROL 访问次数] 作为默认标准化量度。 [!UICONTROL 自动定位] 个性化设置为访客每次访问选择一次体验（正式名称为，每次访问选择一次） [!DNL Adobe Target] 会话)，这意味着向用户显示的体验可以在每次访问时更改。 因此，如果您使用 [!UICONTROL 独特访客] 作为标准化量度，单个用户最终可能会看到多个体验（跨不同访问）这一事实可能会导致转化率令人困惑。

一个简单的示例演示了这一点：请考虑以下场景：两个访客进入了一个只有两个体验的营销活动。 第一个访客访问了两次。 他们在第一次访问时会被分配到体验A，但在第二次访问时会被分配到体验B（由于其配置文件状态在第二次访问时发生变化）。 在第二次访问后，访客通过下订单进行转化。 转化归因于最近显示的体验（体验B）。 第二个访客也访问了两次，并两次向访客显示体验B，但从未转化。

让我们比较访客级别报表和访问级别报表：

| 体验 | 独特访客 | 访问次数 | 转化 | 访客规范。 会议 比率 | 访问规范。 会议 比率 |
| --- | --- | --- | --- | --- | --- |
| 同类群组 | 1 | 1 | - | 0% | 0% |
| B | 2 | 3 | 1 | 50% | 33.3% |
| 总计 | 2 | 4 | 1 | 50% | 25% |

*表1：比较访客标准化和访问标准化的报表以确定决策对访问有粘性的情况（不是访客，与常规A/B测试一样）。 在这种情况下，访客规范化的量度会让人感到困惑。*

如表所示，访客级别的数字明显不一致。 尽管总有两个独特访客，但这并不是每个体验的单个独特访客数的总和。 尽管访客级别的转化率不一定错误，但在对个体体验进行比较时，访问级别的转化率可以说更有意义。 在形式上，分析单位（“访问量”）与决策绑定的单位相同，这意味着可以添加和比较体验级别的量度划分。

## 筛选活动的实际访问次数

此 [!DNL Adobe Analytics] 对访问的默认计数方法 [!DNL Target] 活动可能包括用户未与交互的访问 [!DNL Target] 活动。 这是由于以下方式 [!DNL Target] 活动分配将保留在 [!DNL Analytics] 访客上下文。 因此，访问 [!DNL Target] 活动有时会被夸大，导致转化率下降。

如果您希望报告用户实际与交互的访问 [!UICONTROL 自动定位] 活动（通过输入活动、显示/访问事件或转化），您可以：

1. 创建包含来自以下项点击的特定区段： [!DNL Target] 有问题的活动，然后
1. 筛选 [!UICONTROL 访问次数] 量度。

**要创建区段，请执行以下操作：**

1. 选择 **[!UICONTROL 组件>创建区段]** 中的选项 [!DNL Workspace] 工具栏。
2. 输入 **[!UICONTROL 标题]** 区段的。 在以下示例中，该区段名为 [!DNL "Hit with specific Auto-Target activity"].
3. 拖动 **[!UICONTROL Target活动]** 区段的维度 **[!UICONTROL 定义]** 部分。
4. 使用 **[!UICONTROL 等于]** 运算符。
5. 搜索您的特定 [!DNL Target] 活动。
6. 选择齿轮图标，然后选择 **[!UICONTROL 归因模型>实例]** 如下图所示。
7. 单击&#x200B;**[!UICONTROL 保存]**。

![图5.png](assets/Figure5.png)
*图5：使用如下所示的区段过滤 [!UICONTROL 访问次数] A4T中的量度 [!UICONTROL 自动定位] 报告*

创建区段后，使用该区段过滤 [!UICONTROL 访问次数] 量度，因此 [!UICONTROL 访问次数] 量度仅包括用户与其交互的访问 [!DNL Target] 活动。

**要筛选 [!UICONTROL 访问次数] 使用该区段：**

1. 从组件工具栏中拖动新创建的区段，并将光标悬停在 **[!UICONTROL 访问次数]** 量度标签，直到显示为蓝色 **[!UICONTROL 筛选条件]** 提示出现。
2. 发布区段。 该过滤器将应用于该量度。

最终面板将显示如下。

![图6.png](assets/Figure6.png)
*图6：将“具有特定自动定位活动的点击”区段应用于 [!UICONTROL 访问次数] 量度。 这可以确保仅访问用户实际与 [!DNL Target] 有问题的活动会包含在报表中。*

## 确保目标量度和归因与优化标准一致

A4T集成允许 [!UICONTROL 自动定位] ML模型将为 *已训练* 使用的转化事件数据与 [!DNL Adobe Analytics] 使用至 *生成性能报告*. 然而，在训练机器学习模型时须运用若干假设来解释此数据，此等假设与于报告阶段作出之预设假设有所不同。 [!DNL Adobe Analytics].

具体而言， [!DNL Adobe Target] ML模型使用访问范围的归因模型。 也就是说，他们假设转化必须发生在活动内容的显示所在的同一访问中，以便转化能够“归因”于ML模型做出的决策。 此为必需项 [!DNL Target] 保证模型及时训练； [!DNL Target] 最长无法等待30天的时间进行转换（中报表的默认归因窗口） [!DNL Adobe Analytics])，然后将其包含在其模型的训练数据中。

因此，所使用的归因与所使用的归因之间的差异 [!DNL Target] 模型（在培训期间）与查询数据（在报告生成期间）中使用的默认归因可能会导致差异。 甚至可能显示ML模型表现不佳，而实际上问题在于归因。

>[!TIP]
>
>如果ML模型正在优化某个量度的归因不同于您在报表中查看的量度，则模型可能无法按预期执行！ 要避免出现这种情况，请确保报表上的目标指标使用Target的ML模型使用的相同指标定义和归因。

准确的量度定义和归因设置取决于 [优化准则](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#supported) 您在活动创建期间指定。

### Target定义的转化或Analytics量度，具有 *最大限度地提高每次访问的量度值*

当指标为Target转化或Analytics指标时 **最大限度地提高每次访问的量度值**，则目标量度定义允许在同一访问中发生多个转化事件。
要查看与Adobe Target ML模型使用的归因方法相同的目标量度，请执行以下步骤：

![gearicon.png](assets/gearicon.png)

1. 从生成的菜单中，滚动到 **[!UICONTROL 数据设置]**.
1. 选择 **[!UICONTROL 使用非默认归因模型]** （如果尚未选择）：

![non-defaultattributionmodel.png](assets/non-defaultattributionmodel.png)

1.  点击&#x200B;**[!UICONTROL 编辑]**。
1. 选择 **[!UICONTROL 模型]**： **[!UICONTROL 参与率]**、和 **[!UICONTROL 回看窗口期]**： **[!UICONTROL 访问]**.

![ParticipationbyVisit.png](assets/ParticipationbyVisit.png)

1. 单击&#x200B;**[!UICONTROL 应用]**。

如果发生目标量度事件，这些步骤可确保报表将目标量度归因于体验的显示 *任何时间* （以下简称“参与率”）访客的点击次数。

### Analytics量度 *独特访问转化率*

**使用正量度区段定义访问**

在您选择的场景中 *最大限度地提高独特访问转化率* 作为优化标准，转化率的正确定义是指标值为正的访问次数分数。 这可以通过以下方式实现：创建一个区段过滤器，向下过滤到该指标为正值的访问次数，然后过滤访问次数量度。


1. 与之前一样，选择 **[!UICONTROL 组件>创建区段]** 选项。
2. 输入 **[!UICONTROL 标题]** 区段的。 在以下示例中，该区段名为 [!DNL "Visits with an order"].
3. 将您在优化目标中使用的基本量度拖动到区段中。 在以下示例中，我们使用 **订单** 量度，以便转化率测量记录了订单的访问次数的比例。
4. 在区段定义容器的左上角，选择 **[!UICONTROL 包括]** **访问**.
5. 使用 **[!UICONTROL 大于]** 运算符，并将值设置为0（即，此区段包含订单量度为正值的访问）
6. 单击&#x200B;**[!UICONTROL 保存]**。

![图7.png](assets/Figure7.png)
*图7：筛选顺序列出的访问的区段定义。 根据活动的优化量度，您必须使用适当的量度来替换订单*

**将此项应用于活动过滤量度中的访问**

此区段现在可用于过滤订单数为正数的访问，以及 [!DNL Auto-Target]活动。 筛选量度的过程与之前类似，在将新区段应用于已筛选的访问量度后，报表面板应当类似于图8

![图8.png](assets/Figure8.png)
*图8：具有正确的独特访问转化量度（即记录活动点击的访问次数）且转化量度（此示例中的订单）不为零的报表面板。*


## 最后步骤：创建可捕捉上述神奇的转化率

修改了 [!UICONTROL 访问] 以及前面部分中的目标量度，您应该对默认A4T进行的最终修改 [!UICONTROL 自动定位] “报表”面板用于创建正确比例的转化率，即具有正确归因的目标量度与适当过滤的量度的转化率 [!UICONTROL 访问次数] 量度。

要执行此操作，请使用以下步骤创建计算指标：

1. 选择 **[!UICONTROL “组件”>“创建指标”]** 中的选项 [!DNL Workspace] 工具栏。
1. 输入 **[!UICONTROL 标题]** （对于您的量度）。 例如，“活动XXX的访问校正转化率”。
1. 选择 **[!UICONTROL 格式]** =百分比和 **[!UICONTROL 小数位]** = 2.
1. 拖动活动的相关目标量度(例如， [!UICONTROL 活动转化])，然后使用此目标量度上的齿轮图标将归因模型调整为（参与率|访问），如之前所述。
1. 选择 **[!UICONTROL 添加>容器]** 从的右上角 **[!UICONTROL 定义]** 部分。
1. 选择两个容器之间的除(÷)运算符。
1. 拖动您之前创建的区段（名为“点击特定的”） [!UICONTROL 自动定位] 活动” — 针对此特定活动 [!DNL Auto-Target] 活动。
1. 拖动 **[!UICONTROL 访问次数]** 量度放入区段容器中。
1. 单击&#x200B;**[!UICONTROL 保存]**。

>[!TIP]
>
> 您还可以使用创建此量度 [快速计算量度功能](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html?lang=en).

此处显示了完整的计算量度定义。

![图9.png](assets/Figure9.png)
*图9：修正了访问和归因的模型转化率量度定义。 （请注意，此指标取决于您的目标指标和活动。） 换句话说，此量度定义无法跨活动重复使用。)*

>[!IMPORTANT]
>
>A4T面板中的转化率量度未链接到表中的转化事件或标准化量度。 进行本教程中建议的修改时，转化率不会自动适应这些更改。 因此，如果您对转化事件归因和标准化量度中的一个（或两者）进行修改，则必须记住作为最后一步来修改转化率，如上所示。

## 摘要：最终示例 [!DNL Workspace] 面板 [!UICONTROL 自动定位] 报告

下图将上述所有步骤合并到一个面板中，显示了针对以下项的推荐报告的完整视图： [!UICONTROL 自动定位] A4T活动。 此报表与 [!DNL Target] 用于优化目标指标的ML模型，它合并了本教程中讨论的所有细微差别和建议。 此报表也最接近传统方法中所使用的计数方法 [!DNL Target] — 报告驱动 [!UICONTROL 自动定位] 活动。

![图10.png](assets/Figure10.png)
*图10：最终的A4T [!UICONTROL 自动定位] 报告位置 [!DNL Adobe Analytics] [!DNL Workspace]，其中合并了本文档前面部分中描述的所有量度定义调整。*
