---
title: 如何在中设置A4T报表 [!DNL Analysis Workspace] 对象 [!DNL Auto-Target] 活动
description: 如何在中配置A4T报表 [!DNL Analysis Workspace] 获得运行时的预期结果 [!UICONTROL 自动定位] 活动？
badgePremium: label="Premium" type="Positive" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html#premium newtab=true" tooltip="请参阅Target Premium中包含的内容。"
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
thumbnail: null
kt: null
exl-id: 58006a25-851e-43c8-b103-f143f72ee58d
source-git-commit: 78e5b5f7fa8f4c1a08c06c6d2b0e1a5242cd464c
workflow-type: tm+mt
source-wordcount: '2658'
ht-degree: 1%

---

# 在中设置A4T报表 [!DNL Analysis Workspace] 对象 [!DNL Auto-Target] 活动

>[!IMPORTANT]
>
>对象 [!UICONTROL 自动定位] 活动，则必须签入报表 [!DNL Analytics Workspace] 和手动创建A4T面板。

此 [!UICONTROL 目标分析] (A4T)集成 [!DNL Auto-Target] 活动使用 [!DNL Adobe Target] 集成机器学习(ML)算法，可在使用 [!DNL Adobe Analytics] 目标量度。

尽管中提供了丰富的分析功能， [!DNL Adobe Analytics] [!DNL Analysis Workspace]，对默认进行了一些修改 **[!UICONTROL 目标分析]** 需要面板才能正确解释 [!DNL Auto-Target] 活动，因为试验活动之间的差异(手动 [!UICONTROL A/B测试] 和 [!UICONTROL 自动分配])和个性化活动([!UICONTROL [!UICONTROL 自动定位]])。

本教程将介绍为分析而推荐的修改 [!UICONTROL 自动定位] 中的活动 [!DNL Analysis Workspace]，它们基于以下关键概念：

* 此 **[!UICONTROL 控制与目标]** 维度可用于区分 [!UICONTROL 控件] 体验与 [!UICONTROL 自动定位] 组合ML算法。
* 在查看体验级别的性能划分时，应将访问用作标准化量度。 另外， [Adobe Analytics的默认计数方法可能包括用户实际上看不到活动内容的访问](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-viewing-reports.html#metrics){target=_blank}，但可以使用适当限定范围的区段修改此默认行为（详细信息见下文）。
* 访问回顾范围归因，在规定的归因模型上也称为“访问回顾窗口”，用于 [!DNL Adobe Target] ML模型在其培训阶段使用，在划分目标量度时应使用相同的（非默认）归因模型。

## 为创建A4T [!UICONTROL 自动定位] 面板位于 [!DNL Analysis Workspace]

为创建A4T [!UICONTROL 自动定位] 报告，或者以 **[!UICONTROL 目标分析]** 面板位于 [!DNL Analysis Workspace]，如下所示，或以自由格式表开头。 然后，进行以下选择：

1. **[!UICONTROL 控制体验]**：您可以选择任何体验；但是，您稍后将覆盖此选择。 请注意，对于 [!UICONTROL 自动定位] 活动时，控制体验实际上是一种控制策略，该策略可以为a)在所有体验中随机提供，或b)提供单个体验(此选择是在活动创建时在 [!DNL Adobe Target])。 即使您选择了(b)，您的 [!UICONTROL 自动定位] 活动指定特定体验作为控制。 您仍然应该按照本教程中概述的方法分析A4T [!UICONTROL 自动定位] 活动。
2. **[!UICONTROL 标准化量度]**：选择 [!UICONTROL 访问].
3. **[!UICONTROL 成功量度]**：虽然您可以选择要报告的任何量度，但您通常应该查看与活动创建期间为优化选择的量度有关的报表 [!DNL Target].

   ![[!UICONTROL 目标分析] 面板设置 [!UICONTROL 自动定位] 活动。](assets/Figure1.png)

   *图1 ： [!UICONTROL 目标分析] 面板设置 [!UICONTROL 自动定位] 活动。*

