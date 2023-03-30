---
title: 如何在 [!DNL Analysis Workspace] 表示 [!UICONTROL 自动分配] 活动
description: 如何在 [!DNL Analysis Workspace] 以在运行时获得预期结果 [!UICONTROL 自动分配] 活动。
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: bd8283d3c0e5fa9e690e377bc4dfbf6a147dd577
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 0%

---

# 在中设置A4T报表 [!DNL Analysis Workspace] 表示 [!DNL Auto-Allocate] 活动

安 [!DNL Auto-Allocate] 活动可在两个或更多体验中标识一个入选者，并在测试继续运行和学习期间自动为入选者重新分配更多流量。 的 [!UICONTROL Analytics for Target] (A4T)集成 [!UICONTROL 自动分配] 允许您在 [!DNL Adobe Analytics]，您甚至可以在 [!DNL Analytics].

尽管在 [!DNL Adobe Analytics] [!DNL Analysis Workspace]，对默认值进行一些修改 **[!UICONTROL Analytics for Target]** 面板需要正确解释 [!DNL Auto-Allocate] 活动，由于 [优化标准](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank}.

本教程将演示为分析而推荐的修改 [!DNL Auto-Allocate] 活动 [!DNL Analysis Workspace]. 主要概念包括：

* [!UICONTROL 访客] 应始终用作 [!DNL Auto-Allocate] 活动。
* 当量度为 [!DNL Adobe Analytics] 量度中，转化率的相应分子取决于在活动设置期间选择的优化标准类型。
   * “最大化独特访客转化率”优化标准的转化率为以量度正值表示的独特访客计数的转化率。
   * “每个访客最大量度值”的转化率为 [!DNL Adobe Analytics]. 默认情况下，会在 **[!UICONTROL Analytics for Target]** 面板 [!DNL Analysis Workspace].
