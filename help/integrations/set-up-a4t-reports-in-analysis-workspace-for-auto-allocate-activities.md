---
title: 如何在中设置A4T报表 [!DNL Analysis Workspace] 对象 [!UICONTROL 自动分配] 活动
description: 如何在中配置A4T报表 [!DNL Analysis Workspace] 获得运行时的预期结果 [!UICONTROL 自动分配] 活动。
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: dddb90e66d127782d4fe1347bd43553cd8c04d58
workflow-type: tm+mt
source-wordcount: '1303'
ht-degree: 0%

---

# 在中设置A4T报表 [!DNL Analysis Workspace] 对象 [!DNL Auto-Allocate] 活动

An [!DNL Auto-Allocate] 活动可识别两个或更多体验中的入选者，并在测试继续运行和学习期间，自动为入选者重新分配流量。 此 [!UICONTROL 目标分析] (A4T)集成 [!UICONTROL 自动分配] 允许您在中查看报表数据 [!DNL Adobe Analytics]，您甚至还可以优化中定义的自定义事件或量度 [!DNL Analytics].

尽管中提供了丰富的分析功能， [!DNL Adobe Analytics] [!DNL Analysis Workspace]，对默认进行了一些修改 **[!UICONTROL 目标分析]** 可能需要面板才能正确解释 [!DNL Auto-Allocate] 活动，由于以下各项的细微差别 [优化量度标准](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank}.

本教程将介绍为分析而推荐的修改 [!DNL Auto-Allocate] 中的活动 [!DNL Analysis Workspace]. 关键概念包括：

* [!UICONTROL 访客] 应始终用作中的标准化指标 [!DNL Auto-Allocate] 活动。
* 当指标为 [!DNL Adobe Analytics] 量度，转化率的计算会有所不同，具体取决于活动设置期间定义的优化标准的类型。
   * “每位访客的量度值最大化”：转化率分子是中的常规量度值 [!DNL Adobe Analytics] (默认情况下，这在 [!UICONTROL 目标分析] A中的面板[!DNL nalysis Workspace])。
      * 这意味着：最大化每个访客的转化次数（“为每个访客统计每个转化次数”）。
      * 此方法不需要额外的区段来匹配中显示的转化率。 [!DNL Target] UI。
   * “最大化独特访客转化率”：转化率分子是指具有正量度值的独特访客的计数。
      * 这意味着：转化访客的数量达到最大值（“每位访客计数一次）。
      * 此方法 *DOES* 需要在报表中创建额外的区段，以匹配中显示的转化率。 [!DNL Target] UI。

