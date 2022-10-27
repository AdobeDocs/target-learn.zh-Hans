---
title: 如何在Analysis Workspace中设置A4T报表以自动分配活动
description: 在您部署了Analytics for Target(A4T)集成并运行自动分配活动后，如何确保正确解释结果？ 请按照以下步骤在Analysis Workspace中配置A4T报表，以在运行自动分配活动时获得预期结果。
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: null
source-git-commit: eb7232f1c6ed52860aa5ef86b50427fb96ab7894
workflow-type: tm+mt
source-wordcount: '1087'
ht-degree: 0%

---

# 在Analysis Workspace中为 [!DNL Auto-Allocate] 活动

安 [!DNL Auto-Allocate] 活动可在两个或更多体验中标识一个入选者，并在测试继续运行和学习期间自动为入选者重新分配更多流量。 用于的Analytics for Target(A4T)集成 [!DNL Auto-Allocate] 允许您在Adobe Analytics中查看报表数据，甚至可以优化在Adobe Analytics中定义的自定义事件或量度。

虽然Adobe Analytics Analysis Workspace中提供了丰富的分析功能，但对默认设置进行了一些修改 **[!UICONTROL Analytics for Target]** 面板需要正确解释 [!DNL Auto-Allocate] 活动，由于 [优化标准](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#supported).

本教程将演示为分析而推荐的修改 [!DNL Auto-Allocate] 活动。 主要概念包括：

* 在中，应始终将访客用作标准化量度 [!DNL Auto-Allocate] 活动。
* 当量度是Adobe Analytics量度时，转化率的相应分子取决于在活动设置期间选择的优化标准类型。
   * “最大化独特访客转化率”优化标准的转化率为以量度正值表示的独特访客计数的转化率。
   * “每访客最大量度值*”的转化率为分子是Adobe Analytics中的常规量度值。 默认情况下，会在 **[!UICONTROL Analytics for Target]** 的双曲正切值。
* 当优化量度是Target定义的转化量度时，默认 **[!UICONTROL Analytics for Target]** 面板中可处理配置面板的问题。
* 工作区中显示的置信度数字不反映 [自动分配使用的更保守的统计数据](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html?lang=en#section_98388996F0584E15BF3A99C57EEB7629)，因此应该删除。


## 为创建A4T [!DNL Auto-Allocate] 工作区中的面板

为 [!DNL Auto-Allocate] 报表以 **[!UICONTROL Analytics for Target]** 面板，如下所示。 然后，进行以下选择：

1. **[!UICONTROL 控制体验]**:您可以选择任何体验
2. **[!UICONTROL 标准化量度]**:选择访客 — 自动分配始终按独特访客标准化转化率。
3. **[!UICONTROL 成功量度]**:选择在活动创建期间使用的相同量度 — 如果这是Target定义的转化量度，请选择 **活动转化**. 否则，请选择您使用的Adobe Analytics量度。

![AAFigure1.png](assets/AAFigure1.png)
*图1:Analytics for Target面板设置 [!DNL Auto-Allocate] 活动。*

>[!NOTE]
>
> 您还可以获得预建的 **[!UICONTROL Analytics for Target]** 面板。

## 使用“最大化每位访客的量度值”优化标准定位转化量度或Analytics量度

默认的A4T面板句柄 [!DNL Auto-Allocate] 目标量度为“目标转化”或具有优化标准“最大化每位访客的量度值”的Analytics量度的活动。

此面板的一个示例显示了收入量度，其中在活动创建时选择“每位访客的最大量度值”作为优化标准。 如前所述， [!DNL Auto-Allocate] 使用比 **[!UICONTROL Analytics for Target]** 的上界。 因此，建议您删除置信度量度以及相关的提升度下限和上限量度。

![图2.png](assets/AAFigure2.png)
*图2:推荐的 [!DNL Auto-Allocate] 使用Analytics量度最大化每个访客优化标准的量度值的活动。 对于这些类型的量度以及Target定义的转化量度，默认&#x200B;**[!UICONTROL Analytics for Target]**面板。*


## 具有“最大化独特访客转化率”优化标准的Analytics量度

当将Adobe Analytics量度与 *最大化独特访客转化率*，默认 **[!UICONTROL Analytics for Target]** 必须修改工作区中的面板。

成功量度现在是转化量度为正值的独特访客计数。 可以通过创建一个区段来筛选具有量度正值的点击量，来实现此目的。 按如下方式创建此区段：

1. 选择 **组件** > **创建区段** 选项。
1. 将活动创建时使用的量度从左侧面板拖到 **定义** 框。
1. 选择以下量度的值 **大于** 0的数值。
1. 从 **包括** 下拉列表，选择 **访客**
1. 为您的区段提供适当的名称

下图显示了创建区段的示例，我们在其中选择收入为正的访客。

![图3.png](assets/AAFigure3.png)
*图3:为Adobe Analytics量度创建区段，其优化条件等于最大化独特访客转化率。 在此示例中，量度为收入，优化目标是最大化具有正收入的访客数量。*

创建相应的区段后，默认  **[!UICONTROL Analytics for Target]** 可修改工作区中的面板。

1. 添加秒 **独特访客** 量度以及现有访客量度列
2. 将刚刚创建的区段拖到第一列下，以生成类似于图4的面板。 请注意差异 — 具有正收入的独特访客数是分配给每个体验的独特访客总数的一小部分。
   ![图4.png](assets/AAFigure4.png)
   *图4:按新创建的区段过滤独特访客*
3. 转化率可以为 [快速计算](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html?lang=en) 通过突出显示第一列和第二列，右键单击，选择 **从选定范围中创建量度** > **除数**. 应删除默认转化率，并替换为此新计算量度，如下图所示。 您可能需要编辑新创建的计算量度才能显示为 **格式** > **百分比** 最多保留两位小数，如所示。
   ![图4.png](assets/AAFigure5.png)

   *图4:显示二值化收入转化量度的转化率的最终自动分配面板*


## 结论

上述步骤已演示如何正确配置 [!DNL Workspace] 以显示自动分配报表数据。 总结如下：

* 当量度是Target定义的转化量度，或具有优化条件的Adobe Analytics量度时 *最大化每位访客的量度值*，则应使用配置为将访客作为标准化量度的默认工作区面板。
* 当量度是具有优化条件“最大化独特访客转化率”的Adobe Analytics量度时，您必须使用转化率，该转化率定义为该量度为正值的访客比例。 这是通过创建相应的区段来过滤独特访客量度来完成的。