>[!TIP]
>
>设置您的 [!UICONTROL 目标分析] 面板 [!UICONTROL 自动定位] 活动，选择任意控制体验，选择 [!UICONTROL 访问] 作为标准化量度，并选择在此期间为优化选择的相同目标量度 [!DNL Target] 活动创建。

## 使用 [!UICONTROL 控制与目标] 用于比较 [!DNL Target] 将ML模型集成到控件

默认A4T面板专为classic（手动）设计 [!UICONTROL A/B测试] 或 [!UICONTROL 自动分配] 目标是将各个体验的表现与控制体验进行比较的活动。 在 [!UICONTROL 自动定位] 但是，首先应该对控件之间的值进行比较 *策略* 和目标 *策略*. 换言之，确定 [!UICONTROL 自动定位] 对控制策略进行ML模型集成。

要执行此比较，请使用 **[!UICONTROL 控制与目标（目标分析）]** 维度。 拖放以替换 **[!UICONTROL Target体验]** 维度。

请注意，此替换将使默认内容无效 [!UICONTROL 提升度和置信度] 在A4T面板上的计算。 为避免混淆，您可以从默认面板中删除这些量度，并保留以下报表：

![[!UICONTROL 按活动转化显示的体验] 面板位于 [!DNL Analysis Workspace]](assets/Figure2.png)

*图2：建议的基线报告 [!DNL Auto-Target] 活动。 此报表已配置为将目标流量（由集成ML模型提供）与您的控制流量进行比较。*

>[!NOTE]
>
>目前， [!UICONTROL 提升度和置信度] 数字不可用于 [!UICONTROL 控制与目标] A4T报表的维度 [!UICONTROL 自动定位]. 在添加支持之前， [!UICONTROL 提升度和置信度] 可以通过下载 [置信度计算器](https://experienceleague.adobe.com/docs/target/assets/complete_confidence_calculator.xlsx).

## 添加量度的体验级别细分

要进一步了解集成ML模型的执行情况，可以检查体验级别的 **[!UICONTROL 控制与目标]** 维度。 在 [!DNL Analysis Workspace]，拖动 **[!UICONTROL Target体验]** 将维度添加到报表中，然后分别划分每个控件维度和目标维度。

![[!UICONTROL 按活动转化显示的体验] 面板位于 [!DNL Analysis Workspace]](assets/Figure3.png)

*图3：按Target体验划分目标维度*

此处显示了生成报表的示例。

![[!UICONTROL 按活动转化显示的体验] 面板位于 [!DNL Analysis Workspace]](assets/Figure4.png)

*图4：标准 [!UICONTROL 自动定位] 具有体验级划分的报表。 请注意，您的目标量度可能不同，并且您的控制策略可能只有一个体验。*

>[!TIP]
>
>在 [!DNL Analysis Workspace]，单击齿轮图标以隐藏 [!UICONTROL 转化率] 列，可帮助将焦点始终放在体验转化率上。 转换率随后将格式化为小数，但会相应地将其解释为百分比。

## 为什么”[!UICONTROL 访问]”是正确的标准化量度 [!UICONTROL 自动定位] 活动

分析 [!UICONTROL 自动定位] 活动，始终选择 [!UICONTROL 访问] 作为默认标准化量度。 [!UICONTROL 自动定位] 个性化为访客选择一次体验（正式名称为，每次访问一次） [!DNL Target] 会话)，这意味着向访客显示的体验可以在每次访问时更改。 因此，如果您使用 [!UICONTROL 独特访客] 作为标准化量度，单个用户最终可能会看到多个体验（跨不同访问）这一事实可能会导致转化率混乱。