* 当优化量度为 [!DNL Target] 定义的转化量度，默认 **[!UICONTROL Analytics for Target]** 面板 [!DNL Analysis Workspace] 用于配置面板。
* 适用于所有 [!UICONTROL 自动分配] 活动之前创建 [!DNL Target Standard/Premium] 23.3.1版本（2023年3月30日） [!DNL Analytics Workspace] 和 [!DNL Target] 显示的值与 [!UICONTROL 置信度].

   适用于所有 [!UICONTROL 自动分配] 2023年3月30日之后创建的活动， [!DNL Analysis Workspace] 不反映 [更为保守的统计 [!UICONTROL 自动分配]](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html#section_98388996F0584E15BF3A99C57EEB7629){target=_blank} 如果这些活动 *both* （二）下列条件之一：

   * [!DNL Analytics] 作为报表源(A4T)
   * [!DNL Analytics] 优化量度

   如果 *both* 其中，应从A4T面板中删除置信度量度。 请改为在 [!DNL Target] 报表。

## 为创建A4T [!DNL Auto-Allocate] 面板 [!DNL Analysis Workspace]

为 [!DNL Auto-Allocate] 报表以 **[!UICONTROL Analytics for Target]** 面板 [!DNL Analysis Workspace]，如下所示。 然后，进行以下选择：

1. **[!UICONTROL 控制体验]**:您可以选择任何体验。
2. **[!UICONTROL 标准化量度]**:选择访客。 [!DNL Auto-Allocate] 始终按独特访客将转化率标准化。
3. **[!UICONTROL 成功量度]**:选择在活动创建期间使用的相同量度。 如果这是 [!DNL Target] 定义的转化量度，选择 **活动转化**. 否则，请选择 [!DNL Adobe Analytics] 量度。

![[!UICONTROL Analytics for Target] 面板设置 [!DNL Auto-Allocate] 活动。](assets/AAFigure1.png)

*图1: [!UICONTROL Analytics for Target] 面板设置 [!DNL Auto-Allocate] 活动。*

>[!NOTE]
>
> 您还可以获得预建的 **[!UICONTROL Analytics for Target]** 面板(在 [!DNL Adobe Target].

## [!DNL Target] [!UICONTROL 转化] 量度或 [!DNL Analytics] 具有“最大化每位访客的量度值”优化标准的量度

默认的A4T面板句柄 [!DNL Auto-Allocate] 目标量度为 [!DNL Target] 转化或 [!DNL Analytics] 量度。

此面板的一个示例显示在 [!UICONTROL 收入] 量度中，其中在活动创建时选择“每个访客的最大量度值”作为优化标准。 如前所述， [!DNL Auto-Allocate] 与中使用的置信度计算相比，使用更保守的置信度计算 **[!UICONTROL Analytics for Target]** 的上界。 Adobe建议您从A4T面板中删除置信度量度，以及相关的提升度下限和上限量度。 请在 [!DNL Target] 报表。

![[!UICONTROL Analytics for Target — 自动分配报表] 面板](assets/AAFigure2.png)

*图2:推荐的 [!DNL Auto-Allocate] 活动 [!DNL Analytics] 量度“最大化每个访客优化的量度值”标准。 对于这些类型的量度，以及 [!DNL Target] 定义的转化量度，默认&#x200B;**[!UICONTROL Analytics for Target]**面板 [!DNL Analysis Workspace] 中。*

## [!DNL Analytics] 量度，其中包含“最大化独特访客转化率”优化标准

当 [!DNL Adobe Analytics] 量度与 *最大化独特访客转化率*，默认 **[!UICONTROL Analytics for Target]** 面板 [!DNL Analysis Workspace] 必须修改。

成功量度现在是转化量度为正值的独特访客计数。 可以通过创建一个区段来筛选具有量度正值的点击量，来实现此目的。 按如下方式创建此区段：

1. 选择 **[!UICONTROL 组件]** > **[!UICONTROL 创建区段]** 选项 [!DNL Analysis Workspace] 工具栏。
1. 将活动创建时使用的量度从左侧面板拖到 **[!UICONTROL 定义]** 框。
1. 选择以下量度的值 **大于** 0的数值。
1. 从 **[!UICONTROL 包括]** 下拉列表，选择 **[!UICONTROL 访客]**.
1. 为您的区段提供适当的名称。

下图显示了创建区段的示例，您可在此处选择 [!UICONTROL 收入为正的访客].

![[!UICONTROL 收入为正的访客] 区段 [!DNL Analysis Workspace]](assets/AAFigure3.png)

*图3:创建区段 [!DNL Adobe Analytics] 具有优化条件的量度等于“[!UICONTROL 最大化独特访客转化率].&quot; 在此示例中，量度为 [!UICONTROL 收入]，并且优化目标是最大化具有正收入的访客数量。*

创建相应的区段后，默认  **[!UICONTROL Analytics for Target]** 面板 [!DNL Analysis Workspace] 可修改。

1. 添加秒 **独特访客** 量度旁边 [!UICONTROL 访客] 量度列。
2. 将新创建的区段拖到第一列下，以生成类似于图4的面板。 请注意区别：收入为正的独特访客数是分配给每个体验的独特访客总数的一小部分。

   ![图4.png](assets/AAFigure4.png)

   *图4:筛选 [!UICONTROL 独特访客] 按新创建的区段*

3. 转化率可以为 [快速计算](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html) 加亮第一列和第二列，右键单击，选择 **[!UICONTROL 从选定范围中创建量度]** > **[!UICONTROL 除数]**.

   应删除默认转化率，并将其替换为此新计算量度，如下图所示。 您可能需要编辑新创建的计算量度才能显示为 **[!UICONTROL 格式]** > **[!UICONTROL 百分比]** 最多保留两位小数，如所示。

   ![图5.png](assets/AAFigure5.png)

   *图5:最后 [!UICONTROL 自动分配] 显示二值化收入转化量度的转化率的面板*

## 概要

本教程中的步骤演示了如何正确配置 [!DNL Analysis Workspace] 显示 [!UICONTROL 自动分配] 报表数据。

总结如下：

* 当量度为 [!DNL Target] 定义的转化量度或 [!DNL Adobe Analytics] 具有优化标准“最大化每位访客的量度值”的量度，应使用以访客配置为标准化量度的默认工作区面板。
* 当量度为 [!DNL Adobe Analytics] 量度具有优化标准“最大化独特访客转化率”，则您必须使用一个转化率，该转化率定义为该量度为正数的访客百分比。 这是通过创建一个用于筛选 [!UICONTROL 独特访客] 量度。
