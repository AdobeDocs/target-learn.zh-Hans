---
title: 如何在 [!DNL Analysis Workspace] 中为[!UICONTROL Auto-Allocate]活动设置A4T报告
description: 运行[!UICONTROL Auto-Allocate]活动时，如何在 [!DNL Adobe] [!DNL Analysis Workspace]中配置[!UICONTROL Analytics for Target] (A4T)报告。
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: 190a67832f378e15090115420bfaf8a4af4b9cb9
workflow-type: tm+mt
source-wordcount: '1341'
ht-degree: 0%

---

# 在[!DNL Analysis Workspace]中为[!DNL Auto-Allocate]活动设置A4T报表

[!DNL Adobe Target]中的[[!UICONTROL Auto-Allocate]活动](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html){target=_blank}在两个或更多体验中标识一个入选者，并在测试继续运行和学习期间，自动为入选者重新分配访客流量。 [!UICONTROL Auto-Allocate]的[!UICONTROL Analytics for Target] (A4T)集成允许您在[!DNL Adobe Analytics]中查看报表数据，并且可以针对[!DNL Analytics]中定义的自定义事件或量度进行优化。

尽管[!DNL Adobe Analytics] [!DNL Analysis Workspace]中提供了丰富的分析功能，但可能需要对默认[!UICONTROL Analytics for Target]面板进行一些修改才能正确解释[!UICONTROL Auto-Allocate]活动。 由于[优化量度标准](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank}中的细微差别，需要进行这些修改。

每种类型的优化量度都需要在A4T中使用不同的报表配置，如下所示：

* 使用[!DNL Analytics]指标

   * [!UICONTROL Maximize metric value per visitor]
   * [!UICONTROL Maximize unique visitor conversion rate]

* 使用[!DNL Target]定义的转化量度

本教程涵盖了总体A4T指南以及特定于标准的报表配置步骤。

## 具有“[!UICONTROL Maximize Metric Value Per Visitor]”优化标准的Analytics量度

**定义**：（总体量度值）/（访客数）

要配置报表，请在A4T报表中进行以下更改：

