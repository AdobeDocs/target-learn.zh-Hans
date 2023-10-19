---
title: 如何在中设置A4T报表 [!DNL Analysis Workspace] 对象 [!UICONTROL 自动分配] 活动
description: 如何配置 [!UICONTROL 目标分析] (A4T)报表 [!DNL Adobe] [!DNL Analysis Workspace] 运行时 [!UICONTROL 自动分配] 活动。
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: b22d51d7d231d67af179622755fb4f7ef83474a8
workflow-type: tm+mt
source-wordcount: '1590'
ht-degree: 0%

---

# 在中设置A4T报表 [!DNL Analysis Workspace] 对象 [!DNL Auto-Allocate] 活动

An [!UICONTROL 自动分配] 中的活动 [!DNL Adobe Target] 在两个或更多体验中标识一个入选者，并在测试继续运行和学习期间，自动为入选者重新分配访客流量。 此 [!UICONTROL 目标分析] (A4T)集成 [!UICONTROL 自动分配] 允许您在中查看报表数据 [!DNL Adobe Analytics]，并且您可以优化中定义的自定义事件或量度 [!DNL Analytics].

尽管中提供了丰富的分析功能， [!DNL Adobe Analytics] [!DNL Analysis Workspace]，对默认进行了一些修改 [!UICONTROL 目标分析] 可能需要面板才能正确解释 [!UICONTROL 自动分配] 活动。 由于中的细微差别，需要进行这些修改 [优化量度标准](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank}.

每种类型的优化量度都需要在A4T中使用不同的报表配置，如下所示：

* 使用 [!DNL Analytics] 量度

   * [!UICONTROL 最大化的每位访客量度值]
   * [!UICONTROL 最大限度地提高独特访客转化率]

* 使用 [!DNL Target] — 定义的转化量度

本教程涵盖了总体A4T指南以及特定于标准的报表配置步骤。

## 包含“”的Analytics指标[!UICONTROL 最大化每位访客的量度值]»优化标准

**定义**：（总体量度值）/（访客数）

要配置报表，请在A4T报表中进行以下更改：

