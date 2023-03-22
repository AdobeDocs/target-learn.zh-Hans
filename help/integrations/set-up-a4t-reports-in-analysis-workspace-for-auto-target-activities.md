---
title: 如何在 [!DNL Analysis Workspace] 表示 [!DNL Auto-Target] 活动
description: 如何在 [!DNL Analysis Workspace] 以在运行时获得预期结果 [!UICONTROL 自动定位] 活动？
badgePremium: label="Premium" type="Positive" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html#premium newtab=true" tooltip="See what's included in Target Premium."
badgeBeta: label="Beta" type="Informative" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html#beta newtab=true" tooltip="What are Target Beta release features?"
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
thumbnail: null
kt: null
exl-id: 58006a25-851e-43c8-b103-f143f72ee58d
source-git-commit: 538dfe6a26b4f62c52b24d54a189738677e63bf3
workflow-type: tm+mt
source-wordcount: '2641'
ht-degree: 1%

---

# 在中设置A4T报表 [!DNL Analysis Workspace] 表示 [!DNL Auto-Target] 活动

>[!IMPORTANT]
>
>对于 [!UICONTROL 自动定位] 活动时，必须在 [!DNL Analytics Workspace] 和手动创建A4T面板。

的 [!UICONTROL Analytics for Target] (A4T)集成 [!DNL Auto-Target] 活动使用 [!DNL Adobe Target] 集成机器学习(ML)算法，可在使用 [!DNL Adobe Analytics] 目标量度。

尽管在 [!DNL Adobe Analytics] [!DNL Analysis Workspace]，对默认值进行一些修改 **[!UICONTROL Analytics for Target]** 面板需要正确解释 [!DNL Auto-Target] 活动，因为实验活动(手动 [!UICONTROL A/B测试] 和 [!UICONTROL 自动分配])和个性化活动([!UICONTROL [!UICONTROL 自动定位]])。

本教程将演示为分析而推荐的修改 [!UICONTROL 自动定位] 活动 [!DNL Analysis Workspace]，这些概念基于以下关键概念：

* 的 **[!UICONTROL 控制与目标]** 维度可用于区分 [!UICONTROL 控制] 体验与由提供的体验 [!UICONTROL 自动定位] 集成ML算法。
* 在查看体验级别的性能划分时，应将访问次数用作标准化量度。 此外， [Adobe Analytics的默认计数方法可能包括用户实际看不到活动内容的访问](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-viewing-reports.html#metrics){target=_blank}，但可以使用适当范围的区段修改此默认行为（详细信息如下）。
* 访问回顾范围的归因（也称为指定归因模型上的“访问回顾窗口”）由 [!DNL Adobe Target] ML模型（在其培训阶段），在划分目标量度时应使用相同的（非默认）归因模型。

## 为创建A4T [!UICONTROL 自动定位] 面板 [!DNL Analysis Workspace]

为 [!UICONTROL 自动定位] 报表，以 **[!UICONTROL Analytics for Target]** 面板 [!DNL Analysis Workspace]，如下所示，或以自由格式表开头。 然后，进行以下选择：

1. **[!UICONTROL 控制体验]**:您可以选择任何体验；但是，您以后将覆盖此选项。 请注意，对于 [!UICONTROL 自动定位] 活动时，控制体验实际上是一种控制策略，即a)在所有体验中随机提供，或b)提供单个体验(在 [!DNL Adobe Target])。 即使您选择(b)，您的 [!UICONTROL 自动定位] 活动会指定特定体验作为控制。 您仍应遵循本教程中概述的用于分析 [!UICONTROL 自动定位] 活动。
2. **[!UICONTROL 标准化量度]**:选择 [!UICONTROL 访问次数].
3. **[!UICONTROL 成功量度]**:尽管您可以选择要报告的任何量度，但通常应查看与在 [!DNL Target].

   ![[!UICONTROL Analytics for Target] 面板设置 [!UICONTROL 自动定位] 活动。](assets/Figure1.png)

   *图1: [!UICONTROL Analytics for Target] 面板设置 [!UICONTROL 自动定位] 活动。*

>[!TIP]
>
>设置 [!UICONTROL Analytics for Target] 面板 [!UICONTROL 自动定位] 活动，选择任何控制体验，选择 [!UICONTROL 访问次数] 标准化量度，并选择在 [!DNL Target] 活动创建。

## 使用 [!UICONTROL 控制与目标] 要比较的维度 [!DNL Target] 将ML模型集成到控制

默认的A4T面板专为经典（手动）设计 [!UICONTROL A/B测试] 或 [!UICONTROL 自动分配] 活动，其目标是将各个体验的性能与控制体验进行比较。 在 [!UICONTROL 自动定位] 但是，第一顺序比较应当是控制 *策略* 和目标 *策略*. 换句话说，确定 [!UICONTROL 自动定位] 集成ML模型在控制策略上。