一个简单的示例演示了这一点：考虑一个场景，其中两个访客进入的营销活动只有两个体验。 第一个访客访问了两次。 访客在第一次访问时被分配给体验A，但在第二次访问时被分配给体验B（由于其配置文件状态在第二次访问时发生变化）。 在第二次访问后，访客通过下订单进行转化。 转化归因于最近显示的体验（体验B）。 第二个访客还会访问两次，并且两次都向访客显示体验B，但不会转化。

让我们比较访客级别报表和访问级别报表：

| 体验 | 独特访客 | 访问次数 | 转化 | 访客规范化的转化率 | 访问标准化转化率 |
| --- | --- | --- | --- | --- | --- |
| 同类群组 | 1 | 1 | - | 0% | 0% |
| B | 2 | 3 | 1 | 50% | 33.3% |
| 总计 | 2 | 4 | 1 | 50% | 25% |

*表1：比较访客标准化和访问标准化报表以确定决策对访问（而非访客，如常规A/B测试）有粘性的情况的示例。 在这种情况下，访客规范化的量度会让人感到困惑。*

如表所示，访客级别的数字存在明显的不一致性。 尽管存在两个总独特访客，但这不是每个体验的单个独特访客的总和。 尽管访客级别的转化率不一定错误，但在比较各个体验时，访问级别的转化率可能更有意义。 在形式上，分析单位（“访问量”）与决策绑定的单位相同，这意味着可以添加和比较体验级别的量度细分。

## 筛选活动的实际访问次数

此 [!DNL Adobe Analytics] 对访问的默认计数方法 [!DNL Target] 活动可能包括用户未与交互的访问 [!DNL Target] 活动。 这是由于以下方式 [!DNL Target] 活动分配将保留在 [!DNL Analytics] 访客上下文。 因此，访问 [!DNL Target] 活动有时可能被夸大，导致转化率降低。

如果您希望报告用户实际与交互的访问 [!UICONTROL 自动定位] 活动（通过输入活动、显示或访问事件，或转化），您可以：

1. 创建包含来自以下各项的点击的特定区段： [!DNL Target] 有问题的活动，然后
1. 筛选 [!UICONTROL 访问] 量度。

**要创建区段，请执行以下操作：**

1. 选择 **[!UICONTROL 组件>创建区段]** 中的选项 [!DNL Analysis Workspace] 工具栏。
2. 指定 **[!UICONTROL 标题]** ，以了解您的区段。 在以下示例中，该区段名为 [!DNL "Hit with specific Auto-Target activity"].
3. 拖动 **[!UICONTROL Target活动]** 区段的维度 **[!UICONTROL 定义]** 部分。
4. 使用 **[!UICONTROL 等于]** 运算符。
5. 搜索您的特定 [!DNL Target] 活动。
6. 单击齿轮图标，然后选择 **[!UICONTROL 归因模型>实例]** 如下图所示。
7. 单击&#x200B;**[!UICONTROL 保存]**。

![中的区段 [!DNL Analysis Workspace]](assets/Figure5.png)

*图5：使用如下所示的区段过滤 [!UICONTROL 访问] A4T中的量度 [!UICONTROL 自动定位] 报告*

创建区段后，使用该区段过滤 [!UICONTROL 访问] 量度，因此 [!UICONTROL 访问] 量度仅包括用户与其交互的访问 [!DNL Target] 活动。

**要筛选 [!UICONTROL 访问] 使用该区段：**

1. 从组件工具栏中拖动新创建的区段，并将光标悬停在 **[!UICONTROL 访问]** 量度标签，直到显示为蓝色 **[!UICONTROL 过滤方式]** 出现提示。
2. 发布区段。 过滤器将应用于该量度。

最终面板如下所示：

![[!UICONTROL 按活动转化显示的体验] 面板位于 [!DNL Analysis Workspace]](assets/Figure6.png)

*图6：报表面板，其中将“具有特定自动定位活动的点击”区段应用于 [!UICONTROL 访问] 量度。 此区段确保只有用户实际与交互的访问 [!DNL Target] 相关活动会包含在报表中。*

