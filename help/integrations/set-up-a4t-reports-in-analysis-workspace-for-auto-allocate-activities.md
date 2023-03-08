---
title: 如何在中设置A4T报表 [!DNL Analysis Workspace] 对象 [!UICONTROL 自动分配] 活动
description: 如何在中配置A4T报表 [!DNL Analysis Workspace] 以获取运行时的预期结果 [!UICONTROL 自动分配] 活动。
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: 14a362214dce9d698c78438c3a47424b59aa4632
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 0%

---

# 在中设置A4T报表 [!DNL Analysis Workspace] 对象 [!DNL Auto-Allocate] 活动

An [!DNL Auto-Allocate] 活动可在两个或更多体验中标识一个入选者，并在测试继续运行和学习期间，自动为入选者重新分配更多流量。 此 [!UICONTROL 目标分析] (A4T)集成 [!UICONTROL 自动分配] 允许您在中查看报表数据 [!DNL Adobe Analytics]，您甚至还可以优化中定义的自定义事件或量度 [!DNL Analytics].

尽管中提供了丰富的分析功能， [!DNL Adobe Analytics] [!DNL Analysis Workspace]，对默认进行了一些修改 **[!UICONTROL 目标分析]** 需要面板才能正确解释 [!DNL Auto-Allocate] 活动，由于以下各项的细微差别： [优化标准](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#supported).

本教程介绍了用于分析的建议修改 [!DNL Auto-Allocate] 中的活动 [!DNL Analysis Workspace]. 主要概念包括：

* [!UICONTROL 访客] 应始终用作中的标准化量度 [!DNL Auto-Allocate] 活动。
* 当指标为 [!DNL Adobe Analytics] 量度时，转化率的相应分子取决于在活动设置期间选择的优化标准类型。
   * “最大化独特访客转化率”优化标准的转化率分子是独特访客的计数，且具有量度的正值。
   * “每位访客的最大量度值”的转化率分子是中的常规量度值 [!DNL Adobe Analytics]. 默认情况下，此函数在 **[!UICONTROL 目标分析]** 面板位于 [!DNL Analysis Workspace].
* 当优化指标为 [!DNL Target] 定义的转化量度，默认 **[!UICONTROL 目标分析]** 面板位于 [!DNL Analysis Workspace] 处理面板配置。
* 此 [!UICONTROL 置信度] 中显示的数字 [!DNL Analysis Workspace] 不反映 [更保守的统计数据 [!UICONTROL 自动分配]](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html?lang=en#section_98388996F0584E15BF3A99C57EEB7629)，因此应该删除。

## 为以下对象创建A4T [!DNL Auto-Allocate] 面板位于 [!DNL Analysis Workspace]

为创建A4T [!DNL Auto-Allocate] 报告开始于 **[!UICONTROL 目标分析]** 面板位于 [!DNL Analysis Workspace]，如下所示。 然后，进行以下选择：

1. **[!UICONTROL 控制体验]**：您可以选择任意体验。
2. **[!UICONTROL 标准化量度]**：选择访客。 [!DNL Auto-Allocate] 始终按独特访客将转化率标准化。
3. **[!UICONTROL 成功量度]**：选择您在活动创建期间使用的相同量度。 如果这是 [!DNL Target] 定义的转化量度，选择 **活动转换**. 否则，请选择 [!DNL Adobe Analytics] 您使用的量度。

![[!UICONTROL 目标分析] 面板设置 [!DNL Auto-Allocate] 活动。](assets/AAFigure1.png)

*图1： [!UICONTROL 目标分析] 面板设置 [!DNL Auto-Allocate] 活动。*

>[!NOTE]
>
> 您还可以获得预建的 **[!UICONTROL 目标分析]** 面板中单击报表屏幕上的链接 [!DNL Adobe Target].

## [!DNL Target] [!UICONTROL 转化] 量度或 [!DNL Analytics] 具有“每位访客的量度值最大化”优化标准的量度

默认A4T面板句柄 [!DNL Auto-Allocate] 目标量度为的活动 [!DNL Target] 转化或 [!DNL Analytics] 优化标准为“每位访客的量度值最大化”的量度。

以下示例显示了此面板的 [!UICONTROL 收入] 量度，其中，“每位访客的量度值最大化”被选为活动创建时的优化标准。 如前所述， [!DNL Auto-Allocate] 使用的置信度计算比中使用的更保守 **[!UICONTROL 目标分析]** 面板。 Adobe建议您删除置信度量度，以及相关的下提升度量度和上提升度量度。

![[!UICONTROL Analytics for Target — 自动分配报表] 面板](assets/AAFigure2.png)

*图2：建议的报表 [!DNL Auto-Allocate] 具有的活动 [!DNL Analytics] 量度“每个访客的量度值最大化优化”标准。 对于这些类型的量度，以及 [!DNL Target] 定义的转化量度，默认&#x200B;**[!UICONTROL 目标分析]**面板位于 [!DNL Analysis Workspace] 可以使用。*

## [!DNL Analytics] 具有“最大独特访客转化率”优化标准的量度

当 [!DNL Adobe Analytics] 量度与优化标准一起使用 *最大程度提高独特访客转化率*，默认 **[!UICONTROL 目标分析]** 面板位于 [!DNL Analysis Workspace] 必须修改。

成功量度现在是转化量度为正数的独特访客计数。 这可以通过创建一个区段来实现，该区段会过滤到具有正量度值的点击。 创建此区段如下：

1. 选择 **[!UICONTROL 组件]** > **[!UICONTROL 创建区段]** 中的选项 [!DNL Analysis Workspace] 工具栏。
1. 将活动创建时使用的量度从左侧面板拖动到 **[!UICONTROL 定义]** 框中。
1. 选择以下量度的值 **大于** 数值0。
1. 从 **[!UICONTROL 包括]** 下拉列表，选择 **[!UICONTROL 访客]**.
1. 为区段指定适当的名称。

下图显示了创建区段的示例，您在该图中选择 [!UICONTROL 收入为正的访客].

![[!UICONTROL 收入为正的访客] 中的区段 [!DNL Analysis Workspace]](assets/AAFigure3.png)

*图3：创建区段 [!DNL Adobe Analytics] 优化标准等于&quot;的指标[!UICONTROL 最大程度提高独特访客转化率].” 在此示例中，指标为 [!UICONTROL 收入]，并且优化目标是以正收入最大化访客数量。*

创建相应的区段后，默认  **[!UICONTROL 目标分析]** 面板位于 [!DNL Analysis Workspace] 可以修改。

1. 添加第二个 **独特访客** 量度与现有 [!UICONTROL 访客] 量度列。
2. 将新创建的区段拖到第一列下以生成类似于图4的面板。 请注意差异：具有正收入的独特访客数量是分配给每个体验的独特访客总数的一小部分。

   ![图4.png](assets/AAFigure4.png)

   *图4：筛选 [!UICONTROL 独特访客] 按新创建的区段*

3. 转化率可以是 [快速计算](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html?lang=en) 通过突出显示第一列和第二列，单击右键，选择 **[!UICONTROL 从所选内容创建量度]** > **[!UICONTROL 除]**.

   应删除默认转化率，并将其替换为此新的计算量度，如下图所示。 您可能需要编辑新创建的计算量度以显示为 **[!UICONTROL 格式]** > **[!UICONTROL 百分比]** 最多两位小数，如下所示。

   ![图5.png](assets/AAFigure5.png)

   *图5：决赛 [!UICONTROL 自动分配] 显示二进制收入转化量度的转化率的面板*

## 概要

本教程中的步骤演示了如何正确配置 [!DNL Analysis Workspace] 显示 [!UICONTROL 自动分配] 报表数据。

总结如下：

* 当指标为 [!DNL Target] 定义的转化量度或 [!DNL Adobe Analytics] 应使用优化标准“每位访客的量度值最大化”的量度，该量度配置为将访客作为标准化量度的默认工作区面板。
* 当指标为 [!DNL Adobe Analytics] 优化标准为“最大化独特访客转化率”的量度，您必须使用转化率，该转化率被定义为量度为正的访客比例。 这是通过创建相应的区段来筛选的 [!UICONTROL 独特访客] 量度。