要执行此比较，请使用 **[!UICONTROL 控制与目标(Analytics for Target)]** 维度。 拖放以替换 **[!UICONTROL 定位体验]** 维度。

请注意，此替换将使默认 [!UICONTROL 提升度和置信度] 计算。 为避免混淆，您可以从默认面板中删除这些量度，并保留以下报表：

![[!UICONTROL 按活动转化划分的体验] 面板 [!DNL Analysis Workspace]](assets/Figure2.png)

*图2:建议的基线报告 [!DNL Auto-Target] 活动。 此报表已配置为将目标流量（由组合ML模型提供）与您的控制流量进行比较。*

>[!NOTE]
>
>目前， [!UICONTROL 提升度和置信度] 数字不可用于 [!UICONTROL 控制与目标] 用于A4T报表的维度 [!UICONTROL 自动定位]. 在添加支持之前， [!UICONTROL 提升度和置信度] 可通过下载手动计算 [置信度计算器](https://experienceleague.adobe.com/docs/target/assets/complete_confidence_calculator.xlsx).

## 添加体验级别的量度划分

要进一步了解组合ML模型的执行情况，您可以检查 **[!UICONTROL 控制与目标]** 维度。 在 [!DNL Analysis Workspace]，拖动 **[!UICONTROL 定位体验]** 维度添加到您的报表中，然后分别对每个控制维度和目标维度进行划分。

![[!UICONTROL 按活动转化划分的体验] 面板 [!DNL Analysis Workspace]](assets/Figure3.png)

*图3:按Target体验划分目标维度*

此处显示了结果报表的示例。

![[!UICONTROL 按活动转化划分的体验] 面板 [!DNL Analysis Workspace]](assets/Figure4.png)

*图4:标准 [!UICONTROL 自动定位] 报表。 请注意，您的目标量度可能不同，并且您的控制策略可能只有一个体验。*

>[!TIP]
>
>在 [!DNL Analysis Workspace]，请单击齿轮图标以隐藏 [!UICONTROL 转化率] 列来帮助保持对体验转化率的关注。 然后，转换率将格式化为小数，但会相应地将其解释为百分比。

## 为什么选择“[!UICONTROL 访问次数]“”是 [!UICONTROL 自动定位] 活动

分析 [!UICONTROL 自动定位] 活动，始终选择 [!UICONTROL 访问次数] 作为默认标准化量度。 [!UICONTROL 自动定位] 个性化会为访客在每次访问时选择一次体验(正式为，每次 [!DNL Target] 会话)，这意味着向访客显示的体验在每次访问时都可能会发生更改。 因此，如果您使用 [!UICONTROL 独特访客] 作为标准化量度，单个用户最终可能会看到多个体验（跨不同访问），这将导致转化率混乱。

一个简单的示例说明了这一点：假设有两位访客进入一个只有两个体验的营销活动。 第一个访客两次访问。 在首次访问时，会为体验A分配配置文件，而在第二次访问时，则会为体验B分配配置文件状态（由于第二次访问时，其配置文件状态发生了更改）。 第二次访问后，访客通过下订单进行转化。 转化归因于最近显示的体验（体验B）。 第二位访客也访问了两次，并且两次都显示了体验B，但从不进行转化。

让我们比较访客级别和访问级别的报表：

| 体验 | 独特访客 | 访问次数 | 转化 | 访客标准化转化率 | 访问标准化转化率 |
| --- | --- | --- | --- | --- | --- |
| 同类群组 | 1 | 1 | - | 0% | 0% |
| B | 2 | 3 | 1 | 50% | 33.3% |
| 总计 | 2 | 4 | 1 | 50% | 25% |

*表1:对于决策对访问具有粘滞性（与常规A/B测试一样，对于不是访客）的情况，比较访客标准化报表和访问标准化报表的示例。 在这种情况下，访客标准化量度会造成混淆。*

如表中所示，访客级别的数字存在明显的不协调性。 尽管存在两个独特访客总数，但这并不是每个体验的各个独特访客总数。 虽然访客级别的转化率不一定是错误的，但在比较各个体验时，访问级别的转化率可以说更有意义。 从形式上讲，分析单位（“访问次数”）与决策吸引力单位相同，这意味着可以添加和比较量度的体验级别划分。

## 过滤活动的实际访问量

的 [!DNL Adobe Analytics] 访问的默认计数方法 [!DNL Target] 活动可能包括用户未与交互的访问 [!DNL Target] 活动。 这是因为 [!DNL Target] 活动分配会保留在 [!DNL Analytics] 访客上下文。 因此， [!DNL Target] 活动有时可能会被夸大，从而导致转化率下降。

如果您希望报告用户实际与 [!UICONTROL 自动定位] 活动（通过进入活动、显示或访问事件或转化），您可以：

1. 创建包含来自 [!DNL Target] 活动，然后
1. 筛选 [!UICONTROL 访问次数] 量度。

**要创建区段，请执行以下操作：**

1. 选择 **[!UICONTROL “组件”>“创建区段”]** 选项 [!DNL Analysis Workspace] 工具栏。
2. 指定 **[!UICONTROL 标题]** 的URL。 在以下示例中，该区段名为 [!DNL "Hit with specific Auto-Target activity"].
3. 拖动 **[!UICONTROL Target活动]** 区段维度 **[!UICONTROL 定义]** 中。
4. 使用 **[!UICONTROL 等于]** 运算符。
5. 搜索您的特定 [!DNL Target] 活动。
6. 单击齿轮图标，然后选择 **[!UICONTROL 归因模型>实例]** 如下图所示。
7. 单击&#x200B;**[!UICONTROL 保存]**。

![区段 [!DNL Analysis Workspace]](assets/Figure5.png)

*图5:使用区段（如此处显示的区段）过滤 [!UICONTROL 访问次数] 量度 [!UICONTROL 自动定位] 报告*

创建区段后，使用它过滤 [!UICONTROL 访问次数] 量度，因此 [!UICONTROL 访问次数] 量度仅包括用户与其进行交互的访问 [!DNL Target] 活动。

**过滤 [!UICONTROL 访问次数] 使用此区段：**

1. 将新创建的区段从组件工具栏中拖动，并将鼠标悬停在 **[!UICONTROL 访问次数]** 量度标签，直到蓝色 **[!UICONTROL 过滤依据]** 出现提示。
2. 释放区段。 过滤器将应用于该量度。

最终面板如下所示：

![[!UICONTROL 按活动转化划分的体验] 面板 [!DNL Analysis Workspace]](assets/Figure6.png)

*图6:报表面板，其中“通过特定自动定位活动进行点击”区段应用于 [!UICONTROL 访问次数] 量度。 此区段可确保仅当用户实际与 [!DNL Target] 相关活动包含在报表中。*

## 确保目标量度和归因与您的优化标准保持一致

A4T集成允许 [!UICONTROL 自动定位] ML模型为 *训练有素* 使用与 [!DNL Adobe Analytics] 使用 *生成性能报告*. 然而，于培训ML模型时，在解释此数据时必须采用若干假设，该等假设与 [!DNL Adobe Analytics].

具体而言， [!DNL Adobe Target] ML模型使用访问范围的归因模型。 也就是说，ML模型假定必须在同一访问中发生转化，以显示活动的内容，以便将转化“归因”到ML模型所做的决策。 这是 [!DNL Target] 确保及时培训模式； [!DNL Target] 最长等待30天的转化( [!DNL Adobe Analytics])，然后将其包含在其模型的培训数据中。

因此， [!DNL Target] 模型（在培训期间）与查询数据时使用的默认归因（在报表生成期间）可能会导致差异。 ML模型的性能甚至似乎很差，但实际上问题与归因有关。

>[!TIP]
>
>如果ML模型针对与您在报表中查看的量度不同的量度进行了优化，则这些模型可能不会按预期执行。 要避免这种情况，请确保报表中的目标量度使用与 [!DNL Target] ML型号。

确切的量度定义和归因设置取决于 [优化准则](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank} 您在活动创建期间指定。

### 定位定义的转化，或 [!DNL Analytics] 量度 *最大化每次访问量度值*

当量度为 [!DNL Target] 转化，或 [!DNL Analytics] 量度 **最大化每次访问量度值**，则目标量度定义允许在同一访问中发生多个转化事件。

查看具有与 [!DNL Target] ML模型，请按照以下步骤操作：

1. 将鼠标悬停在目标量度的齿轮图标上：

   ![gearicon.png](assets/gearicon.png)

1. 在生成的菜单中，滚动到 **[!UICONTROL 数据设置]**.
1. 选择 **[!UICONTROL 使用非默认的归因模型]** （如果尚未选择）。

   ![nondefaultattributionmodel.png](assets/non-defaultattributionmodel.png)

1.  点击&#x200B;**[!UICONTROL 编辑]**。
1. 选择 **[!UICONTROL 模型]**: **[!UICONTROL 参与率]**&#x200B;和 **[!UICONTROL 回顾窗口]**: **[!UICONTROL 访问]**.

   ![ParticitionbyVisit.png](assets/ParticipationbyVisit.png)

1. 单击&#x200B;**[!UICONTROL 应用]**。

这些步骤可确保在发生目标量度事件时，您的报表将目标量度归因于体验的显示 *任何时间* （“参与率”）。

### [!DNL Analytics] 量度 *独特访问转化率*

**使用正量度区段定义访问**

在您选择的方案中 *最大化独特访问转化率* 作为优化标准，转化率的正确定义是量度值为正值的访问次数的百分比。 可以通过创建一个客户群细分，以过滤到具有量度正值的访问，然后过滤访问量度来实现此目的。

1. 与之前一样，选择 **[!UICONTROL “组件”>“创建区段”]** 选项 [!DNL Analysis Workspace] 工具栏。
2. 指定 **[!UICONTROL 标题]** 的URL。

   在以下示例中，该区段名为 [!DNL "Visits with an order"].

3. 将您在优化目标中使用的基本量度拖动到区段中。

   在以下示例中，我们使用 **订购** 量度，以便转化率可测量记录订单的访问次数百分比。

4. 在区段定义容器的左上角，选择 **[!UICONTROL 包括]** **访问**.
5. 使用 **[!UICONTROL 大于]** 运算符，并将值设置为0。

   将值设置为0表示此区段包括订单量度为正的访问。

6. 单击&#x200B;**[!UICONTROL 保存]**。

![图7.png](assets/Figure7.png)

*图7:区段定义过滤为按正顺序访问。 根据活动的优化量度，您必须使用相应的量度替换订单*

**将此量度应用于活动过滤量度中的访问次数**

此区段现在可用于筛选订单数为正数且具有 [!DNL Auto-Target] 活动。 过滤量度的过程与之前类似，在将新区段应用到已过滤的访问量度后，报表面板应类似于图8

![图8.png](assets/Figure8.png)

*图8:具有正确独特访问转化量度的报表面板：记录来自活动的点击的访问次数，以及转化量度（本示例中的订购次数）为非零的访问次数。*

## 最后一步：创建可捕获上述神奇功能的转化率

对 [!UICONTROL 访问] 和目标量度，您应该对 [!DNL Auto-Target] 报表面板可创建正确的转化率 — 更正后的目标量度与适当过滤的“访问量”量度的转化率。

通过创建 [!UICONTROL 计算量度] 执行以下步骤：

1. 选择 **[!UICONTROL 组件>创建量度]** 选项 [!DNL Analysis Workspace] 工具栏。
1. 指定 **[!UICONTROL 标题]** 的值。 例如，“活动XXX的访问更正转化率”。
1. 选择 **[!UICONTROL 格式]** =百分比和 **[!UICONTROL 小数位]** = 2。
1. 拖动活动的相关目标量度(例如， [!UICONTROL 活动转化])，并使用此目标量度上的齿轮图标将归因模型调整为（参与率|访问），如前面所述。
1. 选择 **[!UICONTROL 添加>容器]** 从 **[!UICONTROL 定义]** 中。
1. 选择两个容器之间的除法(÷)运算符。
1. 拖动您之前创建的名为“点击特定 [!UICONTROL 自动定位] activity（活动） [!DNL Auto-Target] 活动。
1. 拖动 **[!UICONTROL 访问次数]** 量度。
1. 单击&#x200B;**[!UICONTROL 保存]**。

>[!TIP]
>
> 您还可以使用 [快速计算量度功能](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html).

此处显示了完整的计算量度定义。

![图9.png](assets/Figure9.png)

*图7:已更正访问和已更正归因的模型转化率量度定义。 (请注意，此量度取决于您的目标量度和活动。 换言之，此量度定义在活动中不可重复使用。)*

>[!IMPORTANT]
>
>的 [!UICONTROL 转化] A4T面板中的比率量度未链接到表格中的转化事件或标准化量度。 当您在本教程中建议进行修改时， [!UICONTROL 转化] 比率不会自动适应更改。 因此，如果您对转化事件归因或标准化量度（或同时对这两者进行修改）进行了修改，则您必须记住最后一步来修改 [!UICONTROL 转化] 比率，如上所示。

## 摘要：最终示例 [!DNL Analysis Workspace] 面板 [!UICONTROL 自动定位] 报告

将上述所有步骤组合到一个面板中，下图显示了 [!UICONTROL 自动定位] A4T活动。 此报表与 [!DNL Target] ML模型以优化您的目标量度。 该报表纳入了本教程中讨论的所有细微差别和建议。 此报表还最接近传统方法中使用的计数方法 [!DNL Target]报告驱动 [!UICONTROL 自动定位] 活动。

单击可展开图像。

![中的最终A4T报表 [!DNL Analysis Workspace]](assets/Figure10.png "Analysis Workspace中的A4T报表"){width="600" zoomable="yes"}

*图10:最终的A4T [!UICONTROL 自动定位] 报告 [!DNL Adobe Analytics] [!DNL Workspace]，它将对本教程前几节中所述的量度定义所做的所有调整整合在一起。*