| 所需更改 | [!DNL Target]触发的报告 | A4T面板报告 |
| --- | --- | --- |
| 最大化[!DNL Analytics]量度的量度值 | <ul><li>删除[!UICONTROL Confidence]个量度。</li><li>移除[!UICONTROL Lift (Low)]和[!UICONTROL Lift (High)]。 保留[!UICONTROL Lift (Med)]。</li><li>取消选中[!UICONTROL Conversion Rate]列中的百分比表示法以避免混淆。 请参阅下面的[A4T的整体指南](#guidance)。</li><li>将[!UICONTROL Conversion]比率量度重命名为“量度/访客”。</li></ul> | <ul><li>删除[!UICONTROL Confidence]个量度。</li><li>移除[!UICONTROL Lift (Low)]和[!UICONTROL Lift (High)]，保留[!UICONTROL Lift (Med)]。</li><li>取消选中[!UICONTROL Conversion Rate]列中的百分比表示法以避免混淆。 请参阅下面的[A4T的整体指南](#guidance)。</li><li>将[!UICONTROL Conversion]比率量度重命名为“量度/访客”。</li><li>确保日期和时间范围与您在[!DNL Target]报表中看到的值一致。 请参阅下面的[A4T的整体指南](#guidance)。</li></ul> |

![最大化收入的量度值](/help/integrations/assets/maximize-metric-value-revenue.png)

## 具有“[!UICONTROL Unique Visitor Conversion Rate]”优化标准的[!DNL Analytics]个量度

**定义**： （具有正值的独特访客数）/（独特访客总数）

示例：假设您的优化指标为[!UICONTROL Revenue]。 活动中有五个独特访客，其中三个独特访客进行了购买。 在此示例中，此值= （3位访客的[!UICONTROL Revenue]为正）/（总共5位独特访客）= 0.6 = 60%。

>[!NOTE]
>
>此处引用的转化率可以指订单外的操作，如点击次数、展示次数等。 在这些情况下，标准仍将是分别最大化点击或查看页面的访客计数。

要配置报表，请在A4T报表中进行以下更改：

| 所需更改 | 目标触发的报告 | A4T面板报告 |
| --- | --- | --- |
| 最大化[!DNL Analytics]量度的转化 | <ul><li>删除[!UICONTROL Confidence]个量度。</li><li>删除所有三个[!UICONTROL Lift]量度。</li><li>取消选中[!UICONTROL Conversion Rate]列中的百分比表示法以避免混淆。 请参阅下面的[A4T的整体指南](#guidance)。</li></ul> | <ul><li>删除[!UICONTROL Confidence]个量度。</li><li>删除所有三个[!UICONTROL Lift]量度。</li><li>创建一个区段以筛选具有正量度值的访客，这些访客查看了分析的活动。 请参阅下面的[创建区段](#segment)。</li><li>替换自动填充的[!UICONTROL Conversion Rate]指标，使其成为具有正指标值的[!UICONTROL Unique visitors]和独特访客之间的除。 请参阅下面的[更新转化率量度](#update-conversion-metric)。</li><li>取消选中[!UICONTROL Conversion Rate]列中的百分比表示法以避免混淆。 请参阅下面的[A4T的整体指南](#guidance)。</li><li>确保日期和时间范围与您在[!DNL Target]报表中看到的值一致。 请参阅下面的[A4T的整体指南](#guidance)。</li></ul> |

### 默认A4T面板报告 — 其他指南

以下部分包含有关设置默认A4T面板报表时附加指南的更多信息。

#### 创建区段 {#segment}

1. 单击左边栏中&#x200B;**[!UICONTROL Segments]**&#x200B;旁边的&#x200B;**“+”号**。

   左边栏中的区段旁有![加号。](/help/integrations/assets/plus-sign.png)

1. 将区段命名为“具有正量度值的访客”。
1. 在&#x200B;**[!UICONTROL Definition]**&#x200B;下，选择&#x200B;**[!UICONTROL Include]**&#x200B;旁边的&#x200B;**[!UICONTROL Visitor]**。
1. 在&#x200B;**[!UICONTROL Definition]**&#x200B;下，选择活动中的优化量度。

   在此示例中，假设[!UICONTROL Revenue]作为优化量度。

1. 选择“[!UICONTROL is greater than]”运算符，然后指定“0”。

   这些设置会筛选具有正量度值的所有访客。

1. 单击 **[!UICONTROL Save]**。

   ![正量度值](/help/integrations/assets/positive-metric-value.png)

1. 将新创建的名为“具有正量度值的访客”的区段添加到A4T面板。
1. 将[!UICONTROL Unique Visitors]量度拖放到与“具有正量度值的访客”相同的列中。

   此配置会创建一个区段，其中包含指标值为正的所有独特访客。 在本例中，选择收入大于零的所有独特访客。

#### 更新[!UICONTROL Conversion Rate]量度 {#update-conversion-metric}

1. 如果您尚未这样做，请从面板中删除现有[!UICONTROL Conversion Rate]列，如下所述。
1. 通过单击左边栏中&#x200B;**[!UICONTROL Metrics]**&#x200B;部分旁边的“+”号添加指标。
1. 将量度命名为“转化率”，并将其定义为“（[!UICONTROL Unique Visitors]，具有正量度值）”除以“独特访客”，如下所示。

   将“具有正量度值的访客”、除运算符、分子中的“独特访客”量度以及“独特访客”的新创建区段（下文定义的步骤）添加为分母。

   A4T面板中的![转化率。](/help/integrations/assets/conversion-rate.png)

1. 单击 **[!UICONTROL Save]**。

1. 将新创建的“转化率”指标拖放到现有面板中。
1. 单击齿轮图标，然后取消选中&#x200B;**[!UICONTROL Percent]**&#x200B;复选框，因为此值可能会导致混淆。

   正确配置报告应产生如下图所示的结果：

   A4T面板报表中的![独特访问转化率](/help/integrations/assets/a4t-aa-maximize-metric-value-revenue.png)

## [!DNL Target]定义的转化率

要配置报表，请在A4T报表中进行以下更改：

| 所需更改 | 目标触发的报告 | A4T面板报告 |
| --- | --- | --- |
| 使用[!DNL Target]转化量度的[!DNL Analytics]报表 | <ul><li>删除[!UICONTROL Confidence]个量度。</li><li>移除[!UICONTROL Lift (Low)]和[!UICONTROL Lift (High)]。 保持提升(Med)。</li><li>取消选中[!UICONTROL Conversion Rate]列中的百分比表示法以避免混淆。 请参阅下面的[A4T的整体指南](#guidance)。</li></ul> | <ul><li>删除[!UICONTROL Confidence]个量度。</li><li>移除[!UICONTROL Lift (Low)]和[!UICONTROL Lift (High)]。 保留[!UICONTROL Lift (Med)]。</li><li>取消选中[!UICONTROL Conversion Rate]列中的百分比表示法以避免混淆。 请参阅下面的[A4T的整体指南](#guidance)。</li><li>确保日期和时间范围与您在[!DNL Target]报表中看到的值一致。 请参阅下面的[A4T的整体指南](#guidance)。</li></ul> |

正确配置报告应产生如下图所示的结果：

![活动转换](/help/integrations/assets/optimized-table.png)

## A4T总体指南 {#guidance}

您可以通过单击[!UICONTROL Target]中报告屏幕上的链接来导航到预建[!UICONTROL Analytics for Target]面板（本指南稍后将这种链接称为“[!DNL Target]触发的报告”）。 或者，您也可以在[!DNL Analytics]中构建A4T面板（此部分稍后将介绍详细信息）。

以下部分根据您选择的方法指定所需的配置。 但是，以下步骤可作为A4T的整体指导：

* 无论使用何种面板创建方法，都从A4T面板中删除置信度量度（下文将详细介绍这两种方法）。 请改为在[!DNL Target]报表中引用这些值。 此外，可以在[!DNL Target]报表中确定活动入选者。 有关活动入选者标识的详细信息，请参阅下面的[标识活动入选者](#winner)部分。
&#x200B;>>
* 为避免混淆，请取消选中[!UICONTROL Conversion Rate]量度的“[!UICONTROL Percent]”表示形式。 请参阅下面的[!UICONTROL Conversion Rate]列[&#128279;](#hide-percentage)中的隐藏百分比。
&#x200B;>>
* 如果要构建A4T面板，请确保日期和时间范围与[!DNL Target]报表的日期和时间范围相匹配。 请参阅下面的[在下面的A4T面板中对齐日期和时间](#aligning-date-and-time)。

### 从[!UICONTROL Conversion Rate]列中隐藏百分比 {#hide-percentage}

1. 单击[!UICONTROL Conversion Rate]列标题旁边的&#x200B;**齿轮**&#x200B;图标。

   “转化率”列中的![齿轮图标](/help/integrations/assets/coversion-rate-gear-icon.png)

   显示[!UICONTROL Column]设置对话框：

   ![列设置对话框](/help/integrations/assets/column-settings-dialog-box.png){width="200"}

1. 取消选中&#x200B;**[!UICONTROL Percent]**&#x200B;复选框。

   您的A4T面板现在不包含百分比作为[!UICONTROL Conversion Rate]，并与[!DNL Target]匹配，如下所示：

   ![显示无百分比的“转化率”列](/help/integrations/assets/no-percentages.png)

### 在A4T面板中对齐日期和时间 {#aligning-date-and-time}

1. 在每个面板下方，检查面板引用的日期范围，确保日期范围与[!DNL Target]报表的日期范围匹配。

   A4T面板中的![日期范围](/help/integrations/assets/date-range.png)

1. 在[!DNL Analytics]中，将时间范围设置为凌晨12:00到晚上11:59。

### 确定活动入选者 {#winner}

当具有置信度值大于或等于95%的获胜转化率时，将选择[!DNL Auto-Allocate]个活动获胜者。 这些值应在[!DNL Target]报表中引用，因为置信度计算反映了[!DNL Target]建议用于[!UICONTROL Auto-Allocate]活动的更保守的方法。 查看&#x200B;*[!UICONTROL Adobe Target Business Practitioner Guide]*&#x200B;中自动分配的[统计保证](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/determine-winner.html#section_7AF3B93E90BA4B80BC9FC4783B6A389C){target=_blank}。

>[!NOTE]
>
>“尚未有入选者”和“入选者”徽章在[!DNL Analysis Workspace]的A4T面板中不可用。 此外，应忽略[!UICONTROL Auto-Allocate]活动的[!DNL Target]报表中显示的入选者“星级”徽章。 查看&#x200B;*[!UICONTROL Adobe Target Business Practitioner Guide]*&#x200B;中自动分配和自动定位活动&#x200B;*对* A4T支持的[自动分配](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#aa){target=_blank}。

### 在[!DNL Analysis Workspace]中为[!UICONTROL Auto-Allocate]面板创建A4T

1. 要为[!UICONTROL Auto-Allocate]活动报告创建A4T面板，请从[!DNL Analysis Workspace]中的[!UICONTROL Analytics for Target]面板开始，如下所示。

   ![Analytics for Target — 自动分配报告](/help/integrations/assets/a4t-auto-allocate-report.png)

1. 进行以下选择：

   * **[!UICONTROL Control Experience]**：选择任意体验。
   * **[!UICONTROL Normalizing Metric]**：选择&#x200B;**[!UICONTROL Visitors]**（默认情况下包含在A4T面板中）。 [!UICONTROL Auto-Allocate]始终按独特访客标准化转化率。
   * **成功量度**：选择您在活动创建期间使用的相同（优化）量度。 如果这是[!DNL Target]定义的转化量度，请选择&#x200B;**[!UICONTROL Activity Conversion]**。 否则，请选择您使用的[!DNL Adobe Analytics]量度。