## 确保目标量度和归因与优化标准保持一致

A4T集成允许 [!UICONTROL 自动定位] ML模型将为 *已训练* 使用与以下内容相同的转化事件数据 [!DNL Adobe Analytics] 用于 *生成性能报表*. 然而，在训练ML模型时必须采用若干假设来解释此数据，这与 [!DNL Adobe Analytics].

具体而言， [!DNL Adobe Target] ML模型使用访问范围的归因模型。 也就是说，ML模型假设转化必须与活动内容的显示发生在同一访问中，这样转化才会“归因”到ML模型所做的决策。 这是以下项所必需的 [!DNL Target] 保证及时培训模型； [!DNL Target] 最长不能等待30天进行转换（中报表的默认归因窗口） [!DNL Adobe Analytics])，然后将其包含在其模型的训练数据中。

因此，促销活动使用的归因与 [!DNL Target] 模型（在训练期间）与查询数据时使用的默认归因（在生成报表期间）可能会导致差异。 甚至可能显示ML模型表现不佳，而实际上问题出在归因上。

>[!TIP]
>
>如果ML模型正在针对某个量度进行优化，而该量度的归因不同于您在报表中查看的量度，则模型可能无法按预期发挥作用。 要避免出现这种情况，请确保报表上的目标量度使用的量度定义和归因与使用的相同 [!DNL Target] ml模型。

准确的量度定义和归因设置取决于 [优化准则](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank} 您在活动创建期间指定。

### 目标定义的转化，或 [!DNL Analytics] 量度 *最大限度地提高每次访问的量度值*

当指标为 [!DNL Target] 转化，或 [!DNL Analytics] 量度 **最大限度地提高每次访问的量度值**，则目标量度定义允许在同一次访问中发生多个转化事件。

查看具有相同归因方法的目标量度，这些方法由 [!DNL Target] ML模型，请按照以下步骤操作：

1. 将鼠标悬停在目标量度的齿轮图标上：

   ![gearicon.png](assets/gearicon.png)

1. 从生成的菜单中，滚动到 **[!UICONTROL 数据设置]**.
1. 选择 **[!UICONTROL 使用非默认归因模型]** （如果尚未选择）。

   ![non-defaultattributionmodel.png](assets/non-defaultattributionmodel.png)

1.  点击&#x200B;**[!UICONTROL 编辑]**。
1. 选择 **[!UICONTROL 模型]**： **[!UICONTROL 参与率]**、和 **[!UICONTROL 回看窗口期]**： **[!UICONTROL 访问]**.

   ![ParticipationbyVisit.png](assets/ParticipationbyVisit.png)

1. 单击&#x200B;**[!UICONTROL 应用]**。

如果发生目标量度事件，这些步骤可确保报表将目标量度归因于体验的显示 *任何时间* （“参与率”）访客的点击次数。

### [!DNL Analytics] 量度 *独特访问转化率*

**使用正量度区段定义访问**

在您选择的场景中 *最大限度地提高独特访问转化率* 作为优化标准，转化率的正确定义是指标值为正的访问次数的比例。 可通过以下方法来实现这一点：创建区段过滤以找出指标为正值的访问次数，然后过滤访问次数量度。

1. 与之前一样，选择 **[!UICONTROL 组件>创建区段]** 中的选项 [!DNL Analysis Workspace] 工具栏。
2. 指定 **[!UICONTROL 标题]** ，以了解您的区段。

   在以下示例中，该区段名为 [!DNL "Visits with an order"].

3. 将您在优化目标中使用的基本指标拖动到区段中。

   在下面显示的示例中，我们使用 **订单** 量度，以便转化率测量记录了订单的访问次数。

4. 在区段定义容器的左上角，选择 **[!UICONTROL 包括]** **访问**.
5. 使用 **[!UICONTROL 大于]** 运算符，并将值设置为0。

   将该值设置为0意味着此区段包含订单量度为正值的访问。