* 当您的优化指标为 [!DNL Target] 定义的转化量度，默认 **[!UICONTROL 目标分析]** 面板位于 [!DNL Analysis Workspace] 处理配置面板。
* 全部 [!UICONTROL 自动分配] 之前创建的活动 [!DNL Target Standard/Premium] 23.3.1版本（2023年3月30日） [!DNL Analytics Workspace] 和 [!DNL Target] 显示相同的值 [!UICONTROL 置信度].

  全部 [!UICONTROL 自动分配] 在2023年3月30日之后创建的活动，在中看到的置信区间值 [!DNL Analysis Workspace] 不反映 [更保守的统计数据 [!UICONTROL 自动分配]](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html#section_98388996F0584E15BF3A99C57EEB7629){target=_blank} 如果这些活动具有 *两者* 条件：

   * [!DNL Analytics] 作为报表源(A4T)
   * [!DNL Analytics] 优化量度

  应从A4T面板中删除置信度量度。 请改为引用这些值 [!DNL Target] 报表。

## 为创建A4T [!DNL Auto-Allocate] 面板位于 [!DNL Analysis Workspace]

为创建A4T面板 [!DNL Auto-Allocate] 报告开始于 **[!UICONTROL 目标分析]** 面板位于 [!DNL Analysis Workspace]，如下所示。 然后，进行以下选择：

1. **[!UICONTROL 控制体验]**：您可以选择任意体验。
1. **[!UICONTROL 标准化量度]**：选择访客（默认情况下，访客包含在A4T面板中）。 [!DNL Auto-Allocate] 始终按独特访客标准化转化率。
1. **[!UICONTROL 成功量度]**：选择您在活动创建期间使用的相同量度。 如果这是 [!DNL Target] 定义的转化量度，选择 **活动转换**. 否则，选择 [!DNL Adobe Analytics] 您使用的量度。

![[!UICONTROL 目标分析] 面板设置 [!DNL Auto-Allocate] 活动。](assets/AAFigure1.png)

*图1 ： [!UICONTROL 目标分析] 面板设置 [!DNL Auto-Allocate] 活动。*

您还可以到达一个预建的 **[!UICONTROL 目标分析]** 面板（如果您在中单击报表屏幕中的链接） [!DNL Adobe Target].

## [!DNL Target] [!UICONTROL 转化] 量度或 [!DNL Analytics] 具有“每位访客的量度值最大化”优化标准的量度

当目标指标为：

* 目标转化量度
* 优化标准为“每位访客的量度值最大化”的Analytics量度

默认的A4T面板会自动配置报告。

此面板的一个示例显示于 [!UICONTROL 收入] 量度，其中在活动创建时选择了“每位访客的量度值最大化”作为优化标准。 如前所述， [!DNL Auto-Allocate] 使用的置信度计算比中使用的更保守 **[!UICONTROL 目标分析]** 面板。 Adobe建议您从A4T面板中删除置信度量度，以及相关的下提升度和上提升度指标。 相反，请引用中的置信度值 [!DNL Target] 报表。

>[!NOTE]
>
>A4T报表中的置信度值没有下面那么保守 [!DNL Target] 报表，可能会提前指示入选者 [!UICONTROL 自动分配] 活动。


![[!UICONTROL Analytics for Target — 自动分配报表] 面板](assets/AAFigure2.png)

*图2：建议的报表 [!DNL Auto-Allocate] 具有的活动 [!DNL Analytics] 量度“每位访客的量度值最大化”优化标准。 对于这些类型的量度，以及 [!DNL Target] 定义的转化量度，默认&#x200B;**[!UICONTROL 目标分析]**面板位于 [!DNL Analysis Workspace] 可以使用。*

## [!DNL Analytics] 具有“最大独特访客转化率”优化标准的量度

优化标准“最大独特访客转化率”是指指标值为正的访客计数。 例如，如果将转化率定义为收入，则“最大独特访客转化率”标准将优化收入大于0的独特访客计数。 换句话说，这一标准将最大化产生收入的访客数量，而不是收入本身的价值。

>[!NOTE]
>
>此处引用的转化率可以指订单外的操作，如点击次数、展示次数等。 在这些情况下，标准仍将是分别最大化点击或查看页面的访客计数。

此 [!DNL Analytics for Target] 面板位于 [!DNL Analysis Workspace] 如果将此优化标准与 [!DNL Adobe Analytics] 量度。

使用此优化标准时，成功量度是转化量度为正的独特访客计数。 因此，要查看此值，必须创建一个新区段，以过滤该量度具有正值的点击。

按如下方式创建此区段：

1. 选择 **[!UICONTROL 组件]** > **[!UICONTROL 创建区段]** 中的选项 [!DNL Analysis Workspace] 工具栏。
1. 将活动创建时所使用的量度从左侧面板拖动到 **[!UICONTROL 定义]** 框中。
1. 选择以下量度的值 **大于** 值为0的数值。
1. 从 **[!UICONTROL 包括]** 下拉列表，选择 **[!UICONTROL 访客]**.
1. 为区段指定适当的名称。

下图显示了区段创建的示例，其中成功量度为 [!UICONTROL 收入为正的访客].

![[!UICONTROL 收入为正的访客] 中的区段 [!DNL Analysis Workspace]](assets/AAFigure3.png)

*图3：为创建区段 [!DNL Adobe Analytics] 其优化标准等于&quot;[!UICONTROL 最大程度提高独特访客转化率]“ 在此示例中，量度为 [!UICONTROL 收入]，并且优化目标是以正收入最大化访客数。*

创建相应的区段后，可以修改缺省值  **[!UICONTROL 目标分析]** 面板位于 [!DNL Analysis Workspace] 查看优化标准值。 可通过执行以下操作，实现此目标：

1. 添加秒数 **独特访客** 量度以及现有 [!UICONTROL 访客] 量度列。
2. 将新创建的区段拖动到第一列下以生成类似于图4的面板。 请注意各列值的差异：收入为正的独特访客数应当是分配给每个体验的独特访客总数的一小部分（如下所示）。

   ![图4.png](assets/AAFigure4.png)

   *图4：筛选 [!UICONTROL 独特访客] 按新创建的区段*

3. 转化率可以是 [快速计算](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html) 通过突出显示第一列和第二列，右键单击，选择 **[!UICONTROL 从所选内容创建量度]** > **[!UICONTROL 除]**.

   应该删除默认转化率，并将其替换为此新的计算量度，如下图所示。 您可能需要编辑新创建的计算量度以显示为字段 **[!UICONTROL 格式]** > **[!UICONTROL 百分比]** 最多两位小数，如图所示。

   ![图5.png](assets/AAFigure5.png)

   *图5：决赛 [!UICONTROL 自动分配] 显示二进制收入转化量度的转化率的面板*

## 概要

本教程中的步骤演示了如何正确配置 [!DNL Analysis Workspace] 显示 [!UICONTROL 自动分配] 报表数据。

总结如下：

* 当指标为 [!DNL Target] 定义的转化量度或 [!DNL Adobe Analytics] 应使用优化标准“每位访客的量度值最大化”的量度，该量度是使用将访客配置为标准化量度的默认工作区面板。
* 当指标为 [!DNL Adobe Analytics] 使用优化标准“最大化独特访客转化率”的量度，您必须确定具有正量度值的访客占总访客的比例。 这可以通过创建相应的区段来筛选 [!UICONTROL 独特访客] 在该指标上。
