---
title: 优化Adobe Target实施
description: 大致了解Adobe Target的实施和结构。 了解如何了解和审核贵组织的设置。 了解为团队创建知识存储库的常见故障排除技巧和提示。
solution: Target
feature: Overview
role: Leader, User
exl-id: 49b69f41-0993-437c-bb69-84392be427df
source-git-commit: 20bd1eb17ef6e287f7b76e14f727456e12d6f115
workflow-type: tm+mt
source-wordcount: '1129'
ht-degree: 0%

---

# 优化Adobe Target实施

如果您是组织的新手，并且希望熟悉测试和优化实践中的现有内容，本文可帮助您入门。 我们首先会概述Adobe Target的实施和结构。 您将学习如何了解和审核组织的设置。 最后，我们将讨论常见的故障排除技巧以及有关为团队创建知识存储库的提示。

Adobe Target是一款允许对不同访客测试和定位独特内容的工具。 有关可用功能的概述，[请访问此指南](https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=zh-Hans)。

## Target实施和结构

在我们深入探讨Adobe Target的实施过程或其结构之前，先了解一些关于软件的基础知识很有帮助。

Adobe Target是一种工具，它允许测试和定位面向不同访客的唯一内容，而无需更改本机网站代码。 Target会暂时更改最终用户体验，并在看到更改后跟踪用户的行为。 Target还提供了根据用户档案信息或之前的操作更改最终用户体验的功能。

有三种Target基本活动类型：

1. A/B 测试
2. 多变量测试(MVT)
3. 体验测试

**A/B测试**&#x200B;比较两个或更多体验，以了解在预先指定的测试期间，哪个体验最有利于提高转化。 A/B测试是一种高度受控的流量测量实验，按百分比而不是规则分割，允许您：

* 分析测试数据。
* 以了解有关受众的见解。
* 以确定哪个体验的效果最佳。

**多变量测试** (MVT)比较页面上各元素之间的选件组合，以查看哪个组合对特定受众的表现最佳。 在整个预先指定的测试期间，此测试还会确定页面的哪个元素最有利于提高转化。 MVT提供：

* 在多个元素中显示多个选件的方法。
* 根据特定目标测试生成的独特体验的方法。
* 深入了解哪些元素对访客交互的负面或正面影响最大。

**体验测试**（经验丰富的定位）根据一组营销人员定义的规则和条件向特定受众提供内容。 此方法提供了一种根据一组定义的分配规则将特定内容定位到特定受众的方法。

Target的工作原理

以下是Target工作方式的高级示例：

1. 访客从您的服务器请求一个页面，并在浏览器中显示该页面。
1. 在访客的浏览器中设置第一方Cookie以存储行为。
1. 然后，页面调用Adobe Target。
1. 根据用户活动的规则显示内容。
1. Adobe Target会捕获活动配置中定义的特定指标，以衡量测试体验的影响。

Target构建在“全局Mbox”之上，可提供影响页面上任何内容的功能。 此功能在页面加载时部署为at.js文件的硬编码链接，或者使用标签管理器(如AdobeLaunch)交付。

## 了解您当前的实施

为了解您当前的实施，Adobe建议您查看Target用户界面实施，以及标签管理器和页面加载实施。

**查看您的[!DNL Target]用户界面：**

1. 在[!DNL Target] UI上开始审阅：

   * 查看[!DNL Target]技术栈栈
   * 确认可用的功能
   * 确定部署的位置

1. 审查活动以了解最佳实践：

   * 审查计划成熟度的历史营销活动

1. 取消激活旧活动：

   * 存档和清理不再具有当前或将来用途的[!DNL Target]资源

1. 查看受众。

1. 查看环境定义和关联的域。

1. 查看配置文件脚本的适用性

   * 所有配置文件脚本在每次目标调用时运行
   * 通过删除不适用的脚本来维护调用效率

要查看标记管理器和页面加载，请执行以下操作：

1. 在标记管理器中确认以下内容：

   * 部署预期的[!DNL Target]个JavaScript代码
   * 相应的内容隐藏解决方案
   * 设置必要的规则以使用预期的参数填充[!DNL Target]调用

1. 在页面加载期间确认以下内容：

   * 匹配请求URL和[!DNL Target]请求URL的版本号
   * 填充了体验丰富的云ID值（云正文）
   * 显示预期的集成值（云正文）
   * 已在相应页面上填充[!DNL Target]参数

## [!DNL Target]审核活动

要避免手动遍历每个页面来审核[!DNL Target]Adobe，请使用Auditor帮助了解实施的当前技术状态。 AdobeAuditor由ObservePoint提供支持，可以设置为在手动级别运行，以确定您网站上的高级别实施问题。

AdobeAuditor提供：

* 高站点运行状况
* 实施问题的快速调用

Adobe建议每月对以下对象执行手动审核：

* 识别未标记的页面
* 识别不一致的版本
* 查找最新版本
* 提供可导出的详细信息

## 常见疑难解答

>[!NOTE]
>
>Adobe建议安装Adobe Experience Platform Debugger。

以下是进入Experience时的常规疑难解答提示：

### 缓存和Cookie**

* 清除缓存和Cookie
* 谨慎使用专用模式（例如：Firefox中的专用模式可能会阻止[!DNL Target]）

### 您是否有资格参加活动？

* 检查您是否执行了受众在活动中使用的相同步骤
* 使用`mboxTrace`或响应令牌检查配置文件和区段值

### 验证可视化/功能性时的一般疑难解答提示

如果位于[!DNL Target]体验中，而您没有看到预期的可视化体验：

检查[!DNL Target]响应：

* 如果未执行代码：

1. 检查冲突的活动
1. 联系客户关怀团队

* 如果执行代码：

1. 在该场景中重新使用代码

## 维护知识存储库

知识存储库是用于记录和共享信息的在线平台。 知识存储库包含特定于您的实施的信息，并可包含特定于团队的信息。

理想情况下，存储库应允许在平台中进行编辑和自动保存。 在初始配置后，它便易于维护和保持最新。 知识存储库中的内容是根据用户角色来管理的。

知识存储库中的典型文档包括：

* **概述文档** — 用于明确说明计划目标、目标、流程和结构的文档
* **构思存储库** — 用于管理和优先处理尚未准备好测试过程的潜在构思的文档
* **计划路线图** — 在想法准备好开始测试过程后，用于管理测试活动各个方面的文档
* **活动计划文档** — 用于概述生成和启动活动所需信息的文档
* **活动计划文档** — 用于向利益相关者传达结果和建议后续步骤的文档
* **计划仪表板** — 用于跟踪一段时间内的计划效果、节奏和收入利益的文档。

有关详细信息，请与高级顾问Wilder Freed一起回顾我们的[网络研讨会](https://adobecustomersuccess.adobeconnect.com/p4p7xlp7dh42mp4/)。

在[客户成功](https://experienceleague.adobe.com/docs/customer-success/customer-success/overview.html?lang=zh-Hans)中心了解有关战略和思想领导力的更多信息。