| 所需更改 | [!DNL Target]触发的报告 | A4T面板报告 |
| --- | --- | --- |
| 最大化量度值 [!DNL Analytics] 量度 | <ul><li>[!UICONTROL 置信度] 指标应被删除。</li><li>[!UICONTROL 提升（低）] 和 [!UICONTROL 提升（高）] 应该删除。</li><li>取消选中百分比演示 [!UICONTROL 转化率] 列以避免混淆。 有关更多信息，请参阅 [总体指导](#guidance) 下。</li><li>转化率量度应重命名为“量度/访客”。</li></ul> | <ul><li>[!UICONTROL 置信度] 指标应被删除。</li><li>[!UICONTROL 提升（低）] 和 [!UICONTROL 提升（高）] 应该删除。</li><li>取消选中百分比演示 [!UICONTROL 转化率] 列以避免混淆。 有关更多信息，请参阅 [总体指导](#guidance) 下。</li><li>转化率量度应重命名为“量度/访客”。</li><li>确保日期和时间范围与您在中看到的值一致 [!DNL Target] 报告。 有关更多信息，请参阅 [总体指导](#guidance) 下。</li></ul> |

![最大限度地实现收入的量度值](/help/integrations/assets/maximize-metric-value-revenue.png)

## [!DNL Analytics] 带有&quot;[!UICONTROL 独特访客转化率]»优化标准

**定义**：（“独特访客”数量与指标具有正值）/（独特访客总数）

示例：假设您的优化指标为 [!UICONTROL 收入]. 活动中有五个独特访客，其中三个独特访客进行了购买。 在本例中，此值= (3位访客，其中 [!UICONTROL 收入] 正数)/（总共5个独特访客）= 0.6 = 60%。

>[!NOTE]
>
>此处引用的转化率可以指订单外的操作，如点击次数、展示次数等。 在这些情况下，标准仍将是分别最大化点击或查看页面的访客计数。

要配置报表，请在A4T报表中进行以下更改：

| 所需更改 | 目标触发的报告 | A4T面板报告 |
| --- | --- | --- |
| 最大限度地提高 [!DNL Analytics] 量度 | <ul><li>[!UICONTROL 置信度] 指标应被删除。</li><li>全部 [!UICONTROL 提升] 指标应被删除。</li><li>取消选中百分比演示 [!UICONTROL 转化率] 列以避免混淆。 (有关更多信息，请参阅 [总体指导](#guidance) 下。</li></ul> | <ul><li>[!UICONTROL 置信度] 指标应被删除。</li><li>全部 [!UICONTROL 提升] 指标应被删除。</li><li>创建一个区段以筛选具有正量度值的访客，这些访客查看了分析的活动。 有关更多信息，请参阅 [创建区段](#segment) 下。</li><li>替换自动填充的 [!UICONTROL 转化率] 量度，因此是以下两个指标之间的分界线 [!UICONTROL 独特访客] 具有正的量度值和独特访客。 有关更多信息，请参阅 [更新转化率量度](#update-conversion-metric) 下。</li><li>取消选中百分比演示 [!UICONTROL 转化率] 列以避免混淆。 有关更多信息，请参阅 [总体指导](#guidance) 下。</li><li>确保日期和时间范围与您在中看到的值一致 [!DNL Target] 报告。 有关更多信息，请参阅 [总体指导](#guidance) 下。</li></ul> |

### 默认A4T面板报告 — 其他指南

以下部分包含有关设置默认A4T面板报表时附加指南的更多信息。

#### 创建区段 {#segment}

1. 单击 **“+”符号** 旁边 **[!UICONTROL 区段]** 在左边栏中。

   ![左边栏中区段旁边的加号。](/help/integrations/assets/plus-sign.png)

1. 将区段命名为“具有正量度值的访客”。
1. 下 **[!UICONTROL 定义]**，位于 **[!UICONTROL 包括]**，选择 **[!UICONTROL 访客]**.
1. 下 **[!UICONTROL 定义]**&#x200B;中，选择活动中的优化量度。

   在此示例中，假设 [!UICONTROL 收入] 作为优化量度。

1. 选择&quot;[!UICONTROL 大于]”运算符，然后指定“0”。

   这些设置会筛选具有正量度值的所有访客。

1. 单击&#x200B;**[!UICONTROL 保存]**。

   ![正量度值](/help/integrations/assets/positive-metric-value.png)

1. 将新创建的名为“具有正量度值的访客”的区段添加到A4T面板。
1. 拖放 [!UICONTROL 独特访客] 与“具有正量度值的访客”相同的列中的量度。

   此配置会创建一个区段，其中包含指标值为正的所有独特访客。 在本例中，选择收入大于零的所有独特访客。

#### 更新 [!UICONTROL 转化率] 量度 {#update-conversion-metric}

1. 如果您尚未这样做，请删除现有 [!UICONTROL 转化率] 栏，如下文所述。
1. 通过单击 **[!UICONTROL 量度]** 部分。
1. 将量度命名为“转化率”并将其定义为“([!UICONTROL 独特访客] 正的量度值)”除以“独特访客”，如下所示。

   将“具有正量度值的访客”、除运算符、分子中的“独特访客”量度以及“独特访客”的新创建区段（下文定义的步骤）添加为分母。

   ![A4T面板中的转化率。](/help/integrations/assets/conversion-rate.png)

1. 单击&#x200B;**[!UICONTROL 保存]**。

1. 将您新创建的“转化率”量度拖放到现有面板中。
1. 单击齿轮图标，然后取消选择 **[!UICONTROL 百分比]** 复选框，因为此值可能会导致混淆。

   正确配置报告应产生如下图所示的结果：

   ![A4T面板报表中的独特访问转化率](/help/integrations/assets/a4t-aa-maximize-metric-value-revenue.png)

## [!DNL Target]定义的转化率

要配置报表，请在A4T报表中进行以下更改：

| 所需更改 | 目标触发的报告 | A4T面板报告 |
| --- | --- | --- |
| [!DNL Analytics] 报告 [!DNL Target] 转化量度 | <ul><li>[!UICONTROL 置信度] 指标应被删除。</li><li>[!UICONTROL 提升（低）] 和 [!UICONTROL 提升（高）] 应该删除。</li><li>取消选中百分比演示 [!UICONTROL 转化率] 列以避免混淆。 有关更多信息，请参阅 [总体指导](#guidance) 下。</li></ul> | <ul><li>[!UICONTROL 置信度] 指标应被删除。</li><li>[!UICONTROL 提升（低）] 和 [!UICONTROL 提升（高）] 应该删除。</li><li>取消选中百分比演示 [!UICONTROL 转化率] 列以避免混淆。 有关更多信息，请参阅 [总体指导](#guidance) 下。</li><li>确保日期和时间范围与您在中看到的值一致 [!DNL Target] 报告。 有关更多信息，请参阅 [总体指导](#guidance) 下。</li></ul> |

正确配置报告应产生如下图所示的结果：

![活动转化](/help/integrations/assets/optimized-table.png)

## 总体指导 [!UICONTROL 目标分析] (A4T) {#guidance}

您可以导航到预建的 [!UICONTROL 目标分析] 面板中，单击报表屏幕中的链接 [!UICONTROL Adobe Target] (本指南后面部分将此项称为&quot;[!DNL Target] — 触发的报告”)。 或者，也可以在中构建A4T面板 [!DNL Analytics] （本节后面部分提供了详细信息）。

以下部分根据您选择的方法指定所需的配置。 但是，以下步骤可用作总体指导：

* 无论使用何种面板创建方法，都应从A4T面板中删除置信度量度（下文将详细介绍这两种方法）。 请改为引用这些值 [!DNL Target] 报表。 此外，还可以在以下位置确定活动入选者： [!DNL Target] 报表。 有关活动入选者标识的详细信息，请参阅 [确定活动入选者](#winner) 部分。
>>
* 为避免混淆，请取消选中“[!UICONTROL 百分比]”演示 [!UICONTROL 转化率] 量度。 有关更多信息，请参阅 [隐藏百分比 [!UICONTROL 转化率] 列](#hide-percentage) 下。
>>
* 如果要构建A4T面板，请确保日期和时间范围与 [!DNL Target] 报告。 有关更多信息，请参阅 [在A4T面板中对齐日期和时间](#aligning-date-and-time) 下。

### 隐藏百分比 [!UICONTROL 转化率] 列 {#hide-percentage}

1. 单击 **齿轮** 标题旁边的图标 [!UICONTROL 转化率] 列。

   ![转化率列中的齿轮图标](/help/integrations/assets/coversion-rate-gear-icon.png)

   此 [!UICONTROL 列] 设置对话框显示：

   ![列设置对话框](/help/integrations/assets/column-settings-dialog-box.png){width="200"}

1. 取消选择 **[!UICONTROL 百分比]** 复选框。

   您的A4T面板现在不包含百分比作为转化率和匹配项 [!DNL Target]，如下所示：

   ![显示无百分比的“转化率”列](/help/integrations/assets/no-percentages.png)

### 在A4T面板中对齐日期和时间 {#aligning-date-and-time}

1. 在每个面板下方，检查面板引用的日期范围，以确保日期范围与 [!DNL Target] 报告。

   ![A4T面板中的日期范围](/help/integrations/assets/date-range.png)

1. 在 [!DNL Analytics]，将时间范围设置为凌晨12:00到晚上11:59。

### 确定活动入选者 {#winner}

[!DNL Auto-Allocate] 当具有置信值大于或等于95%的入选转化率时，将选择活动入选者。 应在以下位置引用这些值 [!DNL Target] 报表，因为置信度计算反映了更保守的方法 [!DNL Target] 建议用于 [!UICONTROL 自动分配] 活动。 有关更多信息，请参阅 [自动分配的统计保证](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/determine-winner.html#section_7AF3B93E90BA4B80BC9FC4783B6A389C){target=_blank} 在 *[!UICONTROL Adobe Target商业从业者指南]*.

>[!NOTE]
>
“尚未有入选者”和“入选者”徽章在中的A4T面板中不可用 [!DNL Analysis Workspace]. 此外，入选的“star”徽章会显示在 [!DNL Target] 报告 [!UICONTROL 自动分配] 活动应被忽略。 有关更多信息，请参阅 [自动分配](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#aa){target=_blank} 在 *自动分配和自动定位活动支持A4T* 在 *[!UICONTROL Adobe Target商业从业者指南]*.

### 为创建A4T [!UICONTROL 自动分配] 面板位于 [!DNL Analysis Workspace]

1. 为创建A4T面板 [!UICONTROL 自动分配] 活动报表，从 [!UICONTROL 目标分析] 面板位于 [!DNL Analysis Workspace]，如下所示。

   ![Analytics for Target — 自动分配报表](/help/integrations/assets/a4t-auto-allocate-report.png)

1. 进行以下选择：

   * **[!UICONTROL 控制体验]**：选择任意体验。
   * **[!UICONTROL 标准化量度]**：选择 **[!UICONTROL 访客]** （默认情况下包含在A4T面板中）。 [!UICONTROL 自动分配] 始终按独特访客标准化转化率。
   * **成功量度**：选择您在活动创建期间使用的相同（优化）量度。 如果这是 [!DNL Target]-defined conversion metric（定义的转化量度），选择 **[!UICONTROL 活动转换]**. 否则，选择 [!DNL Adobe Analytics] 您使用的量度。