6. 单击&#x200B;**[!UICONTROL 保存]**。

![图7.png](assets/Figure7.png)

*图7：区段定义过滤顺序列出的访问。 根据活动的优化量度，您必须使用相应的量度替换订单*

**将此项应用于活动过滤量度中的访问**

此区段现在可用于过滤订单数为正数的访问，以及 [!DNL Auto-Target] 活动。 过滤量度的过程与之前类似，如果将新区段应用于已过滤的访问量度，则报表面板的外观应类似于图8

![图8.png](assets/Figure8.png)

*图8：具有正确的独特访问转化量度的报表面板：记录来自活动的点击并且转化量度（本示例中的订单）非零的访问次数。*

## 最后步骤：创建可捕捉上述神奇的转化率

修改了 [!UICONTROL 访问] 以及前面部分中的目标量度，您应该对默认A4T进行的最终修改 [!DNL Auto-Target] 报表面板创建的转化率与经过适当过滤的“访问量”量度之间的比率是正确的 — 即经过更正的目标量度。

做法是创建 [!UICONTROL 计算量度] ，请执行以下步骤：

1. 选择 **[!UICONTROL “组件”>“创建指标”]** 中的选项 [!DNL Analysis Workspace] 工具栏。
1. 指定 **[!UICONTROL 标题]** （对于您的量度）。 例如，“活动XXX的访问校正转化率”。
1. 选择 **[!UICONTROL 格式]** =百分比和 **[!UICONTROL 小数位]** = 2.
1. 拖动活动的相关目标量度(例如， [!UICONTROL 活动转化])，然后使用此目标量度上的齿轮图标将归因模型调整为（参与率|访问），如之前所述。
1. 选择 **[!UICONTROL 添加>容器]** 从的右上角 **[!UICONTROL 定义]** 部分。
1. 选择两个容器之间的除(÷)运算符。
1. 拖动您之前创建的名为“点击特定 [!UICONTROL 自动定位] 活动”一节 [!DNL Auto-Target] 活动。
1. 拖动 **[!UICONTROL 访问]** 量度放入区段容器中。
1. 单击&#x200B;**[!UICONTROL 保存]**。

>[!TIP]
>
> 您还可以使用创建此量度 [快速计算量度功能](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html).

此处显示了完整的计算量度定义。

![图9.png](assets/Figure9.png)

*图7：经访问校正和归因校正的模型转化率量度定义。 (请注意，此指标取决于您的目标指标和活动。 换句话说，此量度定义无法跨活动重复使用。)*

>[!IMPORTANT]
>
>此 [!UICONTROL 转化] A4T面板中的比率量度未链接到表中的转化事件或标准化量度。 进行本教程中建议的修改时， [!UICONTROL 转化] 费率不会自动适应变化。 因此，如果您对转化事件归因或标准化量度（或两者）进行了修改，则必须记住作为最后步骤也是要修改 [!UICONTROL 转化] 比率，如上所示。

## 摘要：最终示例 [!DNL Analysis Workspace] 面板 [!UICONTROL 自动定位] 报表

将以上所有步骤合并到一个面板中，下图显示了针对以下项的推荐报告的完整视图 [!UICONTROL 自动定位] A4T活动。 此报表与 [!DNL Target] 用于优化目标量度的ML模型。 该报告包含本教程中讨论的所有细微差别和建议。 此报表也最接近传统方法中所用的计数方法 [!DNL Target] — 报告驱动 [!UICONTROL 自动定位] 活动。

单击以展开图像。

![中的最终A4T报告 [!DNL Analysis Workspace]](assets/Figure10.png "Analysis Workspace中的A4T报表"){width="600" zoomable="yes"}

*图10：最终的A4T [!UICONTROL 自动定位] 报告位置 [!DNL Adobe Analytics] [!DNL Workspace]，其中包含对本教程前面部分中描述的量度定义进行的所有调整。*
